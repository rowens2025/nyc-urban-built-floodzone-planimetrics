## NYC Urban Built Density and Flood Zone Exposure

*A geospatial data science project*

# Project Overview

This project looks at how construction density across New York City overlaps with present-day flood risk zones. The main idea was to take NYC’s building footprint data, combine it with flood zone maps, and roll everything up to the neighborhood level so patterns could be compared across the city.

What started as a fairly straightforward spatial join turned into a learning exercise around coordinate systems, imperfect historical data, and figuring out how to meaningfully measure risk instead of just mapping shapes.

# Data Sources

- NYC Building Footprints (Planimetric Basemap)
- NYC Neighborhood Tabulation Areas (NTAs)
- NYC Stormwater Flood Maps

# All data comes from NYC Open Data

# Notebook Structure and Flow

## `initial_exploration.ipynb`

This notebook is where I first loaded and inspected the raw datasets. A lot of time here was spent just understanding what each dataset actually contained, what the geometries looked like, and why some measurements seemed “off.” This is also where CRS issues first showed up and started to matter and where the need for a pivot was discovered as historical data was not available as was initially believed.

## `initial_built_density.ipynb`

Here I focused specifically on construction density. The goal was to figure out how to measure how **built up** an area really is, rather than just counting buildings. This is where area calculations became key.

## `01_construction_density.ipynb`

This notebook formalizes the density work. Building footprint areas are calculated in square feet and compared against neighborhood and borough polygon areas to create **density ratios**.

## `02_flood_exposure_and_density.ipynb`

This notebook brings in the flood zone data. Buildings and flood polygons are joined to NTAs using centroid-based spatial joins. Flood exposure flags and flooded area totals are created, which allows density and flood exposure to be analyzed together at the neighborhood level.

## `03_visualizations.ipynb`

The final notebook focuses on mapping and visualization. Bar charts and simple tables are created for quick Top N charts. Choropleths and interactive maps are used to highlight areas with high construction density, flood exposure, and combined risk. This is where the results become easier to interpret visually instead of just through tables, as these maps create the ability to explore the data.

# Outputs

- Neighborhood-level construction density metrics
- Flood exposure indicators based on modeled storm events
- Combined risk scores at the NTA level
- Static and interactive maps highlighting spatial patterns
- Some processed datasets were written out as parquet files to keep later steps faster and cleaner.
