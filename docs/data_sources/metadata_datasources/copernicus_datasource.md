# Copernicus
The **Copernicus** programme is a project coordinated and managed by the **European Commission**, which aims to achieve a comprehensive, continuous and autonomous **high-quality** Earth observation capability, the results of which are freely accessible to the scientific community, authorities and individuals.  

The overall objective is to provide accurate, reliable and continuous information in order to, among other things, improve environmental management and conservation, understand and mitigate the effects of climate change, and ensure civil security. 

It aims to bring together **different sources** of information from environmental satellites and ground-based stations to provide a global view of the Earth's ‘state of health’. 

To this end, Copernicus has **two** sites where the different data it collects can be accessed:

- Climate Data Store (CDS): A tool for accessing more than 140 data sets with information on the state of our climate around the world over the last 100 years. 

- Atmosphere Data Store (ADS): A tool for accessing more than 100 data sets with satellite data from around the world and over the last 100 years. 

The data sets presented are as follows:

- ERA5-Land hourly data from **1950** to the **present**. 

- RA5 hourly data from **1940** to the **present**. 

 
## API
The CDS, developed within the framework of the European Commission's Copernicus programme, makes a wide range of climate and atmospheric data available to the public. To access this information, the CDS API, called **cdsapi**, is mainly used, which is designed for use in Python. 

The API usage flow is simple and combines both the web interface and script automation: 

- **Data selection on the website:** From the Climate Data Store web portal, users can browse more than 140 available datasets, as well as more than 100 offered by the Atmosphere Data Store. Each dataset has filters to specify variables, time intervals, spatial resolution, and output format. 

- **Automatic script generation:** Once the desired parameters have been selected, the platform automatically generates a Python script that uses the cdsapi library. This script can be run locally to download data, facilitating reproducibility and automation of the process. 

- **Download via API:** The cdsapi library manages the connection to the CDS servers, authenticates the user's request, and downloads the selected files in the specified format (e.g., NetCDF or GRIB). 

The API has a large amount of data available. For example, for the ERA5 hourly data set from **1940** to the **present** available from the Climate Data Store, we can download a large amount of data: **temperature** at different levels and soil types, wind, radiation, heat, clouds, lakes, water evaporation, **precipitation** and rain, snow, soil, vertical integrals, vegetation, and waves. 

Regarding **real-time** data, it should be noted that for the data sets analysed, the most recent data is from **6 days** prior to the **current** day. The update time is daily, so each day that passes, data from day **t-6** is added, where t is the current day.  

With regard to **historical data**, ERA 5 and ERA5-Land have records dating back to **1940**, providing data from almost 85 years ago. Figure 12 shows the years of data available for the ERA5 data set. 

<!-- ??? info "More information"
    To access the data, the first step is to register on the [Climate Data Store](https://cds.climate.copernicus.eu/) to obtain the **API Key**. 

    Once you have obtained the API Key, the usual way to request data is through the **CDS website** itself. Once you have selected the dataset in CDS, a menu will open with the download option.

    Once we have the script and the API KEY, the data is downloaded using the CDSAPI package available in Python. This package can be easily downloaded with the Python package installer (PIP) or in an Anaconda environment with (conda).  -->