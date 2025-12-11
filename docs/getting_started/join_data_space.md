# Join Data Space
## Join the PGTEC Data Space

This page explains, at a high level, how organisations will be able to participate in the PGTEC data space once the operational environment is in place.

The approach is aligned with other European Data Space initiatives, where access is based on trusted digital identities and the deployment of interoperable data space connectors.

## Participation roles

There are several ways to interact with PGTEC:

- <strong>Data Consumer</strong>    
  An organisation that wants to reuse PGTEC data (for example in dashboards, decision-support tools or research workflows).

- <strong>Data Provider</strong>    
  An organisation that wants to publish its own climate, hydrological or risk-related data into PGTEC using the agreed Smart Data Models.

- <strong>Service Provider</strong>  
  A partner that builds applications on top of PGTEC, such as early warning services, modelling platforms or analytics tools.

The technical and governance requirements will depend on the chosen role.

## What will you need?

To participate in the data space, we required two main elements:

1. <strong>An organisational digital identity</strong>    
   This is often realised as a verifiable credential or digital certificate that uniquely identifies your organisation and its roles inside the data space. Components like VC issuers and Trust Anchors are used to manage these credentials.

2. <strong>A Data Space connector</strong>    
   A software component deployed in your own infrastructure that handles authentication, authorisation and data exchange with the rest of the ecosystem. In FIWARE-based Data Spaces, reference implementations of connectors are available as open source.

PGTEC plans to follow this pattern so that participants can connect using standard, reusable components instead of custom one-off integrations.

## Join

As we said we have different roles to participate into the Data Space, this are the detailed process to join it.

### Joining as a Data Consumer
The detailed access procedure will be defined as the operational environment stabilises, but the expected steps are:

1. <strong>Request access</strong>    
   Contact the PGTEC operators and explain your intended use case. In future iterations this will likely be handled through a dedicated “Request access” page or portal.

2. <strong>Obtain credentials</strong>    
   After validation, your organisation will receive the necessary credentials or configuration to authenticate against the PGTEC Trust Anchor or identity management system.

3. <strong>Deploy or configure a connector</strong>    
   You can either deploy a full data space connector or, for simple read-only scenarios, configure existing components to call PGTEC APIs exposed by the Context Broker and FastAPI services.

4. <strong>Integrate data into your applications</strong>    
   Once access is granted, you can start using PGTEC data for dashboards, models or other tools, following the Smart Data Models described in the documentation.

### Joining as a Data Provider

If you want to contribute data to PGTEC, the process will extend the consumer steps with additional tasks:

1. <strong>Align with Smart Data Models</strong>   
   Map your internal data structures to the Smart Data Models used in PGTEC so that your information can be interpreted consistently.

2. <strong>Implement ingestion logic</strong>   
   Reuse or adapt SmartFlow pipelines or equivalent scripts to pull or receive your data and transform it into PGTEC entities.

3. <strong>Configure your connector as a provider</strong>  
   Set up your data space connector so that it can publish your entities or expose your own Context Broker in a way that is compatible with the PGTEC governance rules.

4. <strong>Agree on policies and terms of use</strong>  
   Define under which conditions your data can be accessed, including licensing, retention and usage constraints.

## Current status

At the current stage of the project, PGTEC is still in an experimental and pre-production phase. This means that:

- Some access procedures may still be manual and based on direct contact with the project team.
- Endpoints, policies and governance details are subject to change as the data space evolves.
- The documentation will be updated as soon as stable connectors, trust services and self-service registration mechanisms are available.

In the meantime, you can already:

- Explore all public documentation in this site.
- Clone and test the [SmartFlow](../SmartFlow/index.md) repository and its Docker environment.
- Review the [Data Sources](../data_sources/index.md) and [Smart Data Models](../SmartDataModels/index.md) sections to prepare your systems for future integration.

If you are interested in participating, the recommended first step is to reach out to the PGTEC coordinators through the contact information provided in the main project website.
