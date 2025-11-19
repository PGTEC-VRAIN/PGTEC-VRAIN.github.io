---
icon: material/sync
title: Smart Flow
---

## About The Project

This section is part of the tasks developed within the <a href="https://pgtec.webs.upv.es/">PGTEC</a> project. Its main objective is to describe and provide the infrastructure required to deploy a data space using <a href="https://www.fiware.org/">FIWARE</a> technologies, offering a detailed and easy-to-follow guide adaptable to different environments. Specifically, it explains the logic used to download data from multiple sources, transform it into a common language using Smart Data Models, and make it available in two complementary ways:

- **Airflow workflows**: Python scripts that use Airflow logic to automate the execution of data retrieval and transformation tasks, ensuring that climate predictions are periodically processed and ready to use.

- **FastAPI services**: Python scripts built with FastAPI that expose the processed data through RESTful APIs. These services feed a dashboard where users can select the data sources and points of interest required to run the **TETIS hydrological model**. Once the user makes a selection, TETIS automatically triggers the corresponding FastAPI Python scripts described in this section to retrieve and process the climate predictions, which are then used as input for the model’s execution.

This section specifically describes the Python scripts used to:

- Retrieve data from multiple climate data sources such as AEMET, CHJ, Open-Meteo, and Copernicus.

- Convert the raw data into **FIWARE Smart Data Models** to standardize the format.

- The creation of automated Airflow DAGs for pipeline execution.

- The creation of FastAPI scripts to provide data as a service neede to provide a dashboard where users select the data sources to run TETIS model (Hydrological model from IIAMA-UPV)

All the python files are in the <a href="https://github.com/PGTEC-VRAIN/SmartFlow/tree/main/dags">SmartFlow Github Repository</a>

### Built With

The project is built using the following main components:

|                                 |                                    |                                                                  |                                 |
| :-----------------------------: | :--------------------------------: | :--------------------------------------------------------------: | :-----------------------------: |
| [![Python][Python]][Python-url] | [![Airflow][Airflow]][Airflow-url] | [![Smart-data-models][Smart-data-models]][Smart-Data-models-url] | [![Docker][Docker]][Docker-url] |

<!-- GETTING STARTED -->

## Getting Started

To get a local copy up and running follow these simple steps in ubuntu command line:

1. Clone the repo and navigate to the project folder

   ```sh
   git clone https://github.com/PGTEC-VRAIN/SmartFlow
   cd SmartFlow
   ```

2. Initialize docker:

   ```sh
   sudo systemctl start docker
   ```

3. Initialize docker containers
   ```sh
   docker compose up --build -d
   ```

### Airflow Data Sources Overview

This section contains links to detailed explanations of the Python scripts that programmatically download forecasts from different models using Airflow. Specifically, each script description includes:

- The name of the Python file in the <a href="https://github.com/PGTEC-VRAIN/SmartFlow/tree/main/dags">SmartFlow Github Repository</a>

- The data source accessed and the variables of interest

- The Smart Data Model used to standardize the data

- The required API key (if applicable)

- The suggested execution frequency to keep the data up to date

<div class="grid cards cols-5" markdown>

- :material-weather-cloudy: **[HARMONIE/AROME- AEMET](metadata_scripts/Harmonie_AEMET.md)**

- :material-weather-sunny: **[ARPEGE – OpenMeteo](metadata_scripts/ARPEGE.md)**

- :material-water: **[DWD_ICON – OpenMeteo](metadata_scripts/DWD_ICON.md)**

- :material-alert: **[AIFS_ECMWF – OpenMeteo](metadata_scripts/AIFS_ECMWF.md)**

- :material-alert: **[GEPS_ENS_CNC – OpenMeteo](metadata_scripts/GEPS_ENS_CNC.md)**

- :material-alert: **[GFS_NOAA – OpenMeteo](metadata_scripts/GFS_NOAA.md)**

- :material-alert: **[IFS9km_ECMWF – OpenMeteo](metadata_scripts/IFS9km_ECMWF.md)**

- :material-alert: **[Seas5_ECMWF – OpenMeteo](metadata_scripts/Seas5_ECWMF_copernicus.md)**

- :material-alert: **[EFAS – Copernicus](metadata_scripts/EFAS.md)**

- :material-alert: **[EFFIS – Copernicus](metadata_scripts/EFFIS.md)**

</div>

<!--
### Prerequisites

These are the necessary requirements to be able to execute the project:

