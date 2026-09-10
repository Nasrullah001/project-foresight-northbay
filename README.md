# project-foresight-northbay
An end-to-end data science and analytics solution developed for **NorthBay Living** (a D2C home & lifestyle brand) to optimize inventory management, predict SKU-level weekly demand, eliminate stockouts, and identify overstock markdown candidates.

## Executive Summary
NorthBay Living manages ~200 active SKUs across home furnishings, décor, and small appliances. Previously relying on manual spreadsheets and gut-feel planning, the brand experienced frequent stockouts on high-demand items and overstock accumulation on slow movers.

**Project FORESIGHT** establishes a reproducible analytics engine that:

1. **Forecasts SKU-Level Demand:** Predicts weekly demand across a multi-week horizon using machine learning backtested against a seasonal-naive baseline.
2. **Scores Inventory Risk:** Categorizes SKUs into actionable decision quadrants based on lead times, safety stock, and demand forecasts.
3. **Productizes Insights:** Serves operations and merchandising teams via an interactive Streamlit planning dashboard and scoring interface.

## Dataset Overview

The pipeline ingests four relational extracts forming a star schema:
**`sales_daily.csv` (Fact):** Transaction-level daily sales records (`sku_id`, `date`, `units_sold`, `revenue`, `unit_price`, `promo_flag`).
**`sku_master.csv` (Dimension):** Product catalog (`sku_id`, `category`, `subcategory`, `launch_date`, `unit_cost`, `list_price`).
**`calendar.csv` (Dimension):** Date dimensions (`date`, `week`, `month`, `season`, `is_holiday`, `promo_event`).
**`inventory_snapshots.csv` (Snapshot):** Current warehouse stock position (`sku_id`, `on_hand_units`, `on_order_units`, `lead_time_days`, `reorder_point`).

## Decisioning Matrix & Risk Framework

Every SKU is scored using a 2x2 decision grid based on forecast demand vs. available pipeline stock (On Hand + On Order):

Quadrant | Stockout Risk | Overstock Risk | Recommended Operational Action
--
**Reorder Now** | **High** | **Low** | Raise replenishment order before stock runs out.
**Markdown / Clear** | **Low** | **High** | Apply discounts/promotions to liberate tied-up capital.
**Watch / Volatile** | **High** | **High** | Demand is erratic; perform manual inventory audit.
**Healthy** | **Low** | **Low** | Inventory is balanced; no action required.

## Key Results & Impact Metrics
**Baseline Performance:** Evaluated using Weighted Absolute Percentage Error (WAPE) to safeguard against low-volume SKU bias.
**Model Accuracy:** The ML approach beats the seasonal-naive baseline on rolling-origin backtests.
**Capital Optimization:** Identifies specific high-risk stockout SKUs to protect sales revenue and highlights overstocked SKUs for markdown campaigns to free locked working capital.
