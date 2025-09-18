# Government-Contract-Intelligence

Python ETL pipeline to aggregate and visualize federal contract data (100,000+ records) by CBSA regions, using Haversine distance for geospatial grouping and Plotly for interactive visualizations.

Overview

This project is a data engineering pipeline built in Python to extract, transform, and load (ETL) federal contract data from DOE and DOT into SQLite databases, aggregating over $2T in contracts by Core-Based Statistical Areas (CBSAs). It processes datasets from USASpending.gov, standardizing fields like zip codes and NAICS codes, and uses Haversine distance calculations to group contracts by proximity to CBSA centroids. The pipeline generates interactive Plotly scatter maps (e.g., visualizing $2.72T in Knoxville, TN) and structured outputs for analysis, enabling insights into regional funding trends and contractor activity. It supports applications like policy analysis and opportunity identification for government contractors.

Features





ETL Automation: Scripts to merge, clean, and standardize contract data from multiple agencies.



Geospatial Aggregation: Groups contracts by CBSA using Haversine distance for proximity-based analysis.



Database Structure: SQLite tables for contracts and Census Gazetteer data, enabling efficient querying (e.g., 50% faster than CSV parsing).



Interactive Visualizations: Plotly scatter maps showing funding distribution with hover details for CBSA names and totals.



Extensibility: Outputs (CSVs, JSONs, GeoJSONs) ready for further analysis or integration with mapping tools.

Technologies





Python 3.x (with pandas, numpy, geopy, plotly.express, geopandas, sqlite3, json, csv, os).



SQLite for lightweight, file-based databases.



US Census Bureau Gazetteer files (e.g., 2021_Gaz_cbsa_national.txt) for geospatial data.



USASpending.gov contract data (e.g., FY23_DOE_CON.csv, FY23_DOT_CON.csv).

Setup


Clone the Repository:

git clone https://github.com/DeanHak/fed_contract_mining.git
cd fed_contract_mining



Install Dependencies:

pip install pandas numpy geopy plotly geopandas fiona



Data Files:



Place contract CSVs (e.g., FY23_DOE_CON.csv, FY23_DOT_CON.csv) in 00_resources/.



Place Gazetteer files (e.g., 2021_Gaz_cbsa_national.txt, 2022_Gaz_zcta_national.txt) in 00_resources/gaz/.



Place reference files (e.g., contractHeaderReference.json, naicsCodes.csv) in 00_resources/.



Ensure zipcodes.txt (list of zip codes) is in 00_resources/ for coordinate extraction.



Run the Pipeline:





Create database schemas:

python makeDb_uscbGaz.py
python makeDb_fedContracts.py



Load data into databases:

python addData_uscbGaz.py
python addData_fedContracts.py



Extract zip code coordinates:

python getZctaCoords.py



Merge and process data:

python mergeGovContracts.py
python mergeCBITransactions.py



Aggregate by CBSA and county:

python aggregateContracts.py
python contracts_by_county.py



Generate visualizations:

python viz_map.py

Outputs are saved in 02_output/ (e.g., dot_contracts_byCbsa.csv, DOE_FY23_cbsaStats.json) and databases (uscb_gazetter.db, fed_contracts.db) in the working directory.
