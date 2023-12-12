# Objective  
---  
The central goal of this project is to conduct a comprehensive analysis of how wildfires are affecting a particular city in the United States. The project seeks to evaluate the wide-ranging impacts of wildfires on various aspects of the city's ecosystem, encompassing health, tourism, property, and other relevant domains. Through this analysis, the project aims to generate valuable insights and data-driven recommendations.

These insights will serve as a critical resource for local policymakers, city managers, city councils, and civic institutions. They will enable these decision-makers to make well-informed, strategic choices about how to respond to and mitigate the future consequences of wildfires within their city. The project's objective is to empower these stakeholders to develop effective plans and policies to safeguard the city's well-being and resilience in the face of increasingly frequent and severe wildfires in the western US.

# Source Data
1. [USGS Wildland Fire Combined Dataset](https://www.sciencebase.gov/catalog/item/61aa537dd34eb622f699df81)

2. [Wildfire Cities Assignment](https://docs.google.com/spreadsheets/d/1cmTW5fgU3KyH6JbrRao-qWjzu2GovKk_BkA7a-poGFw/edit#gid=1247370552)

3. [Premature Death Rate for Merced County, CA] (https://fred.stlouisfed.org/series/CDC20N2U006047)

# Licensing    
---   
1. [Creative Commons License](https://creativecommons.org/licenses/by/4.0/)

# Helpful API Documentation    
---    
1. [wildire_gro_proximity_example.ipynb](https://drive.google.com/file/d/1qNI6hji8CvDeBsnLDAhJXvaqf2gcg8UV/view?usp=drive_link)

2. [epa_air_quality_history_example.ipynb](https://drive.google.com/file/d/1bxl9qrb_52RocKNGfbZ5znHVqFDMkUzf/view?usp=drive_link)

# Resources
1. [Exponential Smoothing](https://towardsdatascience.com/time-series-in-python-exponential-smoothing-and-arima-processes-2c67f2a52788)

2. [Technical Assistance Document for the Reporting of Daily Air Quality](https://www.airnow.gov/sites/default/files/2020-05/aqi-technical-assistance-document-sept2018.pdf)

3. [PechaKucha](https://en.wikipedia.org/wiki/PechaKucha)

4. [Centers for Disease Control and Prevention, Premature Death Rate for Merced County, CA](https://fred.stlouisfed.org/series/CDC20N2U006047)

# Workflow

In **filtering_wildfires.ipynb**, I use this notebook to extract relevant wildfires from Merced, CA based on a distance threshold and valid date range. First, load and parse the USGS Wildland Fire Combined Dataset JSON file. Define the latitude and longitude coordinates for Merced, CA. You can use online tools or a geographical database to find these coordinates. Loop through the JSON data to extract the relevant wildfires based on the defined criteria (distance threshold and valid date range).

In **aqi_analysis.ipynb**, I use API requests to retrieve daily air quality summaries from an AQI (Air Quality Index) monitoring station. For each day, you collect data on gaseous air pollutants such as ozone, nitrogen dioxide, sulfur dioxide, and carbon monoxide. After collecting daily data over the course of a year, you then calculate yearly aggregates by averaging the pollutant values across months. 

In **modeling.ipynb**, I leveraged the filtered wildfire data to construct a time-series model utilizing exponential smoothing, aiming to forecast smoke estimates from 2021 to 2049. In addition to the modeling, I created three essential graphical representations. The first graph is a histogram displaying the frequency of wildfires within 50-mile distance intervals from the designated city up to the maximum specified range, offering insights into the spatial distribution of fire incidents. The second graph presents a time series, tracking the annual total acres burned by wildfires occurring within the designated proximity to the city, allowing for a visual assessment of yearly fire severity fluctuations. Finally, the third graph juxtaposes the fire smoke estimate for the city with the corresponding Air Quality Index (AQI) estimate, creating a time series that facilitates the comparison of air quality trends and their potential correlation with wildfire events over the specified time frame. I extended this analysis by proposing a hypothesis linking Air Quality Index (AQI) to the number of premature deaths is a significant and insightful proposition. The correlation between environmental factors and public health is a complex area of study, and my observations align with a growing body of research that underscores the profound impact of air quality on human well-being.

# Important Considerations for Data
The GeoJSON dataset is extensive, containing approximately 136,000 fire occurrences, which require in-depth analysis. Due to the substantial dataset size, loading the data is time-consuming, necessitating a robust error handling process during data acquisition. Furthermore, the features associated with each fire exhibit inconsistencies. Some fires lack the 'ring' parameter and instead utilize a 'curved ring,' which mandates special handling and separate treatment. Notably, there is an absence of data for the years 2021, 2022, and 2023 within the dataset.

The AQI data presents its own set of challenges. As different weather stations operate across varying time periods, the data must be consolidated from three distinct stations. This data integration process also requires meticulous exception handling, as the 'aqi' parameter is frequently absent or incomplete. Additionally, in the case of my city locations, there is an absence of data for gaseous pollutants, with only particulate pollutants available. As a result, this specific scenario necessitates unique handling and treatment.

# Intermediate data files
1. aqi_yearly_means_1992_to_2020.json </br>
    The file structure has the key as wildfire_year and the value is the mean AQI year over year </br>
    {"1992": 202, "1993": 205, "1994": 202, "1995": 209...}

2. filtered_fires_1963_to_2023.json </br>
    The file structure has detailed information about the filtered wildfires on the basis on year and distance threshhold as mentioned in the assignment </br>
    {"OBJECTID": 14299, "USGS_Assigned_ID": 14299, "Assigned_Fire_Type": "Wildfire", "Fire_Year": 1963, "Fire_Polygon_Tier": 1, "Fire_Attribute_Tiers": "1 (1), 3 (3)", "GIS_Acres": 40992.45827111476, "GIS_Hectares": 16589.05930244248, "Source_Datasets": "Comb_National_NIFC_Interagency_Fire_Perimeter_History (1), Comb_SubState_MNSRBOPNCA_Wildfires_Historic (1), Comb_SubState_BLM_Idaho_NOC_FPER_Historica_Fire_Polygons (1), Comb_National_BLM_Fire_Perimeters_LADP (1)", "Listed_Fire_Types": "Wildfire (1), Likely Wildfire (3)", "Listed_Fire_Names": "RATTLESNAKE (4)", "Listed_Fire_Codes": "No code provided (4)", "Listed_Fire_IDs": "1963-NA-000000 (2)", "Listed_Fire_IRWIN_IDs": "", "Listed_Fire_Dates": "Listed Wildfire Discovery Date(s): 1963-08-06 (3) | Listed Wildfire Controlled Date(s): 1963-12-31 (3)", "Listed_Fire_Causes": "Unknown (3)", "Listed_Fire_Cause_Class": "Undetermined (4)", "Listed_Rx_Reported_Acres": null, "Listed_Map_Digitize_Methods": "Digitized-Topo (4)", "Listed_Notes": "", "Processing_Notes": "", "Wildfire_Notice": "Redacted (too long)", "Wildfire_and_Rx_Flag": null, "Overlap_Within_1_or_2_Flag": null, "Circleness_Scale": 0.38535519109185146, "Circle_Flag": null, "Exclude_From_Summary_Rasters": "No", "Shape_Length": 73550.42811804128, "Shape_Area": 165890593.0244248, "distance": 521.2144470028175, "smoke_estimate": 157.29594030571133}

Please note, none of the intermediate files have been uploaded to GitHub since it has a 100 MB limit on file uploads.
