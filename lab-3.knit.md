---
title: "Lab 03: COVID-19 Data Wrangling and Visualization"
author: "Yazeed Aljohani"
subtitle: "Data Wrangling and Visualization in R"
date: "2025-03-09"
format: 
  html:
    self-contained: true
    toc: true
execute:
  echo: true
output-dir: "docs"
theme: journal
editor: visual
---



# **Question 1: Public Data**

**Take a moment to reflect on the value of open data: How does easy access to historical and real-time environmental data shape our understanding of climate trends, resource management, and public health? What happens when this data disappears or becomes inaccessible? The role of independent archiving and collaborative stewardship has never been more critical in ensuring scientific progress and accountability.**

Open access to environmental and health data plays a crucial role in helping researchers, policymakers, and the public make informed decisions. Real-time and historical data offer valuable insights into climate trends, resource management, and public health. When this information disappears, transparency and trust are lost, and collaboration between scientists becomes more difficult. Without reliable data, it is harder to track long-term environmental changes or assess the effectiveness of policies. Thankfully, journalists, researchers, and scientists work to archive and protect these records. Platforms like The Internet Archive and Data Refuge help ensure that vital datasets remain available for future use. The New York Times COVID-19 data repository is a prime example of why independent data preservation matters. Its county-level records have been crucial for tracking the pandemic and informing public health responses. Maintaining open access to data is essential for scientific progress and accountability. Efforts to preserve information will support future research and responsible decision-making.

# **Question 2: Daily Summary**





::: {.cell}

```{.r .cell-code}
# 1- Reading in the data

data <- read_csv('https://raw.githubusercontent.com/nytimes/covid-19-data/master/us-counties.csv')
```

::: {.cell-output .cell-output-stderr}

```
Rows: 2502832 Columns: 6
── Column specification ────────────────────────────────────────────────────────
Delimiter: ","
chr  (3): county, state, fips
dbl  (2): cases, deaths
date (1): date

ℹ Use `spec()` to retrieve the full column specification for this data.
ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```


:::
:::



**Data Description:**

The dataset contains 2,502,832 rows and 6 columns, recording COVID-19 case data at the county level across the U.S.

### **Columns:** 

1.  **`date`** – The date of the recorded data.

2.  **`county`** – The name of the county.

3.  **`state`** – The state where the county is located.

4.  **`fips`** – A **5-digit code** identifying each county (first 2 digits = state, last 3 = county).

5.  **`cases`** – The **total** number of confirmed cases (cumulative).

6.  **`deaths`** – The **total** number of reported deaths (cumulative).

2.  **Create an object called `my.date` and set it as “2022-02-01” - ensure this is a `date` object:. Create a object called `my.state` and set it to “Colorado”.**



::: {.cell}

```{.r .cell-code}
# 2- Defining Date and State Variables

my.date <- as.Date("2022-02-01")
my.state <- "Colorado"
```
:::



3.  **The URL based data read from Github is considered our “raw data”. Remember to always leave “raw-data-raw” and to generate meaningful subsets as you go.**



::: {.cell}

```{.r .cell-code}
# 3- Filtering for Colorado and Compute New Cases
colorado <- data |>
filter(state == my.state) |>
group_by(county) |>
arrange(date) |>
mutate(new_cases = cases - lag(cases),
new_deaths = deaths - lag(deaths)) |>
ungroup()
```
:::



4.  **Using your subset, generate (2) tables. The first should show the 5 counties with the most CUMULATIVE cases, and the second should show the 5 counties with the most NEW cases. Remember to use your `my.date` object as a proxy for today’s date:**



::: {.cell}

```{.r .cell-code}
# 4- Finding the 5 Counties with the Most Cumulative Cases
filter (colorado, date == my.date) |>

slice_max(cases, n = 5) |>

select(Date = date, County = county, Cases = cases) |>

flextable() |>

add_header_lines("Most Cumulative Cases")
```

::: {.cell-output-display}

