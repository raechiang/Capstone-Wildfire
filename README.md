![2020 Apple Fire in Beaumont, CA, photograph by Brody Hessin](https://upload.wikimedia.org/wikipedia/commons/3/3f/The_Apple_Fire_burns_north_of_Beaumont%2C_Friday%2C_July_31%2C_2020.jpg)

Wildfire Prediction in California Counties
==============================

# Introduction

In 2020 alone, wildfires burned 4.2 million acres of land, and 31 people died[^1]. Responses to fires were strained; there were not enough resources and crew to take care of the fires. They were forced to request off-duty firefighters to return to work. Aside from direct destruction, fires indirectly affect other aspects of civilian life, including health and business. Evacuations and poor air quality can prevent people from maintaining and using their facilities for extended periods of time. For example, due to the Caldor Fire, a restaurant in South Lake Tahoe lost $10,000 to $13,000 in perishables, even though there was no structural damage to the city, and overall, the city estimated its loss to be over $50 million [^2]. Insurance companies, local governments, or fire control may want to allocate resources or policies or deploy different awareness and mitigation strategies more specifically depending on each region's unique risk. This project aims to find counties that have fires and to determine how many fires they may have each year.

[^1]: J. Cart, “California’s 2020 fire siege: wildfires by the numbers,” Cal Matters, July 2021. ([Link](https://calmatters.org/economy/2021/10/california-wildfires-economic-impact/))
[^2]: G. Gedye, “How much do wildfires really cost California’s economy?” Cal Matters, October 2021. ([Link](https://calmatters.org/environment/2021/07/california-fires-2020/>))

## The Datasets

This project used a handful of data sources, but for the most part, the two CIMIS datasets were not used in the final model.

- Wildfire: 1636 wildfire incidents with 40 columns in the years 2013-2020, scraped by a Kaggle user, from the California Department of Forestry and Fire Protection (CAL FIRE) website. ([Link](https://www.kaggle.com/datasets/ananthu017/california-wildfire-incidents-20132020))
- Climate: 128000 entries with 19 columns of environmental conditions from 2017-2020, scraped by a Kaggle user, from the California Irrigation Management Information System (CIMIS) from the California Department of Water Resources. ([Link](https://www.kaggle.com/datasets/chelseazaloumis/cimis-dataset-with-fire-target))
- Station information: Further station information was taken from CIMIS, using their API, to expand the climate dataset with more location data. ([Link](https://cimis.water.ca.gov/))
- County information: Collected from Wikipedia, which has generic county information and 2022 census information from the National Association of Counties (NACo). ([Link](https://simple.wikipedia.org/wiki/List_of_counties_in_California))
- County geographical information: Downloaded a GEOJSON file containing geographical information of US counties, filtered for California counties only. ([Link](https://public.opendatasoft.com/explore/dataset/us-county-boundaries/table/))

# Project Organization
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

# Data Wrangling

TODO

# Exploratory Data Analysis

TODO

# Preprocessing and Modeling

TODO

# Conclusion and Future Work

TODO
