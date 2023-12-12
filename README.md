# data-512-project
This course project aims to analyze wildfire impacts in Santa Fe, New Mexico. The end goal is to be able to inform policymakers, city managers, city councils, or other civic institutions, to make an informed plan for how they could or whether they should make plans to mitigate future impacts from wildfires.

## Sources:
- [Combined wildland fire datasets for the United States and certain territories, 1800s-Present (combined wildland fire polygons)](https://www.sciencebase.gov/catalog/item/61aa537dd34eb622f699df81)
  - This source was crawled to obtain fire metadata and polygons. The data was then filtered to within 1250 miles of Santa Fe and fire season from May 1st to October 31st and then used to calculate an annual smoke estimate for Santa Fe, NM.
  - The citation is Welty, J.L., and Jeffries, M.I., 2021, Combined wildland fire datasets for the United States and certain territories, 1800s-Present: U.S. Geological Survey data release, https://doi.org/10.5066/P9ZXGFY3.
  - Data Structure: JSON objects. 
  - There are too many data fields to list on this README, so I will only include the relevant attributes for this project. The full attribute list is located here: [](https://www.sciencebase.gov/catalog/file/get/61aa537dd34eb622f699df81?f=__disk__d0%2F63%2F53%2Fd063532049be8e1bc83d1d3047b4df1a5cb56f15&transform=1&allowOpen=true)
  - Data Fields for each fire:
    - attributes
      - Assigned_Fire_Type (str): The fire type assigned to the focal fire boundary during the creation of the dataset
      - Fire_Year (int): The calendar year when the dataset creators determined the fire occurred.
      - GIS_Acres (float): The GIS calculated acres of the fire polygon using the Calculate Geometry tool in ArcGIS Pro.
    - geometry
      - rings (List[List[float]]): Contains one or more polygons along with the polygon coordinates that describe the location of the fire's impacted area.
- [Air Quality System (AQS) API](https://aqs.epa.gov/aqsweb/documents/data_api.html)
  - This API was used to obtain AQI readings from monitoring stations within Santa Fe County
  - Terms of Service located here: https://aqs.epa.gov/aqsweb/documents/data_api.html#:~:text=Request%20Limits%20and%20Terms%20of%20Service
  - Data Structure: JSON objects.
  - Data Fields for each pollutant monitor:
    - year (int): year of the monitor reading.
    - pollutant_type (str): the type of pollutant that the monitor tracked. It can be gaseous or particulate.
    - aqi (int): value for air quality index. More information on AQI values can be found [here](https://www.airnow.gov/aqi/aqi-basics/).
- [New Mexico EPHT Primary Asthma ED Visit Counts](https://nmtracking.doh.nm.gov/dataportal/query/builder/ed/EDAsthma/CountAsthma.html)
  - This dataset was downloaded to obtain the number of asthma-related emergency department visits in Santa Fe County.
  - Terms of Use: See Appendix below
  - [Link to Metadata](https://nmtracking.doh.nm.gov/dataportal/metadata/Asthma_ED_Visits.html)
  - Data Structure: manually input into .csv file
  - Data Fields:
    - Year (int): 2008-2021
    - Area (str): Always Santa Fe County
    - Age Group (str): 0-14, 15-44, 45-64, 65+
    - Sex (str): Male or Female
    - Ethnicity/Race (str): American Indian or Alaska Native, Asian or Pacific Islander, Black or African American, Hispanic, White
- [New Mexico EPHT Asthma Hospital Admissions](https://nmtracking.doh.nm.gov/dataportal/query/builder/hidd/HIDDAsthma/CountAsthma.html)
  - Contains the case counts of hospitalizations where asthma was the primary diagnosis among New Mexico residents. A case count is when an individual has been discharged from a single visit.
  - Terms of Use: See Appendix below
  - [Link to Metadata](https://nmtracking.doh.nm.gov/dataportal/metadata/Asthma_Hospitalization.html)
  - Data Structure: manually input into .csv file
  - Data Fields:
    - Year (int): 1999-2022
    - Area (str): Always Santa Fe County
    - Age Group (str): 0-14, 15-44, 45-64, 65+
    - Sex (str): Male or Female
    - Ethnicity/Race (str): American Indian or Alaska Native, Asian or Pacific Islander, Black or African American, Hispanic, White

## Issues and Special Considerations
- Wildfire Polygon Data:
  - The smoke estimate was calculated using a mixture of variables such as size, distance from the closest point of the fire to Santa Fe, and whether or not the fire was prescribed. Other data fields are missing to calculate an objectively correct smoke estimate such as the wind direction and magnitude, the amount of flammable material in the area, and the topography of the area.
  - This dataset merges many existing wildfire and prescribed fire datasets that are limited in some way.
  - Wildfire notice from the dataset: Wildfire mapping prior to 1984 was inconsistent, infrequent, and done without the aid of more modern fire mapping methods (GPS and satellite imagery). Areas burned prior to 1984 in this dataset represent only a fraction of what actually burned. While areas burned on or after 1984 are much more accurate and complete, errors still can and do occur. This dataset represents the most complete set of digitized polygon fire data available to the public that we, the authors, were able to collect. It is not a complete collection of all wildfires burned during the time period it represents.
  - Prescribed Burn notice from the dataset: Prescribed fire data in this dataset represents only a fraction of the area burned in prescribed burns across all years due to lack of reporting, particularly on private lands. The missing prescribed burn data becomes more pronounced further back in time, particularly in the southeastern U.S.; however, errors and omissions still occur through the most recent years in this dataset. This dataset represents the most complete set of digitized polygon fire data available to the public that we, the authors, were able to collect. It is not a complete collection of all prescribed burns burned during the time period it represents.
- AQI Data:
  - The AQI data for Santa Fe County dates back to 1974, but only a small number of monitors were installed during 1974-1980. The result of this is likely an inflated estimate of AQI during these years.
  - A daily summary of gaseous and particulate AQI is pulled from the EPA's API
  - The AQI for a given day is the maximum reading of gaseous or particulate throughout that day.
  - The daily AQI is calculated for every day in an entire year's fire season, which is from May 1st to October 31st.
  - The average AQI of all days in a year's fire season is the estimated yearly AQI
- Asthma Data:
  - The data does not date very far back, and not as far back as the smoke estimate data. I am only able to incorporate asthma hospital admissions into my smoke estimate for 21 years and incorporate asthma hospital admissions for 12 years.
  - Note that both datasets do not include visits or admissions from Veterans Affairs or Indian Health Service facilities.
  - I am unable to pull the full data and instead have to query for the information I want.
  - I emailed the NMEPHT on 11/17 and got a response on 12/6 reading "Access to the raw dataset would require an Internal Review Board (IRB) approval from your institution as NMDOH cannot release protected health information without it". The approval process would likely take longer than the remaining course duration, so I have to query for the information instead.

## Intermediate Data Files
- annual_smoke_estimate.csv
  - Contains the annual smoke estimate for Santa Fe, NM using the smoke estimate calculation in the part 1 notebook and final report
  - Size: 2KB
  - Data Structure: tabular data (.csv)
  - Data Fields:
    - year (int): Year of the annual smoke estimate. Domain: 1963-2020
    - smoke_estimate (float): estimated smoke impact on Santa Fe residents
- santa_fe_fires.json
  - Contains the fire metadata and polygons of all fires in the last 60 years within 1250 miles of Santa Fe that occured during the annual fire season.
  - Size: 1.7 GB
  - Data Structure: JSON objects
  - Data Fields for each fire:
    - attributes
      - Assigned_Fire_Type (str): The fire type assigned to the focal fire boundary during the creation of the dataset
      - Fire_Year (int): The calendar year when the dataset creators determined the fire occurred.
      - GIS_Acres (float): The GIS calculated acres of the fire polygon using the Calculate Geometry tool in ArcGIS Pro.
    - geometry
      - rings (List[List[float]]): Contains one or more polygons along with the polygon coordinates that describe the location of the fire's impacted area.
- santa_fe_yearly_aqi.json
  - Contains the annual average AQI for Santa Fe during the annual fire season.
  - Size: 2KB
  - Data Structure: JSON objects
  - Data Fields:
    - key | year (str): the year of the annual average AQI. Domain: 1974-2023.
    - value | aqi (float): The mean daily AQI of all days within the annual fire season. 

## Reproducibility
My code creates no output files, but I save intermediate data in a folder called "Intermediate Data". Visualizations for the report and presentation are embedded within the notebooks. Some generated intermediate data files are too big to store in this repository. To generate these files, run the notebook "part_1_common_analysis.ipynb" from top to bottom. To run specific cells in "part_3_presentation_visuals.ipynb", "part_1_common_analysis.ipynb" must be run first from top to bottom to generate intermediate data files used in that notebook. If the part 1 notebook has already been run, results in the part 3 notebook can be generated by running all cells from top to bottom.

## Appendix
### NM EPHT Terms of Use:
The data and information provided through the NM-EPHT Query System are intended to support any individuals or entities engaged in activities designed solely to enhance the well-being of a specific community, which may include the State of New Mexico. Allowed activities include informing evidence-based decision-making in New Mexico to plan and improve health service delivery, evaluate health care interventions and systems, and inform health policy decisions. Other uses are not permissible.

As an NM-EPHT Query System user, I AGREE TO:
1. Use the data for statistical reporting and analysis only.
2. Avoid any attempt to identify or contact individual(s) represented in the NM-EPHT query system data.
3. Avoid disclosure or use of the identity of any individual(s) discovered inadvertently.
4. Avoid linkage of NM-EPHT query system data with other data that, after linkage, might allow identification of an individual represented in the NM-EPHT query system data.
5. Use appropriate safeguards to prevent the identification of any individual(s) represented in the data, including when disclosing NM-EPHT Query System data to others.
6. Report IMMEDIATELY any inadvertent or intentional identity disclosures or violations of this agreement of which I become aware to the Epidemiology and Response Division, New Mexico Department of Health, (505) 827-0006.

