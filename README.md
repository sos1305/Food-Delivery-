# 🍽️ Python Bites – Online Food Ordering System

[![Python Version](https://img.shields.io/badge/Python-3.10%2B-blue.svg)](https://www.python.org/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](#license)
[![Architecture](https://img.shields.io/badge/Architecture-Modular%20MVC-orange.svg)](#project-structure)
[![Tests](https://img.shields.io/badge/Tests-Passing%20(UnitTests)-brightgreen.svg)](#running-unit-tests)

A full-featured, modular food ordering and delivery management system built in Python. Designed with a clean separation of concerns across data models, business logic services, dual-backend persistent storage, and an interactive command-line interface (CLI).

---

## 📌 Table of Contents
- [Project Overview & Objectives](#-project-overview--objectives)
- [Team Members & Contributions](#-team-members--contributions)
- [Key Features](#-key-features)
- [System Architecture & Technologies](#-system-architecture--technologies)
- [Project Structure](#-project-structure)
- [Installation & Execution](#-installation--execution)
- [Running Unit Tests](#-running-unit-tests)
- [Default Credentials](#-default-credentials)
- [Sample Output & Execution Walkthrough](#-sample-output--execution-walkthrough)
- [License](#-license)

---

## 🎯 Project Overview & Objectives

**Python Bites** simplifies online restaurant food delivery through a terminal-based interactive platform with web/Pyodide compatibility. The platform caters to both customers seeking a convenient ordering experience and administrators managing restaurant operations.

### Core Objectives:
1. **Modular Architecture:** Implement a clean separation between data definitions ([models.py](file:///C:/Users/MSI-1/Food-Delivery-/models.py)), persistence ([storage.py](file:///C:/Users/MSI-1/Food-Delivery-/storage.py)), core business logic ([services.py](file:///C:/Users/MSI-1/Food-Delivery-/services.py)), and presentation ([main.py](file:///C:/Users/MSI-1/Food-Delivery-/main.py)).
2. **Dual-Backend Persistence:** Seamlessly support local JSON file storage with atomic writes for CLI execution, alongside browser `localStorage` fallback for Pyodide/web deployments.
3. **Robust Security:** Implement salted PBKDF2-HMAC-SHA256 password hashing with 100,000 iterations to protect user credentials.
4. **Complete E-Commerce Flow:** Deliver end-to-end functionality including dynamic menu filtering, shopping cart management, coupon discount calculations, GST and delivery fee computations, multi-method payment checkouts, real-time order lifecycle tracking, order cancellation, and customer reviews.
5. **Collaborative Git Engineering:** Demonstrate professional version control best practices, including independent feature branching (`feature-member1`, `feature-member2`), peer code reviews, and structured pull request merges into `main`.

---

## 👥 Team Members & Contributions

| Member Name | University Roll No. | GitHub Handle | Assigned Branch | Core Domain & Responsibilities |
| :--- | :---: | :---: | :---: | :--- |
| **Soumya Shubham** | **58** | [`@sos1305`](https://github.com/sos1305) | `feature-member1` | **CLI & Data Architecture:**<br>• Initial repository configuration & `.gitignore`<br>• Core data models & schemas (`models.py`)<br>• Command-Line Interface & display handlers (`main.py`)<br>• Interactive navigation, cart UI, checkout UI, admin panels<br>• Peer review of PR #2 and branch consolidation |
| **Aditya** | **6** | [`@aditya12-here`](https://github.com/aditya12-here) | `feature-member2` | **Business Logic & Backend Storage:**<br>• Authentication, PBKDF2 password hashing (`services.py`)<br>• Menu service, cart logic, billing engine & coupons (`services.py`)<br>• Order lifecycle & admin reporting services (`services.py`)<br>• Dual-backend storage engine with atomic writes (`storage.py`)<br>• Unit test suites `FoodAppTests` & `WebApiTests` (`test_app.py`)<br>• Peer review of PR #1 |

---

## ✨ Key Features

### 👤 User Authentication & Roles
- **Registration & Validation:** Alphanumeric username (3–20 chars), min 6-character password, and 10-digit phone verification.
- **Security:** Salted PBKDF2-HMAC-SHA256 password hashing (100,000 iterations with unique 16-byte cryptographically secure salts).
- **Role-Based Access Control (RBAC):** Distinct interfaces and privileges for **Customers** and **Admins**.

### 📖 Menu Browsing & Filtering
- **Categorized Menus:** Starters, Main Course, Breads, Pizza & Pasta, Desserts, and Beverages.
- **Smart Filtering:** Multi-parameter search by keyword, category, vegetarian-only flag, and price threshold.
- **Dynamic Availability:** Displays real-time item availability.

### 🛒 Shopping Cart & Billing Engine
- **Cart Management:** Add items, modify quantities, remove individual lines, or clear the cart.
- **Automated Billing:** Real-time subtotal, 5% GST computation, and delivery fee calculation (Rs. 30 flat; free on orders over Rs. 500).
- **Coupon Discount System:**
  - `WELCOME10`: 10% off (up to Rs. 100).
  - `FLAT50`: Flat Rs. 50 discount on orders above Rs. 300.
  - `FEAST20`: 20% off (up to Rs. 200) on orders above Rs. 800.

### 📦 Order Placement, Lifecycle & Reviews
- **Flexible Payments:** Cash on Delivery (COD), UPI, and Debit/Credit Card.
- **Order Lifecycle Pipeline:** `PLACED` ➔ `PREPARING` ➔ `OUT_FOR_DELIVERY` ➔ `DELIVERED` (or `CANCELLED`).
- **Cancellation & Feedback:** Customers can cancel orders prior to out-for-delivery status and submit 1–5 star ratings and reviews for delivered meals.

### 🛠️ Administrative Operations
- **Menu Management:** Add new dishes, edit prices/categories, and toggle availability.
- **Order Processing:** Advance order stages through the fulfillment lifecycle.
- **Sales Analytics:** Aggregate revenue calculation and top-selling dish reports.

---

## 💻 System Architecture & Technologies

```
                  +-----------------------------------+
                  |         User Interface            |
                  |             main.py               |
                  +-----------------+-----------------+
                                    |
                                    v
                  +-----------------------------------+
                  |         Business Logic            |
                  |           services.py             |
                  |  (Auth, Menu, Cart, Order, Admin) |
                  +--------+-----------------+--------+
                           |                 |
            +--------------v---+         +---v---------------+
            |    Data Models   |         | Persistence Layer |
            |     models.py    |         |    storage.py     |
            +------------------+         +---------+---------+
                                                   |
                                     +-------------+-------------+
                                     |                           |
                                     v                           v
                             Desktop / CLI               Browser / Web
                             [ data/*.json ]         [ localStorage / Pyodide ]
```

### Technologies Used:
- **Language:** Python 3.10+
- **Standard Library Modules:** `dataclasses`, `hashlib`, `json`, `os`, `re`, `tempfile`, `unittest`, `datetime`, `collections`
- **Persistence:** Atomic JSON file operations (`.tmp` write followed by `os.replace`)
- **Web Compatibility:** Pyodide `js.localStorage` bridge
- **Version Control:** Git, GitHub, Pull Requests, ORT Merge Strategy

---

## 📁 Project Structure

```text
Food-Delivery-/
├── .gitignore          # Git exclusion rules (bytecode, temporary files, caches)
├── main.py             # CLI application entry point and interactive presentation
├── models.py           # Dataclass schemas (MenuItem, User, Order) and lifecycle constants
├── services.py         # Business logic: AuthService, MenuService, Cart, OrderService
├── storage.py          # Persistence layer: atomic file storage and Pyodide fallback
├── test_app.py         # Automated unit test suite (FoodAppTests, WebApiTests)
└── data/               # Persistent JSON storage directory
    ├── menu.json       # Restaurant item catalog and availability state
    ├── orders.json     # Order transaction histories, items, and reviews
    └── users.json      # User credentials, PBKDF2 hashes, salts, and roles
```

---

## 🚀 Installation & Execution

### Prerequisites
- Python 3.10 or higher installed on your system.
- Git installed.

### 1. Clone the Repository
```bash
git clone https://github.com/sos1305/Food-Delivery-.git
cd Food-Delivery-
```

### 2. Run the Application
Launch the interactive command-line interface:
```bash
python main.py
```

---

## 🧪 Running Unit Tests

Automated test suites verify all functional aspects of the application, including authentication, password salting, cart totals, coupon calculations, delivery rules, order state transitions, and error handling:

```bash
python -m unittest test_app -v
```

---

## 🔑 Default Credentials

For testing and demonstration, the following default credentials are provided:

| Role | Username | Password | Notes |
| :--- | :--- | :--- | :--- |
| **Admin** | `admin` | `admin123` | Default management account (auto-created on first run) |
| **Customer** | *(Self-register)* | *(Min 6 chars)* | Register via Option 2 in the main menu |

---

## 🖥️ Sample Output & Execution Walkthrough

The following real execution walkthrough demonstrates the end-to-end customer workflow:

```text
PS C:\Users\MSI-1\food-delivery-> python main.py
==============================================================
  WELCOME TO PYTHON BITES - ONLINE FOOD ORDERING
==============================================================
1. Login   2. Register   0. Exit
> 2
Choose a username: sos13
Choose a password: 123456
Phone (10 digits, optional): 
Address (optional): 
Registration successful. You can now log in.

1. Login   2. Register   0. Exit
> 1
Username: sos12
Password: 123456
! Invalid username or password.

1. Login   2. Register   0. Exit
> 1
Username: sos13
Password: 123456
--------------------------------------------------------------
Hello, sos13!   Cart items: 0
--------------------------------------------------------------
1. Browse / search menu       5. Track an order
2. Manage cart                6. Cancel an order
3. Checkout                   7. Rate a delivered order
4. Order history              0. Logout
> 1

Filters (press Enter to skip each)
Categories: Beverages, Breads, Desserts, Main Course, Pizza & Pasta, Starters
Search by name : paneer tikka
Category       : 
Veg only? (y/N): 
Max price      : 

[Starters]
   1. Paneer Tikka             Rs. 220.00  VEG

--------------------------------------------------------------
Hello, sos13!   Cart items: 0
--------------------------------------------------------------
1. Browse / search menu       5. Track an order
2. Manage cart                6. Cancel an order
3. Checkout                   7. Rate a delivered order
4. Order history              0. Logout
> 2

--- CART ---
Your cart is empty.
1. Add item   2. Change quantity   3. Remove item   4. Apply coupon   5. Clear   0. Back
> 1
Item id: 1
Quantity [1]: 2

--- CART ---
--------------------------------------------------------------
   1. Paneer Tikka              2 x Rs. 220.00 = Rs.  440.00
--------------------------------------------------------------
  Subtotal      : Rs.   440.00
  GST (5%)      : Rs.    22.00
  Delivery fee  : Rs.    30.00
  TOTAL         : Rs.   492.00
1. Add item   2. Change quantity   3. Remove item   4. Apply coupon   5. Clear   0. Back
> 4
Available coupons:
  WELCOME10   10% off (max Rs.100)
  FLAT50      Rs.50 off on orders above Rs.300
  FEAST20     20% off (max Rs.200) on orders above Rs.800
Enter code (blank to remove): WELCOME10
Coupon applied.

--- CART ---
--------------------------------------------------------------
   1. Paneer Tikka              2 x Rs. 220.00 = Rs.  440.00
--------------------------------------------------------------
  Subtotal      : Rs.   440.00
  Discount      : -Rs.   44.00
  GST (5%)      : Rs.    19.80
  Delivery fee  : Rs.    30.00
  TOTAL         : Rs.   445.80
1. Add item   2. Change quantity   3. Remove item   4. Apply coupon   5. Clear   0. Back
> 0

--------------------------------------------------------------
Hello, sos13!   Cart items: 2
--------------------------------------------------------------
1. Browse / search menu       5. Track an order
2. Manage cart                6. Cancel an order
3. Checkout                   7. Rate a delivered order
4. Order history              0. Logout
> 3

--------------------------------------------------------------
   1. Paneer Tikka              2 x Rs. 220.00 = Rs.  440.00
--------------------------------------------------------------
  Subtotal      : Rs.   440.00
  Discount      : -Rs.   44.00
  GST (5%)      : Rs.    19.80
  Delivery fee  : Rs.    30.00
  TOTAL         : Rs.   445.80
Delivery address [required]: Department of Computer Science, DU
Payment method (COD/UPI/CARD) [COD]: UPI
Confirm order? (y/N): y

Order placed! Your order id is #1001. Total Rs.445.80

--------------------------------------------------------------
Hello, sos13!   Cart items: 0
--------------------------------------------------------------
1. Browse / search menu       5. Track an order
2. Manage cart                6. Cancel an order
3. Checkout                   7. Rate a delivered order
4. Order history              0. Logout
> 0

1. Login   2. Register   0. Exit
> 0

Thank you for visiting. Goodbye!
PS C:\Users\MSI-1\food-delivery->
```

---

## 📄 License
This project is developed for educational purposes as part of the collaborative software development curriculum. Distributed under the MIT License.
