# Description

The TETIS Model is a hydrological and sediment cycle simulation model, spatially distributed through a subdivision of the basin into regular cells, with physically-based parameters. It is an integral model, meaning that the same model can be used to solve problems related to both Floods and Erosion (time discretization of minutes or hours) and Water Resources (daily time discretization). Furthermore, it has a powerful automatic calibration algorithm for its effective parameters and the initial values of all state variables, which greatly facilitates its practical implementation. For data input and results visualization, it has an interface developed in the Visual Studio environment.

The advantages of distributed modeling over traditional lumped and semi-distributed modeling mainly consist of:

- A better representation of the spatial variability of the phenomena involved in the Hydrological Cycle, through its inputs and parameters.
- Obtaining results at any point in the basin, without predefining them beforehand and without the need for interpolation methodologies.
- The exploitation of all available spatial information, which is increasingly abundant thanks to the development in recent years of digital cartography, geographic information systems, and remote sensing measurements.
