# COVID-19 Data Analytical Dashboard of Bangladesh

## Table of Contents

- [Overview](#overview)
- [Data Source](#data-source)
    - [Dataset Description](#data-description)
- [Key Features](#key-features)
- [Installation](#installation)
- [File Structure](#file-structure)
- [Methodology](#methodoloogy)
- [Usage](#usage)
- [Insights](#insights)
- [Technology Used](#technology-used)
- [Future Enhancements](#future-enhancements)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)


## Overview

This repository contains an analytical dashboard built using Power BI to visualize and analyze COVID-19 data across different divisions in Bangladesh. The dashboard provides insights into confirmed cases, deaths, survival rates, and other key metrics over time.


## Data Source

The dataset used in this project is sourced from Kaggle. To get data used in this project click [Dataset](https://www.kaggle.com/datasets/rashikrahmanpritom/covid19-cases-in-bangladesh-dataset) .This dataset contains covid cases of all the divisions in bangladesh from 1st March 2020 to 2nd July 2021.

### Dataset Description
| Column Name                 | Description                             |
|-----------------------------|-----------------------------------------|
| Date                        | Record date (daily granularity)         |
| Division                    | Name of the administrative division     |
| Confirmed Cases             | Total confirmed cases per day/division  |
| Deaths                      | Total reported deaths per day/division  |
| Case Rate                   | Cases per 100,000 population (estimated)|
| Death Rate                  | Deaths per 100,000 population (estimated)|

All values are **cleaned**, **normalized**, and **processed**. Missing values were handled using `interpolation` and `forward fill` due to skewed and time series.

## Key Features

### Filters & Slicers:
- **Division Slicer**: Select division to see individual analysis
- **Metric Slicers**: Toggle between Confirmed/Deaths/Survival

### Visual Components:
The dashboard includes the following key visuals:

1. Total Metrics :
    - Total Confirmed Cases
    - Total Deaths
    - Survival Rate
    - Death Rate

2. Division-wise Analysis :
    - Bar chart: Survival rate by division.
    - Line chart: Confirmed vs. Deaths over time.
    - Table: Detailed metrics per division (Confirmed Cases, Deaths, Survival Rate, Death Rate).

3. Time Series Analysis :
    - Line charts showing trends in confirmed cases, deaths, and rates over time.

4. Interactive Filters :
    - Division selector to filter visuals dynamically.


## Installation

1. **Clone the repository:**

    ```bash
    git clone https://github.com/tshihab07/Covid19-Analytical-Dashboard-of-Bangladesh.git
    ```
2. **Navigate to the project directory:**

    ```bash
    cd Covid19-Analytical-Dashboard-of-Bangladesh
    ```
3. Load the Data: Load the data into your visualization tool and ensure the data fields align with the visualizations.
4. Run the Dashboard: If using Power BI, open the .pbix file to view and interact with the dashboard.


## File Structure
This repository contains the following files:
```bash
COVID-19-ANALYTICAL-DASHBOARD/
├── .pbi
│   ├── bg2848537029008278.jpg
│   ├── SharedResources/
│   │   ├── BaseThemes/
│   │   │   └── CY24SU08.json
│   │   ├── definition.pbir
│   │   ├── report.json
│   ├── AnalyticalDashboard.SemanticModel/
│   │   ├── .platform
│   │   ├── definition.pbism
│   │   ├── diagramLayout.json
│   │   └── model.bim
│   ├── files/
│   │   ├── bg-template.pptx
│   │   ├── covid_dataset_cleaned.csv
│   │   ├── covid_dataset_unpivot.csv
│   │   └── covid_dataset.csv
│   ├── graphs/
│   │   ├── boxplots.png
│   │   ├── CaseRate_VS_DeathsRate_Relation.png
│   │   └── ConfirmedCase_VS_CaseRate_Relation.png
└── README.md
```


## Methodology

### 1. **Data Cleaning & Processing**
- Filled missing values using `group-wise median imputation`
- Converted wide format to long format (unpivoted)
- Standardized dates and formatted correctly
- Removed fully-NaN rows
- Treated outliers using IQR and Z-score where appropriate

### 2. **Exploratory Data Analysis**
- **Histograms**: To analyze distributions
- **Boxplots**: To detect outliers
- **Scatter Plots**: To explore correlations between case rate and death rate
- **Heatmaps**: For correlation among features

### 3. **Feature Engineering**
- `Total Survival` = `Confirmed Cases` - `Deaths`
- `Survival Rate` = `(Total Survival / Confirmed Cases) * 100`
- `Death Rate` = `(Deaths / Confirmed Cases) * 100`


## Usage

1. Install Required Tools
    - Power BI Desktop : Download and install from Microsoft Power BI .
    - Python (Optional): If you want to reproduce the data cleaning steps.

2. Open the Power BI Report
    - Open Power BI Desktop .
    - Navigate to the .pbi directory and open AnalyticalDashboard.Report.
    - Ensure that the data sources are correctly linked to the cleaned CSV files (covid_dataset_cleaned.csv or covid_dataset_unpivot.csv).

3. Explore the Dashboard
    - Use the interactive visuals to explore trends and patterns in COVID-19 data across different divisions.
    - Apply filters (e.g., date range, division) to focus on specific regions or time periods.

4. Reproduce Data Cleaning Steps (Optional)
    - If you want to reproduce the data cleaning process:

5. Load covid_dataset.csv into Python.
    - Follow the preprocessing steps outlined in the data_preprocessing.ipynb notebook (if available).
    - Save the cleaned dataset as covid_dataset_cleaned.csv.


## Insights

- The highest number of confirmed and death cases.
- The second-highest confirmed cases but higher survival rate.
- Comparatively low numbers but significant death percentages.
- Death rate and Survival Rate.
- Day to day comparison of confirmed cases and death cases.
- Day to day comparison of survival rate and death rate.


## Technology Used

- Power BI : For building the interactive dashboard.
- Python : For data cleaning and preprocessing.
- Jupyter Notebook : For exploratory data analysis and visualization.


## Future Enhancements

- Add vaccination data if available.
- Incorporate predictive analytics for future trends.
- Improve interactivity with bookmarks and custom visuals.


## Contributing

Contributions are welcome! If you'd like to contribute:

- Fork the repository.
- Make changes and submit a pull request.
- Ensure that any new features or improvements are well-documented.

## License

This project is licensed under the [MIT License](LICENSE).

## Contact

E-mail: tushar.shihab13@gmail.com <br>
More Projects: 👉🏿 [Projects](https://github.com/tshihab07?tab=repositories)<br>
LinkedIn: [Tushar Shihab](https://www.linkedin.com/in/tshihab07/)