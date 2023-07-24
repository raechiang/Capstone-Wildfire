<p align="center">
  <img src="https://upload.wikimedia.org/wikipedia/commons/3/3f/The_Apple_Fire_burns_north_of_Beaumont%2C_Friday%2C_July_31%2C_2020.jpg" alt="2020 Apple Fire in Beaumont, CA, photograph by Brody Hessin">
</p>

Wildfire Prediction in California Counties
==============================

This is my first capstone project for Springboard.

## Introduction

Fires can be bad because they can be destructive. Although they are a natural part of our ecosystem, we should try to understand and control them, or at least we should be able to respond to them efficiently and try to minimize the negative impacts on us. There are clear direct impacts on us, such as the damage to buildings or to our health, with deaths, trauma, and air pollution. Even proximity to a fire can be detrimental to civilians, with evacuations and restrictions on travel. Some other economic impacts include a reduction in work stability in fire risk areas or business closures and civilian displacement due to fire threat or damage.

2018 and 2020 were notoriously bad years for us. In 2020, wildfires burned 4 and a half million acres of land, and 31 people died [^1]. Responses to fires were strained; there were not enough resources and crew to take care of the fires. They were forced to request off-duty firefighters to return to work. In 2018, we experienced the most destructive and deadliest fire that we have had on record, with 85 deaths and nearly 19000 structures destroyed, which resulted in about $10 billion in property damage [^2]. In total, the 2018 California wildfires cost the economy $148.5 billion dollars [^3].

Top 5 Most Destructive Wildfires up to 2022[^4]

| Fire Name (County/Counties) | Date | Structures | Deaths |
| --- | --- | --- | --- |
| Camp Fire (Butte) | November 2018 | 18,804 | 85 |
| Tubbs Fire (Napa & Sonoma) | October 2017 | 5636 | 22 |
| Tunnel Fire (Alameda) | October 1991 | 2900 | 25 |
| Cedar Fire (San Diego) | October 2003 | 2820 | 15 |
| North Complex (Butte, Plumas, Yuba) | August 2020 | 2352 | 15 |

In recent years, we have been experiencing bigger fires. The reasons for this change is up for debate, with some pointing at climate change and others at longer fire seasons and others at poor environmental maintenance, but whatever the case, it overall does not seem to be getting much better. Cal Fire started reliably recording wildfires in 1932, and when looking at the largest fires, the deadliest of fires, and the most destructive fires, 48 out of 60 of them were within the past two centuries.

California wildfires over time
<p align="center">
  <img src="/reports/figures/acresburned_1987-2018.png" alt="Acres burned in the years 1987-2018 in California">
</p>

Of course, anyone close to a high-risk fire area is immediately impacted by fires. Others should be concerned as well, and US citizens around the nation are even affected [^3]. Insurance companies, local governments, or fire control may want to allocate resources or policies or deploy different awareness and mitigation strategies more specifically depending on each region's unique risk. This project aims to find counties that have fires and to determine how many fires they may have each year. Specifically, this project uses the county and its size to try to predict the fires. Admittedly, this is an oversimplification for influences on a fire, but it can be sufficient for the scope of this project.

