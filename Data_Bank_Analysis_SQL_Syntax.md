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

~~~ SQL 
/*the unique count and total amount for each transaction type*/
SELECT txn_type, count(distinct txn_amount) as unique_count, sum(txn_amount) as total_amount 
FROM cs3_bankdata_dwd.customer_transactions
group by 1;
~~~

**Result**
|txn_type|unique_count|total_amount|
|---|---|---|
|deposit|929|1359168|
|purchase|815|806537|
|withdrawal|804|793003|

~~~ SQL 
/*average total historical deposit counts and amounts for all customers*/
SELECT AVG(deposit_count) AS avg_deposit_count, AVG(deposit_amount) AS avg_deposit_amount
FROM (
    SELECT customer_id, COUNT(*) AS deposit_count, SUM(txn_amount) AS deposit_amount
    FROM customer_transactions
    where txn_type = 'deposit'
    GROUP BY customer_id
) AS deposit_summary
~~~

**Result**
|avg_deposit_count|avg_deposit_amount|
|---|---|
|5.3420|2718.3360|

~~~ SQL 
/*Data Bank customers make more than 1 deposit and either 1 purchase or 1 withdrawal in a single month*/
SELECT DATE_FORMAT(txn_date, '%Y-%m') AS year_mont, COUNT(DISTINCT customer_id) AS customer_count
FROM customer_transactions
WHERE txn_type IN ('purchase', 'withdrawal') AND customer_id IN (
    SELECT customer_id
    FROM customer_transactions
    WHERE txn_type = 'deposit'
    GROUP BY customer_id
    HAVING COUNT(*) > 1
)
GROUP BY year_mont;
~~~

**Result**
|year_mont|customer_count|
|---|---|
|2020-01|283|
|2020-02|389|
|2020-03|399|
|2020-04|238|

~~~ SQL 
/*closing balance for each customer at the end of the month*/
SELECT customer_id, DATE_FORMAT(txn_date, '%Y-%m-%d') AS year_mont, SUM(txn_amount) AS closing_balance
FROM customer_transactions
WHERE txn_date = (
    SELECT MAX(txn_date)
    FROM customer_transactions AS sub
    WHERE YEAR(sub.txn_date) = YEAR(customer_transactions.txn_date)
      AND MONTH(sub.txn_date) = MONTH(customer_transactions.txn_date)
      AND sub.customer_id = customer_transactions.customer_id
)
GROUP BY customer_id, year_mont
order by customer_id;
~~~

**Result**
|year_mont|customer_count|
|---|---|
|2020-01|283|
|2020-02|389|
|2020-03|399|
|2020-04|238|

~~~ SQL 
/*closing balance for each customer at the end of the month*/
SELECT customer_id, DATE_FORMAT(txn_date, '%Y-%m-%d') AS year_mont, SUM(txn_amount) AS closing_balance
FROM customer_transactions
WHERE txn_date = (
    SELECT MAX(txn_date)
    FROM customer_transactions AS sub
    WHERE YEAR(sub.txn_date) = YEAR(customer_transactions.txn_date)
      AND MONTH(sub.txn_date) = MONTH(customer_transactions.txn_date)
      AND sub.customer_id = customer_transactions.customer_id
)
GROUP BY customer_id, year_mont
order by customer_id;
~~~

**Result(first 5 rows)** 
|customer_id|year_mont|year_mont|
|---|---|---|
|1|2020-01-02|312|
|1|2020-03-19|664|
|2|2020-01-03|549|
|2|2020-03-24|61|
|3|2020-01-27|144|
