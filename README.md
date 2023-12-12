# Wildfires' Impact on the Regional Socio-Economy for the city of Twin Falls, Idaho
## DATA512 - Introduction to Human Centered Data Science

### Goal

More and more frequently, summers in the western US have been characterized by wildfires with smoke billowing across multiple western states. There are many proposed causes for this: climate change, US Forestry policy, growing awareness, just to name a few. Regardless of the cause, the impact of wildland fires is widespread. There is a growing body of work pointing to the negative impacts of smoke on health, tourism, property, and other aspects of society.

Due to its relatively dry conditions especially during summer months, and the presence of forests, grasslands, and vegetation that can act as a fuel for wildfires, Twin Falls, Idaho faces a high susceptibility to wildfires. This makes it crucial to understand the various repercussions on the region’s prosperity and well-being. Moreover, the total socio-economic impacts of wildfires go well beyond the cost of damages, as they lead to industry disruption, business closures, economic losses, and affect the job opportunities of people living in the affected regions. This in turn exacerbates economic disparities. All these reasons are the key motivation to pursue this study which is an attempt to solve the real problem of the socio-economic ramifications caused by wildfires.

This analysis thus studies the wildfires in detail and is divided into two parts. The first part focuses on studying the wildland fires within 1250 miles of the city of Twin Falls, Idaho for the last 60 years (1963-2020). A smoke estimate is then created to estimate the wildfire smoke impact which is later modeled to make predictions for the next 30 years (until 2049). The second part of the project further extends this analysis to a specific impact focus - regional socio-economy and assesses how this sector is impacted by wildfires. Four indicators - Gross Domestic Product (GDP), unemployment rate, income, and income inequality form the basis for this study. Specifically, the analysis wanted to focus on four research questions,

1. Do the years affected by heavy smoke experience dips in economic productivity? The aim is to assess the impact on GDP growth during periods of intense wildfires.

2. Do unemployment rates increase during and immediately after wildfire events due to disruptions in economic activities? The goal is to analyze how wildfires affect unemployment rates in periods experiencing severe smoke exposure.

3. Did years with higher smoke exposure experience declines in personal income? The goal is to investigate how wildfires influence personal income per capita.

4. Finally, do low-income groups suffer disproportionately due to wildfires’ economic impacts? The aim is to explore if income inequality exacerbates the economic vulnerability of low-income groups during and after wildfires.

The final goal is to equip policy makers, city managers, city councils, or other civic institutions with data-driven information allowing them to make informed decisions related to public safety measures and resource allocation during wildfire events.

### Data Descriptions

