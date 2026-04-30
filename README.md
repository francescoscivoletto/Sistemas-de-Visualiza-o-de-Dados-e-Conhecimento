# Sistemas-de-Visualiza-o-de-Dados-e-Conhecimento
# Global Energy Transition Dashboard

## Project Overview

This project analyzes the OWID Energy Dataset using Power BI.

The main objective is to create an interactive dashboard that helps users understand how electricity generation has changed from 2000 to 2023 and how different energy sources contribute to the global electricity mix.

The analysis focuses on the energy transition, with particular attention to the relationship between fossil fuels, renewable energy and low-carbon sources. Through the dashboard, users can compare countries, observe trends over time and identify which energy sources have the greatest impact on electricity generation.

The project aims to communicate the following messages:

- electricity generation has changed significantly over time;
- fossil fuels still play an important role in global electricity production;
- renewable energy is becoming increasingly relevant;
- countries differ strongly in their electricity mix and carbon intensity;
- visual analytics can help understand the progress and limitations of the energy transition.

The dashboard tries to answer these questions:

- How has electricity generation changed over time?
- How important are renewable sources compared to fossil fuels?
- Which countries generate the most electricity?
- What is the composition of the electricity mix?
- How does the energy mix change across countries and years?
---

## Dataset

The dataset contains energy-related information for many countries and years.

For this project, I focused mainly on electricity generation and selected only the columns useful for the analysis, such as:

- country
- year
- electricity generation
- renewable electricity
- fossil electricity
- low-carbon electricity
- electricity by source
- carbon intensity
- electricity per capita

---

## Data Preparation

The dataset was cleaned and transformed in Power Query.

The main preparation steps were:

- selected only the relevant columns;
- filtered the years from 2000 to 2023;
- removed rows without `iso_code`;
- removed rows without `electricity_generation`;
- corrected numeric formats using the `en-US` locale;
- created a `Date` column using the first day of each year;
- created a `Country Year Key` to connect the tables.

I did not remove all null values because some missing values are normal in this dataset.

Values equal to `0` were kept because they can represent real cases where a country did not produce electricity from a specific source.

---

## Energy Mix Transformation

To analyze the electricity sources, I created a second table called `Energy Mix`.

In the original dataset, the energy sources were stored in separate columns, for example:

- coal electricity;
- gas electricity;
- nuclear electricity;
- hydro electricity;
- solar electricity;
- wind electricity.

I transformed these columns into a long format using the Unpivot operation.

The new table contains:

- country;
- year;
- energy source;
- electricity value;
- source group.

I also created a `Source Group` column:

- Coal, Gas and Oil → Fossil
- Nuclear → Low Carbon
- Hydro, Solar, Wind, Biofuel and Other Renewables → Renewable

This transformation made it easier to compare energy sources in the dashboard.

---

## Measures

The main DAX measures created were:

```DAX
Total Electricity Generation =
SUM('Energy'[electricity_generation])
```

```DAX
Renewable Electricity =
SUM('Energy'[renewables_electricity])
```

```DAX
Fossil Electricity =
SUM('Energy'[fossil_electricity])
```

```DAX
Low Carbon Electricity =
SUM('Energy'[low_carbon_electricity])
```

```DAX
Renewable Share % =
DIVIDE([Renewable Electricity], [Total Electricity Generation], 0)
```

```DAX
Fossil Share % =
DIVIDE([Fossil Electricity], [Total Electricity Generation], 0)
```

```DAX
Average Carbon Intensity =
AVERAGE('Energy'[carbon_intensity_elec])
```

```DAX
Number of Countries =
DISTINCTCOUNT('Energy'[country])
```

```DAX
Total Electricity by Source =
SUM('Energy Mix'[Electricity])
```

---

## Dashboard Structure

The Power BI report is divided into two pages:

1. Energy Overview
2. Energy Mix Analysis

---

## Page 1: Energy Overview

The first page gives a general overview of electricity generation.

It includes:

- total electricity generation;
- renewable electricity;
- renewable share;
- fossil share;
- average carbon intensity;
- electricity generation trend over time;
- top countries by electricity generation;
- country performance table.

The purpose of this page is to quickly understand the general situation of electricity generation and the role of renewable and fossil sources.

---

## Page 2: Energy Mix Analysis

The second page focuses on the composition of electricity generation.

It includes:

- electricity generation by source over time;
- energy mix by source group;
- top energy sources;
- detailed table by country, year and source.

The purpose of this page is to show which sources are used to produce electricity and how the energy mix changes over time.

---

## Main Insights

The analysis shows that electricity generation increased between 2000 and 2023.

Fossil fuels still represent a large part of global electricity generation, even if renewable electricity has grown over time.

The dashboard also shows that electricity generation is concentrated in a limited number of countries.

Finally, the energy mix changes a lot depending on the country. Some countries rely more on fossil fuels, while others have a higher share of renewable or low-carbon electricity.

---


## Limitations and Improvements

Some countries do not have complete data for every year or every energy source.

The analysis focuses only on electricity generation and not on the whole energy system.

Possible future improvements include:

- adding drill-through pages for single countries;
- analyzing solar and wind growth in more detail;
- comparing countries by electricity per capita;
- improving tooltips and interactivity.

---

## Conclusion

This dashboard shows how Power BI can be used to analyze a large energy dataset.

The main message is that electricity generation has increased over time, renewable sources are becoming more important, but fossil fuels are still a major part of global electricity production.
