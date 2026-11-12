# DA401 Capstone Project - Gus Nelson

## Project Title
Structural Change in the U.S. Energy Industry as Solar Grows, 2015–2025

## Research Question
Which parts of the U.S. energy industry have grown and which have shrunk from 2015 through 2025, using solar's increasing share of electricity generation as a reference point?

This project examines changes in the U.S. electricity generation mix alongside changes in energy-related employment. It focuses on whether shifts in electricity generation are reflected in employment trends across fossil and non-fossil energy sectors.

## Data Source
U.S. Energy Information Administration (EIA): Annual U.S. electricity generation data by energy source, covering 2015–2025.

U.S. Bureau of Labor Statistics (BLS): Monthly employment estimates for fossil and non-fossil electric power generation, averaged by calendar year.

U.S. Department of Energy (DOE): Supporting background information on energy employment and industry trends.

The generation analysis examines coal, natural gas, nuclear, solar, and wind. Fossil generation is grouped as coal and natural gas, while non-fossil generation is grouped as nuclear, solar, and wind. Employment is analyzed using broader fossil and non-fossil categories. Because the employment data do not separate every energy source, the project cannot directly identify solar-specific job growth.
## Methods
This project uses quantitative, observational analysis to examine changes in electricity generation and employment over the 2015–2025 period. No variables are manipulated, and the analysis is not designed to establish causation.

Methods used include:
* Descriptive trend analysis: Examining how electricity generation shares and employment levels changed over time.

* Year-over-year change analysis: Comparing annual changes in generation shares with annual percentage changes in employment.

* Pearson correlation: Measuring the strength and direction of the relationship between generation-share changes and employment changes, both overall and separately for fossil and non-fossil categories.

* Category-adjusted OLS regression: Examining the relationship between generation changes and employment changes while accounting for differences between fossil and non-fossil categories.

* Interaction regression: Testing whether the relationship between generation changes and employment changes differs between the two categories.

* Regression diagnostics: Checking model assumptions and potential issues involving residual normality, heteroskedasticity, multicollinearity, and autocorrelation.

The analysis was conducted in Python using Marimo, pandas, SciPy, statsmodels, and Matplotlib.

## Expected Timeline
* Research design: Finalized the research question, study period, and overall approach.

* Data collection: Retrieved annual electricity generation data from EIA and employment data from BLS.

* Data preparation: Cleaned, organized, and combined the datasets into annual observations covering 2015–2025.

* Exploratory analysis: Examined generation and employment trends across fossil and non-fossil categories.

* Statistical analysis: Calculated year-over-year changes, Pearson correlations, regression models, and diagnostic tests.

* Writing and revision: Developed the figures, tables, findings, limitations, and final research paper.

## Google Drive 
https://drive.google.com/drive/folders/1P5T_nhLKAnS6GhX-vkfgK9L4vTIZaTGX?usp=drive_link

## Repository Structure
- code/: Python analysis scripts and Marimo notebooks.

- writing/: Research proposal, paper drafts, and final paper.

- figures/: Graphs, charts, and other visualizations used in the analysis.

- data/: Small sample datasets and documentation. Large datasets are stored in Google Drive.