```{=html}
<div class="tabwid"><style>.cl-8d4f2520{}.cl-8d345ae2{font-family:'Arial';font-size:11pt;font-weight:normal;font-style:normal;text-decoration:none;color:rgba(0, 0, 0, 1.00);background-color:transparent;}.cl-8d394eda{margin:0;text-align:right;border-bottom: 0 solid rgba(0, 0, 0, 1.00);border-top: 0 solid rgba(0, 0, 0, 1.00);border-left: 0 solid rgba(0, 0, 0, 1.00);border-right: 0 solid rgba(0, 0, 0, 1.00);padding-bottom:5pt;padding-top:5pt;padding-left:5pt;padding-right:5pt;line-height: 1;background-color:transparent;}.cl-8d394ef8{margin:0;text-align:left;border-bottom: 0 solid rgba(0, 0, 0, 1.00);border-top: 0 solid rgba(0, 0, 0, 1.00);border-left: 0 solid rgba(0, 0, 0, 1.00);border-right: 0 solid rgba(0, 0, 0, 1.00);padding-bottom:5pt;padding-top:5pt;padding-left:5pt;padding-right:5pt;line-height: 1;background-color:transparent;}.cl-8d39764e{width:0.75in;background-color:transparent;vertical-align: middle;border-bottom: 1.5pt solid rgba(102, 102, 102, 1.00);border-top: 1.5pt solid rgba(102, 102, 102, 1.00);border-left: 0 solid rgba(0, 0, 0, 1.00);border-right: 0 solid rgba(0, 0, 0, 1.00);margin-bottom:0;margin-top:0;margin-left:0;margin-right:0;}.cl-8d397658{width:0.75in;background-color:transparent;vertical-align: middle;border-bottom: 1.5pt solid rgba(102, 102, 102, 1.00);border-top: 1.5pt solid rgba(102, 102, 102, 1.00);border-left: 0 solid rgba(0, 0, 0, 1.00);border-right: 0 solid rgba(0, 0, 0, 1.00);margin-bottom:0;margin-top:0;margin-left:0;margin-right:0;}.cl-8d397659{width:0.75in;background-color:transparent;vertical-align: middle;border-bottom: 0 solid rgba(0, 0, 0, 1.00);border-top: 0 solid rgba(0, 0, 0, 1.00);border-left: 0 solid rgba(0, 0, 0, 1.00);border-right: 0 solid rgba(0, 0, 0, 1.00);margin-bottom:0;margin-top:0;margin-left:0;margin-right:0;}.cl-8d397662{width:0.75in;background-color:transparent;vertical-align: middle;border-bottom: 0 solid rgba(0, 0, 0, 1.00);border-top: 0 solid rgba(0, 0, 0, 1.00);border-left: 0 solid rgba(0, 0, 0, 1.00);border-right: 0 solid rgba(0, 0, 0, 1.00);margin-bottom:0;margin-top:0;margin-left:0;margin-right:0;}.cl-8d397716{width:0.75in;background-color:transparent;vertical-align: middle;border-bottom: 1.5pt solid rgba(102, 102, 102, 1.00);border-top: 0 solid rgba(0, 0, 0, 1.00);border-left: 0 solid rgba(0, 0, 0, 1.00);border-right: 0 solid rgba(0, 0, 0, 1.00);margin-bottom:0;margin-top:0;margin-left:0;margin-right:0;}.cl-8d397720{width:0.75in;background-color:transparent;vertical-align: middle;border-bottom: 1.5pt solid rgba(102, 102, 102, 1.00);border-top: 0 solid rgba(0, 0, 0, 1.00);border-left: 0 solid rgba(0, 0, 0, 1.00);border-right: 0 solid rgba(0, 0, 0, 1.00);margin-bottom:0;margin-top:0;margin-left:0;margin-right:0;}</style><table data-quarto-disable-processing='true' class='cl-8d4f2520'><thead><tr style="overflow-wrap:break-word;"><th  colspan="3"class="cl-8d39764e"><p class="cl-8d394eda"><span class="cl-8d345ae2">Most Cumulative Cases</span></p></th></tr><tr style="overflow-wrap:break-word;"><th class="cl-8d39764e"><p class="cl-8d394eda"><span class="cl-8d345ae2">Date</span></p></th><th class="cl-8d397658"><p class="cl-8d394ef8"><span class="cl-8d345ae2">County</span></p></th><th class="cl-8d39764e"><p class="cl-8d394eda"><span class="cl-8d345ae2">Cases</span></p></th></tr></thead><tbody><tr style="overflow-wrap:break-word;"><td class="cl-8d397659"><p class="cl-8d394eda"><span class="cl-8d345ae2">2022-02-01</span></p></td><td class="cl-8d397662"><p class="cl-8d394ef8"><span class="cl-8d345ae2">El Paso</span></p></td><td class="cl-8d397659"><p class="cl-8d394eda"><span class="cl-8d345ae2">170,673</span></p></td></tr><tr style="overflow-wrap:break-word;"><td class="cl-8d397659"><p class="cl-8d394eda"><span class="cl-8d345ae2">2022-02-01</span></p></td><td class="cl-8d397662"><p class="cl-8d394ef8"><span class="cl-8d345ae2">Denver</span></p></td><td class="cl-8d397659"><p class="cl-8d394eda"><span class="cl-8d345ae2">159,022</span></p></td></tr><tr style="overflow-wrap:break-word;"><td class="cl-8d397659"><p class="cl-8d394eda"><span class="cl-8d345ae2">2022-02-01</span></p></td><td class="cl-8d397662"><p class="cl-8d394ef8"><span class="cl-8d345ae2">Arapahoe</span></p></td><td class="cl-8d397659"><p class="cl-8d394eda"><span class="cl-8d345ae2">144,255</span></p></td></tr><tr style="overflow-wrap:break-word;"><td class="cl-8d397659"><p class="cl-8d394eda"><span class="cl-8d345ae2">2022-02-01</span></p></td><td class="cl-8d397662"><p class="cl-8d394ef8"><span class="cl-8d345ae2">Adams</span></p></td><td class="cl-8d397659"><p class="cl-8d394eda"><span class="cl-8d345ae2">126,768</span></p></td></tr><tr style="overflow-wrap:break-word;"><td class="cl-8d397716"><p class="cl-8d394eda"><span class="cl-8d345ae2">2022-02-01</span></p></td><td class="cl-8d397720"><p class="cl-8d394ef8"><span class="cl-8d345ae2">Jefferson</span></p></td><td class="cl-8d397716"><p class="cl-8d394eda"><span class="cl-8d345ae2">113,240</span></p></td></tr></tbody></table></div>
```

:::
:::



The table shows the five Colorado counties with the highest cumulative COVID-19 cases as of February 1, 2022. El Paso, Denver, Arapahoe, Adams, and Jefferson had the most confirmed cases



::: {.cell}

```{.r .cell-code}
# 4- Finding the 5 Counties with the Most New Cases

filter(colorado, date == my.date) |>
slice_max(cases, n = 5) |>
select(Date = date, County = county, Cases = new_cases) |>
flextable() |>
add_header_lines("Most New Cases")
```

::: {.cell-output-display}

