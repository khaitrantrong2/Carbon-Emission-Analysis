## Carbon-Emission-Analysis

This report aims to analyze carbon emissions to examine the carbon footprint across various industries. We aim to identify sectors with the highest levels of emissions by analyzing them across countries and years, as well as to uncover trends.

## Overview

<img width="640" height="427" alt="image" src="https://github.com/user-attachments/assets/d9a52d41-013e-4111-b000-fe0f832b34f1" />\

<b>What is the project about? <b>\
Carbon emissions account for over 75% of global emissions and represent a major environmental challenge. These emissions contribute to the accumulation of greenhouse gases in the atmosphere, leading to climate change, planetary warming, and various environmental disasters. Identifying sectors with the highest levels of emissions is crucial. By analyzing data across countries and years, we can observe trends and better understand the environmental impact of different industries. This supports informed decision-making in sustainable development.

## Data structure
### Table 1:

Use query below to view data:

```sql
SELECT *
FROM product_emissions pe 
LIMIT 5;
```

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

```sql
SELECT * FROM companies
LIMIT 5;
```

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

```sql
SELECT * FROM countries
LIMIT 5;
```

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

```sql
SELECT * FROM industry_groups
LIMIT 5;
```

Result:
|id|industry_group|
|--|--------------|
|1|"Consumer Durables, Household and Personal Products"|
|2|"Food, Beverage & Tobacco"|
|3|"Forest and Paper Products - Forestry, Timber, Pulp and Paper, Rubber"|
|4|"Mining - Iron, Aluminum, Other Metals"|
|5|"Pharmaceuticals, Biotechnology & Life Sciences"|


### Review duplicate:

Use query below to view data:

```sql
SELECT COUNT(product_name) AS 'Total number of products',
       COUNT(DISTINCT product_name) AS 'Number of distinct products'
FROM product_emissions pe;
```

Results:
|Total number of products|Number of distinct products|
|------------------------|---------------------------|
|1037|661|

## Questions to research
### 1.Which products contribute the most to carbon emissions?

Use query below to view data:

```sql
SELECT 
    pe.product_name,
    ROUND(AVG(pe.carbon_footprint_pcf),2) AS Average_cacbon_footprint
FROM product_emissions pe
GROUP BY pe.product_name
ORDER BY Average_cacbon_footprint DESC
LIMIT 10;
```

Results: <b>Top 10 products with highest contribution to Carbon Emissions</b>

|product_name|Average_cacbon_footprint|
|------------|------------------------|
|Wind Turbine G128 5 Megawats|3718044.00|
|Wind Turbine G132 5 Megawats|3276187.00|
|Wind Turbine G114 2 Megawats|1532608.00|
|Wind Turbine G90 2 Megawats|1251625.00|
|Land Cruiser Prado. FJ Cruiser. Dyna trucks. Toyoace.IMV def unit.|191687.00|
|Retaining wall structure with a main wall (sheet pile): 136 tonnes of steel sheet piles and 4 tonnes of tierods per 100 meter wall|167000.00|
|TCDE|99075.00|
|Mercedes-Benz GLE (GLE 500 4MATIC)|91000.00|
|Mercedes-Benz S-Class (S 500)|85000.00|
|Mercedes-Benz SL (SL 350)|72000.00|

Conclusion:

Large-scale products like wind turbines and heavy vehicles have the highest carbon footprints. While some serve sustainable purposes, their production still emits heavily. Identifying these helps guide cleaner design and smarter manufacturing choices.

### 2.What are the industry groups of these products?

Use query below to view data:

```sql
SELECT 
    industry_group,
    ROUND(SUM(pe.carbon_footprint_pcf),2) AS Total_cacbon_footprint
FROM product_emissions pe JOIN industry_groups ig ON pe.industry_group_id = ig.id
GROUP BY industry_group 
ORDER BY Total_cacbon_footprint DESC
LIMIT 10;
```

Results: <b>Top 10 industry group of products with highest contribution to Carbon Emissions</b>

|industry_group|Total_cacbon_footprint|
|--------------|----------------------|
|Electrical Equipment and Machinery|9801558.00|
|Automobiles & Components|2582264.00|
|Materials|577595.00|
|Technology Hardware & Equipment|363776.00|
|Capital Goods|258712.00|
|"Food, Beverage & Tobacco"|111131.00|
|"Pharmaceuticals, Biotechnology & Life Sciences"|72486.00|
|Chemicals|62369.00|
|Software & Services|46544.00|
|Media|23017.00|

Conclusion:

Electrical Equipment and Automobiles lead in emissions due to energy-intensive production. Focusing sustainability efforts on these sectors can drive meaningful reductions in overall carbon impact.

### 3.What are the industries with the highest contribution to carbon emissions?

Use query below to view data:

```sql
SELECT 
    industry_group,
    ROUND(SUM(pe.carbon_footprint_pcf),2) AS Total_cacbon_footprint
FROM product_emissions pe JOIN industry_groups ig ON pe.industry_group_id = ig.id
GROUP BY industry_group 
ORDER BY Total_cacbon_footprint DESC
LIMIT 1;
```

