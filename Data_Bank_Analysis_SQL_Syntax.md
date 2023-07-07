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

**Result**
|node_id|days_diff|
|---|---|
|4|14.81|
|5|14.71|
|3|16|
|1|14.818|
|2|15.16|

~~~ SQL 
/*median, 80th and 95th percentile for this same reallocation days metric for each region*/
SELECT
  r.region_name,
  SUBSTRING_INDEX(SUBSTRING_INDEX(GROUP_CONCAT(DATEDIFF(end_date, start_date) ORDER BY DATEDIFF(end_date, start_date)), ',', COUNT(*) / 2 + 1), ',', -1) AS median_reallocation_days,
  SUBSTRING_INDEX(SUBSTRING_INDEX(GROUP_CONCAT(DATEDIFF(end_date, start_date) ORDER BY DATEDIFF(end_date, start_date)), ',', COUNT(*) * 0.8 + 1), ',', -1) AS 80th_percentile_reallocation_days,
  SUBSTRING_INDEX(SUBSTRING_INDEX(GROUP_CONCAT(DATEDIFF(end_date, start_date) ORDER BY DATEDIFF(end_date, start_date)), ',', COUNT(*) * 0.95 + 1), ',', -1) AS 95th_percentile_reallocation_days
FROM customer_nodes cn
join regions r
on cn.region_id = r.region_id 
GROUP BY
  r.region_name;
~~~

**Result**
|region_name|median_reallocation_days|80th_percentile_reallocation_days|95th_percentile_reallocation_days|
|---|---|---|---|
|Africa|18|2|2|
|America|18|1|1|
|Asia|17|||
|Australia|17|||
|Europe|18|||
