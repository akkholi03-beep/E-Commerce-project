# 🛒 E-Commerce SQL Data Analysis Project

This project focuses on analyzing an **E-Commerce database using SQL** to solve real-world business problems and extract meaningful insights from customer, product, order, and payment data.

The project demonstrates practical SQL skills through a collection of queries ranging from **basic to advanced concepts**.

---

## 📌 Project Objectives

- Analyze customer purchasing behavior
- Explore product and order data
- Calculate sales and revenue metrics
- Identify high-value customers
- Analyze product performance
- Solve real-world business questions using SQL
- Strengthen SQL and data analysis skills

---

## 🛠️ SQL Concepts Covered

- `SELECT`
- `WHERE`
- `ORDER BY`
- `TOP`
- `DISTINCT`
- `BETWEEN`
- Aggregate Functions — `COUNT()`, `SUM()`, `AVG()`, `MIN()`, `MAX()`
- `GROUP BY`
- `HAVING`
- `INNER JOIN`
- `LEFT JOIN`
- Subqueries
- Correlated Subqueries
- Common Table Expressions (CTEs)
- Window Functions
- `DENSE_RANK()`
- Date & Time Functions
- Data Filtering
- Data Aggregation

---

## 🗂️ Database Tables

The project works with related E-Commerce tables such as:

- 👤 `customers`
- 📦 `products`
- 🛒 `orders`
- 🧾 `order_items`
- 💳 `payments`

---

## 📊 Analysis Performed

Some of the business problems explored in this project include:

- Finding the most expensive and cheapest products
- Analyzing customer orders and spending
- Calculating total and average revenue
- Identifying frequently used payment methods
- Finding customers who have not placed orders
- Finding products that have never been purchased
- Analyzing revenue over time
- Identifying high-spending customers
- Finding the second-highest product price
- Analyzing customer order frequency
- Exploring product stock and sales information

---

## 💡 Key Learning

This project helped me practice how to:

1. Understand relational database structures
2. Write SQL queries to answer business questions
3. Combine data from multiple tables using joins
4. Aggregate and filter data
5. Use subqueries and CTEs for complex analysis
6. Apply window functions for ranking and comparisons
7. Convert raw database information into useful insights

---

## 🧰 Tools & Technologies

- **SQL**
- **SQL Server**
- **Relational Database Concepts**

---

## 📁 Project Files

