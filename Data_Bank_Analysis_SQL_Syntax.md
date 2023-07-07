~~~ SQL
/*Number of nodes per region*/

SELECT region_name, count(node_id) 
FROM customer_nodes cn
join regions r
on cn.region_id = r.region_id
group by region_name
order by 1;

~~~

**Result**
|region_name|count(node_id)|
|---|---|
|Africa|714|
|America|735|
|Asia|665|
|Australia|770|
|Europe|616|

~~~ SQL 
/*No. customers are allocated to each region*/

SELECT region_name, count(distinct cn.customer_id) as no_customers 
FROM customer_nodes cn
join regions r
on cn.region_id = r.region_id
join customer_transactions ct
on cn.customer_id = ct.customer_id
group by region_name
order by 1;
~~~

**Result**
|region_name|no_customers|
|---|---|
|Africa|102|
|America|105|
|Asia|95|
|Australia|110|
|Europe|88|

~~~ SQL 
/*No.days on average are customers reallocated to a different node */
SELECT node_id, avg(DATEDIFF(end_date, start_date)) AS days_diff
FROM cs3_bankdata_dwd.customer_nodes
group by node_id;
~~~

|node_id|days_diff|
|---|---|
|4|14.81|
|5|14.71|
|3|16|
|1|14.818|
|2|15.16|

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