This analysis used five pre-existing datasets (wildfires, GDP, unemployment rate, personal income per capita, and income inequality)and generated an additional dataset (Air Quality Index)using an API. The five pre-existing datasets are available in the [Data folder](https://github.com/TanushreeYandra/data-512-final-project/tree/main/Data) of this repository.

The first dataset is the [Combined Wildland Fire Datasets for the United States and certain territories, 1800s-Present (combined wildland fire polygons)](https://www.sciencebase.gov/catalog/item/61aa537dd34eb622f699df81) dataset which was used to retrieve the historical data of wildfires. This dataset was collected and aggregated by the US Geological Survey, and is relatively well documented. Fire polygons in this dataset are available in ArcGIS and GeoJSON formats. The dataset had multiple features about the wildfire including a unqiue ID, fire year, area of fire, fire name, fire type, coordinates of the fire perimeter, etc. 

The datasets for the four indicators were sourced from four different datasets from the [Federal Reserve Economic Data (FRED)](https://fredhelp.stlouisfed.org/fred/about/about-fred/what-is-fred/), maintained by the Research Department at the Federal Reserve Bank of St. Louis. It is an online database consisting of hundreds of thousands of economic data time series from multiple national, international, public, and private sources. All the four datasets are under the [FredⓇ Services General License](https://fred.stlouisfed.org/legal/#property-rights). They are under copyright; but, provided that one has not engaged in any prohibited uses, one may use these data series with proper attribution of the source. For more information, please refer to the [Terms of Use](https://fred.stlouisfed.org/legal/#fred-terms). The four data sources and their descriptions have been mentioned below:

1. Gross Domestic Product: For this, the dataset of [Real Gross Domestic Product: All Industries in Twin Falls County](https://fred.stlouisfed.org/series/REALGDPALL16083) was used. This is an annual dataset from 2001 to 2021 representing the GDP - a measure of the market value of final goods and services produced within a county in a particular period. The dataset contains only two columns - date in the YYYY-MM-DD format, and the GDP.

2. Unemployment Rate: For this, the dataset of [Unemployment Rate in Twin Falls County](https://fred.stlouisfed.org/series/IDTWIN5URN) was used. This is a monthly dataset from 1990 to 2023 representing the percentage of unemployed people in the total civilian labor force. The dataset contains only two columns - date in the YYYY-MM-DD format, and the unemployment rate as a percentage.

3. Personal Income per Capita: For this, the dataset of [Per Capita Personal Income in Twin Falls County](https://fred.stlouisfed.org/series/PCPI16083) was used. This is an annual dataset from 1969 to 2022 representing the personal income of the residents in the area divided by the resident population. The dataset contains only two columns - date in the YYYY-MM-DD format, and the per capita personal income.

4. Income Inequality: For this, the dataset of [Income Inequality in Twin Falls County](https://fred.stlouisfed.org/series/2020RATIO016083) was used. This is an annual dataset from 2010 to 2021 representing the ratio of the mean income for the highest quintile (top 20 percent) of earners divided by the mean income of the lowest quintile (bottom 20 percent) of earners in a particular county. The dataset contains only two columns - date in the YYYY-MM-DD format, and the income inequality ratio.

### API and Documentation:

Air Quality Data was needed to evaluate the performance of the smoke estimate created. This data was requested from the US Environmental Protection Agency (EPA) Air Quality Service (AQS) API. This is a historical API and does not provide real-time air quality data. The [documentation](https://aqs.epa.gov/aqsweb/documents/data_api.html) for the API provides definitions of the different call parameter and examples of the various calls that can be made to the API.

The US EPA was created in the early 1970's. The EPA reports that they only started broad based monitoring with standardized quality assurance procedures in the 1980's. Many counties will have data starting somewhere between 1983 and 1988. However, some counties still do not have any air quality monitoring stations. The API helps resolve this by providing calls to search for monitoring stations and data using either station ids, or a county designation or a geographic bounding box. Some [additional information on the Air Quality System can be found in the EPA FAQ](https://www.epa.gov/outdoor-air-quality-data/frequent-questions-about-airdata) on the system.

### Intermediate Data Files Documentation: 

In this study, four intermediate data files were generated. Two data files were generated in the first step - [Data Retrieval](https://github.com/TanushreeYandra/data-512-final-project/blob/main/Analysis/Wildfires_Analysis_Data_Retrieval.ipynb). These are:

1. 'final_wildfire_data.json': This dataset is in the format of a JSON file which was extracted from the original [Wildland Fires Dataset](https://github.com/TanushreeYandra/data-512-final-project/blob/main/Data/USGS_Wildland_Fire_Combined_Dataset.json.zip) and has the data of 84319 wildfire instances that are within 1250 miles of Twin Falls, Idaho between the years 1963 and 2020. This dataset has a total of 31 columns some of them being a unqiue ID, fire year, area of fire, fire name, fire type, coordinates of the fire perimeter, etc.
  
2. 'Yearly_AQI_Data.csv': This CSV file was retrieved from the data obtained during the API call, and contains the maximum AQI data for every fire season (May 1st to October 31st) on an yearly basis for Twin Falls, Idaho. The dataset contains 35 rows and two columns - 'Year' which is an integer, and the AQI which is a float value. This data covers the AQI values for the period of 1986 through 2020.

The third intermediate file was generated during the second step of the analysis - [Data Preprocessing](https://github.com/TanushreeYandra/data-512-final-project/blob/main/Analysis/Wildfires_Analysis_Data_Preprocessing.ipynb). This file is:

1. 'Wildlife_Data_Processed.csv': This CSV file contains the processed wildfires dataset. It was created by removing irrelevant columns, filtering out overlapping wildfires, and ignoring circular fires of size greater than 1 acre from the [final_wildfire_data.json](https://github.com/TanushreeYandra/data-512-final-project/blob/main/Results/final_wildfire_data.json.zip) file. The final dataset had 72608 wildfire instances and the number of columns were brought down to 9 from the initial 31. This dataset contained features including 'USGS_Assigned_ID', 'Assigned_Fire_Type', 'Fire_Year', 'GIS_Acres', 'Listed_Fire_Names', 'Circleness_Scale', 'Shape_Length', 'Shape_Area', and 'Distance'.

The fourth intermediate file was generated during the third step of the analysis - [Smoke Estimate Generation and Modeling](https://github.com/TanushreeYandra/data-512-final-project/blob/main/Analysis/Wildfires_Analysis_Smoke_Estimates_and_Modeling.ipynb). This file is:

1. 'Yearly_Smoke_Estimate.csv': This CSV file was generated after creating the smoke estimate and taking a cumulative value of all wildfire instances on an yearly basis. Since the “smoke emitted” was being analyzed, it made more sense if a cumulative of the smoke estimate was taken instead of average. This would take the large number of wildfires in recent times into account and not provide any biased results. The dataset contains 57 rows and two columns - 'Fire_Year' which is a datetime object, and the 'Smoke_Estimate' which is a float value. This dataset covers the AQI values for the period of 1963 through 2020.

All these four intermediate data files have been stored in the [Intermediate Data Files](https://github.com/TanushreeYandra/data-512-final-project/tree/main/Results/Intermediate%20Data%20Files) section of the [Results](https://github.com/TanushreeYandra/data-512-final-project/tree/main/Results) directory.

### Known Issues or Special Considerations with the Data:

While the study was conducted with appropriate assumptions and keeping human-centered data science principles in mind, there are a few considerations with the data that are important to know:

1. It is important to note that the wildfires dataset may not be the most accurate especially for wildfires in the earlier years due to lack of proper reporting measures. Wildfires might have been underreported or not systematically documented in earlier periods, especially in remote or less populated areas, leading to incomplete or inaccurate datasets.

2. Since fires are irregularly shaped, defining the notion of ‘distance’ of the fire from Twin Falls, Idaho was challenging. For example, should the distance be calculated from the closest point of the fire perimeter or the centroid of the region? For this study, the average distance of all perimeter points was taken because for some very large fires, including just the shortest distance seemed biased. However, this is an assumption that can affect the ultimate results since the ‘Distance’ variable factors into the final smoke estimate.

3. The wildfires dataset had the data for both prescribed fires and wildfires. A prescribed fire is a planned fire intentionally ignited by park managers to meet management objectives whereas a wildfire is unplanned caused by natural causes, by accidental (or arson-caused) human ignitions, or by an escaped prescribed fire. While prescribed fires are intentional and usually in control, they still do contribute to air pollution. For this analysis, it was assumed that prescribed fires and wildfires contribute to the same amount of pollution for a given land within the same area. This assumption of equal impact could have led to inaccurate estimations of pollution levels and can affect the overall results.

4. Overlapping fires were removed from the dataset since there is another fire already existing in the database with more than 10% overlap. While the overlap flag may or may not be correct, it is assumed that another row pertaining to the same fire exists for those fires that are flagged. This assumption however holds to be valid, only if the dataset was accurate in terms of documenting the overlapping fires. There is a possibility of overlapping fires still existing in the dataset or “non-overlapping” fires being removed.

5. The AQI data obtained from the US EPA had a few missing values. While these values were dealt by taking the rolling average of the previous five years which makes for a reasonable assumption, it still does create a caveat.

6. The data available for the four socio-economic indicators was widely inconsistent in terms of the timelines for which it was available. While some indicators had a longer period of data, the income inequality dataset had data only for 10 years. Thus, generalizing the relation between such indicators with the smoke estimate was difficult. However, for the scope of this assignment, this factor was neglected. Any correlation existing, even for a 10 year period, was taken into account.

### Results

Eight visualizations were generated which have been stored in the [Visualizations](https://github.com/TanushreeYandra/data-512-final-project/tree/main/Results/Visualizations) section of the [Results](https://github.com/TanushreeYandra/data-512-projectpart1/tree/main/Results) directory. These are briefly explained below:

1. Histogram of the distribution of wildfires by their distance from Twin Falls, Idaho
  
2. Line graph of the total acres burned by wildfires every year

3. Time series graph containing the cumulative smoke estimate and the maximum AQI estimate for every year

### Research Implications:

This assignment was an eye-opener on the number of wildfires that have taken place in the US in the last 60 years. It also taught me to deal with a new type of data files - GeoJSON. Secondly, having a keen interest in sustainability, this project was really fun and insightful. It felt like detective work where one probes further and further into the data to understand why a certain phenomenon is taking place. The whole aspect of creating a smoke estimate from scratch, trying out different combinations of features, finding the best combination, evaluating it, and then finally modeling was tedious yet very exciting to work on. The modeling process especially was very difficult as I tried several models before arriving at the moving average model. This assignment thus taught me about the various models that can be used to model a data with a lot of peaks and dips when one has little to no predictors.
