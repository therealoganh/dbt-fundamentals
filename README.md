# dbt Fundamentals: Jaffle Shop Pipeline

A foundational analytics engineering project modeling raw e-commerce data into modular, dimensional data marts using **dbt Studio** and **Snowflake**. Built following dbt Labs best practices for transformation layering, testing, and documentation.

---

## 🏗️ Architecture & Lineage

The transformation pipeline follows a two-tier dimensional architecture:

* **Staging (`stg_`)**: Cleans, standardizes data types, and renames raw source columns 1:1 (`stg_jaffle_shop__customers`, `stg_jaffle_shop__orders`, `stg_stripe__payments`).
* **Marts (`dim_`, `fct_`)**: Final business-facing dimensional and fact tables (`dim_customers`, `fct_orders`) materialized as tables/views for reporting and BI consumption.

```
raw_sources (customers, orders, payments)
  └── staging models (stg_*)
              ├── dim_customers
              └── fct_orders
```

---

## 🧪 Testing & Data Quality

Configured automated generic schema tests with YAML to enforce data accuracy & relationship integrity:

* `unique` & `not_null` constraints on primary keys (`customer_id`, `order_id`, `payment_id`).
* `relationships` tests ensuring foreign key parity between `orders` and `customers`.
* `accepted_values` validation on order and payment status dimensions (`placed`, `shipped`, `completed`, `fail`, `success`).

---