```{=html}
<div class="tabwid"><style>.cl-8d6e96e4{}.cl-8d635c0c{font-family:'Arial';font-size:11pt;font-weight:normal;font-style:normal;text-decoration:none;color:rgba(0, 0, 0, 1.00);background-color:transparent;}.cl-8d679998{margin:0;text-align:right;border-bottom: 0 solid rgba(0, 0, 0, 1.00);border-top: 0 solid rgba(0, 0, 0, 1.00);border-left: 0 solid rgba(0, 0, 0, 1.00);border-right: 0 solid rgba(0, 0, 0, 1.00);padding-bottom:5pt;padding-top:5pt;padding-left:5pt;padding-right:5pt;line-height: 1;background-color:transparent;}.cl-8d6799ac{margin:0;text-align:left;border-bottom: 0 solid rgba(0, 0, 0, 1.00);border-top: 0 solid rgba(0, 0, 0, 1.00);border-left: 0 solid rgba(0, 0, 0, 1.00);border-right: 0 solid rgba(0, 0, 0, 1.00);padding-bottom:5pt;padding-top:5pt;padding-left:5pt;padding-right:5pt;line-height: 1;background-color:transparent;}.cl-8d67c18e{width:0.75in;background-color:transparent;vertical-align: middle;border-bottom: 1.5pt solid rgba(102, 102, 102, 1.00);border-top: 1.5pt solid rgba(102, 102, 102, 1.00);border-left: 0 solid rgba(0, 0, 0, 1.00);border-right: 0 solid rgba(0, 0, 0, 1.00);margin-bottom:0;margin-top:0;margin-left:0;margin-right:0;}.cl-8d67c198{width:0.75in;background-color:transparent;vertical-align: middle;border-bottom: 1.5pt solid rgba(102, 102, 102, 1.00);border-top: 1.5pt solid rgba(102, 102, 102, 1.00);border-left: 0 solid rgba(0, 0, 0, 1.00);border-right: 0 solid rgba(0, 0, 0, 1.00);margin-bottom:0;margin-top:0;margin-left:0;margin-right:0;}.cl-8d67c199{width:0.75in;background-color:transparent;vertical-align: middle;border-bottom: 0 solid rgba(0, 0, 0, 1.00);border-top: 0 solid rgba(0, 0, 0, 1.00);border-left: 0 solid rgba(0, 0, 0, 1.00);border-right: 0 solid rgba(0, 0, 0, 1.00);margin-bottom:0;margin-top:0;margin-left:0;margin-right:0;}.cl-8d67c1a2{width:0.75in;background-color:transparent;vertical-align: middle;border-bottom: 0 solid rgba(0, 0, 0, 1.00);border-top: 0 solid rgba(0, 0, 0, 1.00);border-left: 0 solid rgba(0, 0, 0, 1.00);border-right: 0 solid rgba(0, 0, 0, 1.00);margin-bottom:0;margin-top:0;margin-left:0;margin-right:0;}.cl-8d67c1a3{width:0.75in;background-color:transparent;vertical-align: middle;border-bottom: 1.5pt solid rgba(102, 102, 102, 1.00);border-top: 0 solid rgba(0, 0, 0, 1.00);border-left: 0 solid rgba(0, 0, 0, 1.00);border-right: 0 solid rgba(0, 0, 0, 1.00);margin-bottom:0;margin-top:0;margin-left:0;margin-right:0;}.cl-8d67c1ac{width:0.75in;background-color:transparent;vertical-align: middle;border-bottom: 1.5pt solid rgba(102, 102, 102, 1.00);border-top: 0 solid rgba(0, 0, 0, 1.00);border-left: 0 solid rgba(0, 0, 0, 1.00);border-right: 0 solid rgba(0, 0, 0, 1.00);margin-bottom:0;margin-top:0;margin-left:0;margin-right:0;}</style><table data-quarto-disable-processing='true' class='cl-8d6e96e4'><thead><tr style="overflow-wrap:break-word;"><th  colspan="3"class="cl-8d67c18e"><p class="cl-8d679998"><span class="cl-8d635c0c">Most New Cases</span></p></th></tr><tr style="overflow-wrap:break-word;"><th class="cl-8d67c18e"><p class="cl-8d679998"><span class="cl-8d635c0c">Date</span></p></th><th class="cl-8d67c198"><p class="cl-8d6799ac"><span class="cl-8d635c0c">County</span></p></th><th class="cl-8d67c18e"><p class="cl-8d679998"><span class="cl-8d635c0c">Cases</span></p></th></tr></thead><tbody><tr style="overflow-wrap:break-word;"><td class="cl-8d67c199"><p class="cl-8d679998"><span class="cl-8d635c0c">2022-02-01</span></p></td><td class="cl-8d67c1a2"><p class="cl-8d6799ac"><span class="cl-8d635c0c">El Paso</span></p></td><td class="cl-8d67c199"><p class="cl-8d679998"><span class="cl-8d635c0c">630</span></p></td></tr><tr style="overflow-wrap:break-word;"><td class="cl-8d67c199"><p class="cl-8d679998"><span class="cl-8d635c0c">2022-02-01</span></p></td><td class="cl-8d67c1a2"><p class="cl-8d6799ac"><span class="cl-8d635c0c">Denver</span></p></td><td class="cl-8d67c199"><p class="cl-8d679998"><span class="cl-8d635c0c">389</span></p></td></tr><tr style="overflow-wrap:break-word;"><td class="cl-8d67c199"><p class="cl-8d679998"><span class="cl-8d635c0c">2022-02-01</span></p></td><td class="cl-8d67c1a2"><p class="cl-8d6799ac"><span class="cl-8d635c0c">Arapahoe</span></p></td><td class="cl-8d67c199"><p class="cl-8d679998"><span class="cl-8d635c0c">401</span></p></td></tr><tr style="overflow-wrap:break-word;"><td class="cl-8d67c199"><p class="cl-8d679998"><span class="cl-8d635c0c">2022-02-01</span></p></td><td class="cl-8d67c1a2"><p class="cl-8d6799ac"><span class="cl-8d635c0c">Adams</span></p></td><td class="cl-8d67c199"><p class="cl-8d679998"><span class="cl-8d635c0c">326</span></p></td></tr><tr style="overflow-wrap:break-word;"><td class="cl-8d67c1a3"><p class="cl-8d679998"><span class="cl-8d635c0c">2022-02-01</span></p></td><td class="cl-8d67c1ac"><p class="cl-8d6799ac"><span class="cl-8d635c0c">Jefferson</span></p></td><td class="cl-8d67c1a3"><p class="cl-8d679998"><span class="cl-8d635c0c">291</span></p></td></tr></tbody></table></div>
```

:::
:::



The table displays the five Colorado counties with the highest new COVID-19 cases on February 1, 2022. El Paso, Denver, Arapahoe, Adams, and Jefferson reported the most new infections, indicating higher transmission rates in these areas on that date.

# **Question 3: Normalizing Data**



::: {.cell}

```{.r .cell-code}
# Define the URL
pop_url <- 'https://www2.census.gov/programs-surveys/popest/datasets/2020-2023/counties/totals/co-est2023-alldata.csv'

# Read the population data
pop <- read.csv(pop_url)
```
:::



1.  **Given the above URL, and guidelines on string concatenation and formatting, read in the population data and (1) create a five digit FIP variable and only keep columns that contain “NAME” or “2021” (remember the tidyselect option found with `?dplyr::select`). Additionally, remove all state level rows (e.g. COUNTY FIP == “000”)**



::: {.cell}

```{.r .cell-code}
# 1- filtering, and processing the data
pop <- read.csv(pop_url) |>
filter(COUNTY != 0) |>
mutate(fips = paste0(sprintf("%02d", STATE), sprintf("%03d", COUNTY))) |>
select(fips, contains('NAME'), contains('2021'))
```
:::



2.  **Now, explore the data … what attributes does it have, what are the names of the columns? Do any match the COVID data we have? What are the dimensions… In a few sentences describe the data obtained after modification:**







The dataset has 3,195 rows and 67 columns, providing county-level population estimates from the U.S. Census Bureau.

### **Key Details:**

-   **Geography:** It includes **state and county names** (`STNAME`, `CTYNAME`) and **FIPS codes** for identification.

-   **Population Estimates:** Covers **2020-2023** (`POPESTIMATE2020-2023`).

-   **Births & Deaths:** Tracks **annual births, deaths, and natural population changes**.

-   **Migration:** Includes **domestic and international migration** numbers per county.

-   **Growth Trends:** Shows **yearly population changes**.

### **How It Relates to COVID-19 Data:**

-   Both datasets **use FIPS codes**, so they can be **merged**.

-   **Population estimates help normalize COVID-19 data** (cases per capita).

-   **Annual data** means we’ll use **2021 estimates** for normalization.

3.  **What is the range of populations seen in Colorado counties in 2021:**



::: {.cell}

```{.r .cell-code}
range(filter(pop, STNAME == "Colorado")$POPESTIMATE2021, na.rm = TRUE)
```

::: {.cell-output .cell-output-stdout}

```
[1]    741 737287
```


:::
:::



The result \[1\] 741 737287 represents the range of populations seen in Colorado counties in 2021:

1.  741 – The smallest county population in Colorado in 2021.

2.   737287 – The largest county population in Colorado in 2021

4.  **Join the population data to the Colorado COVID data and compute the per capita cumulative cases, per capita new cases, and per capita new deaths:**



::: {.cell}

