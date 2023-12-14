# golden-feather-grass-habitats
Habitat suitability model for Golden Feather Grass in North America

This model runs on a mostly modular python scripts that takes inputs for both study site and fuzzy logic model parameters from a seperate and easily editable .json file. 
It is desiged so that if a set of boundaries are fed into it, it will retreive all relevant rasters from the designated datasets based on the coordinates of the study site, and the parameters specificed in the settings.json.
Once all files are loaded in, the model will iterate over each pixel and determine its weighting via the fuzzy logic paramters set in the settings file, and return a level of habitat suitability based on the rules and relationships 
provided in the file, by multiplying all the fuzzy factored rasters together.

This model was created to assess the habitat suitability of National Grasslands under anthropogenic climate change but can theoretically be used with any boundary georeferenced dataset.  

tbe
gfdgdsfhsfd
