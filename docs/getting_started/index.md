---
icon: material/rocket-outline
title: Getting started
---

## Getting Started

This section is the entry point to PGTEC for anyone who has never heard about the project before.

The goal of this guide is to answer three basic questions:

1.  <strong>What is PGTEC?</strong>
2.  <strong>What does PGTEC offer?</strong>
3.  <strong>How can I join the PGTEC data space?</strong>

### Who is this documentation for?

PGTEC documentation is meant for different types of users:

- Public authorities and emergency management teams interested in accessing harmonised climate and hydrological information.
- Researchers and technical partners who want to reuse PGTEC data for modelling, analytics or decision-support systems.
- Developers and integrators who want to deploy connectors, data pipelines or services using PGTEC building blocks.

If you are in at least one of these groups, the following pages will guide you step by step.

### Organization of the guide

The guide follows this points:

1. [What is PGTEC?](what_is_pgtec.md)  
   An overview of PGTEC as a climate and weather data space, its objectives and main components.

2. [Data and Services](data_and_services.md)  
   A guided tour of the data sources and services that PGTEC exposes, and how they are prepared using the PGTEC data pipeline and Smart Data Models.

3. [Join the Data Space](join_data_space.md)  
   A high-level description of how organisations will be able to connect to PGTEC, request access and deploy a data space connector.

The following sections have more detailed information:

- [Data Sources](../data_sources/index.md) explains the different climate and hydrological sources used in the project and how they are integrated.
- [Data Flow](../pipeline/index.md) describes the end-to-end pipeline from raw data to context information stored in a FIWARE Context Broker.
- [Smart Data Models](../SmartDataModels/index.md) introduces the harmonised data models used to represent climate, hydrological and risk entities.
- [SmartFlow](../SmartFlow/index.md) explains how the Airflow and FastAPI components orchestrate data retrieval, transformation and exposure as services.
- [Decentralized Identifiers](../DID/index.md) presents how self-sovereign identity and DIDs are used to identify entities inside the data space.

!!! Tip "More details"

    If you just want a high-level understanding, reading this Getting Started section is enough.  

    If you plan to deploy infrastructure or contribute data, you will probably want to follow all the links to the detailed sections.