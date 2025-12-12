---
icon: material/hub
title: Data Space
---
## PGTEC Data Space

The PGTEC data space is a climate and hydrometeorological data space designed to share information between organisations in a governed and interoperable way. It is not just a file repository, but an infrastructure where data, models and services can be exchanged under clear rules for access and quality.

This section explains the role of the data space inside the project and serves as an entry point to the rest of the technical documentation.

### What is the PGTEC data space?

The PGTEC data space connects organisations that:

- Produce climate, hydrological and meteorological data
- Exploit that data for prediction, risk analysis and early warning services
- Need guarantees about governance, traceability and responsible use of information

Some key principles of the data space are:

- <strong>Semantic interoperability</strong>   
  Data is represented using common information models, based on Smart Data Models, so that different systems can understand each other.

- <strong>Technical interoperability</strong>   
  Data exchange happens through standardised APIs and components, using FIWARE and NGSI technologies.

- <strong>Governance and trust</strong>   
  Participants are identified using cryptographic identifiers and, progressively, verifiable credentials that describe their roles and permissions.

- <strong>Service orientation</strong>   
  Besides raw datasets, the data space exposes processing flows, models and services that can be directly integrated into external applications.

### Main building blocks

The PGTEC data space is built on several functional blocks, each described in its own section:

- <strong>Data Sources and Services</strong>   
  Description of climate and hydrological data providers, their variables, frequency, coverage and usage conditions.  
  See [Data Sources](../data_sources/index.md) and [Data and services](../getting_started/data_and_services.md).

- <strong>Common information models</strong>   
  Shared data models for forecast series, observations and streamflow, based on Smart Data Models.  
  See [Smart Data Models](../SmartDataModels/index.md).

- <strong>Data Flow and processing</strong>   
  Ingestion, normalisation, historical storage and publication of data, implemented with SmartFlow and FIWARE components.  
  See [Data Flow](../pipeline/index.md) and [SmartFlow](../SmartFlow/index.md).

- <strong>Identity, trust and access</strong>   
  The identity layer of the data space, where participants, their identifiers and the credentials that control access are managed.  
  See [Identities and verifiable credentials](identities_and_credentials.md).

### How to use this section?

If you are new to PGTEC and want to understand its data space, a reasonable path is:

1. Read this introduction.  
2. Review the [data space architecture](arquitecture.md) to see the key components and how they interact.  
3. Dive into [identities and verifiable credentials](identities_and_credentials.md) if you are interested in access and trust.  
4. Go to [Join data space](../getting_started/join_data_space.md) to see the planned steps for onboarding as a participant.