Results: <b>Top 1 Industry Group with highest contribution to Carbon Emissions</b>

|industry_group|Total_cacbon_footprint|
|--------------|----------------------|
|Electrical Equipment and Machinery|9801558.00|

Conclusion:


### 4.What are the companies with the highest contribution to carbon emissions?

Use query below to view data:

```sql
SELECT 
    company_name,
    ROUND(SUM(pe.carbon_footprint_pcf),2) AS Total_cacbon_footprint
FROM product_emissions pe JOIN companies c ON pe.company_id = c.id
GROUP BY company_name  
ORDER BY Total_cacbon_footprint DESC
LIMIT 1;
```

Conclusion:


Results: <b>Top 1 Company with highest contribution to Carbon Emissions</b>

|company_name|Total_cacbon_footprint|
|------------|----------------------|
|"Gamesa Corporación Tecnológica, S.A."|9778464|

Conclusion:


### 5.What are the countries with the highest contribution to carbon emissions?

Use query below to view data:

```sql
SELECT 
    country_name,
    ROUND(SUM(pe.carbon_footprint_pcf),2) AS Total_cacbon_footprint
FROM product_emissions pe JOIN countries ctr ON pe.country_id = ctr.id
GROUP BY country_name  
ORDER BY Total_cacbon_footprint DESC
LIMIT 1;
```

Results: <b>Top 1 Country with highest contribution to Carbon Emissions</b>

|country_name|Total_cacbon_footprint|
|------------|----------------------|
|Spain|9786130.00|

Conclusion:


### 6.What is the trend of carbon footprints (PCFs) over the years?

Use query below to view data:

```sql
SELECT 
	pe.year,
	ROUND(SUM(pe.carbon_footprint_pcf), 2) AS Total_Carbon_footprint,
	ROUND(AVG(pe.carbon_footprint_pcf), 2) AS AVG_Carbon_footprint
FROM product_emissions pe
GROUP BY pe.year
ORDER BY year;
```

Results: <b> Trend of carbon footprints (PCFs) over the years</b>

|year|Total_Carbon_footprint|AVG_Carbon_footprint|
|----|----------------------|--------------------|
|2013|503857.00|2399.32|
|2014|624226.00|2457.58|
|2015|10840415.00|43188.90|
|2016|1640182.00|6891.52|
|2017|340271.00|4050.85|

Conclusion:


### 7.Which industry groups has demonstrated the most notable decrease in carbon footprints (PCFs) over time?

Use query below to view data:

```sql
SELECT
    industry_group,
    ROUND(SUM(CASE WHEN pe.`year` = 2013 THEN pe.carbon_footprint_pcf ELSE 0 END),2) AS '2013',
    ROUND(SUM(CASE WHEN pe.`year` = 2014 THEN pe.carbon_footprint_pcf ELSE 0 END),2) AS '2014',
    ROUND(SUM(CASE WHEN pe.`year` = 2015 THEN pe.carbon_footprint_pcf ELSE 0 END),2) AS '2015',
    ROUND(SUM(CASE WHEN pe.`year` = 2016 THEN pe.carbon_footprint_pcf ELSE 0 END),2) AS '2016',
    ROUND(SUM(CASE WHEN pe.`year` = 2017 THEN pe.carbon_footprint_pcf ELSE 0 END),2) AS '2017',
    ROUND(SUM(pe.carbon_footprint_pcf)) AS Total_cacbon_footprint
FROM product_emissions pe
JOIN industry_groups ig
ON pe.industry_group_id = ig.id
GROUP BY industry_group
ORDER BY Total_cacbon_footprint DESC
LIMIT 10;
```

Results: <b> Top 10 Industry groups has demonstrated the most notable decrease in carbon footprints (PCFs) over time</b>

|industry_group|2013|2014|2015|2016|2017|Total_cacbon_footprint|
|--------------|----|----|----|----|----|----------------------|
|Electrical Equipment and Machinery|0.00|0.00|9801558.00|0.00|0.00|9801558|
|Automobiles & Components|130189.00|230015.00|817227.00|1404833.00|0.00|2582264|
|Materials|200513.00|75678.00|0.00|88267.00|213137.00|577595|
|Technology Hardware & Equipment|61100.00|167361.00|106157.00|1566.00|27592.00|363776|
|Capital Goods|60190.00|93699.00|3505.00|6369.00|94949.00|258712|
|"Food, Beverage & Tobacco"|4995.00|2685.00|0.00|100289.00|3162.00|111131|
|"Pharmaceuticals, Biotechnology & Life Sciences"|32271.00|40215.00|0.00|0.00|0.00|72486|
|Chemicals|0.00|0.00|62369.00|0.00|0.00|62369|
|Software & Services|6.00|146.00|22856.00|22846.00|690.00|46544|
|Media|9645.00|9645.00|1919.00|1808.00|0.00|23017|

Conclusion:






