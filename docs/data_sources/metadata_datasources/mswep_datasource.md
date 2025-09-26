# MSWEP
Multi-Source Weighted-Ensemble Precipitation (MSWEP) is a **high-resolution** global **precipitation** dataset. It does not include variables such as temperature, humidity, etc. Its main feature is that it combines or merges different types of data sources to obtain the most accurate and reliable rainfall estimate possible. The amount of precipitation is expressed in **mm/3h**. It is not an instantaneous precipitation rate. To obtain daily values, the eight 3-hour intervals that make up a day must be added together. To obtain average hourly rates, the 3-hour value would be divided by three.  

The data is obtained through: 

- Data from land-based weather stations. 

- Satellite estimates (including oceans and remote areas). 

- Climate reanalysis data (atmospheric models that reconstruct past climate). 

By merging each source, MSWEP is able to correct for the weaknesses of each source individually.  

 
## API
MSWEP does **not** offer an API to which requests are made in real time. Instead, access to data is managed through standard protocols and formats for handling large scientific data sets, mainly through files. 

As mentioned above, the only data it contains is **precipitation**. It is presented as the amount of rainfall over a 3-hour period, measured in millimetres (mm).  

There are two versions of the data: 

- **Near-Real-Time (NRT):** updated with a delay of approximately 3 to 12 hours.  

- **Research version:** this is a corrected and more accurate version that is updated with a delay of several months. 

One of its features is full access to the **historical record**. Data is available from **1979** to the **present**, allowing for the analysis of trends, past extreme events, and the training of models with a very solid database. 

Access to MSWEP data is **public** for research and educational purposes. To access it, please contact MSWEP:

- If you are affiliated with a commercial entity and would like to try MSWEP, please fill out the [application form](https://www.gloh2o.org/contact/).  

- If you do not have a commercial affiliation and intend to use the product for non-commercial purposes, please use the [Apply here form ](https://www.gloh2o.org/mswep/) in the Data licence section. Once you have completed the form, you will receive a link to the shared Google Drive folder once your request has been approved. 

<!-- ??? info "More information"
    Once you have access to the **Google Drive** repository, there are three folders with data for the following date ranges: 

    - **Past_nogauge:** contains data from 1 January 1979 at 12:00 to 23 September 2007 at 06:00. 

    - **Past:** contains data from 28 January 1979 at 09:00 to 25 December 2020 at 06:00. 

    - **Near real time (NRT): **contains data from 25 November 2020 at 18:00 to the present day. 

    There are several options for downloading the data:

    - **Direct download: **once you have access to the repository on Google Drive, you can download the data files directly, organised by year and frequency (3 hours, daily, monthly).    

    - **Programmatic download (rclone):** to acquire the complete historical record or automate downloads, the official documentation recommends the use of tools such as rclone, which allows local directories to be synchronised with cloud storage.  

    - **Remote access (OPeNDAP): **data centres, such as the Integrated Climate Data Centre (ICDC) at the University of Hamburg, host replicas of MSWEP and provide access via the OPeNDAP protocol. Access to the data is restricted; you must contact them and request a customer account.  -->