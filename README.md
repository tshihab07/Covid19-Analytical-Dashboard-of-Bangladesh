# COVID-19 Data Analytical Dashboard of Bangladesh

## Table of Contents

- [Overview](#overview)
- [Data Source](#data-source)
    - [Dataset Description](#data-description)
- [Key Features](#key-features)
    - [Filters & Slicers](#filters--slicers)
    - [Visual Components](#visual-components)
- [Installation](#installation)
- [File Structure](#file-structure)
- [Methodology](#methodoloogy)
    - [Data Cleaning & Processing](#1-data-cleaning--processing)
    - [Exploratory Data Analysis](#2-exploratory-data-analysis)
    - [Missing Value Handling](#3-Missing-Value-Handling)
    - [Outliers Treatment](#4-outliers-treatment)
    - [Feature Engineering](#5-feature-engineering)
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

The dataset used in this project is sourced from Kaggle. To get data used in this project, click [Dataset](https://www.kaggle.com/datasets/rashikrahmanpritom/covid19-cases-in-bangladesh-dataset). This dataset contains COVID-19 cases of all the divisions in Bangladesh from 1st March 2020 to 2nd July 2021.

### Dataset Description
| Column Name                 | Description                             |
|-----------------------------|-----------------------------------------|
| Date                        | Record date (daily granularity)         |
| Division                    | Name of the administrative division     |
| Confirmed Cases             | Total confirmed cases per day/division  |
| Deaths                      | Total reported deaths per day/division  |
| Case Rate                   | Cases per 100,000 population (estimated)|
| Death Rate                  | Deaths per 100,000 population (estimated)|

All values are **cleaned**, **normalized**, and **processed**. Missing values were handled using `interpolation` and `forward fill` due to skewed time series.


## Key Features

### Filters & Slicers
- **Division Slicer**: Select division to see individual analysis
- **Metric Slicers**: Toggle between Confirmed/Deaths/Survival

### Visual Components
Here are the most useful visuals included in the final dashboard:

1. **Time-Series Analysis**
    - Line chart showing trends over time for confirmed cases vs deaths and confirmed cases vs survival.
    - Filterable by metric selector.

2. **Division-wise Comparison**
    - Clustered bar charts comparing total confirmed cases vs Survival
    - Impact table showing confirmed cases, deaths, survival rate, case rate, and death rate for each division.

4. **Distribution Charts**
    - Donut chart displaying the overall survival rate and death rate across Bangladesh
    - Bar chart displaying total confirmed cases for each division

5. **Summary Metrics**
    - Total confirmed cases
    - Total deaths
    - Total Survival

6. **Interactive Filters**
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
├── AnalyticalDashboard.Report/
│   ├── .pbi/
│   │   │   └── localSettings.json
│   ├── StaticResources/
│   │   │   └── RegisteredResources/
│   │   │   │   └── bg2848537029008278.jpg
│   ├── SharedResources/
│   │   │   └── CY24SU08.json
│   │   ├── definition.pbir
│   │   ├── report.json
├── AnalyticalDashboard.SemanticModel/
│   │   ├── .platform
│   │   ├── definition.pbism
│   │   ├── diagramLayout.json
│   │   └── model.bim
├── files/
│   │   ├── bg-template.pptx
│   │   ├── covid_dataset_cleaned.csv
│   │   ├── covid_dataset_unpivot.csv
│   │   └── covid_dataset.csv
├── graphs/
│   │   ├── boxplots.png
│   │   ├── CaseRate_VS_DeathsRate_Relation.png
│   │   └── ConfirmedCase_VS_CaseRate_Relation.png
├── output
│   ├── bg.jpg
│   ├── dashboard.png
│   ├── initial_dashboard_design.jpg
├── .gitignore
├── AnalyticalDashboard.pbix
├── AnalyticalDashboard.pbip
├── data_preprocessing.ipynb
└── README.md
```


## Methodology

### 1. Data Cleaning & Processing
Before importing the data into Power BI, it underwent several important preprocessing steps in Python:

1. Date Formatting
    - The `Date` column was parsed correctly using `pd.to_datetime()` with a custom format.
    - Missing or inconsistent dates were coerced to `NaT` and corrected if possible.
2. Data Type Handling
    - All numeric columns were converted to numeric types using pd.to_numeric().
    - Non-numeric values were set to `NaN` and later handled appropriately.
3. Column Renaming & Division List
    - Standardized column names for consistency.
    - Defined list of divisions: `Barisal`, `Chittagong`, `Dhaka`, `Khulna`, `Mymensingh`, `Rajshahi`, `Rangpur`, `Sylhet`.

### 2. Exploratory Data Analysis
- **Histograms**: To analyze distributions
- **Boxplots**: To detect outliers
- **Scatter Plots**: To explore correlations between case rate and death rate

### 3. Missing Value Handling
Handling missing values was done carefully based on the type of metric:

1. Confirmed Cases & Deaths
    - These represent real-world events — missing values likely mean no activity .
    - Therefore, all missing values in these columns were filled with 0.

2. Rate Columns (Case Rate, Death Rate)
    - Rates should only be calculated when there are confirmed cases or deaths.
    - We interpolated rate values only where confirmed cases > 0, to avoid introducing false trends.
    - Remaining missing values (e.g., at the start/end of the time series) were filled using forward/backward fill.

This ensures:
- No artificial rates appear where no cases existed
- Smooth trends where data was sparse but active

### 4. Outliers Treatment
Outliers can distort visualizations and analysis. To handle them effectively:
We applied a **`rolling window approach`** to detect and cap extreme values dynamically, where each division’s confirmed cases and deaths were processed separately.

This helps:
 - Reduce noise while preserving actual surges
 - Prevent false peaks from distorting visualizations

### 5. Feature Engineering
- `Total Survival` = `Confirmed Cases` - `Deaths`
- `Survival Rate` = `(Total Survival / Confirmed Cases) * 100`
- `Death Rate` = `(Deaths / Confirmed Cases) * 100`


## Usage

1. Install Required Tools
    - Power BI Desktop: Download and install from Microsoft Power BI.
    - Python (Optional): If you want to reproduce the data cleaning steps.

2. Open the Power BI Report
    - Open Power BI Desktop.
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
- The second-highest confirmed cases, but higher survival rate.
- Comparatively low numbers but significant death percentages.
- Death Rate and Survival Rate.
- Day-to-day comparison of confirmed cases and deaths.
- Day-to-day comparison of survival rate and death rate.


## Technology Used

- Power BI: For building the interactive dashboard.
- Python: For data cleaning and preprocessing.
- Jupyter Notebook: For exploratory data analysis and visualization.


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
