## Carbon-Emission-Analysis

This report aims to analyze carbon emissions to examine the carbon footprint across various industries. We aim to identify sectors with the highest levels of emissions by analyzing them across countries and years, as well as to uncover trends.

## Overview

<img width="640" height="427" alt="image" src="https://github.com/user-attachments/assets/d9a52d41-013e-4111-b000-fe0f832b34f1" />\

<b>What is the project about? <b>\
Carbon emissions account for over 75% of global emissions and represent a major environmental challenge. These emissions contribute to the accumulation of greenhouse gases in the atmosphere, leading to climate change, planetary warming, and various environmental disasters. Identifying sectors with the highest levels of emissions is crucial. By analyzing data across countries and years, we can observe trends and better understand the environmental impact of different industries. This supports informed decision-making in sustainable development.

## Data structure
### Table 1:
Use query below to view data:
``sql
SELECT *
FROM product_emissions pe 
LIMIT 5;``

Result:
|id|company_id|country_id|industry_group_id|year|product_name|weight_kg|carbon_footprint_pcf|upstream_percent_total_pcf|operations_percent_total_pcf|downstream_percent_total_pcf|
|--|----------|----------|-----------------|----|------------|---------|--------------------|--------------------------|----------------------------|----------------------------|
|10056-1-2014|82|28|2|2014|Frosted Flakes(R) Cereal|0.7485|2|57.50|30.00|12.50|
|10056-1-2015|82|28|15|2015|"Frosted Flakes, 23 oz, produced in Lancaster, PA (one carton)"|0.7485|2|57.50|30.00|12.50|
|10222-1-2013|83|28|8|2013|Office Chair|20.68|73|80.63|17.36|2.01|
|10261-1-2017|14|16|25|2017|Multifunction Printers|110.0|1488|30.65|5.51|63.84|
|10261-2-2017|14|16|25|2017|Multifunction Printers|110.0|1818|25.08|4.51|70.41|

### Table 2:
Use query below to view data:
``sql
SELECT * FROM companies
LIMIT 5;``
Result:
|id|company_name|
|--|------------|
|1|"Autodesk, Inc."|
|2|"Casio Computer Co., Ltd."|
|3|"Cisco Systems, Inc."|
|4|"CNX Coal Resources, LP"|
|5|"Coca-Cola Enterprises, Inc."|


### Table 3:
Use query below to view data:
``sql
SELECT * FROM countries
LIMIT 5;``
Result:
|id|country_name|
|--|------------|
|1|Australia|
|2|Belgium|
|3|Brazil|
|4|Canada|
|5|Chile|


### Table 4:
Use query below to view data:
``sql
SELECT * FROM industry_groups
LIMIT 5;``
Result:
|id|industry_group|
|--|--------------|
|1|"Consumer Durables, Household and Personal Products"|
|2|"Food, Beverage & Tobacco"|
|3|"Forest and Paper Products - Forestry, Timber, Pulp and Paper, Rubber"|
|4|"Mining - Iron, Aluminum, Other Metals"|
|5|"Pharmaceuticals, Biotechnology & Life Sciences"|


### 
Use query below to view data:
sql``
SELECT COUNT(product_name) AS 'Total number of products',
       COUNT(DISTINCT product_name) AS 'Number of distinct products'
FROM product_emissions pe;``

Results:
|Total number of products|Number of distinct products|
|------------------------|---------------------------|
|1037|661|