```{.r .cell-code}
# Merging COVID and population data

perCap <- inner_join(
  colorado, 
  select(pop, fips, pop = POPESTIMATE2021), 
  by = "fips"
) |>
  filter(date == my.date) |>
  mutate(
    cumPerCap = cases / pop,
    newCasesPerCap = new_cases / pop,
    newDeathsPerCap = new_deaths / pop
  )
```
:::



5.  **Generate (2) new tables. The first should show the 5 counties with the most cumulative cases per capita on 2021-01-01, and the second should show the 5 counties with the most NEW cases per capita on the same date. Your tables should have clear column names and descriptive captions.**



::: {.cell}

```{.r .cell-code}
# 5- Top 5 Counties by Cumulative Cases per Capita

perCap |>
select(County = county, Cases = cumPerCap) |>
slice_max(Cases, n = 5) |>
flextable() |>
add_header_lines("Most Cummulitive Cases Per Capita")
```

::: {.cell-output-display}

```{=html}
<div class="tabwid"><style>.cl-8e7e8f76{}.cl-8e72a5c6{font-family:'Arial';font-size:11pt;font-weight:normal;font-style:normal;text-decoration:none;color:rgba(0, 0, 0, 1.00);background-color:transparent;}.cl-8e767a34{margin:0;text-align:left;border-bottom: 0 solid rgba(0, 0, 0, 1.00);border-top: 0 solid rgba(0, 0, 0, 1.00);border-left: 0 solid rgba(0, 0, 0, 1.00);border-right: 0 solid rgba(0, 0, 0, 1.00);padding-bottom:5pt;padding-top:5pt;padding-left:5pt;padding-right:5pt;line-height: 1;background-color:transparent;}.cl-8e767a3e{margin:0;text-align:right;border-bottom: 0 solid rgba(0, 0, 0, 1.00);border-top: 0 solid rgba(0, 0, 0, 1.00);border-left: 0 solid rgba(0, 0, 0, 1.00);border-right: 0 solid rgba(0, 0, 0, 1.00);padding-bottom:5pt;padding-top:5pt;padding-left:5pt;padding-right:5pt;line-height: 1;background-color:transparent;}.cl-8e769fa0{width:0.75in;background-color:transparent;vertical-align: middle;border-bottom: 1.5pt solid rgba(102, 102, 102, 1.00);border-top: 1.5pt solid rgba(102, 102, 102, 1.00);border-left: 0 solid rgba(0, 0, 0, 1.00);border-right: 0 solid rgba(0, 0, 0, 1.00);margin-bottom:0;margin-top:0;margin-left:0;margin-right:0;}.cl-8e769faa{width:0.75in;background-color:transparent;vertical-align: middle;border-bottom: 1.5pt solid rgba(102, 102, 102, 1.00);border-top: 1.5pt solid rgba(102, 102, 102, 1.00);border-left: 0 solid rgba(0, 0, 0, 1.00);border-right: 0 solid rgba(0, 0, 0, 1.00);margin-bottom:0;margin-top:0;margin-left:0;margin-right:0;}.cl-8e769fab{width:0.75in;background-color:transparent;vertical-align: middle;border-bottom: 0 solid rgba(0, 0, 0, 1.00);border-top: 0 solid rgba(0, 0, 0, 1.00);border-left: 0 solid rgba(0, 0, 0, 1.00);border-right: 0 solid rgba(0, 0, 0, 1.00);margin-bottom:0;margin-top:0;margin-left:0;margin-right:0;}.cl-8e769fb4{width:0.75in;background-color:transparent;vertical-align: middle;border-bottom: 0 solid rgba(0, 0, 0, 1.00);border-top: 0 solid rgba(0, 0, 0, 1.00);border-left: 0 solid rgba(0, 0, 0, 1.00);border-right: 0 solid rgba(0, 0, 0, 1.00);margin-bottom:0;margin-top:0;margin-left:0;margin-right:0;}.cl-8e769fb5{width:0.75in;background-color:transparent;vertical-align: middle;border-bottom: 1.5pt solid rgba(102, 102, 102, 1.00);border-top: 0 solid rgba(0, 0, 0, 1.00);border-left: 0 solid rgba(0, 0, 0, 1.00);border-right: 0 solid rgba(0, 0, 0, 1.00);margin-bottom:0;margin-top:0;margin-left:0;margin-right:0;}.cl-8e769fbe{width:0.75in;background-color:transparent;vertical-align: middle;border-bottom: 1.5pt solid rgba(102, 102, 102, 1.00);border-top: 0 solid rgba(0, 0, 0, 1.00);border-left: 0 solid rgba(0, 0, 0, 1.00);border-right: 0 solid rgba(0, 0, 0, 1.00);margin-bottom:0;margin-top:0;margin-left:0;margin-right:0;}</style><table data-quarto-disable-processing='true' class='cl-8e7e8f76'><thead><tr style="overflow-wrap:break-word;"><th  colspan="2"class="cl-8e769fa0"><p class="cl-8e767a34"><span class="cl-8e72a5c6">Most Cummulitive Cases Per Capita</span></p></th></tr><tr style="overflow-wrap:break-word;"><th class="cl-8e769fa0"><p class="cl-8e767a34"><span class="cl-8e72a5c6">County</span></p></th><th class="cl-8e769faa"><p class="cl-8e767a3e"><span class="cl-8e72a5c6">Cases</span></p></th></tr></thead><tbody><tr style="overflow-wrap:break-word;"><td class="cl-8e769fab"><p class="cl-8e767a34"><span class="cl-8e72a5c6">Crowley</span></p></td><td class="cl-8e769fb4"><p class="cl-8e767a3e"><span class="cl-8e72a5c6">0.5117698</span></p></td></tr><tr style="overflow-wrap:break-word;"><td class="cl-8e769fab"><p class="cl-8e767a34"><span class="cl-8e72a5c6">Bent</span></p></td><td class="cl-8e769fb4"><p class="cl-8e767a3e"><span class="cl-8e72a5c6">0.4118749</span></p></td></tr><tr style="overflow-wrap:break-word;"><td class="cl-8e769fab"><p class="cl-8e767a34"><span class="cl-8e72a5c6">Pitkin</span></p></td><td class="cl-8e769fb4"><p class="cl-8e767a3e"><span class="cl-8e72a5c6">0.3429659</span></p></td></tr><tr style="overflow-wrap:break-word;"><td class="cl-8e769fab"><p class="cl-8e767a34"><span class="cl-8e72a5c6">Lincoln</span></p></td><td class="cl-8e769fb4"><p class="cl-8e767a3e"><span class="cl-8e72a5c6">0.3424082</span></p></td></tr><tr style="overflow-wrap:break-word;"><td class="cl-8e769fb5"><p class="cl-8e767a34"><span class="cl-8e72a5c6">Logan</span></p></td><td class="cl-8e769fbe"><p class="cl-8e767a3e"><span class="cl-8e72a5c6">0.3047701</span></p></td></tr></tbody></table></div>
```

