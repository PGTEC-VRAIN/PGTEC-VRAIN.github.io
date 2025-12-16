[:material-arrow-left: Back to Data Sources](../index.md){ .pg-back-button }

## AEMET (Spain02)
The [Spain02](https://www.aemet.es/es/serviciosclimaticos/cambio_climat/datos_diarios/ayuda/rejilla_20km) dataset is the result of institutional collaboration between the State Meteorological Agency (AEMET) and the Santander Meteorology Group (SMG) at the University of Cantabria-CSIC.  

The dataset consists of a **20 km resolution** grid covering mainland Spain and the Balearic Islands, generated using interpolation techniques based on daily observations at meteorological stations. The aim is to provide a homogeneous and continuous basis of climate information, suitable for regional analyses and climate change impact studies. 

Similar to the ROCIO grid, Spain02 includes **precipitation** and **maximum** and **minimum temperature** series, offering a homogeneous and continuous product over time, suitable for regional analyses, hydrological studies, climate change impact assessments and climate modelling. The availability of multiple interpolation versions and resolutions allows the data to be adapted to different scales of analysis and modelling methodologies, ensuring the robustness of the scientific studies that use them. 

### API
The only way to access the SPAIN02 grid data is through the **THREDDS** data centre, which stores a replica of the data files. This data centre is developed and maintained by the **University of Cantabria**. This server allows you to browse the catalogue of available datasets and, using the **OPeNDAP** (Open-source Project for a Network Data Access Protocol) protocol, remotely query and extract only the necessary variables or subsets, without having to download the entire files. 

Update times are **unknown**. The data files only cover up to the year **2022**, so there is **no real-time** data available. With regard to **historical data**, the data files contain data from **1951** onwards, so there are large volumes of historical data available. 