|                    Software                              | Version / Notes |
| --------------------------------------------------------:|:------- |
| [Python](https://www.python.org/) | 3.x.x  |
| [Airflow](https://airflow.apache.org/) | 2.x  |


### Cheatsheet

* Python (Recommended to create an environment from anaconda / miniconda)
  ```bash
    # Download Miniconda installer (Linux x86_64)
    wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda.sh

    # Run the installer
    bash ~/miniconda.sh

    # Follow the prompts (accept license, choose install path, initialize conda)

    # Initialize conda for bash
    source ~/.bashrc

    # Create a project environment (Python 3.12.3)
    conda create -n pgtec_env python=3.12.3 -y
    conda activate pgtec_env
  ```

<p align="right">(<a href="#readme-top">back to top</a>)</p>

-->

<!-- USAGE EXAMPLES -->

## Usage

This section describes how to run and test the main components of the PGTEC platform — the Airflow workflows for data processing and the FastAPI services for data delivery and dashboard integration. Both components can be deployed together using the provided Docker Compose environment.

It is supposed that the enviroment has been cloned following the instructions of Getting Started section.

### 1. Running Airflow Workflows

The Airflow DAGs automate the process of retrieving and transforming climate and hydrological data from different sources (AEMET, CHJ, Open-Meteo, Copernicus...).

🧩 Steps

1.1 Start the containers:

```sh
docker-compose up -d
```

The -d option runs the containers in detached mode, hiding Airflow logs and keeping the terminal clean.

##### 1.1. Access the Airflow web interface:

👉 http://localhost:8080

##### 1.2. Enable the DAGs:

Inside the Airflow UI, activate the desired workflows (e.g., AEMET_HARMONIE_AROME, AIFS_ECMWF, etc.).

##### 1.3. Monitor execution:

You can visualize the data extraction and transformation progress directly in the DAG view.

Below is an example of a Python script running in the Airflow user interface, showing the logs of its execution:

![Airflow DAG example](images/airflow_running.png){ width="900" align="center" }

In the screenshot, the DWD_ICON.py workflow is being executed. In just 4.04 seconds, it retrieves several points of interest from the Valencian Community and stores them using the WeatherForecastSeries Smart Data Model format.

### 2. Running FastAPI scripts.

The FastAPI services expose the processed data as REST APIs, allowing other applications — such as the TETIS dashboard — to access the latest standardized data stored in the FIWARE Context Broker.

Each service corresponds to a specific data source or Smart Data Model and can be easily extended to include new ones.

🧩 Steps

##### 2.1. Make sure the Docker environment is running:

```sh
docker-compose up -d
```

##### 2.2. Access the FastAPI documentation:

👉 http://localhost:8000/docs

This interface allows you to explore and test all available endpoints interactively.

##### 2.3. Test an endpoint:

For example, you can retrieve the latest weather forecast data by calling:

```sh
GET /weather?source=AEMET&variable=temperature
```

###### 2.4 Integration with the TETIS dashboard:

The FastAPI services feed the TETIS dashboard, allowing users to select:

- The data sources (e.g., AEMET, DWD, ECMWF)

- The points of interest (catchments, stations, or coordinates)

Once the user selects these options, TETIS automatically triggers the corresponding API calls — which execute the same Python scripts described in the SmartFlow section — to retrieve and process the forecast data used as inputs for hydrological simulations.

📁 Example folder structure

```text
SmartFlow/FastAPI/
├── main.py           # FastAPI entry point
├── routes/
│   ├── AEMET.py      # Endpoints for WeatherObserved / Forecast data
│   ├── DWD_ICON.py   # Endpoints for CHJ flow data
│   └── ...
└── models/
    ├── AEMET.py
    └── DWD_ICON.py
```

🧠 Tip: You can add new endpoints easily by creating a new Python file in the routes/ folder and registering it in main.py.

<!-- ROADMAP
## Roadmap

- [x] Add Changelog
- [x] Add back to top links
- [ ] Add Additional Templates w/ Examples
- [ ] Add "components" document to easily copy & paste sections of the readme
- [ ] Multi-language Support
    - [ ] Chinese
    - [ ] Spanish

See the [open issues](https://github.com/othneildrew/Best-README-Template/issues) for a full list of proposed features (and known issues).

<p align="right">(<a href="#readme-top">back to top</a>)</p>
-->

<!-- CONTRIBUTING
## Contributing

Contributions are what make the open source community such an amazing place to learn, inspire, and create. Any contributions you make are **greatly appreciated**.

If you have a suggestion that would make this better, please fork the repo and create a pull request. You can also simply open an issue with the tag "enhancement".
Don't forget to give the project a star! Thanks again!

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request
-->
<!---
### Top contributors:

<a href="https://github.com/othneildrew/Best-README-Template/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=othneildrew/Best-README-Template" alt="contrib.rocks image" />
</a>

<p align="right">(<a href="#readme-top">back to top</a>)</p>

-->

<!-- LICENSE -->

## License

Distributed under the AGPL-3.0 License. See `LICENSE` for more information.

<!-- CONTACT -->

## Contact

Project Link: [https://github.com/PGTEC-VRAIN](https://github.com/PGTEC-VRAIN)

<!-- References -->

## References

- [Readme Template](https://github.com/othneildrew/Best-README-Template)
- Smart Data Models [Weather Smart Data Model - Fiware](https://github.com/smart-data-models/dataModel.Weather)

<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->

[Python]: https://img.shields.io/badge/python-3.12.11+-blue.svg?logo=python&logoColor=white
[Python-url]: https://www.python.org/
[Airflow]: https://img.shields.io/badge/airflow-3.0.6-green.svg?logo=apacheairflow&logoColor=white
[Airflow-url]: https://airflow.apache.org/
[Smart-data-models]: https://img.shields.io/badge/SmartDataModels-purple.svg
[Smart-Data-models-url]: https://github.com/smart-data-models/dataModel.Weather
[Docker-url]: https://www.docker.com/
[Docker]: https://img.shields.io/badge/docker-44.4.3+-red.svg?logo=python&logoColor=white
