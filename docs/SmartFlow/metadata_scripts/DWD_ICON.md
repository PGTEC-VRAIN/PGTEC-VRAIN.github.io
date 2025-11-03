# Model ICON_EU - DWD

This section describes the ICON_EU data integration process.

- `DWD_ICON_EU.py`: Python script that retrieves weather data from the Open-Meteo API programmatically using airflow sintaxis.

  - **Data**: processes it into a standardized format using `WeatherForecastSeries.py` Smart Data Model. 

  - **Raw Data**: The input data are JSON files. The variables we are currently using are:
    - Temperature 
    - Precipitation

  - **API Key**: No API key is required for execution as we are downloading public data from Open-Meteo API.

  - **Run script**: Run hourly to ensure the latest forecasts are always retrieved and processed.

[⬅️ Back to overview](../index.md)
