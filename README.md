# Objective  
---  
The central goal of this project is to conduct a comprehensive analysis of how wildfires are affecting a particular city in the United States. The project seeks to evaluate the wide-ranging impacts of wildfires on various aspects of the city's ecosystem, encompassing health, tourism, property, and other relevant domains. Through this analysis, the project aims to generate valuable insights and data-driven recommendations.

These insights will serve as a critical resource for local policymakers, city managers, city councils, and civic institutions. They will enable these decision-makers to make well-informed, strategic choices about how to respond to and mitigate the future consequences of wildfires within their city. The project's objective is to empower these stakeholders to develop effective plans and policies to safeguard the city's well-being and resilience in the face of increasingly frequent and severe wildfires in the western US.

# Source Data
1. [USGS Wildland Fire Combined Dataset](https://www.sciencebase.gov/catalog/item/61aa537dd34eb622f699df81)

2. [Wildfire Cities Assignment](https://docs.google.com/spreadsheets/d/1cmTW5fgU3KyH6JbrRao-qWjzu2GovKk_BkA7a-poGFw/edit#gid=1247370552)

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

# Workflow

In **filtering_wildfires.ipynb**, I use this notebook to extract relevant wildfires from Merced, CA based on a distance threshold and valid date range. First, load and parse the USGS Wildland Fire Combined Dataset JSON file. Define the latitude and longitude coordinates for Merced, CA. You can use online tools or a geographical database to find these coordinates. Loop through the JSON data to extract the relevant wildfires based on the defined criteria (distance threshold and valid date range).

In **aqi_analysis.ipynb**, I use API requests to retrieve daily air quality summaries from an AQI (Air Quality Index) monitoring station. For each day, you collect data on gaseous air pollutants such as ozone, nitrogen dioxide, sulfur dioxide, and carbon monoxide. After collecting daily data over the course of a year, you then calculate yearly aggregates by averaging the pollutant values across months. 

In **modeling.ipynb**, I leveraged the filtered wildfire data to construct a time-series model utilizing exponential smoothing, aiming to forecast smoke estimates from 2021 to 2049. In addition to the modeling, I created three essential graphical representations. The first graph is a histogram displaying the frequency of wildfires within 50-mile distance intervals from the designated city up to the maximum specified range, offering insights into the spatial distribution of fire incidents. The second graph presents a time series, tracking the annual total acres burned by wildfires occurring within the designated proximity to the city, allowing for a visual assessment of yearly fire severity fluctuations. Finally, the third graph juxtaposes the fire smoke estimate for the city with the corresponding Air Quality Index (AQI) estimate, creating a time series that facilitates the comparison of air quality trends and their potential correlation with wildfire events over the specified time frame.

# Important Considerations for Data
The GeoJSON dataset is extensive, containing approximately 136,000 fire occurrences, which require in-depth analysis. Due to the substantial dataset size, loading the data is time-consuming, necessitating a robust error handling process during data acquisition. Furthermore, the features associated with each fire exhibit inconsistencies. Some fires lack the 'ring' parameter and instead utilize a 'curved ring,' which mandates special handling and separate treatment. Notably, there is an absence of data for the years 2021, 2022, and 2023 within the dataset.

The AQI data presents its own set of challenges. As different weather stations operate across varying time periods, the data must be consolidated from three distinct stations. This data integration process also requires meticulous exception handling, as the 'aqi' parameter is frequently absent or incomplete. Additionally, in the case of my city locations, there is an absence of data for gaseous pollutants, with only particulate pollutants available. As a result, this specific scenario necessitates unique handling and treatment.

# Intermediate data files
1. aqi_yearly_means_1992_to_2020.json </br>
    The file structure has the key as wildfire_year and the value is the mean AQI year over year </br>
    {"1992": 202, "1993": 205, "1994": 202, "1995": 209...}

2. feature_list_135k.json
3. filtered_fires_1963_to_2023.json

Please note, none of these files have been uploaded to GitHub since it has a 100 MB limit on file uploads.
