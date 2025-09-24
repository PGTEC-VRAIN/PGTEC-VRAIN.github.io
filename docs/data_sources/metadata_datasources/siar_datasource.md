# Sistema de Información Agroclimática para el Regadío (SiAR)

[The Agroclimatic Information System for Irrigation (SiAR)](https://www.mapa.gob.es/es/desarrollo-rural/temas/gestion-sostenible-regadios/sistema-informacion-agroclimatica-regadio/presentacion) of the Ministry of Agriculture, Fisheries and Food is a network of **more than 520 weather stations** that captures, records and disseminates agroclimatic data necessary to determine the water demand of irrigated farms. 

The Sub-Directorate General for Irrigation, Natural Roads and Rural Infrastructure of the Ministry of Agriculture has been developing, maintaining and updating SiAR for **more than 20 years**. SiAR is currently the largest source of agroclimatic information provided by both the Ministry and the autonomous communities. 

The SiAR network places special emphasis on maintaining the **high quality** and **accuracy of the data** it provides. 

There are **more than 360 stations** managed by the Ministry and **more than 160 managed** by the autonomous communities. [The SiAR network in the Valencian Community](http://riegos.ivia.es/red-siar) has 55 stations located in irrigated areas. 

## API

SiAR **allows access to all your data via REST API**, provided that the maximum number of requests and the maximum amount of data queried per day and per minute are respected. Each user has different restrictions regarding the maximum number of requests. 


??? info "More information"
    The [technical manual](https://servicio.mapa.gob.es/websiar/ControlesDatosAPI/Manual%20Web%20API%20SiAR%20Versi%C3%B3n%201.0.pdf) for using the SIAR API specifies: 

    "Each web client is restricted in the number of requests it can make throughout a day and within a one-minute interval. Similarly, and for identical reasons, the number of agroclimatic data that can be consulted in a day and in a minute will also be limited" 
    (Ministry of Agriculture, Fisheries and Food [MAPA], 2023, p. 12). 

    To find out about the restrictions, **each user** can check their limitations via the following URL: https://servicio.mapama.gob.es/apisiar/API/v1/Info/Accesos?ClaveAPI={PUT_API_KEY}. When using the API key provided, the SIAR returns a response in JSON format indicating the limitations of API use to the user. The results are:

    - **Maximum number of accesses per minute**: 15

    - **Maximum number of accesses per day**: 240

    - **Maximum number of records per minute**: 100

    - **Maximum number of records per day**: 10,000 

With regard to the amount of **data available**, SIAR allows data to be downloaded at the autonomous community, province and station level for the whole of Spain. For example, there are **41 weather stations in the province of Valencia**. 

The SIAR has been storing data since **1999**, so the time span is **25 years**. This means that historical data is **accessible**. 

With regard to **real-time data**, attempts have been made to download the most recent data for several stations, and the most recent data returned by the API is from **two hours ago**.

The data update times are **not known exactly**. The update time is estimated to be **30 minutes**, given that the finest temporal granularity is every 30 minutes. 

Regarding temporal resolution, the technical manual explains the different granularities for accessing data according to the required time span (hourly, daily, weekly, monthly, etc.). 


??? info "More information"
    The SiAR API is **public**, but you must fill out a form on the website with your personal details and the purpose for which you will use the data. SiAR will then decide whether to accept your request and send you the API key. 

    To access the SiAR REST API, you must use the **key provided after registering** on their [website](https://servicio.mapa.gob.es/websiar/). Registration requires you to provide your personal details (ID number, first name, surname, email address), the organisation you work for and the intended use of the data. 

    Once registered, you will receive an **email with an API key** that you will need to provide in each query to identify yourself. 