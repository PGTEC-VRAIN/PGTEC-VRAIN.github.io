# AEMET (ROCIO)

The abbreviation **ROCIO** stands for Rejilla Observacional Con Interpolación Óptima (Optimal Interpolation Observation Grid). AEMET has two types of grids to cover all island areas. The first **high-resolution** grid, approximately 5 km, covering mainland Spain and the Balearic Islands is called ROCIO_IBEB, and the second 2.5 km grid covering the Canary Islands is ROCIO_CAN. In both, the daily data on accumulated **precipitation** in 24 hours, **maximum temperature** and **minimum temperature** from a large number of stations of the State Meteorological Agency have been interpolated.   

Therefore, for each grid there are **two** types of data sets available:  

- Precipitation. 

- Maximum and minimum temperatures. 

With regard to the **ROCIO_IBEB** grid, the version 2 precipitation dataset has been generated using all the stations available in the AEMET National Climate Data Bank, i.e. 3,236 rainfall stations. This grid covers the period from **1951** to **2022** and is updated periodically.  

The extreme temperature (maximum and minimum) datasets, version 1, have been generated using all the stations available in AEMET's National Climate Data Bank, **1,800 thermometric** stations. These grids begin in 1951 and are updated until **December 2022**. Unlike the precipitation grid, they use climatology based on historical analyses of the [HIRLAM](https://www.aemet.es/es/idi/prediccion/prediccion_numerica)numerical prediction model operated by AEMET as initial information, or first estimate, which is corrected by observations.  

With regard to the **ROCIO_CAN** grid, the precipitation and temperature datasets have been compiled in the same way as those for ROCIO_IBEB, but with projections using regular coordinates (latitude and longitude) thanks to the use of the [HARMONIE](https://www.aemet.es/es/eltiempo/prediccion/modelosnumericos/harmonie_arome) model. In addition, the data cover the period from 1990 to 2022 but are updated periodically.  

## API
The ROCIO grid data is available on the **AEMET website** and also from the THREDDS server at the University of Cantabria, displayed using the OpeNDAP protocol. This protocol allows access to variables such as precipitation and temperatures (maximum and minimum) on a 20 km grid, covering mainland Spain and the Balearic Islands. The dataset includes **historical series** since **1950** and is not updated in real time, as it consists of interpolated observational data. Therefore, there is no real-time data from the ROCIO grid. As a result, update times are unknown. 
<!-- 
??? info "More information"
    The data is available both on the AEMET website and on the **THREDDS server** maintained by the Santander Climate Data Service. Below are the two ways to access the data:

    **Access from the website:** On the web portal, the data is provided in compressed files in (.tar.gz) format organised by: 

    - Grid (IBEB (Balearic Islands) or CAN (Canary Islands)).

    - Type of variable (precipitation, maximum temperature, minimum temperature).

    - Available years. 

    The file format is **netCDF** or **ASCII**, depending on the variable. The annex shows an image with the directory structure for the Canary Islands grid (ROCIO_CAN), where different versions of the data can be seen. The most recent version includes the updated files. 
 -->
