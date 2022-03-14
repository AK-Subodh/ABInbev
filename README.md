# ABInbev
Hackathon solution

**Problem Statement** : Compliance Analytics

## Why forecast weather?
Weather warnings are important forecasts because they are used to protect life and property. Forecasts based on temperature and precipitation are important to agriculture, and therefore to traders within commodity markets. Temperature forecasts are used by utility companies to estimate demand over coming days.

## Tasks
CSV file provided contains weather data, having multiple factors that affect the temperature of a day. We have to predict the temperature of the day based on other parameters provided to us. In this process, we are also supposed to perform the following to draw out smoe conclusions:
- Data Preprocessing: Data Cleaning, Data Manipulation, Data Transformation and dimentionality reduction.
- Exploratory Data Analysis: Univariate, Bivariate, Multivariate
- Test-Train split
- Building models
- Verify Hypothesis

## First Look at the data (& preparing the data dictionary)

As we could see, our dataset contains total of 8768 rows and 20 columns. We checked the column names present in the dataset and then checked the total number of null values which is zero. SO the dataset does not have any missing values. 

But as the data type for the columns is not correctly assigned, leaving it as it is may cause problems in dealing with them later. For example, time is in int and date is described as 'object'. We need to perform type conversion. For this we need to have close look at the columns of the dataset and then decide which data type should be assigned to them.

| Sr. No.    | Name | Description  | Current Data Type  | New Data Type  | Conversion Needed? | Detailed Description  |
| :---       |    :----:   | :---        |    :----:   |    :----:   |    :----:   | :---        |
| 1 | time  | Hour of the day | int64 | datetime | Yes | - |
| 2 | date  | Date of reading | object | datetime | Yes | - |
| 3 | tempC | Temp. in deg. Celsius | int64 | int64 | NO | Atmospheric Temperature |
| 4 | windspeedMiles | Wind speed in miles/hr | int64 | int64 | NO | wind speed, or wind flow speed, is a fundamental atmospheric quantity caused by air moving from high to low pressure, usually due to changes in temperature.  |
| 5 | windspeedKmph | Wind speed in Km/hr | int64 | int64 | NO | wind speed, or wind flow speed, is a fundamental atmospheric quantity caused by air moving from high to low pressure, usually due to changes in temperature.  |
| 6 | winddirDegree | Wind Direction in degrees | int64 | int64 | NO | Wind direction is generally reported by the direction from which it originates. Reading is in degrees here. |
| 7 | winddir16Point | Wind Direction in 16 point compass | object | Category | Yes | Wind direction is generally reported by the direction from which it originates. 16 point compass reading is used here. |
| 8 | weatherCode | Code assigned to weather | int64 | category | Yes | - |
| 9 | weatherDesc | Weather description | object | category | Yes | Cloudy, sunny, etc. |
| 10 | precipMM  | Precipitation in mm | float64 | float64 | NO | precipitation is any product of the condensation of atmospheric water vapor that falls under gravitational pull from clouds. The main forms of precipitation include drizzling, rain, sleet, snow, ice pellets, graupel and hail. |
| 11 | precipInches | Precipitation in inches | float64 | float64 | NO | precipitation is any product of the condensation of atmospheric water vapor that falls under gravitational pull from clouds. The main forms of precipitation include drizzling, rain, sleet, snow, ice pellets, graupel and hail. |
| 12 | humidity | Humidity in % | int64 | int64 | NO | Humidity is a measure of the amount of water vapor in the air. |
| 13 | visibility | Visibility in Km | int64 | int64 | NO | Visibility is a measure of the horizontal opacity of the atmosphere at the point of observation and is expressed in terms of the horizontal distance at which a person should be able to see and identify |
| 14 | visibilityMiles | Visibility in miles | int64 | int64 | NO | Visibility is a measure of the horizontal opacity of the atmosphere at the point of observation and is expressed in terms of the horizontal distance at which a person should be able to see and identify |
| 15 | pressure | Pressure in mmHg | int64 | int64 | NO | Atmospheric pressure, also known as barometric pressure, is the pressure within the atmosphere of Earth |
| 16 | pressureInches | Pressure in inches of Hg | int64 | int64 | NO | Atmospheric pressure, also known as barometric pressure, is the pressure within the atmosphere of Earth |
| 17 | cloudcover | Cloud cover in % | int64 | int64 | NO | A gust or wind gust is a brief increase in the speed of the wind, usually less than 20 seconds. |
| 18 | WindGustMiles | Wind Gust speed in Miles/hr | int64 | int64 | NO |
| 19 | WindGustKmph | Wind Gust speed in Km/hr | int64 | int64 | NO | A gust or wind gust is a brief increase in the speed of the wind, usually less than 20 seconds. |
| 20 | uvIndex | UV Index | int64 | int64 | NO | The UV index tells you how much ultraviolet radiation is around at ground level on a given day, and its potential to harm your skin.|

