# Model EFAS  - Copernicus

This section describes the data integration process of EFAS model from Copernicus Early Warning Data Store (EWDS).

- `EFAS.py`: Python script that retrieves weather data from the EWDS dataset (https://ewds.climate.copernicus.eu/datasets/efas-forecast?tab=overview) and download data programamatically using airflow sintaxis.

  - **Data**: processes it into a standardized format using `WeatherForecastSeries.py` Smart Data Model. 

  - **Raw Data**: The input data are NetCDF (.nc) files containing the following weather variable:
    - River discharge last 6 hours

  - **API Key**: An API key is required for execution. To get an API key, you need to register on the Copernicus Climate Data Store website: https://cds.climate.copernicus.eu

  - **Run script**: Run this script daily because Copernicus updates the data once a day. It has been configured to automatically detect the latest available forecast.