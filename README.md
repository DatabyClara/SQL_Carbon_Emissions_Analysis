# Carbon Emissions Analysis Using SQL
The dataset, sourced from [Nature.com](https://www.nature.com/articles/s41597-022-01178-9), contains emissions data from 2013 to 2017 for various products, industries, companies, and countries, categorized by lifecycle stage (upstream, operations, and downstream). The data was collected through the Carbon Disclosure Project (CDP), where companies voluntarily reported their PCFs in response to CDP's Climate Change Questionnaire.

### Tools & Languages:
![SQL](https://img.shields.io/badge/SQL-4479A1?style=for-the-badge&logo=sql&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-336791?style=for-the-badge&logo=postgresql&logoColor=white) 

![Python](https://img.shields.io/badge/Python-3670A0?logo=python&logoColor=white&style=for-the-badge)
![Plotly Express](https://img.shields.io/badge/Plotly-Orange?logo=plotly&logoColor=white&style=for-the-badge)


### What was done?
Analyzed a dataset of Product Carbon Footprints (PCFs) using SQL in a PostgreSQL environment to identify top carbon emitters and patterns across industries, lifecycle stages, and countries from 2013 to 2017 in our database.

### Objective
Analyze Product Carbon Footprints (PCFs), which is the amount of greenhouse gas emissions (GHG) associated with a specific product that is measured in CO₂e (carbon dioxide equivalent), in order to:
- Identify the major sources of emissions across industries, products, and countries both throughout the entire study period and specifically in 2017.
- Understand how emissions are distributed across different lifecycle stages (upstream, operations, downstream).

### 📊 Results:

**Most recent data shows (2017):**
- Materials and Capital Goods were the top emitting industries in 2017.
- The Food, Beverages & Tobacco industry showed a consistent reduction in emissions over time, even with consistent data reporting.
- The product with the highest emissions recorded in 2017 in this dataset was TCDE, from the Materials industry. Lifecycle analysis for this product showed that most emissions occurred in the upstream stage. Emission breakdown: 60% upstream, 34.4% operations, and less than 1% downstream.

**Over the entire study period (2013–2017):**
- The top three emitting industry sectors in this dataset were Electrical Equipment and Machinery, Automobiles & Components, and Materials.
- Spain had the highest total emissions in this dataset, mainly due to the Electrical Equipment and Machinery sector in 2015. Germany, Japan, and the U.S. followed as top emitters.
- China and India reported relatively low emissions, likely due to data gaps or underreporting.

### 📝 Recommendations
- Prioritize policies and investments to decarbonize the Materials and Capital Goods industries, as they were the largest emitters in 2017.
- Pursue cleaner technologies and sustainable production processes for the products with the highest carbon emissions.
- Understand the key products within the target industries (e.g., Materials) to develop more efficient and scalable decarbonization solutions.
- Encourage more companies to share their emissions data and keep updating it regularly to have accurate information.

### 📈 Potential Extensions
- Compare carbon footprints across similar products to highlight best practices.
- Perform time series forecasting to predict future emissions and evaluate intervention scenarios.
- Collect more recent data to monitor ongoing trends and evaluate the effectiveness of emission reduction efforts.
- Develop targeted decarbonization strategies for upstream, operations, and downstream stages.
- Use Machine Learning models to detect unusual reporting patterns or data inconsistencies.


# 🔍 Sample SQL queries
**-- Explore database**
```sql
SELECT * FROM product_emissions
LIMIT 5;
```
Answer:
```
id              year  product_name                                                       company               country  industry_group                    weight_kg  carbon_footprint_pcf  upstream_percent_total_pcf   operations_percent_total_pcf  downstream_percent_total_pcf
10056-1-2014    2014  Frosted Flakes(R) Cereal                                           Kellogg Company       USA      Food, Beverage & Tobacco          0.7485     2                     57.50%                        30.00%                        12.50%
10056-1-2015    2015  Frosted Flakes, 23 oz, produced in Lancaster, PA (one carton)      Kellogg Company       USA      Food & Beverage Processing        0.7485     2                     57.50%                        30.00%                        12.50%
10222-1-2013    2013  Office Chair                                                       KNOLL INC             USA      Capital Goods                     20.68      72.54                 80.63%                        17.36%                        2.01%
10261-1-2017    2017  Multifunction Printers                                             Konica Minolta, Inc.  Japan    Technology Hardware & Equipment   110        1488                  30.65%                         5.51%                        63.84%
10261-2-2017    2017  Multifunction Printers                                             Konica Minolta, Inc.  Japan    Technology Hardware & Equipment   110        1818                  25.08%                         4.51%                        70.41%

```
---
**-- Identify available time range**
```sql
SELECT DISTINCT year AS available_time_range 
FROM product_emissions
ORDER BY year;
```
Answer:
| available_time_range |
|----------------------|
| 2013                 |
| 2014                 |
| 2015                 |
| 2016                 |
| 2017                 |

---
**--  Top Industry groups emitters in 2017**
```sql
SELECT industry_group,
	ROUND(SUM(carbon_footprint_pcf),2) AS total_emissions
FROM product_emissions
WHERE year = 2017
GROUP BY industry_group
ORDER BY total_emissions DESC;
```
Answer:
| industry_group                      | total_emissions |
|-------------------------------------|-----------------|
| Materials                           | 107129          |
| Capital Goods                       | 94942.6724      |
| Technology Hardware & Equipment     | 21865.086       |
| Food, Beverage & Tobacco            | 3161.47         |
| Commercial & Professional Services  | 740.6           |
| Software & Services                 | 690             |

---
**-- Lifecycle emission breakdown considering only 2017 data**
```sql
SELECT company,
	industry_group,
	product_name,
	carbon_footprint_pcf,
	upstream_percent_total_pcf,
	operations_percent_total_pcf,
	downstream_percent_total_pcf
FROM product_emissions
WHERE year = 2017 
ORDER BY carbon_footprint_pcf DESC
LIMIT 5;
```
Answer: 
```
company                                 industry_group   product_name                      carbon_footprint_pcf   upstream_percent_total_pcf                        operations_percent_total_pcf                        downstream_percent_total_pcf                     
Mitsubishi Gas Chemical Company, Inc.   Materials        TCDE                              99075                  64.95%                                            34.40%                                              0.66%                                           
Daikin Industries, Ltd.                 Capital Goods    Commercial Air Conditioner        51066                  0.98%                                             0.13%                                               98.88%                                           
Daikin Industries, Ltd.                 Capital Goods    Light commercial Air Conditioner  39653                  0.70%                                             0.10%                                               99.21%                                           
Mitsubishi Gas Chemical Company, Inc.   Materials        Super-pure hydrogen peroxide      6469                    N/a (product with insufficient stage-level data) N/a (product with insufficient stage-level data)    N/a (product with insufficient stage-level data)    
Daikin Industries, Ltd.                 Capital Goods    Residential Air Conditioner       4218                   3.96%                                             0.55%                                               95.50%     
```

---
**-- Lifecycle emission breakdown considering only Materials industry data in 2017**
```sql
SELECT  company,
	product_name,
	carbon_footprint_pcf,
	upstream_percent_total_pcf,
	operations_percent_total_pcf,
	downstream_percent_total_pcf
FROM product_emissions
WHERE year = 2017 
	AND industry_group = 'Materials'
ORDER BY carbon_footprint_pcf DESC
LIMIT 5;
```
Answer: 
```
company                               industry_group  product_name                                                       carbon_footprint_pcf  upstream_percent_total_pcf                         operations_percent_total_pcf                        downstream_percent_total_pcf    
Mitsubishi Gas Chemical Company, Inc. Materials       TCDE                                                               99075                 64.95%                                             34.40%                                              0.66%  
Mitsubishi Gas Chemical Company, Inc. Materials       Super-pure hydrogen peroxide                                       6469                  N/a (product with insufficient stage-level data)   N/a (product with insufficient stage-level data)    N/a (product with insufficient stage-level data) 
Tata Chemicals                        Materials       Soda Ash                                                           870                   N/a (product with insufficient stage-level data)   N/a (product with insufficient stage-level data)    N/a (product with insufficient stage-level data) 
Mitsubishi Gas Chemical Company, Inc. Materials       Paraformaldehyde                                                   200                   56.50%                                             29.93%                                              13.57% 
Johnson Matthey                       Materials       Complete catalyst system for diesel-powered passenger car exhaust  188                   N/a (product with insufficient stage-level data)   N/a (product with insufficient stage-level data)    N/a (product with insufficient stage-level data)  

```

---
**-- Country coverage**
```sql
SELECT country,
	ROUND(SUM(carbon_footprint_pcf),2) AS total_footprint
FROM product_emissions
GROUP BY country
ORDER BY total_footprint DESC;
```

---
**-- Industry group with highest emissions in Spain**
```sql
SELECT year,
    company, 
    industry_group,
    SUM(carbon_footprint_pcf) AS total_carbon_footprint
FROM product_emissions
WHERE country = 'Spain'
GROUP BY year,
    company,
    industry_group
ORDER BY total_carbon_footprint DESC
LIMIT 5;
```
Answer:
| year | company                                          | industry_group                         | total_carbon_footprint |
|------|--------------------------------------------------|----------------------------------------|-------------------------|
| 2015 | Gamesa Corporación Tecnológica, S.A.            | Electrical Equipment and Machinery     | 9778464                 |
| 2016 | Compañía Española de Petróleos, S.A.U. CEPSA    | Energy                                 | 6999                    |
| 2016 | Agraz                                            | Food, Beverage & Tobacco               | 340.23                  |
| 2015 | Crimidesa                                        | Chemicals                              | 180                     |
| 2016 | Crimidesa                                        | Materials                              | 140                     |


# 🔍 Sample Python Visualization:

**- Top emitters visualization:**
```python
import plotly.express as px

px.bar(total_footprint_df, x='country', y='total_footprint', title="Total Carbon emission by country",
       labels={
        "country": "Country",
        "total_footprint": "Total Emissions (tCO₂e)"
    })
```
Answer:
<img src="https://github.com/user-attachments/assets/9dcb1bc0-c5bc-410d-9bbe-b0f2c3901bf3" width="600"/>

---
**- Top industry groups emitters in 2017 visualization:**
```python
px.bar(df_ind_total_emissions_2017, x = "industry_group", y ="total_emissions", color="industry_group", title="Total Carbon Footprint by Industry Sector in 2017",
       labels={
        "total_emissions": "Total Emissions (tCO₂e)",
        "industry_group": "Industry sector"
    })
```
<img src="https://github.com/user-attachments/assets/fc501d43-9602-4005-b52a-b89e04d7cf09" width="600"/>

---
# Final Thoughts:
This project highlights how SQL can be used to extract meaningful insights from carbon emissions data at the product level. Understanding where emissions are concentrated helps guide more effective decarbonization strategies and supports data-driven environmental decision-making.
