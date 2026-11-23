# StockPilot — Inventory & Sales Management System

## Project Overview
StockPilot is a browser-based web application designed to manage product inventory, stock levels, and sales workflows efficiently. It prevents overselling through real-time stock validation, enforces role-based access control, and provides actionable dashboard summaries.

## Problem Statement
Manual or disconnected inventory tracking often causes stock mismatches, accidental overselling, lack of role accountability, and delayed visibility into low-stock items and daily sales performance.

## Group Members
| Name | Student ID | Primary Responsibility |
| :--- | :--- | :--- |
| Member 1 (Your Name) | ID-1 | System Architecture, Authentication, Role Control, Product & Stock Management |
| Member 2 | ID-2 | Sales Workflow, Stock Deduction Logic, Search & Filtering |
| Member 3 | ID-3 | Dashboard & Summary Reports, SRS & Documentation, Testing |

## Technology Stack
- **Frontend:** [e.g., HTML, CSS, JavaScript / React / Tailwind CSS]
- **Backend:** [e.g., Python / Django / Node.js / Express / PHP / Laravel]
- **Database:** [e.g., MySQL / PostgreSQL / SQLite / MongoDB]

## User Roles & Permissions
- **Admin:** Full access to user/role management, categories, products, stock restocking, sales, and reports.
- **Inventory Manager:** Manage categories and products, restock inventory, and monitor low-stock alerts.
- **Sales Staff:** View available products, search/filter inventory, and create validated sales orders.

## Core Features
- Secure authentication (login/logout) with hashed passwords and role-based route protection
- Category and product management with SKU, unit price, and low-stock thresholds
- Real-time stock validation (prevents selling more than available stock) and automatic stock updates on sale
- Database-driven search and filtering (by product name/SKU, category, stock status, and sales date)
- Dashboard overview cards and summary tables for total products, low-stock items, and sales performance

## Setup & Installation
1. **Clone the repository:**
   ```bash
   git clone [https://github.com/](https://github.com/)<your-username>/stockpilot-inventory-sales.git
   cd stockpilot-inventory-sales# stockpilot-inventory-sales
