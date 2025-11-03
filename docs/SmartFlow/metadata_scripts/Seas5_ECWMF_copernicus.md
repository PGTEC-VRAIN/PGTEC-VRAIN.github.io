# Model Seas5  - Europe Centre Medium Weather Forecasts (ECMWF)

This section describes the data integration process of Seas5 model from Copernicus.

- `Seas5_ECWMF_copernicus.py`: Python script that retrieves weather data from the Open-Meteo API programamatically using airflow sintaxis.

  - **Data**: processes it into a standardized format using `WeatherForecastSeries.py` Smart Data Model. 

  - **Raw Data**: The input data are JSON files. The variables we are currently using are:
    - Temperature 
    - Precipitation
    - Wind Speed
    - Solar Radiation

  - **API Key**: No API key is required for execution as we are downloading public data from Open-Meteo API.

  - **Run script**: Run hourly to ensure the latest forecasts are always retrieved and processed.

The last two scrips retrieve data from Copernicus Climate Data Store (CDS) API and Early Warning Data Store (EWDS):
