# Overview

There are two models:

- An hourly model that determines the current state of the basin. Its input is the weather observed of the last 5 days. Its output are the parameters that define the current state of the system. This will be used in the next model.
- A 10 minute model that will give a forecast of the following 24 hours. Its input is the current state of the system and the precipitation forecast of the following 24 hours. Its output are the river flow rates of the basin with a 10 minute time interval.
