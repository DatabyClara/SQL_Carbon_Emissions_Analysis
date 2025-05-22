# Carbon Emissions Analysis Using SQL
All SQL queries applied in this project are available in the "SQL_Queries.sql" section above. However, a small sample of SQL queries will be displayed at the end of this page.

The dataset, sourced from [Nature.com](https://www.nature.com/articles/s41597-022-01178-9), contains emissions data from 2013 to 2017 for various products, industries, companies, and countries, categorized by lifecycle stage (upstream, operations, and downstream).

### Tools & Languages:
![SQL](https://img.shields.io/badge/SQL-4479A1?style=for-the-badge&logo=sql&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-336791?style=for-the-badge&logo=postgresql&logoColor=white) ![Python](https://img.shields.io/badge/Python-3670A0?logo=python&logoColor=white&style=for-the-badge)
![Plotly Express](https://img.shields.io/badge/Plotly-Orange?logo=plotly&logoColor=white&style=for-the-badge)


### What was done?
Analyzed a dataset of Product Carbon Footprints (PCFs) using SQL in a PostgreSQL environment to identify top carbon emitters and patterns across industries, lifecycle stages, and countries from 2013 to 2017 in our database.

### Objective
Analyze Product Carbon Footprints (PCFs), which is the amount of greenhouse gas emissions (GHG) associated with a specific product that is measured in CO₂e (carbon dioxide equivalent), in order to:
- Identify the major sources of emissions across industries, products, and countries both throughout the entire study period and specifically in 2017.
- Understand how emissions are distributed across different lifecycle stages (upstream, operations, downstream).

### 📊 Results:

**Most recent data shows:**
- Materials and Capital Goods were the top emitting industries in 2017.
- The Food, Beverages & Tobacco industry showed a consistent reduction in emissions over time, even with consistent data reporting.
- The company that had the most emissions in 2017 was Mitsubishi Gas Chemical, located in Japan, due to a product (TCDE) in the Materials industry group, which generated the highest emissions during the upstream stage.
Emission breakdown: 60% upstream, 34.4% operations, and less than 1% downstream.

**Over the entire study period:**
- Spain reported the highest total emissions, mainly driven by the Electrical Equipment and Machinery sector in 2015.
- Belgium had only one company reporting emissions, Solvay S.A., indicating strong commitment, transparency, and sector leadership. This provides the company with a competitive sustainability advantage within the country.

### 📝 Recommendations
-Prioritize policies and investments to decarbonize the Materials and Capital Goods industries, as they were the largest emitters in 2017.
- Pursue cleaner technologies and sustainable production processes for the products with the highest carbon emissions.
- Understand the key products within the target industries (e.g., Materials) to develop more efficient and scalable decarbonization solutions.
- Encourage more companies to share their emissions data and keep updating it regularly to have accurate information.

### 📈 Potential Extensions
-Compare carbon footprints across similar products to highlight best practices.
- Perform time series forecasting to predict future emissions and evaluate intervention scenarios.
- Collect more recent data to monitor ongoing trends and evaluate the effectiveness of emission reduction efforts.
- Develop targeted decarbonization strategies for upstream, operations, and downstream stages.
- Use Machine Learning models to detect unusual reporting patterns or data inconsistencies.


# 🔍 Sample SQL queries
**-- Explore database**

SELECT * FROM product_emissions;

**-- Identify available time range**

<img src="https://github.com/user-attachments/assets/4cf75d90-2099-4a97-bc15-277613deda47" width="400"/>

**--  Top Industry groups emitters in 2017**

<img src="https://github.com/user-attachments/assets/0f132917-f780-492d-9d00-9ccef181a365" width="400"/>

Result:

<img src="https://github.com/user-attachments/assets/c37a6e14-ec20-410c-a398-de0a06e5708d" width="400"/>


**-- Lifecycle emission breakdown**

<img src="https://github.com/user-attachments/assets/e0dd7559-d472-4a9f-a09a-50d46c047ac0" width="400"/>

Result: 

![image](https://github.com/user-attachments/assets/6c72f66b-653c-4c04-b71f-8b896d1f1886)


**-- Country coverage**

<img src="https://github.com/user-attachments/assets/730c03aa-3cea-43fa-85b2-9d4906f9d873" width="400"/>

**-- Industry group with highest emissions in Spain**

<img src="https://github.com/user-attachments/assets/06936405-82d2-43f0-9c34-cf4d2d2e0ace" width="400"/>


# 🔍 Sample Python Visualization:

**- Top emitters visualization:**

<img src="https://github.com/user-attachments/assets/a0b4795f-06bb-42a7-a26b-f77a7e69c171" width="600"/>

<img src="https://github.com/user-attachments/assets/9dcb1bc0-c5bc-410d-9bbe-b0f2c3901bf3" width="600"/>

**- Top industry groups emitters in 2017 visualization:**

<img src="https://github.com/user-attachments/assets/9edbaf81-6a54-42d2-b677-28e76ac9e0a0" width="600"/>

<img src="https://github.com/user-attachments/assets/fc501d43-9602-4005-b52a-b89e04d7cf09" width="600"/>


# Final Thoughts:
This project highlights how SQL can be used to extract meaningful insights from carbon emissions data at the product level. Understanding where emissions are concentrated helps guide more effective decarbonization strategies and supports data-driven environmental decision-making.
