# golden-feather-grass-habitats
Habitat suitability model for Golden Feather Grass in North America

One of the key consequences of global climate change is the environmental disruptions of organism habitat zones.  For animals such as polar bears and coral reefs, this is widely reported on and studied. For plants, chaning habitat boundaries can have far reaching effects due to plants forming the basis for most food chains on the planet. 


This model runs on a mostly modular python scripts that takes inputs for both study site and fuzzy logic model parameters from a seperate and easily editable .json file. 
It is desiged so that if a set of boundaries are fed into it, it will retreive all relevant rasters from the designated datasets based on the coordinates of the study site, and the parameters specificed in the settings.json.
Once all files are loaded in, the model will iterate over each pixel and determine its weighting via the fuzzy logic paramters set in the settings file, and return a level of habitat suitability based on the rules and relationships 
provided in the file, by multiplying all the fuzzy factored rasters together.

This model was created to assess the habitat suitability of National Grasslands under anthropogenic climate change but can theoretically be used with any boundary georeferenced dataset.  

tbe
gfdgdsfhsfd
# Habitat Suitability Model for Golden Feather Grass in North America

## Introduction

This document provides a detailed overview of a Python-based habitat suitability model developed for assessing potential habitats of Golden Feather Grass across North America, with a focus on adaptability to changing climatic conditions.

## Model Overview

The model integrates geospatial data processing with fuzzy logic principles, offering a flexible approach to habitat suitability analysis.

### Data Input and Processing

- **Study Site Specification**: Users input geographical boundaries for the study area using a GeoJSON file, which guides the spatial focus of the habitat analysis.
- **Data Retrieval**: Based on the study site's coordinates, the model automatically fetches relevant raster datasets, including climate projections, soil characteristics, and elevation.
- **Data Harmonization**: Ensures compatibility of datasets by aligning spatial resolution and coordinate reference systems.

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

## Conclusion

This model provides a technical yet flexible approach for habitat suitability analysis, particularly useful for researchers and environmental planners focusing on species distribution under environmental changes.
