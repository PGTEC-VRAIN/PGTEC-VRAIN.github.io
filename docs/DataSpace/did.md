## Decentralized Identifiers

In the PGTEC data space, decentralized identifiers (DIDs) are used to represent identities in a portable and cryptographically verifiable way. They are especially useful to identify organisations, services or components without relying on a single central authority.

This page gives a practical introduction to DIDs and shows how to generate did:web and did:key identifiers using Docker, as used in the PGTEC experiments.

For a higher-level description of how identities and credentials are used in the data space, see the page on identities and verifiable credentials in the Data Space section.

## What is a DID?

A decentralized identifier (DID) is a URI-like identifier that is:

- Globally unique and persistent
- Bound to one or more public keys
- Resolvable to a DID document, which is a JSON file containing public keys (for authentication and verification) and service endpoints (for communication).

A DID has three parts:

- The scheme, always `did:`
- The DID method name
- The method-specific identifier

For example, in:

```text
did:web:example.com

## did:web method
The did:web method leverages existing web infrastructure, specifically HTTPS and Domain Name System (DNS), to create and resolve DIDs.

A did:web DID is constructed directly from a domain name (and optional path), making it highly readable and familiar. For example: ```did:web:example.com```

Resolution: The DID document is hosted on the corresponding web server at a *well-known* location like this: ```https://example.com/.well-known/did.json```

## did:key method
The did:key method is the simplest form of DID, as the identifier is directly derived from a cryptographic public key.

The DID method-specific identifier is an encoded representation of the public key material. For example: ```did:key:z6MkjBWPPa1njEKygyr3LR3pRKkqv714vyTkfnUdP6ToFSH5```

Resolution: The DID document can be generated entirely from the DID string itself without requiring any external network lookup. It is self-contained.

## Automated setup with Docker

We use a docker image to create the DIDs from a key pair and a certificate.

We can create the key pair and the certificate like this:

```sh
mkdir example

# Create a key pair.
openssl ecparam -genkey -name prime256v1 -noout -out example/key-pair.pem

# That can be read like this:
openssl ec -in example/key-pair.pem -text -noout

# Create a self-signed certificate from the key pair.
openssl req -x509 -new -key example/key-pair.pem -out example/cert.pem -days 365 -nodes

# That can be read like this:
openssl x509 -in example/cert.pem -text -noout
```

### did:web setup

Once we have the certificate associated to our key pair we can generate the did.json running a docker container:

```sh
docker run -p 8080:8080 -v ./example/cert.pem:/certs/tls.crt -it mortega5/did-helper:0.0.1 -didType web -hostUrl example.com -outputFormat json_jwk -certPath /certs/tls.crt
```

This will print out the contents of a JSON file. That content should be accessible from ```example.com/.well-known/did.json``` if we are using a home page like example.com.

If we want to use a deep link we have to run the docker container with the full link:

```sh
docker run -p 8080:8080 -v ./example/cert.pem:/certs/tls.crt -it mortega5/did-helper:0.0.1 -didType web -hostUrl example.com/specific/page -outputFormat json_jwk -certPath /certs/tls.crt
```

And make the JSON that it prints accessible from ```example.com/specific/page/did.json```. The idintifier in this case would be did:web:example.com:specific:page

### did:key setup

Once we have the certificate associated to our key pair we can generate the did:key and did.json by running a docker container:

```sh
docker run -p 8080:8080 -v ./example/cert.pem:/certs/tls.crt -v ./example/key-pair.pem:/certs/tls.key -it mortega5/did-helper:0.0.2 -didType key -certPath /certs/tls.crt -keyPath /certs/tls.key
```

If we get the error ```exec /did-helper/did-helper: exec format error``` we have to run:

```sh
docker run --rm --privileged multiarch/qemu-user-static --reset -p yes
```

before rerunning the docker.

We don't need to host the did:key's did.json anywhere. We just use out identifier and use out private key (stored in example/key-pair.pem) to prove we are the holders of that did:key.


## License

Distributed under the AGPL-3.0 License. See `LICENSE` for more information.

<!-- CONTACT -->

## Contact

Project Link: [https://github.com/PGTEC-VRAIN](https://github.com/PGTEC-VRAIN)