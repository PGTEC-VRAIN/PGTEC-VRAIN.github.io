## Overview
### Identities and verifiable credentials

The PGTEC Data Space needs a reliable way to identify organisations, services and technical components that participate in it. This identity layer is the foundation for governance, access control and auditability.

This page describes, at a high level, how identities and verifiable credentials are used in the data space. For concrete details on the DID formats and how to generate them with Docker, see [Decentralized identifiers](did.md).

### Roles in the Data Space

From the point of view of identity and access, the main roles in the PGTEC data space are:

- <strong>Data Space operator</strong>   
  Manages the core services of the data space, defines governance rules and operates shared infrastructure.

- <strong>Data Provider</strong>   
  Publishes climate, hydrological or risk-related data into the data space using agreed information models and interfaces.

- <strong>Data Consumer</strong>   
  Accesses data and services from the data space for visualisation, modelling, decision support or research.

- <strong>Service Provider</strong>  
  Offers applications or analytical services that run on top of PGTEC data (for example, early warning tools or hydrological simulations).

- <strong>Technical integrator</strong>     
  Develops and operates connectors, pipelines or adapters that link external systems to the data space.

Each organisation can hold one or more of these roles, and the identity and credential system needs to reflect that.

## Decentralized Identifiers in PGTEC

To represent identities in a portable and cryptographically verifiable way, PGTEC uses decentralized identifiers (DIDs). A DID:

- Is a URI-like identifier that is globally unique and persistent
- Resolves to a DID document containing public keys and service endpoints
- Is not tied to a single central registry or certificate authority

In PGTEC experiments, two DID methods are used:

- <strong>did:web</strong>, which binds identities to existing web domains and HTTPS infrastructure
- <strong>did:key</strong>, which derives identifiers directly from public keys and is convenient for tests and internal services

The practical details of did:web and did:key, including Docker-based helpers, are described in [Decentralized identifiers](./did.md).

## Verifiable Credentials

On top of DIDs, the data space uses verifiable credentials to express claims about identities in a standardised way.

A verifiable credential typically contains:

- An issuer identifier (the DID of the entity that issues the credential)
- A subject identifier (the DID of the entity the credential talks about)
- A set of claims (for example, roles, permissions or attributes)
- Cryptographic proofs that allow any verifier to check authenticity and integrity

Verifiable credentials are designed to be:

- Machine-readable and interoperable between systems
- Selective, so that holders can disclose only what is necessary
- Verifiable without contacting the issuer each time, using public keys published in DID documents

### Example credential types in PGTEC

In the context of the PGTEC data space, typical credential types include:

- <strong>Membership and Role Credentials</strong>     
  State that a given organisation is a recognised data provider, data consumer or service provider in PGTEC.

- <strong>Data Access Credentials</strong>     
  Grant the holder the right to access specific categories of data, spatial domains, temporal ranges or service endpoints.

- <strong>Connector Atestation Credentials</strong>     
  Describe a deployed connector or technical component, including its operator, capabilities and compliance with PGTEC policies.

- <strong>Delegation Credentials</strong>   
  Allow an organisation to delegate certain rights or actions to another organisation or to a specific technical component.

The precise schemas for these credentials can evolve as the data space matures, but they all follow the same basic pattern of issuer, subject, claims and proof.

### Credential Lifecycle 

The identity and credential model follows a simple lifecycle:

1. <strong>Registration</strong>     
   An organisation or component is identified and onboarded into the data space. The operator verifies its identity and assigns an initial DID.

2. <strong>Issuance</strong>     
   The operator or another trusted issuer creates and signs verifiable credentials that describe the roles and rights of that subject.

3. <strong>Storage</strong>     
   The holder stores the credentials in a secure wallet or internal system, under its control.

4. <strong>Presentation</strong>     
   When accessing data or services, the holder presents one or more credentials to prove that it has the required roles or permissions.

5. <strong>Verification</strong>     
   The receiving service (verifier) checks the proofs on the credentials, validates the issuer’s DID document and applies its local access policies.

6. <strong>Revocation and update</strong>     
   Credentials can be revoked or replaced if roles change, access is withdrawn or errors are found.

### Using identities and credentials for access control

In the PGTEC data space, services use identities and credentials to make access decisions. A typical pattern is:

- Authenticate the caller using its DID and cryptographic material
- Request verifiable credentials that prove specific roles or attributes
- Evaluate those credentials against local policy (for example, “only holders of a valid data-provider credential for region X can publish entities in this context”)
- Grant or deny the requested operation based on the result

This approach allows:

- Fine-grained access control that is independent of any single platform
- Explicit governance rules encoded in credentials and policies
- Better traceability of who accessed what, under which authorisation

## Current status 

The identity and credential layer in PGTEC is being developed progressively:

- DIDs and DID documents are used in experimental setups to model participants and services.
- Docker-based tools are provided to generate DIDs from existing keys and certificates.
- The verifiable credential schemas and onboarding workflows are being refined based on project requirements.

As the data space moves towards a more operational state, the processes described in [Join data space](../getting_started/join_data_space.md) will rely increasingly on this identity and credential model to onboard, manage and audit participants in a scalable way.