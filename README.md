# SQL-Project
Restaurant orders analysis 
# Restaurant Orders & Menu Analysis (SQL)

A beginner-friendly SQL project with a sample dataset that analyses a restaurant's **menu** and **customer orders** from the first quarter of 2023. Using MySQL, it answers questions about pricing, item popularity, order size and spending, and turns the results into a 10-page PDF report.

**Tools:** MySQL · SQL  
**Period analysed:** 1 Jan 2023 – 31 Mar 2023  
**Full report:** [`Restaurant_SQL_Project_Report.pdf`](Restaurant_SQL_Project_Report.pdf)

---

## Project Objectives

1. **Explore the menu:** how many dishes exist, what they cost, and how prices differ by cuisine.
2. **Explore the orders:** the date range, number of orders and items sold, and the size of a typical order.
3. **Combine both tables:** use a join to find the most and least popular dishes and the highest-spending orders.

---

## Dataset

| File | Rows | Description |
|---|---|---|
| `menu_items.csv` | 32 | One row per dish: `menu_item_id`, `item_name`, `category`, `price` |
| `order_details.csv` | 12,234 | One row per item ordered: `order_details_id`, `order_id`, `order_date`, `order_time`, `item_id` |

The tables are linked by `order_details.item_id = menu_items.menu_item_id`.

```
order_details                         menu_items
-------------                         ----------
order_details_id (PK)                 menu_item_id (PK)
order_id                              item_name
order_date                            category
order_time                            price
item_id (FK)  ------------------->
```

---

## Repository Structure

```
restaurant_db_project/
├── README.md
├── Restaurant_SQL_Project_Report.pdf      # 10-page report with queries, results and charts
├── data/
│   ├── menu_items.csv
│   └── order_details.csv
├── setup/
│   └── create_restaurant_db.sql           # creates restaurant_db, both tables and loads the data
└── queries/
    ├── project_menu_items.sql             # menu exploration
    ├── project_order_details.sql          # orders exploration
    ├── project_table_joins.sql            # joins across both tables
    └── all_queries_combined.sql           # all three files in one script
```

---

## How to Run

1. Open **MySQL Workbench** (or any MySQL client).
2. Run `setup/create_restaurant_db.sql`. This creates the `restaurant_db` database, builds both tables and loads all the data.
3. Open any file in `queries/` (or `all_queries_combined.sql`) and run the queries.

---

## Questions Answered

| Area | Business question | SQL concepts used |
|---|---|---|
| Menu | How many items are on the menu? | `COUNT` |
| Menu | What are the least and most expensive items? | `ORDER BY`, `DESC` |
| Menu | How many Italian dishes are there, and which are cheapest and priciest? | `WHERE`, `ORDER BY` |
| Menu | How many dishes and what average price per category? | `GROUP BY`, `COUNT`, `AVG` |
| Orders | What is the date range of the data? | `MIN`, `MAX` |
| Orders | How many orders and items were there? | `COUNT(DISTINCT)`, `COUNT` |
| Orders | Which order had the most items, and how many had more than 12? | `GROUP BY`, `HAVING`, subquery |
| Joined | What are the least and most ordered items and their categories? | `LEFT JOIN`, `GROUP BY` |
| Joined | Which 5 orders spent the most money? | `SUM`, `ORDER BY`, `LIMIT` |
| Joined | What did the highest-spending order contain? | `LEFT JOIN`, `WHERE`, `GROUP BY` |

---

## Key Findings

- **Volume:** 5,370 orders and 12,234 items were ordered in the quarter, about 2.3 items per order.
- **Menu:** 32 dishes across 4 cuisines, priced from $5.00 (Edamame) to $19.95 (Shrimp Scampi).
- **Pricing by cuisine:** Italian has the highest average dish price ($16.75); American has the lowest ($10.07).
- **Most ordered:** Hamburger (622), Edamame (620) and Korean Beef Bowl (588).
- **Least ordered:** Chicken Tacos (123), well below the next-lowest dish (205).
- **Revenue:** Italian earns the most (about $49.5K, roughly 31% of menu revenue) even though Asian dishes sell more items.
- **Large orders are rare:** only 20 of 5,370 orders had more than 12 items; the largest have 14.
- **Top spend:** the highest-spending order (#440) spent $192.15 across 14 items, 8 of them Italian. The top 5 orders are mostly the largest orders (13 to 14 items).

### Data quality note

137 order lines (1.1%) have no `item_id`. A `LEFT JOIN` keeps these rows, so they appear with `NULL` item name, category and price. They count as items ordered but add no revenue, so revenue is slightly understated. 27 orders consist only of such lines.

---

## Skills Demonstrated

- Filtering, sorting and limiting results
- Aggregation (`COUNT`, `SUM`, `AVG`, `MIN`, `MAX`) with `GROUP BY` and `HAVING`
- Subqueries
- `LEFT JOIN` across two tables
- Spotting data quality issues from query results
- Turning query results into insights and a written report

---

## Author

**Amit Bisht**

