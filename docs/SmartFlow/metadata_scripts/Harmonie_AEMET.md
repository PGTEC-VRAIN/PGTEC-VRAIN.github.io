# Model HARMONIE/AROME - AEMET

This section describes the AEMET data integration process.

- `AEMET_HARMONIE_AROME.py`: Python script that retrieves weather forecast data from the AEMET website and processes it programatically using airflow sintaxis

  - **Data**: All the data is processed into a standardized format defined by the `WeatherForecastSeries.py` Smart Data Model. The variables we are currently using are:
    - Temperature 
    - Precipitation
    - Wind Speed 

  - **Raw Data**: The input data are GeoTIFF (.tif) files containing weather variables encoded as color values. Using a color scale provided by AEMET, the script converts these color codes (RGBA) into real physical values such as temperature, wind speed, and precipitation.

  - **API Key**: No API key is required for execution as we are downloading public data from AEMET website.

  - **Run script**: Run hourly to ensure the latest forecasts are always retrieved and processed.

[⬅️ Back to overview](../index.md)