# Internet Access Among Single-Person Households in Europe

**A Data Visualization course project** exploring changes in household internet access across Europe using official Eurostat statistics. The work combines Python-based data preparation with time-series and country-comparison visualizations.

## Project Overview

**Research question:** How has internet access changed over time among single-person households in European countries?

The project also investigates how **Italy** compares with **Germany, France, and the EU-27 aggregate**, which geographies have the highest access levels in the latest available year, and whether disparities persist.

The submitted report describes strong long-term growth, a narrowing of some country differences, and remaining gaps in the latest observations. These are **descriptive patterns**, not a causal analysis of digital infrastructure or public policy.

## Visualizations

### Trends over time

![Time-series chart of internet access among single-person households](assets/time_series.png)

A line chart compares Italy, Germany, France, and the EU-27 aggregate over time. Also see the [published Datawrapper time-series graphic](https://datawrapper.dwcdn.net/7kElk/1/) referenced in the report.

### Latest-year comparison

![Top 15 geographies by latest-year percentage of single-person households with internet access](assets/country_ranking.png)

The notebook creates top-15 and bottom-15 horizontal bar charts and exports a comparison table. The original ranking can include **regional aggregates** (e.g., EU-27 or Euro area), so the notebook's visual is a ranking of *geographies*, not necessarily 15 independent countries. See the [published Flourish comparison](https://public.flourish.studio/visualisation/27197512/) referenced in the report.

The embedded images above are extracted from the submitted notebook's saved outputs; they have not been regenerated from a newly downloaded dataset.

## Dataset

- **Provider:** [Eurostat](https://ec.europa.eu/eurostat/databrowser/view/isoc_ci_in_h/default/table?lang=en)
- **Dataset:** `isoc_ci_in_h` — *Households: level of internet access* ([DOI: 10.2908/isoc_ci_in_h](https://doi.org/10.2908/isoc_ci_in_h))
- **Filters used in the notebook:** annual frequency (`freq == "A"`), percentage of households (`unit == "PC_HH"`), and single-person households (`hhtyp == "A1"`)
- **Measure:** percentage of single-person households with home internet access
- **Data availability:** the precise number of countries and the latest usable year depend on the Eurostat export used.

The source CSV is not included in this repository. The original notebook expects a Eurostat **CSV export containing the descriptive label columns** (e.g., `Type of household` and `Geopolitical entity (reporting)`); an API/TSV export with different headers will require corresponding column-name adjustments.

## Methods and Implementation

1. Load the Eurostat CSV into a Pandas DataFrame.
2. Retain relevant columns, normalize names, and convert year/access values to numeric.
3. Keep annual percentage observations for single-person households and remove observations missing essential values.
4. Pivot the observations for selected European geographies into a time-series table.
5. Identify the most recent year in the provided dataset; aggregate observations by geography and sort by percentage.
6. Export analysis tables to CSV and create line/bar charts using Matplotlib.

**Tools:** Python, Pandas, Matplotlib, Jupyter Notebook, Google Colab (optional), Datawrapper and Flourish (for the graphics linked in the report).

## Repository Structure

```text
internet-access-single-person-households-europe/
├── README.md
├── internet_access_analysis.ipynb
├── project_report.pdf            # Public-safe copy: student ID/email hidden
├── requirements.txt
├── .gitignore
├── assets/
│   ├── time_series.png
│   └── country_ranking.png
└── data/
    └── .gitkeep                 # Download the source CSV separately
```

## How to Run

1. Download dataset `isoc_ci_in_h` from [Eurostat](https://ec.europa.eu/eurostat/databrowser/view/isoc_ci_in_h/default/table?lang=en). Export as CSV with both code and descriptive label columns, matching the original course export.
2. Save the file as `data/isoc_ci_in_h_linear_2_0.csv`, relative to the working directory where Jupyter is launched. Alternatively, set `EUROSTAT_CSV` to an absolute path for the downloaded CSV.
3. Install Python dependencies and start Jupyter:

   ```bash
   python -m pip install -r requirements.txt
   jupyter notebook
   ```

4. Open `internet_access_analysis.ipynb` and run cells in order. The original author's Google Colab Drive location is supported as a fallback if the relative CSV is not present.
5. The notebook writes two CSV files to the **current working directory**:
   - `viz1_single_person_time_series.csv`
   - `viz2_single_person_country_comparison_<year>.csv`

**Note:** This repository packages the submitted analysis. It does not download the Eurostat dataset automatically and requires the original column layout. Previous notebook outputs may differ from newer Eurostat revisions.

## Findings and Limitations

**Findings documented in the course report:**
- Internet access grew substantially among single-person households in Europe.
- Italy showed catch-up relative to some major European benchmarks.
- Access levels converged at high values in recent years, but cross-country differences remain.

**Interpretation limits:** missing country-year values; potential survey/methodology differences and time-series breaks; no urban/rural split in this analysis; regional aggregates included in the original ranking; and no causal identification of the factors driving access.

## Report and Attribution

See [project_report.pdf](project_report.pdf) for the course presentation and discussion of the results. The report identifies **Mahsa Bahri** as its author and states that the slides are licensed under **[CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/)**. A public-safe report copy removes student ID and email from its title page. That slide license does **not automatically assign a license to the notebook code**.

**Data source:** Eurostat, *Households — level of internet access* (`isoc_ci_in_h`), DOI [10.2908/isoc_ci_in_h](https://doi.org/10.2908/isoc_ci_in_h).