:::
:::



The table ranks Colorado counties with the highest cumulative COVID-19 cases per capita as of February 1, 2022. Crowley, Bent, Pitkin, Lincoln, and Logan counties had the most infections relative to their populations



::: {.cell}

```{.r .cell-code}
# 5- Top 5 Counties by New Cases per Capitav
perCap |>
select(County = county, Cases = newCasesPerCap) |>
slice_max(Cases, n = 5) |>
flextable() |>
add_header_lines("Most New Cases Per Capita")
```

::: {.cell-output-display}

```{=html}
<div class="tabwid"><style>.cl-8e9f757e{}.cl-8e9147d8{font-family:'Arial';font-size:11pt;font-weight:normal;font-style:normal;text-decoration:none;color:rgba(0, 0, 0, 1.00);background-color:transparent;}.cl-8e97c6da{margin:0;text-align:left;border-bottom: 0 solid rgba(0, 0, 0, 1.00);border-top: 0 solid rgba(0, 0, 0, 1.00);border-left: 0 solid rgba(0, 0, 0, 1.00);border-right: 0 solid rgba(0, 0, 0, 1.00);padding-bottom:5pt;padding-top:5pt;padding-left:5pt;padding-right:5pt;line-height: 1;background-color:transparent;}.cl-8e97c6e4{margin:0;text-align:right;border-bottom: 0 solid rgba(0, 0, 0, 1.00);border-top: 0 solid rgba(0, 0, 0, 1.00);border-left: 0 solid rgba(0, 0, 0, 1.00);border-right: 0 solid rgba(0, 0, 0, 1.00);padding-bottom:5pt;padding-top:5pt;padding-left:5pt;padding-right:5pt;line-height: 1;background-color:transparent;}.cl-8e97efca{width:0.75in;background-color:transparent;vertical-align: middle;border-bottom: 1.5pt solid rgba(102, 102, 102, 1.00);border-top: 1.5pt solid rgba(102, 102, 102, 1.00);border-left: 0 solid rgba(0, 0, 0, 1.00);border-right: 0 solid rgba(0, 0, 0, 1.00);margin-bottom:0;margin-top:0;margin-left:0;margin-right:0;}.cl-8e97efcb{width:0.75in;background-color:transparent;vertical-align: middle;border-bottom: 1.5pt solid rgba(102, 102, 102, 1.00);border-top: 1.5pt solid rgba(102, 102, 102, 1.00);border-left: 0 solid rgba(0, 0, 0, 1.00);border-right: 0 solid rgba(0, 0, 0, 1.00);margin-bottom:0;margin-top:0;margin-left:0;margin-right:0;}.cl-8e97efd4{width:0.75in;background-color:transparent;vertical-align: middle;border-bottom: 0 solid rgba(0, 0, 0, 1.00);border-top: 0 solid rgba(0, 0, 0, 1.00);border-left: 0 solid rgba(0, 0, 0, 1.00);border-right: 0 solid rgba(0, 0, 0, 1.00);margin-bottom:0;margin-top:0;margin-left:0;margin-right:0;}.cl-8e97efd5{width:0.75in;background-color:transparent;vertical-align: middle;border-bottom: 0 solid rgba(0, 0, 0, 1.00);border-top: 0 solid rgba(0, 0, 0, 1.00);border-left: 0 solid rgba(0, 0, 0, 1.00);border-right: 0 solid rgba(0, 0, 0, 1.00);margin-bottom:0;margin-top:0;margin-left:0;margin-right:0;}.cl-8e97efde{width:0.75in;background-color:transparent;vertical-align: middle;border-bottom: 1.5pt solid rgba(102, 102, 102, 1.00);border-top: 0 solid rgba(0, 0, 0, 1.00);border-left: 0 solid rgba(0, 0, 0, 1.00);border-right: 0 solid rgba(0, 0, 0, 1.00);margin-bottom:0;margin-top:0;margin-left:0;margin-right:0;}.cl-8e97efdf{width:0.75in;background-color:transparent;vertical-align: middle;border-bottom: 1.5pt solid rgba(102, 102, 102, 1.00);border-top: 0 solid rgba(0, 0, 0, 1.00);border-left: 0 solid rgba(0, 0, 0, 1.00);border-right: 0 solid rgba(0, 0, 0, 1.00);margin-bottom:0;margin-top:0;margin-left:0;margin-right:0;}</style><table data-quarto-disable-processing='true' class='cl-8e9f757e'><thead><tr style="overflow-wrap:break-word;"><th  colspan="2"class="cl-8e97efca"><p class="cl-8e97c6da"><span class="cl-8e9147d8">Most New Cases Per Capita</span></p></th></tr><tr style="overflow-wrap:break-word;"><th class="cl-8e97efca"><p class="cl-8e97c6da"><span class="cl-8e9147d8">County</span></p></th><th class="cl-8e97efcb"><p class="cl-8e97c6e4"><span class="cl-8e9147d8">Cases</span></p></th></tr></thead><tbody><tr style="overflow-wrap:break-word;"><td class="cl-8e97efd4"><p class="cl-8e97c6da"><span class="cl-8e9147d8">Crowley</span></p></td><td class="cl-8e97efd5"><p class="cl-8e97c6e4"><span class="cl-8e9147d8">0.009764603</span></p></td></tr><tr style="overflow-wrap:break-word;"><td class="cl-8e97efd4"><p class="cl-8e97c6da"><span class="cl-8e9147d8">Bent</span></p></td><td class="cl-8e97efd5"><p class="cl-8e97c6e4"><span class="cl-8e9147d8">0.004120622</span></p></td></tr><tr style="overflow-wrap:break-word;"><td class="cl-8e97efd4"><p class="cl-8e97c6da"><span class="cl-8e9147d8">Sedgwick</span></p></td><td class="cl-8e97efd5"><p class="cl-8e97c6e4"><span class="cl-8e9147d8">0.003869304</span></p></td></tr><tr style="overflow-wrap:break-word;"><td class="cl-8e97efd4"><p class="cl-8e97c6da"><span class="cl-8e9147d8">Washington</span></p></td><td class="cl-8e97efd5"><p class="cl-8e97c6e4"><span class="cl-8e9147d8">0.002875924</span></p></td></tr><tr style="overflow-wrap:break-word;"><td class="cl-8e97efde"><p class="cl-8e97c6da"><span class="cl-8e9147d8">Las Animas</span></p></td><td class="cl-8e97efdf"><p class="cl-8e97c6e4"><span class="cl-8e9147d8">0.002651039</span></p></td></tr></tbody></table></div>
```

:::
:::



The table ranks Colorado counties with the highest new COVID-19 cases per capita on JFebruary 1, 2021. Crowley, Bent, Sedgwick, Washington, and Las Animas counties had the most new infections relative to their populations

# **Question 4: Rolling thresholds**

