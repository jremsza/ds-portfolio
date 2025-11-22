---
title: Creating a Relational Database
seo_title: Portfolio Project 6
summary: This portfolio project was performed in my database course. The project takes retail data from a fictitious store where it is loaded into a SQLite database and SQL queries are performed.
description: SQL Demonstration
slug: portfolio-project-6
author: Jake Remsza

draft: false
date: 2021-02-20T03:52:30-05:00
lastmod: 
expiryDate: 
publishDate: 

feature_image: 
feature_image_alt: 

tags:
  - Databases
  - SQL

categories:
  - SQL Query
  - Databases and Data preperation

project types: 
  - Academic
  - Personal
techstack:
    - SQL

#live_url: https://hugo-liftoff.netlify.app
#source_url: https://github.com/wjh18/hugo-liftoff
---

## Project Overview 📝

This project showcases fundamental database management and analysis skills using SQL. Working with a dataset from a fictitious retail store, I designed a relational database schema, loaded the data into SQLite, and executed a series of queries to extract actionable business insights. The goal was to answer common questions a retail manager might have about sales, inventory, customers, and suppliers.

## Database Design: The ERD

A well-structured database is the foundation of any reliable data analysis. Before writing any queries, I mapped out the relationships between the different data entities (like customers, products, and invoices) in an **Entity-Relationship Diagram (ERD)**. This critical step ensures data integrity and makes querying more efficient and intuitive.

*The ERD for the retail database, illustrating tables for customers, invoices, products, and vendors, along with their relationships.*

![alt text](/images/proj-5/image.png)

---

### Business Questions and SQL Queries 🔍

Here are some of the key business questions I answered using SQL. Each query demonstrates different aspects of SQL, from simple selections to complex joins and aggregations.

#### 1. How many invoices and customers do we have?

**Business Goal:** Understand the scale of sales activity and the size of our customer base.

**SQL Skills:** `SELECT`, `COUNT()`

**Query & Result:**

![alt text](/images/proj-5/image-2.png)
![alt text](/images/proj-5/image-4.png)

**Insight:** The database contains **8 invoices** and **10 unique customers**, providing a baseline for our sales analysis.

---

#### 2. Who are our suppliers and where are they located?

**Business Goal:** Profile our vendor network to understand geographic distribution.

**SQL Skills:** `SELECT`, `GROUP BY`, `COUNT()`

**Query & Result:**

![alt text](/images/proj-5/image-6.png)

**Insight:** We have a diverse set of vendors, with the majority located in TN. This could inform logistics and supply chain strategies.

---

#### 3. What is our most expensive product?

**Business Goal:** Identify high-value items in our inventory, which is crucial for sales strategy and inventory management.

**SQL Skills:** `ORDER BY`, `LIMIT` (or equivalent)

**Query & Result:**

![alt text](/images/proj-5/image-7.png)

**Insight:** The **16-inch hicut chain saw** is our premium product. With 11 units on hand, we can assess if this stock level is appropriate for a high-ticket item.

---

#### 4. Which products have a discount greater than 5%?

**Business Goal:** Monitor promotional activity and its impact on product offerings.

**SQL Skills:** `SELECT`, `WHERE`

**Query & Result:**

![alt text](/images/proj-5/image-8.png)

**Insight:** This query quickly identifies all products currently on promotion, which can be used for marketing campaigns or to analyze the effectiveness of our discount strategy.

---

#### 5. What is the average discount offered by each vendor?

**Business Goal:** Evaluate vendor pricing strategies and partnership value.

**SQL Skills:** `JOIN`, `GROUP BY`, `AVG()`, `ROUND()`

**Query & Result:**

![alt text](/images/proj-5/image-10.png)

**Insight:** There's a clear variation in the average discount across vendors. For example, **"All Season Tools"** offers a significantly higher average discount than others, which could be a point of negotiation or a key feature of our partnership.

---

#### 6. Which customer has spent the most?

**Business Goal:** Identify our most valuable customers to inform marketing efforts and loyalty programs.

**SQL Skills:** `JOIN`, `GROUP BY`, `SUM()`, `ORDER BY`

**Query & Result:**

![alt text](/images/proj-5/image-14.png)

**Insight:** Customer **#10014, "The B&G Club,"** is our top customer by total spending. This is valuable information for the sales team and for building strong customer relationships.

---

#### 7. Are there any customers who haven't made a purchase recently?

**Business Goal:** Identify inactive or dormant customers who could be targeted with re-engagement campaigns.

**SQL Skills:** `LEFT JOIN`, `WHERE ... IS NULL`

**Query & Result:**

![alt text](/images/proj-5/image-15.png)

**Insight:** Two customers have not made purchases in this invoice cycle. This list provides a direct target for a "we miss you" marketing campaign to encourage them to return.

---

#### 8. What is the total value of our current inventory?

**Business Goal:** Get a snapshot of the total value of assets tied up in inventory, broken down by vendor.

**SQL Skills:** `JOIN`, `GROUP BY`, `SUM()` with calculation

**Query & Result:**

![alt text](/images/proj-5/image-16.png)

**Insight:** We have over **$31,000** in inventory value. **"D&E Supply"** is our largest supplier by inventory value, holding over half of the total. This is a key metric for financial planning and inventory auditing.
