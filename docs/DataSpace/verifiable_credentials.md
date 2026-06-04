## Introduction

The purpose of this section is to describe and document the process for performing a Machine-to-Machine (M2M) data transaction by terminal using Verifiable Credentials (VCs) to access the data space and request data from the Orion-LD Context Broker through the APISIX component, which acts as an API Gateway.

The previous page [Decentralized identifiers](did.md) gives a practical introduction to DIDs and shows how to generate did:web and did:key identifiers using Docker. It is recommended to follow this section first, as it is the basis for the current section.

All commands used can be executed from the Ubuntu CLI. The steps to follow in order to perform the data transaction are described below.

## Components

The components that form part of the data transaction process in the data space are:

- VCs: Verifiable Credentials
- DIDs: Decentralized Identifiers used to represent identities in a portable and cryptographically verifiable way.
- VPs: Verifiable Presentations
- Keycloak: Tool for user and role management (IAM)
- Verifier: Component of the data space Trust Anchor responsible for validating participants' credentials.
- Context Broker: Service that stores data with context using the [NGSI-LD](https://es.wikipedia.org/wiki/NGSI-LD) protocol.
- APISIX: API Gateway that acts as a firewall to prevent direct access to data space services. It checks the identities of requesters before granting access to services.

## Data transaction guide

This section describes the process to follow in order to request data from the Orion-LD context broker within the PGTEC data space.

### 0º: DID generator

To create DIDs and certificates, you can follow the code below, although we recommend reading the previous section to understand in detail how DIDs are used and created.

```sh
mkdir wallet-identity
chmod o+rw wallet-identity
docker run -v $(pwd)/wallet-identity:/cert quay.io/wi_stefan/did-helper:0.1.1
sudo chmod -R o+rw wallet-identity/private-key.pem
```

### 1º: VC creation

The first step is to create a VC using Keycloak. To do this, run the following parameterizable script:

```sh
#!/bin/bash

# --- Updated Default Values to match your working environment ---
BASE_URL="https://keycloak-consumer.pgtec-vrain-dataspace.eu"
REALM="consumer"
CLIENT_ID="account-console"
USERNAME="operator"
PASSWORD="test"
CRED_CONFIG_ID="operator-credential"
OUTPUT_FILE="./wallet-identity/vc.jwt"
FORMAT="vc+sd-jwt"
DEBUG=false

# Usage helper
usage() {
  echo "Usage: $0 [-b url] [-r realm] [-c client_id] [-u user] [-p pass] [-i cred_id] [-o output_file] [-d]"
  echo ""
  echo "Options:"
  echo "  -b    Base URL (Default: $BASE_URL)"
  echo "  -r    Realm Name (Default: $REALM)"
  echo "  -c    Client ID (Default: $CLIENT_ID)"
  echo "  -u    Username (Default: $USERNAME)"
  echo "  -p    Password (Default: $PASSWORD)"
  echo "  -i    Credential Configuration ID (Default: $CRED_CONFIG_ID)"
  echo "  -f    Choose the format (Default: $FORMAT)"
  echo "  -o    File to save the credential (Optional)"
  echo "  -d    Enable Debug mode (Print raw curl responses)"
  exit 1
}

# --- Helper: Debug Logger ---
debug_log() {
    local step="$1"
    local content="$2"
    if [ "$DEBUG" = true ]; then
        echo "--------------------------------------------------" >&2
        echo "DEBUG [$step] RAW RESPONSE:" >&2
        echo "$content" >&2
        echo "--------------------------------------------------" >&2
    fi
}

# --- Parse Flags ---
while getopts "b:r:c:u:p:i:o:f:hd" opt; do
  case $opt in
    b) BASE_URL="$OPTARG" ;;
    r) REALM="$OPTARG" ;;
    c) CLIENT_ID="$OPTARG" ;;
    u) USERNAME="$OPTARG" ;;
    p) PASSWORD="$OPTARG" ;;
    i) CRED_CONFIG_ID="$OPTARG" ;;
    o) OUTPUT_FILE="$OPTARG" ;;
    f) FORMAT="$OPTARG"  ;;
    d) DEBUG=true ;;
    h) usage ;;
    *) usage ;;
  esac
done

BASE_URL=${BASE_URL%/}

# --- 1. Get Initial Access Token ---
echo "Logging in as $USERNAME..." >&2
response_1=$(curl -s -X POST "$BASE_URL/realms/$REALM/protocol/openid-connect/token" \
  --header 'Accept: */*' \
  --header 'Content-Type: application/x-www-form-urlencoded' \
  --data "grant_type=password" \
  --data "client_id=$CLIENT_ID" \
  --data "username=$USERNAME" \
  --data "password=$PASSWORD" \
  --data "scope=openid")

debug_log "1. Initial Access Token" "$response_1"

access_token=$(echo "$response_1" | jq '.access_token' -r)

if [ "$access_token" == "null" ] || [ -z "$access_token" ]; then
    echo "Error: Failed to obtain access token. Check your credentials, URL, Realm, or enable debug (-d) to see raw error." >&2
    exit 1
fi

# --- 2. Get Credential Offer URI ---
echo "Fetching Credential Offer URI for $CRED_CONFIG_ID..." >&2
response_2=$(curl -s -X GET "$BASE_URL/realms/$REALM/protocol/oid4vc/credential-offer-uri?credential_configuration_id=$CRED_CONFIG_ID" \
  --header "Authorization: Bearer ${access_token}")

debug_log "2. Credential Offer URI" "$response_2"

offer_uri=$(echo "$response_2" | jq '"\(.issuer)\(.nonce)"' -r)

# --- 3. Get Pre-Authorized Code ---
echo "Requesting Pre-Authorized Code..." >&2
# Note: Ensure offer_uri is a valid URL. If step 2 failed logic, this might fail.
response_3=$(curl -s -X GET "${offer_uri}" \
  --header "Authorization: Bearer ${access_token}")

debug_log "3. Pre-Authorized Code" "$response_3"

pre_authorized_code=$(echo "$response_3" | jq '.grants."urn:ietf:params:oauth:grant-type:pre-authorized_code"."pre-authorized_code"' -r)

# --- 4. Exchange Pre-Auth Code for Credential Access Token ---
echo "Exchanging code for Credential Access Token..." >&2
response_4=$(curl -s -X POST "$BASE_URL/realms/$REALM/protocol/openid-connect/token" \
  --header 'Accept: */*' \
  --header 'Content-Type: application/x-www-form-urlencoded' \
  --data "grant_type=urn:ietf:params:oauth:grant-type:pre-authorized_code" \
  --data "pre-authorized_code=${pre_authorized_code}")

debug_log "4. Credential Access Token" "$response_4"

credential_access_token=$(echo "$response_4" | jq '.access_token' -r)

# --- 5. Request the Verifiable Credential ---
echo "Issuing Credential..." >&2
response_5=$(curl -s -X POST "$BASE_URL/realms/$REALM/protocol/oid4vc/credential" \
  --header 'Accept: */*' \
  --header 'Content-Type: application/json' \
  --header "Authorization: Bearer ${credential_access_token}" \
  --data "{\"credential_identifier\":\"$CRED_CONFIG_ID\", \"format\":\"$FORMAT\"}")

debug_log "5. Verifiable Credential" "$response_5"

credential=$(echo "$response_5" | jq '.credential' -r)

# --- Output Handling ---
if [ "$credential" == "null" ] || [ -z "$credential" ]; then
    echo "Error: Failed to retrieve credential. Enable debug (-d) to inspect the API response." >&2
    exit 1
fi

if [ -n "$OUTPUT_FILE" ]; then
    # Ensure directory exists
    mkdir -p "$(dirname "$OUTPUT_FILE")"
    echo "$credential" > "$OUTPUT_FILE"
    echo "Success! Credential saved to: $OUTPUT_FILE" >&2
else
    echo "--- BEGIN CREDENTIAL ---" >&2
    echo "$credential"
    echo "--- END CREDENTIAL ---" >&2
fi
```

The script is designed to be parameterizable to adapt to different use cases. You can choose the URL where Keycloak is located, the type of Keycloak client, the user, the configuration, and the format of the VC to be created. To create and run the script, execute the following line:

```bash
nano get_credentials.sh #then copy and paste the script code
./get_credentials.sh #also can be used bash ./get_credentials.sh
```

When executed, a VC issued by Keycloak will be created in the ``sh wallet-identity`` folder called ``sh vc.jwt`` . The credential format is JSON Web Token.

### 2º: Creation of the VP and the Access token.

In this section, the Verifiable Presentation is created using the newly created VC, the DID key, and did.json generated before. The script is configured so that the DIDs are located in the ``sh wallet-identity`` folder. The path can be configured in the scripts:

```sh
#!/bin/bash

# --- Default Values ---
BASE_URL="https://verifier.pgtec-vrain-dataspace.eu/services/data-service"
SCOPE="operator"
CLIENT_ID="account-console"
DID_FILE="wallet-identity/did.json"
KEY_FILE="wallet-identity/private-key.pem"
VC_INPUT="./wallet-identity/vc.jwt"
DEBUG=false
OUTPUT_FILE="./wallet-identity/vp.jwt"  

usage() {
  echo "Usage: $0 [-v vc_jwt_or_file] [-b url] [-s scope] [-d did_file] [-k key_file] [-c client_id] [-o output_file] [-x]"
  echo "Options:"
  echo "  -o    File to write the access token to"
  echo "  -x    Enable debug mode (prints curl commands and raw responses)"
  exit 1
}

# --- Parse Flags ---
while getopts "b:v:s:d:k:c:o:xh" opt; do
  case $opt in
    b) BASE_URL="$OPTARG" ;;
    v) VC_INPUT="$OPTARG" ;;
    s) SCOPE="$OPTARG" ;;
    d) DID_FILE="$OPTARG" ;;
    k) KEY_FILE="$OPTARG" ;;
    c) CLIENT_ID="$OPTARG" ;;
    o) OUTPUT_FILE="$OPTARG" ;;
    x) DEBUG=true ;;
    h|*) usage ;;
  esac
done

# --- 1. Validation & Input Handling ---
if [ ! -f "$VC_INPUT" ] && [[ ! "$VC_INPUT" == ey* ]]; then
    echo "Error: VC input not found as file and doesn't look like a JWT string." >&2
    exit 1
fi

if [ -f "$VC_INPUT" ]; then
    [ "$DEBUG" = true ] && echo "--- DEBUG: Reading VC from file $VC_INPUT ---" >&2
    VC_JWT=$(cat "$VC_INPUT" | tr -d '[:space:]')
else
    VC_JWT="$VC_INPUT"
fi

# --- 2. Discovery & Identity Extraction ---
token_endpoint=$(curl -s -X GET "${BASE_URL}/.well-known/openid-configuration" | jq -r '.token_endpoint')
holder_did=$(jq '.id' -r < "$DID_FILE")

# --- 3. Construct Verifiable Presentation (VP) ---
verifiable_presentation=$(jq -n \
  --arg vc "$VC_JWT" \
  --arg holder "$holder_did" \
  '{
    "@context": ["https://www.w3.org/2018/credentials/v1"],
    "type": ["VerifiablePresentation"],
    "verifiableCredential": [$vc],
    "holder": $holder
}')

# --- 4. JWT Helpers ---
b64url() {
  openssl base64 -A | tr '+/' '-_' | tr -d '='
}

# --- 5. Create Signed VP Token (JWT) ---
jwt_header=$(echo -n "{\"alg\":\"ES256\", \"typ\":\"JWT\", \"kid\":\"${holder_did}\"}" | b64url)
payload=$(echo -n "{\"iss\": \"${holder_did}\", \"sub\": \"${holder_did}\", \"vp\": ${verifiable_presentation}}" | b64url)
signature=$(echo -n "${jwt_header}.${payload}" | openssl dgst -sha256 -binary -sign "$KEY_FILE" | b64url)
vp_jwt="${jwt_header}.${payload}.${signature}"

# --- 6. Exchange VP for Access Token ---
if [ "$DEBUG" = true ]; then
    echo "--- DEBUG: CURL COMMAND ---" >&2
    echo "curl -X POST $token_endpoint \\" >&2
    echo "  --header 'Content-Type: application/x-www-form-urlencoded' \\" >&2
    echo "  --data-urlencode \"grant_type=vp_token\" \\" >&2
    echo "  --data-urlencode \"client_id=$CLIENT_ID\" \\" >&2
    echo "  --data-urlencode \"vp_token=$vp_jwt\" \\" >&2
    echo "  --data-urlencode \"scope=$SCOPE\"" >&2
    echo "----------------------------" >&2
fi

# Capture raw response to debug failures
response=$(curl -s -X POST "$token_endpoint" \
      --header 'Accept: */*' \
      --header 'Content-Type: application/x-www-form-urlencoded' \
      --data-urlencode "grant_type=vp_token" \
      --data-urlencode "client_id=$CLIENT_ID" \
      --data-urlencode "vp_token=${vp_jwt}" \
      --data-urlencode "scope=$SCOPE")

access_token=$(echo "$response" | jq '.access_token' -r)

if [ "$access_token" == "null" ] || [ -z "$access_token" ]; then
    echo "Error: Failed to obtain access token." >&2
    echo "Raw Response from Keycloak:" >&2
    echo "$response" | jq . >&2
    exit 1
fi

# --- 7. Output Handling ---
if [ -n "$OUTPUT_FILE" ]; then
    echo "$access_token" > "$OUTPUT_FILE"
    echo "Access token written to $OUTPUT_FILE" >&2
else
    echo "$access_token"
fi
```

Again, to run the script, the file must be created. This can be done by:

```sh
nano get_access_token.sh #then copy and paste the script code
./get_access_token.sh #also can be used bash ./get_access_token.sh
```

In this case, the steps taken are:

- 1: The VP is created with the VC and the user's did key.
- 2: The VP is signed with the user's private key.
- 3: The VP is exchanged with the data space Verifier.
- 4: The Verifier checks the validity of the VP.
- 5: The response token issued by the Verifier is stored if successful.

### 3º: Access to Broker data (Orion-LD)

With the access token issued by the Verifier, data can be requested from the Orion-LD Broker through APISIX. This component is responsible for protecting the data space services to limit their use only to participants who can make use of them. Below is an example of a query to APISIX to request data from Orion-LD. Two sample queries have been created. The first does not have a valid token to access the service, and the second does. The APISIX responses are described below:

#### 3.1º: Invalid query

This query to APISIX does not contain a token issued by the Verifier, which generates an authentication error:

```sh
export TOKEN=1234
curl -G 'https://mp-data-service.pgtec-vrain-dataspace.eu/ngsi-ld/v1/entities'   -H "Authorization: Bearer ${TOKEN}"   -H 'Accept: application/ld+json'   -H 'Link: <https://uri.etsi.org/ngsi-ld/v1/ngsi-ld-core-context-v1.8.jsonld>; rel="http://www.w3.org/ns/json-ld#context"; type="application/ld+json"'   --data-urlencode 'type=WeatherStation'
```

The answer is as follows:

<html>
<head><title>401 Authorization Required</title></head>
<body>
<center><h1>401 Authorization Required</h1></center>
<hr><center>openresty</center>
<p><em>Powered by <a href="https://apisix.apache.org/">APISIX</a>.</em></p></body>
</html>

#### 3.2º Valid query

This query to APISIX contains the token issued by the Verifier in section 2, so the response is successful:

```sh
export TOKEN=$(cat ./wallet-identity/vp.jwt)
curl -G 'https://mp-data-service.pgtec-vrain-dataspace.eu/ngsi-ld/v1/entities'   -H "Authorization: Bearer ${TOKEN}"   -H 'Accept: application/ld+json'   -H 'Link: <https://uri.etsi.org/ngsi-ld/v1/ngsi-ld-core-context-v1.8.jsonld>; rel="http://www.w3.org/ns/json-ld#context"; type="application/ld+json"'   --data-urlencode 'type=WeatherStation' --data-urlencode 'limit=1' --data-urlencode 'attrs=precipitation,temperature,latitude,longitude' | jq
```

The answer is as follows:

```json
[
  {
    "id": "urn:ngsi-ld:WeatherObserved:AVAMET:c11m148e01",
    "type": "WeatherStation",
    "latitude": {
      "type": "Property",
      "value": 39.498399,
      "observedAt": "2026-02-24T12:30:00.000Z"
    },
    "longitude": {
      "type": "Property",
      "value": -0.59539,
      "observedAt": "2026-02-24T12:30:00.000Z"
    },
    "precipitation": {
      "type": "Property",
      "value": 0,
      "observedAt": "2026-02-24T12:30:00.000Z",
      "unitCode": "l/m2"
    },
    "temperature": {
      "type": "Property",
      "value": 20.5,
      "observedAt": "2026-02-24T12:30:00.000Z",
      "unitCode": "CEL"
    },
    "@context": [
      "https://uri.etsi.org/ngsi-ld/v1/ngsi-ld-core-context-v1.8.jsonld",
      "https://uri.etsi.org/ngsi-ld/v1/ngsi-ld-core-context-v1.7.jsonld"
    ]
  }
]
```

APISIX has validated the access token and allows data to be requested from Orion-LD.

### Current Status

Keycloak and Verifier are fully integrated and have operational ODRL access policies for operator profiles. The system is currently in the process of extending governance rules, with additional granular policies being deployed for new users and roles while maintaining technical validation of VCs and VPs as a basic trust criterion.

Furthermore, access via the [EUDI Wallet](https://ec.europa.eu/digital-building-blocks/sites/spaces/EUDIGITALIDENTITYWALLET/pages/694487738/EU+Digital+Identity+Wallet+Home) is being implemented so that the process does not have to be performed manually from the command line.

## License

Distributed under the AGPL-3.0 License. See `LICENSE` for more information.

<!-- CONTACT -->

## Contact

Project Link: [https://github.com/PGTEC-VRAIN](https://github.com/PGTEC-VRAIN)