## Parameters Given and finding relevant ones:
The dataset contains parameters in multiple units systems. After picking the one we want to work with, we are left with the unique parameters.
Unique Attributes collected in dataset:
1. Wind Speed
2. Wind Direction
3. Weather type
4. Precipitation
5. Humidity
6. Visibility
7. Pressure
8. Cloud Cover
9. Wind Gust
10. UV Index
11. Date
12. Hour

## Hypothesis and Assumptions
Now that we know about the relevant features, before proceeding we have to decide for roadmaps/approches and questions that we want to be answered in order to get insights and perform feature selection for prediction.

Some questions:
1. Univariate Analysis:

2. Bivariate Analysis:
(with the target variable)
- How are precipitation and temperature related?
- How are Wind Speed and temperature related?
- How are Wind DIrection and temperature related?
- How are weather type and temperature related?
- How are humidity and temperature related?
- How are Visibility and temperature related?
- How are pressure and temperature related?
- How are cloud cover and temperature related?
- How are wind gust and temperature related?
- How are UV Index and temperature related?
- How are hour of the day and temperature related?
- How are season and temperature related?

3. Multivariate Analysis:
(with the attributes)
- **Visibility** : Visibility could be affected by Humidity and Precipitation. Check how are they related.

- **Wind** : Wind flows from high pressure region to low pressure region. The movement of wind and this pressure difference decides the wind direction. However, different region have their own characteristic wind nature. Thus, How are pressure, wind speed and wind direction related?

- **Cloud Cover and weather** : How are the % of cloud cover and different weather types related? For example, during snowfall, clouds contain snow crystals within then. Of course sunny day does not have much of cloud cover. 

- **Cloud Cover and precipitation** :  "The type and amount of clouds that commonly form over a region impact the precipitation conditions." Thus , how are precipitation and cloud cover related? 

- **Cloud Cover and UV Index** :"CLOUD COVER, if heavy, can block most UV radiation. Thin or broken clouds allow most UV rays through. Puffy, fair-weather clouds deflect rays and can increase UV radiation reaching the surface." What is the relationship between UVIndex and CloudCover?

- **Wind Gust** : "The fundamental difference between the wind gust and wind is duration. A sustained wind is defined as the average wind speed over two minutes. A sudden burst in wind speed is called the wind gusts and typically lasts under 20 seconds". Could it be that a day having high wind speed, face more wind gust?

- **Season**: Season affects all the attributes. Thus, there has to be some sesonal relationship between these attributes and seasons .


4. Time Series

**Hypothesis** : 
- Since we are dealing with temperature of the day, seasons have come into play. Summer will have high temperature and winters will have low. The difference could range up to >20 degree celcius.
- Data belongs to a same location
- Precipitation is the amount of rainfall
- Weather desc and weather code are not same
- On a day of high wind speed, there will  be high windgust
- On any day, cloud cover could be affected by UVIndex, season, wind speed and could affect precipitation, temperature, humidity.
- On any day, visibility could be affected by humidity, precipitation and cloud cover
- Pressure, wind speed and wind direction should share some relation as pressure difference creates the wind and decides its direction.



    