**Filter the merged COVID/Population data to only include the last 14 days. *Remember this should be a programmatic request and not hard-coded*. Then, use the `group_by`/`summarize` paradigm to determine the total number of new cases in the last 14 days per 100,000 people. Print a table of the top 5 counties, and, report the number that meet the watch list condition: “More than 100 new cases per 100,000 residents over the past 14 days…”**



::: {.cell}

```{.r .cell-code}
safe <- pop |>
inner_join(colorado, by = "fips") |>
filter(between(date, my.date - 13, my.date)) |>
group_by(county) |>
summarize(lag = sum(new_cases) / (POPESTIMATE2021[1]/100000)) |>
ungroup()
```
:::

::: {.cell}

```{.r .cell-code}
safe |>
select(County = county, Cases = lag) |>
slice_max(Cases, n = 10) |>
flextable() |>
add_header_lines("Cases per 100,000 in the last 14 days")
```

::: {.cell-output-display}

```{=html}
<div class="tabwid"><style>.cl-8ec25cb0{}.cl-8eb591e2{font-family:'Arial';font-size:11pt;font-weight:normal;font-style:normal;text-decoration:none;color:rgba(0, 0, 0, 1.00);background-color:transparent;}.cl-8eb97302{margin:0;text-align:left;border-bottom: 0 solid rgba(0, 0, 0, 1.00);border-top: 0 solid rgba(0, 0, 0, 1.00);border-left: 0 solid rgba(0, 0, 0, 1.00);border-right: 0 solid rgba(0, 0, 0, 1.00);padding-bottom:5pt;padding-top:5pt;padding-left:5pt;padding-right:5pt;line-height: 1;background-color:transparent;}.cl-8eb9730c{margin:0;text-align:right;border-bottom: 0 solid rgba(0, 0, 0, 1.00);border-top: 0 solid rgba(0, 0, 0, 1.00);border-left: 0 solid rgba(0, 0, 0, 1.00);border-right: 0 solid rgba(0, 0, 0, 1.00);padding-bottom:5pt;padding-top:5pt;padding-left:5pt;padding-right:5pt;line-height: 1;background-color:transparent;}.cl-8eba66d6{width:0.75in;background-color:transparent;vertical-align: middle;border-bottom: 1.5pt solid rgba(102, 102, 102, 1.00);border-top: 1.5pt solid rgba(102, 102, 102, 1.00);border-left: 0 solid rgba(0, 0, 0, 1.00);border-right: 0 solid rgba(0, 0, 0, 1.00);margin-bottom:0;margin-top:0;margin-left:0;margin-right:0;}.cl-8eba66ea{width:0.75in;background-color:transparent;vertical-align: middle;border-bottom: 1.5pt solid rgba(102, 102, 102, 1.00);border-top: 1.5pt solid rgba(102, 102, 102, 1.00);border-left: 0 solid rgba(0, 0, 0, 1.00);border-right: 0 solid rgba(0, 0, 0, 1.00);margin-bottom:0;margin-top:0;margin-left:0;margin-right:0;}.cl-8eba66eb{width:0.75in;background-color:transparent;vertical-align: middle;border-bottom: 0 solid rgba(0, 0, 0, 1.00);border-top: 0 solid rgba(0, 0, 0, 1.00);border-left: 0 solid rgba(0, 0, 0, 1.00);border-right: 0 solid rgba(0, 0, 0, 1.00);margin-bottom:0;margin-top:0;margin-left:0;margin-right:0;}.cl-8eba66ec{width:0.75in;background-color:transparent;vertical-align: middle;border-bottom: 0 solid rgba(0, 0, 0, 1.00);border-top: 0 solid rgba(0, 0, 0, 1.00);border-left: 0 solid rgba(0, 0, 0, 1.00);border-right: 0 solid rgba(0, 0, 0, 1.00);margin-bottom:0;margin-top:0;margin-left:0;margin-right:0;}.cl-8eba66f4{width:0.75in;background-color:transparent;vertical-align: middle;border-bottom: 1.5pt solid rgba(102, 102, 102, 1.00);border-top: 0 solid rgba(0, 0, 0, 1.00);border-left: 0 solid rgba(0, 0, 0, 1.00);border-right: 0 solid rgba(0, 0, 0, 1.00);margin-bottom:0;margin-top:0;margin-left:0;margin-right:0;}.cl-8eba66f5{width:0.75in;background-color:transparent;vertical-align: middle;border-bottom: 1.5pt solid rgba(102, 102, 102, 1.00);border-top: 0 solid rgba(0, 0, 0, 1.00);border-left: 0 solid rgba(0, 0, 0, 1.00);border-right: 0 solid rgba(0, 0, 0, 1.00);margin-bottom:0;margin-top:0;margin-left:0;margin-right:0;}</style><table data-quarto-disable-processing='true' class='cl-8ec25cb0'><thead><tr style="overflow-wrap:break-word;"><th  colspan="2"class="cl-8eba66d6"><p class="cl-8eb97302"><span class="cl-8eb591e2">Cases per 100,000 in the last 14 days</span></p></th></tr><tr style="overflow-wrap:break-word;"><th class="cl-8eba66d6"><p class="cl-8eb97302"><span class="cl-8eb591e2">County</span></p></th><th class="cl-8eba66ea"><p class="cl-8eb9730c"><span class="cl-8eb591e2">Cases</span></p></th></tr></thead><tbody><tr style="overflow-wrap:break-word;"><td class="cl-8eba66eb"><p class="cl-8eb97302"><span class="cl-8eb591e2">Crowley</span></p></td><td class="cl-8eba66ec"><p class="cl-8eb9730c"><span class="cl-8eb591e2">3,923.278</span></p></td></tr><tr style="overflow-wrap:break-word;"><td class="cl-8eba66eb"><p class="cl-8eb97302"><span class="cl-8eb591e2">Lincoln</span></p></td><td class="cl-8eba66ec"><p class="cl-8eb9730c"><span class="cl-8eb591e2">3,599.488</span></p></td></tr><tr style="overflow-wrap:break-word;"><td class="cl-8eba66eb"><p class="cl-8eb97302"><span class="cl-8eb591e2">Alamosa</span></p></td><td class="cl-8eba66ec"><p class="cl-8eb9730c"><span class="cl-8eb591e2">3,594.909</span></p></td></tr><tr style="overflow-wrap:break-word;"><td class="cl-8eba66eb"><p class="cl-8eb97302"><span class="cl-8eb591e2">Mineral</span></p></td><td class="cl-8eba66ec"><p class="cl-8eb9730c"><span class="cl-8eb591e2">3,336.921</span></p></td></tr><tr style="overflow-wrap:break-word;"><td class="cl-8eba66eb"><p class="cl-8eb97302"><span class="cl-8eb591e2">Conejos</span></p></td><td class="cl-8eba66ec"><p class="cl-8eb9730c"><span class="cl-8eb591e2">3,152.203</span></p></td></tr><tr style="overflow-wrap:break-word;"><td class="cl-8eba66eb"><p class="cl-8eb97302"><span class="cl-8eb591e2">Fremont</span></p></td><td class="cl-8eba66ec"><p class="cl-8eb9730c"><span class="cl-8eb591e2">3,097.264</span></p></td></tr><tr style="overflow-wrap:break-word;"><td class="cl-8eba66eb"><p class="cl-8eb97302"><span class="cl-8eb591e2">Huerfano</span></p></td><td class="cl-8eba66ec"><p class="cl-8eb9730c"><span class="cl-8eb591e2">2,682.434</span></p></td></tr><tr style="overflow-wrap:break-word;"><td class="cl-8eba66eb"><p class="cl-8eb97302"><span class="cl-8eb591e2">Bent</span></p></td><td class="cl-8eba66ec"><p class="cl-8eb9730c"><span class="cl-8eb591e2">2,659.674</span></p></td></tr><tr style="overflow-wrap:break-word;"><td class="cl-8eba66eb"><p class="cl-8eb97302"><span class="cl-8eb591e2">Montezuma</span></p></td><td class="cl-8eba66ec"><p class="cl-8eb9730c"><span class="cl-8eb591e2">2,649.234</span></p></td></tr><tr style="overflow-wrap:break-word;"><td class="cl-8eba66f4"><p class="cl-8eb97302"><span class="cl-8eb591e2">Mesa</span></p></td><td class="cl-8eba66f5"><p class="cl-8eb9730c"><span class="cl-8eb591e2">2,573.695</span></p></td></tr></tbody></table></div>
```

