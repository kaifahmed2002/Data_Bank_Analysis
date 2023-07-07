~~~ SQL
/*Median medical Charges by each Region*/

SELECT distinct region, median_value AS Median
FROM (
  SELECT distinct region,
         charges AS median_value,
         ROW_NUMBER() OVER (PARTITION BY region ORDER BY charges) AS row_num,
         COUNT(*) OVER (PARTITION BY region) AS total_rows
  FROM cs2_personalmedicalcost.medical_data_dataset
) AS subquery
WHERE row_num IN (FLOOR((total_rows+1)/2), FLOOR((total_rows+2)/2));

~~~

**Result**
|Region|Region_Median|
|---|---|
|northeast|10058|
|northwest|8966|
|southeast|8871|

~~~ SQL 
/*Averages medical Charges by each Region*/

SELECT distinct region, avg(charges) 
FROM cs2_personalmedicalcost.medical_data_dataset
group by region
order by 2
~~~

**Result**
|Region|Region_Median|
|---|---|
|northwest|12417|
|northeast|13406|
|southeast|14483|


~~~ SQL 
/*Average medical Charges by Gender */
SELECT distinct sex, avg(charges) 
FROM cs2_personalmedicalcost.medical_data_dataset
group by sex
order by 2 desc 
~~~

|Sex|avg(charges)|
|---|---|
|male|13968|
|female|12945|

~~~ SQL 
/*Male and Female Median Charges*/
SELECT 
  DISTINCT Sex,
  ROUND(PERCENTILE_CONT(charges, 0.50) OVER (PARTITION BY Sex),2) AS Sex_Median
FROM `single-being-353600.Medical_Insurance_Data.Insurance_Data`;
~~~

**Result**

|Sex|Sex_Median|
|---|---|
|male|9369.62|
|female|9412.96|
