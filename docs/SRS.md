# Software Requirements Specification (SRS)
## Project: StockPilot — Inventory & Sales Management System

---

## 1. Introduction

### 1.1 Purpose
This document specifies the functional and non-functional requirements for **StockPilot**, a web-based Inventory and Sales Management System designed for small to medium-sized retail and wholesale businesses. It serves as the primary technical reference for system design, backend/frontend development, and quality assurance testing.

### 1.2 Scope
StockPilot streamlines daily stock tracking, product categorization, sales billing, and low-stock monitoring. The system eliminates manual spreadsheet errors by automatically updating inventory quantities upon each completed sale and enforcing role-based access control.

### 1.3 Definitions, Acronyms, and Abbreviations
* **SRS:** Software Requirements Specification
* **SKU:** Stock Keeping Unit (unique product identifier)
* **RBAC:** Role-Based Access Control
* **CRUD:** Create, Read, Update, Delete

---

## 2. Overall Description

### 2.1 Product Perspective
StockPilot is a standalone, decoupled web application consisting of:
* **Frontend:** Responsive web interface for dashboards, inventory tables, and point-of-sale billing.
* **Backend:** RESTful API handling authentication, business logic, stock validation, and transaction processing.
* **Database:** Relational database (`users`, `categories`, `products`, `sales`, `sale_items`).

### 2.2 User Classes and Characteristics
| Role | Responsibilities & Access Level |
| :--- | :--- |
| **Admin** | Full system access: manage users/roles, categories, products, sales records, and system settings. |
| **Inventory Manager** | Manage product categories, add/update products, adjust stock quantities, and monitor low-stock alerts. |
| **Sales Staff** | View available products, create customer sales orders, and view personal/recent sales history. |

### 2.3 Operating Environment
* **Client Side:** Modern web browsers (Chrome, Firefox, Edge, Safari) on desktop or tablet devices.
* **Server Side:** Linux/Windows server running Python/Node.js runtime and MySQL/PostgreSQL database.

### 2.4 Design and Implementation Constraints
* Passwords must be stored as cryptographic hashes (`password_hash`), never in plain text.
* Sales transactions must execute atomically so stock quantities never become negative due to concurrent orders.
* Sensitive configuration (database credentials, secret keys) must reside in `.env` and remain excluded from version control.

---

## 3. Specific Requirements

### 3.1 Functional Requirements

#### FR-1: Authentication & User Management
* **FR-1.1:** Users shall log in using a registered email address and password.
* **FR-1.2:** The system shall restrict API endpoints and UI views according to the authenticated user's assigned role (`admin`, `inventory_manager`, `sales_staff`).
* **FR-1.3:** Admins shall be able to create new user accounts and assign or update user roles.

#### FR-2: Category Management
* **FR-2.1:** Admins and Inventory Managers shall be able to create, view, update, and delete product categories.
* **FR-2.2:** Each category name must be unique across the system.

#### FR-3: Product & Stock Management
* **FR-3.1:** Admins and Inventory Managers shall be able to add new products with name, unique SKU, category, unit price, initial stock quantity, and low-stock threshold.
* **FR-3.2:** Users shall be able to search and filter products by name, SKU, or category.
* **FR-3.3:** The system shall flag products whose `stock_quantity` is less than or equal to their `low_stock_threshold`.

#### FR-4: Sales & Billing Processing
* **FR-4.1:** Authorized staff shall be able to create a sale by selecting one or more products and specifying quantities.
* **FR-4.2:** Before confirming a sale, the system shall verify that requested quantities do not exceed current `stock_quantity`.
* **FR-4.3:** Upon sale confirmation, the system shall calculate line subtotals and total amount, record entries in `sales` and `sale_items`, and deduct sold quantities from `products.stock_quantity` within a single database transaction.

#### FR-5: Dashboard & Reporting
* **FR-5.1:** The dashboard shall display total products, low-stock item count, total sales count, and total revenue summary.

---

### 3.2 Non-Functional Requirements

#### NFR-1: Security
* All passwords must be hashed using a strong one-way algorithm (e.g., bcrypt/Argon2).
* All user inputs must be validated and sanitized to prevent SQL injection and XSS attacks.

#### NFR-2: Performance
* Standard CRUD API responses and product search queries shall complete within 500 ms under normal load (up to 10,000 product records).

#### NFR-3: Reliability & Data Integrity
* Foreign key constraints (`category_id`, `created_by`, `sale_id`, `product_id`) and `ON DELETE CASCADE` rules on `sale_items` must preserve referential integrity.
* Database transactions must roll back automatically if any step of a sale creation fails.

#### NFR-4: Usability
* Common workflows (adding a product or recording a 3-item sale) shall be completable within 3 clicks/steps from the main navigation.