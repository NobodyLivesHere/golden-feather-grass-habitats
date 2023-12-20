[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.10408812.svg)](https://doi.org/10.5281/zenodo.10408812)

# Habitat Suitability Model for Golden Feather Grass in North America

## Introduction
One of the key consequences of global climate change is the environmental disruptions of organism habitat zones.  For animals such as polar bears and coral reefs, this is widely reported on and studied. For plants, changing habitat boundaries can have far reaching effects due to plants forming the basis for most food chains on the planet. For grasses in particular, their habitat domains can very easily be measured quantitatively and tracked through time.  Thus if the parameters associated with habitability are represented and projected into the future, one may be able to generate a rough forecast of what this may be for that particular space.  

This project aims to do this with a particular grass - Sorghastrum nutans, commonly called yellow Indian grass of Golden Feather Grass- as a means of assessing the habitability of certain US National Grasslands give past, future, and present soil data, climate change forecast models, and DEM satellite data. It aims to also create a generalized template for running the same time of fuzzy matrix analysis over any bounded geodataframe and allows the user to directly edit the configurations to taylor it to their own analysis. 

This document provides a detailed overview of a Python-based habitat suitability model developed for assessing potential habitats of Golden Feather Grass across North America, with a focus on adaptability to changing climatic conditions.

## Model Overview

The model integrates geospatial data processing with fuzzy logic principles, offering a flexible approach to habitat suitability analysis. For the time being, it is a proof of concept only, as it currently is still being debugged.

### Data Input and Processing

- **Study Site Specification**: Users input geographical boundaries for the study area using a GeoJSON file, which guides the spatial focus of the habitat analysis.
- **Data Retrieval**: Based on the study site's coordinates, the model automatically fetches relevant raster datasets, including climate projections, soil characteristics, and elevation.
- **Data Harmonization**: Ensures compatibility of datasets by aligning spatial resolution and coordinate reference systems.
#### Notes on Datasets
- **soils**: Uses the Polaris dataset, which holds a grid-level measurements for a wide vareity of relevant soil properiies and statistics for the Continental United Stae.  For this analysis, we use the mean pH of the soil, but a user can edit the script to retrieve other tiffs as needed. Currently the soil dataset is neceesary to compute any other dataset, as it is used as the reference raster during harmonization. Therefore one would need to make significant changes to the code to remove it from the anlaysis.
- **elevation** Uses the SRTM dataset flown in February of 2000.  Data is feathed using the NASA EArth Appeears API and a valid login will be needed by the user when the model gets to this step. User can edit where the download data is cached to with the JSON file.
- **slope** This value is dervied from the raster created by importing the data downloaded from Apppeears, as such it cannot be computed without this data. Users can edit the save path for the slope.tiff in the JSON file.
- **Climate** From the MACAv2 dataset, user will need to supply a url into the JSON to get this to compute properly. By default, the script is set to take the time averaged montly mean precipitaiton for any given year, in the Kiowa Grassland  this is fromt he histroical dataset for the year 1950.  The Caddo run uses the year 2050 instead under RCP Scenario 4.5. This file is finicky and can sometimes have issues with inconsistent shapes and layers, though most of this has been accounted for in the code.

#### Data Citations
- Chaney, N. W., Wood, E. F., McBratney, A. B., Hempel, J. W., Nauman, T. W., Brungard, C. W., &amp; Odgers, N. P. (2016). Polaris: A 30-meter probabilistic soil series map of the contiguous United States. Geoderma, 274, 54–67. https://doi.org/10.1016/j.geoderma.2016.03.025
- Climate forcings in the MACAv2-METDATA were drawn from a statistical downscaling of global climate model (GCM) data from the Coupled Model Intercomparison Project 5 (CMIP5, Taylor et al. 2010) utilizing a modification of the Multivariate Adaptive Constructed Analogs (MACA, Abatzoglou and Brown, 2012) method with the METDATA(Abatzoglou, 2011) observational dataset as training data.
- Farr, T. G., Rosen, P. A., Caro, E., Crippen, R., Duren, R., Hensley, S., Kobrick, M., Paller, M., Rodriguez, E., Roth, L., Seal, D., Shaffer, S., Shimada, J., Umland, J., Werner, M., Oskin, M., Burbank, D., &amp; Alsdorf, D. (2007). The shuttle radar topography mission. Reviews of Geophysics, 45(2). https://doi.org/10.1029/2005rg000183
- US Department of Agriculture, National Grassland Units. A National Grassland unit designated by the Secretary of Agriculture and permanently held by the Department of Agriculture under Title III of the Bankhead-Jones Farm Tenant Act.

  
### Fuzzy Logic Application

- **Membership Function Configuration**: The model allows users to define fuzzy logic membership functions for each environmental variable in a separate JSON file.
- **Fuzzy Set Generation**: It generates fuzzy sets for each environmental variable, indicating the degree of match between pixel conditions and habitat suitability criteria.
- **Rule-Based Analysis**: A set of user-defined fuzzy logic rules are applied to integrate the fuzzy sets, determining the overall habitat suitability.

### Output

- **Habitat Suitability Map**: The output is a raster map where each pixel value indicates the suitability level for Golden Feather Grass.
- **Export Options**: The map can be exported in various formats for GIS analysis or further research.

## Usage Guidelines

1. **Prepare Study Site Data**: Define the study area's geographical boundaries in a GeoJSON file.
2. **Configure Model Parameters**: Edit the JSON file to set membership functions and fuzzy logic rules.
3. **Run the Model**: Process the data to generate the habitat suitability map.
4. **Interpret Results**: Use the output map to assess suitable habitats for Golden Feather Grass.

## Bugs and Features to Implement

- **Model currently is unable to be projected into a Mercator (UTM) projection for unknown reasons.**  When applying a reproject on any of the datasets including the boundary geodataframe, the data becomes so skewed that it is unusable and cannot be parsed through by the model.
This occurus when the PlateCaree projection is changed to a Mercator projection, which is necessary to properly compute the slope and elevation data. As a result, the values passed to the fuzzy logic model from the downloaded datasets will not proprely compute an output that would reflect reality. The way the code is written allows one to easily excise certain datasets from analysis by removing them or adding them to the json and commenting out relevant sections in the Jupyter Notebook. This will be necessary for further debuggin.
- **Model outputs an array of NaN values.** This is related to the issue above, in that some of the datasets have certain NaN points that end up propagating through the resultant functions when doing the matrix logic calcuations.  There still needs to be addtional NaN handilng built into the code to either drop or assign a default value to these points.  This combined with being abvle to get all the sets into a Mercator projection properly should eleiminate the issue.
- **Features to Implement:**
  better intterface for editing and loading josn.
  Better organization of json.
  Ability to process logic model while excluding certain datasets.
  Ability to add additional datasets and paramters without messing much with notebook code.
  Better use of maps.