[^1]: J. Cart, “California’s 2020 fire siege: wildfires by the numbers”, Cal Matters, July 2021. ([Link](https://calmatters.org/economy/2021/10/california-wildfires-economic-impact/))
[^2]: N. Reiff, "How Fire Season Affects Economy", Investopedia, 2022. ([Link](https://www.investopedia.com/how-fire-season-affects-the-economy-5194059))
[^3]: K. Corry, “Full cost of California’s wildfires to the US revealed”, 2020. ([Link](https://www.ucl.ac.uk/news/2020/dec/full-cost-californias-wildfires-us-revealed))
[^4]: California Department of Forestry and Fire Protection, 2022.

### The Datasets

This project used a handful of data sources, but for the most part, the two CIMIS datasets were not used in the final model.

- Wildfire: 1636 wildfire incidents with 40 columns in the years 2013-2020, scraped by a Kaggle user, from the California Department of Forestry and Fire Protection (CAL FIRE) website. ([Link](https://www.kaggle.com/datasets/ananthu017/california-wildfire-incidents-20132020))
- Climate: 128000 entries with 19 columns of environmental conditions from 2017-2020, scraped by a Kaggle user, from the California Irrigation Management Information System (CIMIS) from the California Department of Water Resources. ([Link](https://www.kaggle.com/datasets/chelseazaloumis/cimis-dataset-with-fire-target))
- Station information: Further station information was taken from CIMIS, using their API, to expand the climate dataset with more location data. ([Link](https://cimis.water.ca.gov/))
- County information: Collected from Wikipedia, which has generic county information and 2022 census information from the National Association of Counties (NACo). ([Link](https://simple.wikipedia.org/wiki/List_of_counties_in_California))
- County geographical information: Downloaded a GEOJSON file containing geographical information of US counties, filtered for California counties only. ([Link](https://public.opendatasoft.com/explore/dataset/us-county-boundaries/table/))

## Project Organization
------------

    ├── LICENSE
    ├── Makefile           <- Makefile with commands like `make data` or `make train`
    ├── README.md          <- The top-level README for developers using this project.
    ├── data
    │   ├── external       <- Data from third party sources.
    │   ├── interim        <- Intermediate data that has been transformed.
    │   ├── processed      <- The final, canonical data sets for modeling.
    │   └── raw            <- The original, immutable data dump.
    │
    ├── models             <- Trained and serialized models, model predictions, or model summaries
    │
    ├── notebooks          <- Jupyter notebooks. Naming convention is a number (for ordering),
    │                         the creator's initials, and a short `-` delimited description, e.g.
    │                         `1.0-jqp-initial-data-exploration`.
    │
    ├── references         <- Data dictionaries, manuals, and all other explanatory materials.
    │
    ├── reports            <- Generated analysis as HTML, PDF, LaTeX, etc.
    │   └── figures        <- Generated graphics and figures to be used in reporting
    │
    ├── requirements.txt   <- The requirements file for reproducing the analysis environment, e.g.
    │                         generated with `pip freeze > requirements.txt`
    │
    ├── setup.py           <- makes project pip installable (pip install -e .) so src can be imported
    ├── src                <- Source code for use in this project.
    │   ├── __init__.py    <- Makes src a Python module
    │   │
    │   ├── data           <- Scripts to download or generate data
    │   │   └── make_dataset.py
    │   │
    │   ├── features       <- Scripts to turn raw data into features for modeling
    │   │   └── build_features.py
    │   │
    │   ├── models         <- Scripts to train models and then use trained models to make
    │   │   │                 predictions
    │   │   ├── predict_model.py
    │   │   └── train_model.py
    │   │
    │   └── visualization  <- Scripts to create exploratory and results oriented visualizations
    │       └── visualize.py
    │
    └── tox.ini            <- tox file with settings for running tox; see tox.readthedocs.io


--------

<p><small>Project based on the <a target="_blank" href="https://drivendata.github.io/cookiecutter-data-science/">cookiecutter data science project template</a>. #cookiecutterdatascience</small></p>

## Data Wrangling

[Notebook link](notebooks/1.0-rc-data-wrangling.ipynb).

At this step, data was collected and defined and underwent a preliminary cleaning. The wildfire dataset contained a lot of missing values, and much of the information did not seem to be standardized. A few important numerical features were mostly provided, such as the names, location information, number of acres burned, and dates. Other information that would have been nice to know could include the fuel type, the cause of fire, and more robust location data. There were some duplicate fires because if one fire could occur in multiple counties, but these could be determined using their unique IDs. The environmental conditions dataset was almost completely populated and clean, and the ranges and seeming outliers looked acceptable. However, this dataset was lacking information about the location of each data point or station. Furthermore, data was not retrieved from every station, so some areas of California were missing. Using the CIMIS API, a station information was added to our collection of datasets. By the end of this notebook, there were three dataframes: `fire_df` containing the wildfire dataset, `climate_df` containing the environmental conditions dataset, and `stations_df` containing information about the stations that recorded the data in `climate_df`.

<details>
<summary>Data descriptions for the original wildfire and environmental conditions datasets.</summary>

<details>
<summary>The wildfire dataset.</summary>

| Column | Dtype | Description |
| --- | --- | --- |
| AcresBurned | float64 | Acres of land affected by wildfires |
| Active | bool | Is the fire active or contained? |
| AdminUnit | object | Administrative unit |
| AirTankers | float64 | Resources assigned |
| ArchiveYear | int64 | Year the data was archived |
| CalFireIncident | bool | Is the incident treated as a CalFire incident? |
| CanonicalUrl | object | Part of URL for the information source |
| ConditionStatement | object | Descriptive status updates |
| ControlStatement | object | Information about current road closures and threats |
| Counties | object | Name of county origin |
| CountyIds | object | List of county IDs involved |
| CrewsInvolved | float64 | Resources assigned |
| Dozers | float64 | Resources assigned |
| Engines | float64 | Resources assigned |
| Extinguished | object | Date the fire was extinguished |
| Fatalities | float64 | Fatality count |
| Featured | bool | (Unknown but was 98% False) |
| Final | bool | (Unknown but was almost 100% True) |
| FuelType | object | Fuel type of the fire |
| Helicopters | float64 | Resources assigned |
| Injuries | float64 | Count of injured personnel |
| Latitude | float64 | Latitude of wildfire incident |
| Location | object | Description of the location |
| Longitude | float64 | Longitude of the wildfire incident |
| MajorIncident | bool | Is the fire considered a major incident? |
| Name | object | Name of the wildfire |
| PercentContained | float64 | Percent of the fire that is contained |
| PersonnelInvolved | float64 | Resources assigned |
| Public | bool | (Unknown but was 100% True) |
| SearchDescription | object | "Description" meta content in HTML head |
| SearchKeywords | object | "Keywords" meta content in HTML head |
| Started | object | Date the fire started |
| Status | object | Status of the fire |
| StructuresDamaged | float64 | Count of structures damaged |
| StructuresDestroyed | float64 | Count of structures destroyed |
| StructuresEvacuated | float64 | Count of structures evacuated |
| StructuresThreatened | float64 | Count of structures threatened |
| UniqueId | object | Unique ID for the wildfire incident |
| Updated | object | Last date of update |
| WaterTenders | float64 | Resources assigned |

</details>

<details>
<summary>The environmental conditions dataset.</summary>

| Column | Dtype | Description |
| --- | --- | --- |
| Stn Id | int64 | ID of the station |
| Stn Name | object | Name of the station |
| CIMIS Region | object | Region of the station |
| Date | object | Date of the measurements |
| ETo (in) | float64 | Reference evapotranspiration |
| Precip (in) | float64 | Precipitation |
| Sol Rad (Ly/day) | float64 | Average solar radiation |
| Avg Vap Pres (mBars) | float64 | Average vapor pressure |
| Max Air Temp (F) | float64 | Maximum air temperature |
| Min Air Temp (F) | float64 | Minimum air temperature |
| Avg Air Temp (F) | float64 | Average air temperature |
| Max Rel Hum (%) | float64 | Maximum relative humidity |
| Min Rel Hum (%) | float64 | Minimum relative humidity |
| Avg Rel Hum (%) | float64 | Average relative humidity |
| Dew Point (F) | float64 | Dew point |
| Avg Wind Speed (mph) | float64 | Average wind speed |
| Wind Run (miles) | float64 | Wind run |
| Avg Soil Temp (F) | float64 | Average soil temperature |
| Target | int64 | Geography or weather station of interest |

</details>
</details>

## Exploratory Data Analysis

[Notebook link](notebooks/2.1-rc-exploratory-data-analysis.ipynb).

Here we explored the data to understand each feature and their relationships with one another, and we engineered some features. Mostly, a lot of cleaning was required, and some data was verified or fixed after some investigation.

### A. Fire Data

The fire data was pruned somewhat aggressively; if a feature had more than 20% missing values, then it was dropped. Features with missing values that were deemed potentially important at the time were cross-referenced with online sources or filled by imputation.

**Dates**: Larger wildfire incidents’ dates could be fixed by checking their values in the Redbooks, which are written and released by the California Department of Forestry and Fire Protection. For the bad dates of smaller fires, most of them were approximated by considering all three of the incident’s dates (Started, Extinguished, and Updated) and occasionally the canonical URL (which corresponds to an incident’s Started date), since in most cases, only one of the three were erroneous. Finally, if both using existing dates and using the canonical URL failed, the yet remaining small fires were simply assigned to have lasted only one day. Two features were extracted from the existing date information: the year and month of the started date.

**Geographic coordinates**: The dataset contained some bad latitude and longitude coordinates, and an investigation revealed that in most cases, this was generally a repeat input, a swap of the two coordinates, a typo, or an arbitrary input. About 160 bad coordinates for latitude and longitude were found using a generous rectangular range of California’s boundaries. There was only one coordinate that skipped this basic filter that was revealed in a plot of the coordinates. The bad coordinates were simply reassigned to match the center coordinates of the fire’s county.

**Days active**: A new feature was created from existing features: the ActiveDays feature represents the number of days that the fire burned. This was simply a subtraction of the Started date from the Extinguished date, which revealed that there were unfortunately *many* unreliable Extinguished dates. A lot of dates appeared to be default dates. Namely, some fires were extinguished in the following January, even tiny fires that may have started in early summer. The correct date was imputed primarily using medians of subsets of fires, since the mean can be very volatile because a few outlier fires can burn substantially longer than most.

### B. Environmental Conditions Data

Counties were added to the environmental conditions (climate) dataset from the `stations_df`. There were not too many missing values in the `climate_df`, so these missing values were imputed using the mean values within the same month from either the same station in a different year or from the same county if that station always had missing values for every year and month combination. The climate data was also aggregated in months per county for further exploration.

### C. County Data

County characteristics were scraped from the “List of counties in California” Wikipedia page. Two features were basically added to the existing county data: the population in 2022 and the area in square miles. We lack information about the environments of these fire incidents, but the size and population density may hint at environmental characteristics. Wildfires need fuel, which means that they would prefer places with a lot of things to burn, such as forests and chaparrals, so a larger size and lower population density may be favored by fires, though houses can serve as fuel as well. Other features were aggregated and engineered for the counties, such as population density, fire proportions, and monthly statistics.

### D. Visualizations

**Fires and months**: The number of acres burned and days active have extreme outliers, and a vast majority of the fires were small and short. Summer and autumn months (June to October) experienced the most fires, though there were a few outliers in December and February, and the two years that had the most fires were 2017 and 2018.

<details>
<summary>Monthly fire figures</summary>

<p align="center">
  <img src="/reports/figures/permonth_totalfires.png" alt="Total fires started per month">
</p>

<p align="center">
  <img src="/reports/figures/permonth_totaldays.png" alt="Days burned from fires started in month">
</p>

<p align="center">
  <img src="/reports/figures/permonth_acresburned.png" alt="Acres burned per month">
</p>

</details>

**Fires and climate**: When all fires are compared to the environmental conditions, there does not seem to be strong correlations between them, but when looking at only the larger fires, there seems to be a bit more correlation with climate; however, it is still not particularly strong. Certain climate conditions may spread fires more and other climate conditions may obstruct response teams. Perhaps small fires may more often be started by random or unnatural causes that make them more unrelated to environmental conditions.

**Maps**: To illustrate the fires’ general locations, a quick scatterplot can be generated using their geographic coordinates, but a heatmap can more clearly depict intensities and frequencies of the wildfires. The maps clearly show specific areas where wildfires more commonly and intensely occur. These are often mountainous regions with a lot of forests and chaparrals. Sunnier, hotter regions such as those along the southern part of California also seem to experience a lot of wildfires.

<p align="center">
  Heatmap of all wildfires in 2013-2020
  <img src="/reports/figures/heatmap_allfires.png" alt="Heatmap of all wildfires in 2013-2020">
</p>

<details>
<summary>Scatter plot of latitude and longitude of fires</summary>

<p align="center">
  <img src="/reports/figures/latlongfirescatter.png" alt="Scatter plot of lat/long of fires">
</p>

</details>

While we do not have particularly robust or detailed geographic data, we do have some basic county information. The numbers and sizes of fires tend to be slightly higher for larger counties, and counties with lower populations tend to have larger and more numerous fires. Although the relationship between the size of a county and the number of fires in the county is not extraordinarily strong, it may suffice for the scope of this project.

Area in square miles of a county versus the number of fires in the county
<p align="center">
  <img src="/reports/figures/areavfire.png" alt="County area in square miles vs number of fires">
</p>

There are limitations with using counties to aggregate the data. It is not specific enough in representing a local area because counties have irregular boundaries and diverse terrains. The geographic coordinates would probably be better at generalizing the environment of the fires. Using county-based information can lead to loss in the value of climate information because the climate can vary drastically within a county. (For example, within San Bernardino County, certain areas like Chino or Redlands tend to be hotter throughout the year, yet it can be snowing at the higher altitudes, such as in the San Bernardino Mountains.) However, aggregation by county is perhaps not wholly irrelevant because larger counties tend to encompass one or more areas that may frequently have fires, so a county's size may be able to abstractly express these biomes somewhat. A different potentially useful point of generalizing by county is that policies, economics, and resources may be divided by county or city, so maybe countywide statistics still do matter.

<details>
<summary>Fire metrics per county</summary>

<p align="center">
  <img src="/reports/figures/percounty_fires.png" alt="Number of fires started per county">
</p>

Riverside is a somewhat large county with a lot of chaparral areas, and it's warm to hot year-round. San Diego is also a somewhat large county, and it has similar biomes and climate (and has a sprinkle of forests) to Riverside, but it is against the coast, so the humidity and moisture levels are higher than Riverside's. However, San Diego County also receives a lot of sunlight and is one of the closest counties to the equator. Imperial is its neighbor along the lower border of California, but it has no fires because much of the region is agricultural or desert. Butte and Shasta are more medium-sized counties, but they should have a lot of mountainous and forested regions.

<p align="center">
  <img src="/reports/figures/percounty_acresburned.png" alt="Number of acres burned per county">
</p>

Colusa and Shasta have a lot of fuel to burn, as they are both regions with lots of forest. Interestingly, Santa Barbara has a lot of acres burned and it is a bit of an oddball if you take a glance of the top ten, but Santa Barbara's leading position is actually almost all due to one fire--the Thomas Fire burned nearly 300,000 acres!

Thinking of these two together (and perhaps graphing these two features together), Riverside and San Diego have a lot of fires started but not very many acres burned. Perhaps proximity to human civilization and population density influence intensity and frequency, which would make sense. Responders will probably have easier access if it's in a more developed area. Fires will be contained faster if there is less fuel to burn, or if humans are more in danger. But this is speculation.

</details>

## Preprocessing and Modeling

[Notebook link](notebooks/3.0-rc-preprocessing-training.ipynb).

To prepare the data, fires were aggregated per county per year, and zeroes were filled in appropriately for counties and years that did not have fires. Each county was also dummy-encoded, and Alameda was dropped. For the training and testing split, the data were split into two partitions of 290 and 116 data points, which is a test split of about 28.6%, witht he training set containing the first five years 2013-2017 and the testing set containing the latter two years 2018-2019.

[Notebook link](notebooks/4.0-rc-modeling.ipynb).

Five preliminary models were quickly created and evaluated: LinearRegression, Ridge, RandomForestRegressor, GradientBoostingRegressor, and AdaBoostRegressor. The linear model performed decently with an R-squared of 0.57. The closer that the Ridge model's alpha was to zero, the better it performed, so it was close to the Linear Regressor anyway. Although the three tree-based algorithms were initially tested with arbitrary hyperparameters, they performed decently enough, so the Random Forest and Gradient Boosting models were moved forward to hyperparameter tuning using GridSearchCV.

<details>
<summary>Preliminary model metrics</summary>

| Model | R^2 | RMSE | MAE |
| --- | --- | --- | --- |
| Linear | 0.574 | 3.328 | 2.224 |
| Ridge α=0.01 | 0.573 | 3.330 | 2.226 |
| Ridge α=0.1 | 0.568 | 3.349 | 2.236 |
| Ridge α=1.0 | 0.528 | 3.503 | 2.311 |
| Ridge α=10.0 | 0.292 | 4.290 | 2.849 |
| Random Forest | 0.379 | 4.017 | 2.831 |
| Gradient Boosting | 0.455 | 3.763 | 2.589 |
| Ada Boost | 0.520 | 3.533 | 2.608 |

</details>

The hyperparameters selected for the RandomForestRegressor were the number of max features (`max_features`) of 0.2 and the number of estimators (`n_estimators`) of 297. The hyperparameters selected for the GradientBoostingRegressor were the learning rate (`learning_rate`) of 0.4, max depth (`max_depth`) of 2, and the number of estimators (`n_estimators`) of 12.

Cross-validation of the two models found that the gradient boosting regressor's R-squared fell into a generally better range, but the medians of both were comparable. When scored using the testing set (entirely unseen data) the random forest regressor slightly outperformed the gradient boosting regressor. This could perhaps be explained by the fact that the random forest regressor put at least some weight on every county and is more exhaustive in its evaluations, whereas the gradient boosting model disregarded most of the counties and put much more weight on just the area (size) of the county. The tuned random forest model also performs slightly better than the first linear regression model.

| Model | R^2 | RMSE | MAE |
| --- | --- | --- | --- |
| Random Forest | 0.575 | 3.324 | 2.221 |
| Gradient Boosting | 0.490 | 3.641 | 2.506 |

In terms of prediction, the random forest model would be the better choice. However, the gradient boosting model was about 20 and 40 times faster in learning speed and prediction speed, respectively. Still, there is only a finite number of counties, and the period used here is yearly, so having a larger computation time may not be too problematic.

County map of predicted number of fires in 2019
<p align="center">
  <img src="/reports/figures/2019_pred.png" alt="Predicted number of fires in 2019">
</p>

County map of true number of fires in 2019
<p align="center">
  <img src="/reports/figures/2019_true.png" alt="True number of fires in 2019">
</p>

Generally, it predicted fewer fires than there were in each county in 2018 and 2019, but as mentioned before, 2018 was a notoriously bad year for fires. Still, it may represent a decent baseline prediction for the fires, especially considering that the number and intensities of fires tends to wax and wane.

## Conclusion and Future Work

The random forest model predicts the number of fires in each county per year. This can perhaps be used by groups like CAL FIRE for resource allocation and preparation of response teams or equipment to high-risk areas, or it could be used by insurance companies to help understand which counties are likely to experience high risk in a year.

Wildfires are complex and difficult to predict in both their beginnings and their degrees of destruction. There are so many factors that go into their beginnings and intensities. This model is far from perfect, and a lot more work can be done about wildfires. As stated before, the county information and historical numbers of fires are very broad, but fires rely heavily on local conditions. It also doesn’t take well into account time: the fire seasons, the fluctuations of fires over time (the waxing and waning), and the overall increase in the number and intensities of fires over time. Other kinds of data could be considered for prediction, such as using geographic coordinates or other location divisions. Maybe we could find use for our climate data, or maybe we could look for oxygen levels or topographical information.

Altogether different kinds of projects can also be explored. Maybe counties can be arranged in a hierarchy of risk, or the risk of the spread of a fire could be predicted or visualized. Image recognition using photographs of the local environment or satellite images could also help us know the fuel availability for fires.
