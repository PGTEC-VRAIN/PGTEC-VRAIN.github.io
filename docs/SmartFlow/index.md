---
icon: material/sync
title: Information
hide:
  - toc
---

<script>
    // Hide sidebar. This script is only executed in the data sources page.
    document.addEventListener('DOMContentLoaded', function () {
        const sidebar = document.querySelector('.md-sidebar--secondary');
        if (document.querySelector('.catalog-header') && sidebar) {
            sidebar.style.display = 'none';
            sidebar.style.width = '0';
            sidebar.style.padding = '0';
            sidebar.style.margin = '0';
        }
    });
</script>

# Overview

This repository is part of the tasks developed within the **PGTEC** project. Its main objective is to describe and provide the infrastructure required to deploy a data space using FIWARE technologies, offering a detailed and easy-to-follow guide adaptable to different environments.

This repository specifically contains the Python scripts used to:

- Retrieve data from multiple climate data sources such as AEMET, CHJ, Open-Meteo, and Copernicus.

- Convert the raw data into **FIWARE Smart Data Models** to standardize the format.

- The creation of automated Airflow DAGs for pipeline execution.

- The creation of FastAPI scripts to provide data as a service neede to provide a dashboard where users select the data sources to run TETIS model (Hydrological model from IIAMA-UPV) 

<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#about-the-project">About The Project</a>
      <ul>
        <li><a href="#built-with">Built With</a></li>
      </ul>
    </li>
    <li>
      <a href="#getting-started">Getting Started</a>
      <ul>
        <!--<li><a href="#prerequisites">Prerequisites</a></li>-->
        <!--<li><a href="#cheatsheet">Cheatsheet</a></li>-->
      </ul>
    </li>
    <li><a href="#usage">Usage</a></li>
    <!--<li><a href="#roadmap">Roadmap</a></li>-->
    <!--<li><a href="#contributing">Contributing</a></li>-->
    <li><a href="#license">License</a></li>
    <li><a href="#contact">Contact</a></li>
    <li><a href="#references">References</a></li>
  </ol>
</details>

This README provides an overview of the project’s purpose, setup instructions, usage examples, and references for further development.

<!-- ABOUT THE PROJECT -->
# About The Project

Its main objective is to describe and provide the infrastructure required to deploy a data space using <a href="https://www.fiware.org/">FIWARE</a> technology, offering a detailed and easy-to-follow guide for different environments.

This repository is part of the tasks developed within the <a href="https://pgtec.webs.upv.en/">PGTEC</a> project. Its main objective is to describe and provide the infrastructure required to deploy a data space using  <a href="https://www.fiware.org/">FIWARE</a> technologies, offering a detailed and easy-to-follow guide adaptable to different environments.

The goal of PGTEC is to build a data platform that periodically retrieves historical and forecasted climate and weather data from multiple APIs, standardizes them using Smart Data Models, and stores them in a FIWARE Context Broker with historical persistence — enabling the development of machine learning and deep learning models.

This repository specifically contains the Python scripts used to:

- Retrieve data from multiple climate data sources such as AEMET, CHJ, Open-Meteo, and Copernicus.

- Convert the raw data into FIWARE Smart Data Models to standardize the format.

- The creation of automated Airflow DAGs for pipeline execution.


## Built With

The project is built using the following main components:

| | | | |
|:-------------------------------------------:|:--------------------:|:-------------------:|:---------------------:|
| [![Python][Python]][Python-url] | [![Airflow][Airflow]][Airflow-url] | [![Smart-data-models][Smart-data-models]][Smart-Data-models-url] | [![Docker][Docker]][Docker-url] |


<!-- GETTING STARTED -->
# Getting Started 

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

# Data Sources Overview

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
# Usage

This is an example to use the environment using the scripts to download data and convert to Smart Data Models format:

To fill...
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
# License

Distributed under the AGPL-3.0 License. See `LICENSE` for more information.

<!-- CONTACT -->
# Contact

Project Link: [https://github.com/PGTEC-VRAIN](https://github.com/PGTEC-VRAIN)


<!-- References -->
# References

* [Readme Template](https://github.com/othneildrew/Best-README-Template)
* Smart Data Models [Weather Smart Data Model - Fiware](https://github.com/smart-data-models/dataModel.Weather)

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