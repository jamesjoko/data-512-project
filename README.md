# data-512-project
The goal of this course project is to analyze wildfire impacts in Santa Fe, New Mexico. The end goal is to be able to inform policymakers, city managers, city councils, or other civic institutions, to make an informed plan for how they could or whether they should make plans to mitigate future impacts from wildfires.

Sources:
- [Combined wildland fire datasets for the United States and certain territories, 1800s-Present (combined wildland fire polygons)](https://www.sciencebase.gov/catalog/item/61aa537dd34eb622f699df81)
  - This source was crawled to obtain fire metadata and polygons in GeoJSON format. The data was then used to obtain an annual smoke estimate.
  - The citation is: Welty, J.L., and Jeffries, M.I., 2021, Combined wildland fire datasets for the United States and certain territories, 1800s-Present: U.S. Geological Survey data release, https://doi.org/10.5066/P9ZXGFY3.
- [Air Quality System (AQS) API](https://aqs.epa.gov/aqsweb/documents/data_api.html)
  - This API was used to obtain AQI readings from monitoring stations within Santa Fe County
  - Terms of Service located here: https://aqs.epa.gov/aqsweb/documents/data_api.html#:~:text=Request%20Limits%20and%20Terms%20of%20Service
 
There are no output files created by my code, but I do save intermediate data in a folder called "Intermediate Data". The files generated are too big for this repository. To generate these files, run the notebook "part_1_common_analysis" from top to bottom. Visualizations are embedded within the notebook.