:::
:::



The table ranks Colorado counties with the highest COVID-19 cases per 100,000 residents in the last 14 days before February 1, 2022. Crowley, Lincoln, and Alamosa counties had the highest infection rates.

# **Question 5: Death toll**

Given we are assuming it is February 1st, 2022. Your leadership has asked you to determine what percentage of deaths in each county were attributed to COVID last year (2021). You eagerly tell them that with the current Census data, you can do this!

From previous questions you should have a `data.frame` with daily COVID deaths in Colorado and the Census based, 2021 total deaths. For this question, you will find the ratio of total COVID deaths per county (2021) of all recorded deaths. In a plot of your choosing, visualize all counties where COVID deaths account for 20% or more of the annual death toll.



::: {.cell}

```{.r .cell-code}
x <- colorado |>
mutate(year = lubridate :: year(date)) |>
filter(year == 2021) |>
group_by(fips) |>
summarize(deaths = sum(new_deaths, na.rm = TRUE)) |>
left_join(pop, by = c("fips")) |>
mutate(death_ratio = 100 * (deaths / DEATHS2021)) |>
select(CTYNAME, deaths, DEATHS2021, death_ratio) |>
filter(death_ratio > 20)


ggplot(x, aes(x = death_ratio, y = reorder(CTYNAME, death_ratio))) +
  geom_col(fill = "red") +  
  theme_light() +
  labs(
    title = "Counties Where COVID Deaths Were >20% of Total Deaths (2021)",
    x = "COVID-19 Death Percentage (%)",
    y = "County"
  )
```

::: {.cell-output-display}
![](lab-3_files/figure-html/unnamed-chunk-15-1.png){width=672}
:::
:::



The bar chart displays Colorado counties where COVID-19 deaths accounted for more than 20% of total deaths in 2021. Conejos, Bent, and San Miguel counties had the highest percentages, exceeding 30-40%.

# **Question 6: Multi-state**

In this question, we are going to look at the story of 4 states and the impact scale can have on data interpretation. The states include: **New York**, **Colorado**, **Alabama**, and **Ohio**. Your task is to make a *faceted* bar plot showing the number of daily, **new** cases at the state level.

1.  First, we need to `group/summarize` our county level data to the state level, `filter` it to the four states of interest, and calculate the number of daily new cases (`diff/lag`) and the 7-day rolling mean.



    ::: {.cell}
    
    ```{.r .cell-code}
    library(tidyverse)
    library(zoo)
    
    state_covid <- data |>
      filter(state %in% c("New York", "Ohio", "Colorado", "Alabama")) |>  
      group_by(date, state) |>
       summarise(cases = sum(cases, na.rm = TRUE), .groups = "drop") |>  
      arrange(state, date) |>  
      group_by(state) |>  
      mutate(
        newCases = cases - lag(cases, default = 0), 
        roll = zoo::rollmean(newCases, k = 7, align = "right", fill = NA)  
      ) |>
      ungroup()
    ```
    :::



2.  **Using the modified data, make a facet plot of the daily new cases and the 7-day rolling mean. Your plot should use compelling geoms, labels, colors, and themes.**



::: {.cell}

```{.r .cell-code}
library(ggplot2)

ggplot(state_covid, aes(x = date)) +
  geom_col(aes(y = newCases), fill = "lightblue", col = "purple") +  
  geom_line(aes(y = roll), color = "darkblue", size = 1) +  
  theme_linedraw() +  
  facet_wrap(~state, nrow = 2, scales = "free_y") +   
  labs(
    title = "Cumulative COVID-19 Cases",
    x = "Date",
    y = "Case Count"
  )
```

::: {.cell-output .cell-output-stderr}

```
Warning: Using `size` aesthetic for lines was deprecated in ggplot2 3.4.0.
ℹ Please use `linewidth` instead.
```


:::

::: {.cell-output .cell-output-stderr}

```
Warning: Removed 6 rows containing missing values or values outside the scale range
(`geom_line()`).
```


:::

::: {.cell-output-display}
![](lab-3_files/figure-html/unnamed-chunk-17-1.png){width=672}
:::
:::



The facted plot displays daily new COVID-19 cases and 7-day rolling averages for Alabama, Colorado, New York, and Ohio. Peaks in cases align with major COVID-19 waves, showing significant surges in late 2020 and early 2022, with New York experiencing the highest spikes.

3.  **The story of raw case counts can be misleading. To understand why, lets explore the cases per capita of each state. To do this, join the state COVID data to the population estimates and calculate the** newcases/totalpopulation**. Additionally, calculate the 7-day rolling mean of the new cases per capita counts. This is a tricky task and will take some thought, time, and modification to existing code (most likely)!**



::: {.cell}

```{.r .cell-code}
library(tidyverse)
library(zoo)

state_pop <- pop |>
  group_by(STNAME) |>
  summarise(state_pop = sum(POPESTIMATE2021, na.rm = TRUE))  

state_covid_per_capita <- state_covid |>
  inner_join(state_pop, by = c("state" = "STNAME")) |>  
  mutate(
    perCap = newCases / state_pop,  
    roll = zoo::rollmean(perCap, k = 7, align = "right", fill = NA)  
  ) |>
  ungroup()
```
:::

::: {.cell}

