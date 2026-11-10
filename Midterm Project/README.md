# Education and Poverty Across U.S. Counties

ECON 3916 Midterm Project - Subeen Jung

## Question
Do U.S. counties with a higher share of adults (25+) holding a bachelor's degree have lower poverty rates, after controlling for rural–urban status, median age, and state?

## Data
- **ACS 2020–2024 5-year estimates** (U.S. Census Bureau): S1701 (poverty rate), S1501 (bachelor's share, adults 25+), B01002 (median age). https://data.census.gov
- **Rural-Urban Continuum Codes 2023** (USDA Economic Research Service). https://www.ers.usda.gov/data-products/rural-urban-continuum-codes
- Downloaded on November 3, 2026. All four files are in the `data/` folder.
- The files are joined on the 5-digit county FIPS code. Puerto Rico is dropped, leaving 3,144 counties (50 states + DC).

## How to run
1. Open `Econ_3916_Midterm.ipynb` in Google Colab.
2. Upload the four files from the `data/` folder into Colab's `content` folder (Files panel on the left).
3. Run **Runtime → Run all**. The last cell, *Numbers my report quotes*, prints every number used in the report.

## Headline finding
Within the same state, rural–urban category, and median age, a county with a 1-percentage-point higher bachelor's share has a poverty rate about 0.19 points lower (95% CI: −0.22 to −0.15, SEs clustered by state). The result holds with population weights, without influential counties, and in logs. It is an association, not a causal effect: college graduates may also move to places that already have good jobs.

## Files
- `Econ_3916_Midterm.ipynb`: analysis notebook
- `Econ3916 Midterm Project.pdf`: written report
- `data/`: the four raw data files