```text
E-Commerce-SQL-Data-Analysis/

--Sql E-Commerce PROJECT 
 
--My Analysis & Findings

--1.**Check the data**
select*
from customers


--2 **Fetch only the customer ID, first name, and email from the customers table.** 

select customer_id,first_name,email
from customers

--3.List all products that belong to the Clothing category. 
select *
from products
where category='clothing'

--4.Retrieve all orders where the total purchase amount is greater than $500
select *
from orders
where total_amount>500

--5.Find all customers who joined the platform after January 1, 2023. 
select*
from customers
where join_date>'2023-01-01'

--6.Display the top 5 most expensive products available in the database. 
select top 5*
from products
order by price desc

--7️.List the latest 10 orders placed, sorted by order date in descending order. 
select top 10*
from orders
order by order_date desc

--8️.Retrieve all orders that have a status of "Completed"
select*
from orders
where order_status='completed'

--9.Find all orders that were placed between February 1, 2023, and February 28, 2023. 
select*
from orders
where order_date between '2023-02-01' and '2023-02-28'

--10.List all products that have a price between $50 and $100.
select *
from products
where price between 50 and 100 


-- Intrmediate questions.

--1.Count the total number of customers in the database. 
select count(*) as total_customer
from customers

--2.Find the average order amount from the orders table. 
select avg(total_amount) as avg_amount
from orders

--3. Retrieve the highest and lowest priced products from the product list.
select max(price) as highest_price,min(price) as lowest_price
from products

--4.Count the number of products in each category, grouping by category. 
select category,count(*) as total_product
from products
group by category

--5.Calculate the total revenue generated from all orders. 
select sum(total_amount) as total_amount
from orders

--6. Find the total number of orders placed by each customer, sorted by highest to lowest.
select customer_id,count(*)as Total_Orders
from orders
group by customer_id
order by Total_Orders desc

--7️.Calculate the total revenue generated for each month in 2023.
select MONTH(order_date)as month, sum(total_amount) as total_revenue
from orders
where year (order_date)=2023
group by month(order_date)
order by month

--8️. List all customers who have placed more than 5 orders.
select customer_id,count(*) as total_orders
from orders
group by customer_id
having count(order_id)>5

--9. Identify the most frequently used payment method based on the number of transactions.
select top 1 payment_method, count(*) as total_transactions
from payments
group by payment_method
order by total_transactions desc

--10.Find the average product price for each category.
select category,avg(price) as avg_price
from products
group by category


-- Advanced questions.

--1.Retrieve all order details along with the customer’s first and last name
select o.*,c.first_name,c.last_name
from orders as o
join customers as c
on o.customer_id=c.customer_id

--2.Fetch order items with product names, quantities, and subtotal values
select oi.order_item_id, p.product_name,oi.quantity,oi.subtotal
from order_items as oi
join products as p
on oi.product_id=p.product_id

--3.List all payment transactions along with the corresponding order details
select p.*,o.order_id,o.order_date,o.total_amount
from payments as p
join orders as o
on p.order_id=o.order_id

--4.Identify customers who have never placed an order
select c.customer_id,c.first_name,c.last_name,o.order_status
from customers as c
left join orders as o
on c.customer_id=o.customer_id
where o.order_status is null

--5.Find all products that have never been purchased (i.e., do not appear in any order).
select p.*
from products as p
left join order_items as oi
on p.product_id=oi.product_id
where oi.product_id is null

--6.Retrieve customers and their total spending by summing up all their orders.
select c.customer_id,c.first_name,c.last_name,sum(o.total_amount) as total_spending
from customers as c
join orders as o
on c.customer_id=o.customer_id
group by c.customer_id,c.first_name,c.last_name

--7️.Get the total number of products ordered by each customer. 
select c.customer_id,c.first_name,c.last_name,sum(oi.quantity) as total_products
from orders as o
join customers as c
on o.customer_id=c.customer_id
join order_items as oi
on o.order_id=oi.order_id
group by c.customer_id,c.first_name,c.last_name

--8️.Display all orders along with the names of the products included in each order.
select o.order_id,p.product_name
from order_items as oi
join products as p
on oi.product_id=p.product_id
join orders as o
on oi.order_id=o.order_id

--9. Find orders that do not have any associated payments recorded.
select o.*
from payments as p
join orders as o
on p.order_id=o.order_id
where p.payment_id is null

--10.Retrieve customers along with the last date they placed an order.
select c.customer_id,c.first_name,c.last_name,max(o.order_date) as last_order_date
from customers as c
join orders as o
on c.customer_id=o.customer_id
group by c.customer_id,c.first_name,c.last_name


select c.*,o.order_date as last_order_date
from customers as c
join orders as o
on c.customer_id=o.customer_id
order by o.order_date desc

--Subqueries & Advanced Filters 

--1.Find the most expensive product in the store using a subquery.
select*
from products
where price=
(
	select top 1 price
	from products
	order by price desc
)

--2. Retrieve the list of customers who have placed at least one order.
select*
from customers
where customer_id in
(
	select distinct customer_id
	from orders
)

-- 3.Display orders where the total amount is greater than the average order amount.
select*
from orders
where total_amount>(
	select avg(total_amount)
	from orders
)

--4.Find the cheapest product in each category using a correlated subquery.
select *
from products
where price=
(
	select min(price)
	from products
	where category=category
)

--5.Identify the customer who has placed the highest number of orders. 
select top 1 customer_id,count(order_id) as highest_order
from orders
group by customer_id
order by count(order_id) desc

--6.Fetch the second most expensive product using an alternative ranking method.
-- Normal method
select top 2*
from products
order by price desc

--Using subquery

select top 1*
from(
	select top 2 *
from products
order by price desc) as t
order by price


-- windows function

select*
from
(
	select*, dense_rank() over(order by price desc) as dr
	from products
) as p
where dr=2;

--CTE Use
with price as
(
	select*,dense_rank() over(order by price desc) as dr
	from products
)
select*
from price
where dr=2


--7️.List all customers who have never made a payment for any order.
select*
from customers
where customer_id in(
	select customer_id
	from orders
	where order_id  not in (
		select distinct order_id
		from payments
	)
)

--8️.Retrieve all products with stock levels below the average stock quantity.
select*
from products
where stock_quantity<(
	select avg(stock_quantity)
	from products
)

--9.Find customers who have spent more than $2000 in total on orders
select*
from customers
where customer_id in
(
	select customer_id
	from orders
	group by customer_id
	having sum(total_amount)>2000
)

│
├── E_commerace Project.sql
└── README.md
```

---

## 🎯 Career Goal

This project is part of my **Data Analyst learning journey** and demonstrates my ability to use SQL to explore data, solve business problems, and generate meaningful insights.

I am continuously improving my skills in **SQL, Python, Power BI, and Excel** and building projects to develop my practical Data Analytics experience.

---

⭐ **If you find this project useful, feel free to explore the repository!**