```{.r .cell-code}
library(ggplot2)

# Plot the 7-day rolling average per capita
ggplot(state_covid_per_capita, aes(x = date, y = roll, color = state)) +
  geom_line(size = 1.2) +  # Line graph for rolling average
  theme_linedraw() +  # Better grid theme
  labs(
    title = "COVID-19 Cases Per Capita (7-Day Rolling Average)",
    subtitle = "Comparing New York, Ohio, Colorado, and Alabama",
    x = "Date",
    y = "Cases Per 100,000 People",
    color = "State"
  ) +
  scale_color_manual(values = c("New York" = "blue", "Ohio" = "purple", 
                                "Colorado" = "red", "Alabama" = "green")) +
  theme(
    text = element_text(size = 14),
    plot.title = element_text(face = "bold", hjust = 0.5),
    legend.position = "top"
  )
```

::: {.cell-output .cell-output-stderr}

```
Warning: Removed 6 rows containing missing values or values outside the scale range
(`geom_line()`).
```


:::

::: {.cell-output-display}
![](lab-3_files/figure-html/unnamed-chunk-19-1.png){width=672}
:::
:::



The graph shows the 7-day rolling average of COVID-19 cases per 100,000 people for New York, Ohio, Colorado, and Alabama. Major surges occurred in late 2020 and early 2022, with New York peaking highest.

5.  **Briefly describe the influence scaling by population had on the analysis? Does it make some states look better? Some worse? How so?**

Scaling by population allows for a fair comparison of COVID-19 severity across states. Initially, New York appeared worst due to its high total cases, while smaller states seemed less affected. After adjusting per capita, Alabama and Colorado showed comparable or even higher infection rates, revealing that outbreaks were more intense relative to their population sizes. This adjustment prevents misleading conclusions and highlights hidden trends in smaller states, making the analysis more accurate.

# **Question 7: Space & Time**



::: {.cell}

```{.r .cell-code}
library(tidyverse)
library(ggplot2)
library(maps)
```

::: {.cell-output .cell-output-stderr}

```
Warning: package 'maps' was built under R version 4.4.3
```


:::

::: {.cell-output .cell-output-stderr}

```

Attaching package: 'maps'
```


:::

::: {.cell-output .cell-output-stderr}

```
The following object is masked from 'package:purrr':

    map
```


:::

```{.r .cell-code}
covid_geo <- read_csv('https://raw.githubusercontent.com/mikejohnson51/csu-ess-330/refs/heads/main/resources/county-centroids.csv') |>
  inner_join(data, by = "fips") 
```

::: {.cell-output .cell-output-stderr}

```
Rows: 3221 Columns: 3
```


:::

::: {.cell-output .cell-output-stderr}

```
── Column specification ────────────────────────────────────────────────────────
Delimiter: ","
chr (1): fips
dbl (2): LON, LAT

ℹ Use `spec()` to retrieve the full column specification for this data.
ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```


:::

```{.r .cell-code}
meta <- covid_geo |>
  group_by(date) |>
  summarise(
    wmX_c = sum(LON * cases, na.rm = TRUE) / sum(cases, na.rm = TRUE),  
    wmY_c = sum(LAT * cases, na.rm = TRUE) / sum(cases, na.rm = TRUE),  
    cases = sum(cases, na.rm = TRUE)  
  ) |>
  arrange(date) |>
  mutate(d = row_number())  


ggplot(meta) +
  borders("state", fill = "gray90", colour = "white") +  
  geom_point(aes(x = wmX_c, y = wmY_c, size = cases), color = "red", alpha = 0.5) +  
  theme_linedraw() +
  labs(
    color = "Time",
    size = "Total Cases",
    x = "Longitude",
    y = "Latitude",
    title = "Weighted Center of COVID-19 Cases in the USA"
  ) +
  theme(legend.position = "right")  
```

::: {.cell-output-display}
![](lab-3_files/figure-html/unnamed-chunk-20-1.png){width=672}
:::
:::



The COVID-19 weighted mean center was initially concentrated in the Northeast, where early outbreaks in New York and New Jersey fueled a surge in cases. Over time, it gradually shifted west and south, reflecting the spread of the virus into the Midwest and Southern states. This movement was influenced by population density, travel patterns, and changing public health policies. As the pandemic evolved, major waves like Delta and Omicron caused rapid shifts, highlighting how different regions experienced surges at different times.

# **Question 8: Cases vs. Deaths**



::: {.cell}

```{.r .cell-code}
library(tidyverse)
library(ggplot2)
library(patchwork)


meta <- read_csv('https://raw.githubusercontent.com/mikejohnson51/csu-ess-330/refs/heads/main/resources/county-centroids.csv') %>%
  inner_join(data, by = "fips") %>%
  group_by(date) %>%
  summarise(
    wmx_c = sum(LON * cases, na.rm = TRUE) / sum(cases, na.rm = TRUE),  
    WMY_c = sum(LAT * cases, na.rm = TRUE) / sum(cases, na.rm = TRUE),  
    cases = sum(cases, na.rm = TRUE),  
    wmx_d = sum(LON * deaths, na.rm = TRUE) / sum(deaths, na.rm = TRUE),  
    WMY_d = sum(LAT * deaths, na.rm = TRUE) / sum(deaths, na.rm = TRUE), 
    deaths = sum(deaths, na.rm = TRUE)  
  ) %>%
  arrange(date) %>%
  mutate(d = row_number())  
```

::: {.cell-output .cell-output-stderr}

```
Rows: 3221 Columns: 3
── Column specification ────────────────────────────────────────────────────────
Delimiter: ","
chr (1): fips
dbl (2): LON, LAT

ℹ Use `spec()` to retrieve the full column specification for this data.
ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```


:::

```{.r .cell-code}
p1 <- ggplot(meta) +
  borders("state", fill = "gray98", colour = "white") +
  geom_point(aes(x = wmx_c, y = WMY_c, size = cases), color = "red", alpha = 0.25) +
  theme_linedraw() +
  labs(
    color = "Time",
    size = "Cases",
    x = "",
    y = "",
    title = "Weighted Center of COVID-19 Cases"
  ) +
  theme(legend.position = "right")

p2 <- ggplot(meta) +
  borders("state", fill = "gray98", colour = "white") +
  geom_point(aes(x = wmx_d, y = WMY_d, size = deaths), color = "navy", alpha = 0.25) +
  theme_linedraw() +
  labs(
    color = "Time",
    size = "Deaths",
    x = "",
    y = "",
    title = "Weighted Center of COVID-19 Deaths"
  ) +
  theme(legend.position = "right")


p1 + p2
```

::: {.cell-output .cell-output-stderr}

```
Warning: Removed 39 rows containing missing values or values outside the scale range
(`geom_point()`).
```


:::

::: {.cell-output-display}
![](lab-3_files/figure-html/unnamed-chunk-21-1.png){width=672}
:::
:::

