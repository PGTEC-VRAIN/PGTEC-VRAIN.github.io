 # Architecture 

## Hourly configuration update internal service

### Cron Job

The hourly service is runned as cronned job. It updates the redis database, which will be used to serve the 10 minute models. 
It follows the following structure.

Extract the last n-days, determined by the IIAMA group, of the precipition observed in a given set of weather stations. 

From this we run the Toparc, Hantec executables, which define a base configuration to run. Once all the parameters are correctly defined, we ran tetis and save the Hantec2 and Sedantec2 files to the rd database. 



## Base Service

### Cron Job

We retrieve the weather forecast of the following day of different weather forecast providers. We retrieve and save the current state of the basin through the redis database. 

We solve each different scenario depending on the weather forecast. And save them to the redis database. 

### API Service

The API retrieves ,through the redis database, and sends the river flow forecasts of all the cells defined. 
