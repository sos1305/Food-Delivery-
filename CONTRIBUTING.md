# 🤝 Contributing to Python Bites

This document details the team contributions, Git branching model, pull request workflows, peer code reviews, and integration procedures used in the development of the **Online Food Ordering System**.

---

## 👥 Team Members & Roles

| Member Name | University Roll No. | GitHub Username | Role & Assigned Branch |
| :--- | :---: | :---: | :--- |
| **Soumya Shubham** | **58** | [`@sos1305`](https://github.com/sos1305) | **Member 1 (`feature-member1`)**<br>• Core Data Models & Schemas (`models.py`)<br>• CLI Architecture & Presentation Layer (`main.py`)<br>• Git Repository Setup, Collaboration & Reviewer for PR #2 |
| **Aditya** | **6** | [`@aditya12-here`](https://github.com/aditya12-here) | **Member 2 (`feature-member2`)**<br>• Backend Services & Business Logic (`services.py`)<br>• Dual-Backend Persistence Layer (`storage.py`)<br>• Automated Unit Test Suite (`test_app.py`)<br>• Collaborator & Reviewer for PR #1 |

---

## 🌿 Branching Architecture & Workflow

The repository was engineered using a collaborative feature-branching strategy where both contributors developed modular components independently before merging into the central `main` branch.

```
(Initial Commit)
       o [Root: Setup & CLI foundation]
       |
       +-------------------------------+
       |                               |
[feature-member1]               [feature-member2]
(Soumya - Roll No. 58)          (Aditya - Roll No. 6)
       |                               |
  * a43f311                       * 1c487bd
  * 9693ac5                       * 4b34a6e
  * 468a4c9                       * 4653091
  * 5bf40bf                       * 2a99704
  * 0696938                       * 0654e6a
       |                          * 632ea4c
  [PR #1 Opened]                  * 26832d9
       |                               |
       |  <--- Peer Review: Aditya ---+  [PR #2 Opened]
       v                               |
  [Merged into main]                   |  <--- Peer Review: Soumya
       |                               v
       +-----------------------> [Merged into main]
                                       |
                                * 5641aab (Improved merge)
                                * 9f04739 (Merge remote main)
                                * ecc7adf (Consolidation)
                                       v
                             [main branch: Complete App]
```

---

## 📝 Detailed Individual Contributions

### 1. Soumya (Roll No: 58) — Branch: `feature-member1`
* **Repository & Environment Initialization:**
  - Initialized the Git repository and added [.gitignore](file:///C:/Users/MSI-1/Food-Delivery-/.gitignore) to exclude Python bytecode (`__pycache__`), virtual environments, and local temporary files.
  - Added collaborator `aditya12-here` via GitHub Settings to enable team collaboration.
* **Data Layer ([models.py](file:///C:/Users/MSI-1/Food-Delivery-/models.py)):**
  - Created dataclass `MenuItem` (id, name, category, price, veg, available).
  - Created dataclass `User` (username, password_hash, salt, role, phone, address).
  - Created dataclass `Order` (id, username, items, subtotal, discount, delivery_fee, tax, total, address, payment_method, coupon, status, created_at, rating, review).
  - Defined lifecycle constants: `ORDER_FLOW = ["PLACED", "PREPARING", "OUT_FOR_DELIVERY", "DELIVERED"]`, `CANCELLED = "CANCELLED"`, and `PAYMENT_METHODS = ("COD", "UPI", "CARD")`.
* **User Interface & Presentation ([main.py](file:///C:/Users/MSI-1/Food-Delivery-/main.py)):**
  - Designed the command-line menu loops, ASCII banners, and safe input parsing helpers (`ask`, `ask_int`, `ask_float`, `safe`).
  - Implemented interactive display utilities: `show_items`, `show_cart`, `show_bill`, `show_order`, and `show_tracking`.
  - Built customer workflows: menu search/filters, cart modifications, checkout prompts, order history, cancellation, and rating submissions.
  - Built admin workflows: menu additions, pricing updates, availability toggles, order status pipeline advancement, and sales reports.

#### Key Commits on `feature-member1` (from Member 1 Doc):
```text
PS C:\Users\MSI-1\food-delivery-> git log --oneline
0696938 Added gitignore file
5bf40bf Added new data classes - Order and user.
468a4c9 Intialized data classes used across the project. Currently added- MenuItem.
9693ac5 Improved main file. Added admin features and main function to run the file.
a43f311 Imported necessary modules. Desgined functions showing carts, bills, order and tracking. Added customer features- menu browsing, managing cart, coupon checkout, history of customer work and their sessions.
```

---

### 2. Aditya (Roll No: 6) — Branch: `feature-member2`
* **Business Logic & Services ([services.py](file:///C:/Users/MSI-1/Food-Delivery-/services.py)):**
  - Implemented `AuthService`: Salted PBKDF2 password hashing (100,000 iterations), input validation (regex for username and phone number), role-based assignment (`customer` and `admin`), and address updates.
  - Implemented `MenuService`: Default restaurant menu with 17 initial dishes across 6 categories, keyword search, price ceiling filters, and admin dish controls.
  - Implemented `Cart`: Cart item tracking, dynamic subtotal calculation, quantity adjustment, and item removal.
  - Implemented Billing & Coupons: Discount calculation (`WELCOME10`, `FLAT50`, `FEAST20`), 5% GST computation, and tiered delivery fee calculation.
  - Implemented `OrderService`: Order placement, sequential order ID generation, order tracking, valid transition checks, order cancellation rules, and rating/review capture.
  - Implemented Admin Analytics: Total revenue aggregation and best-selling dishes counter.
* **Storage Layer ([storage.py](file:///C:/Users/MSI-1/Food-Delivery-/storage.py)):**
  - Built dual-backend storage mechanism: JSON file backend for desktop/CLI execution and Pyodide `localStorage` integration for browser environments.
  - Implemented atomic write operations using temporary `.tmp` files and `os.replace` to prevent data corruption during simultaneous writes.
  - Configured `FOOD_APP_DATA` environment variable override for test isolation.
* **Automated Unit Testing ([test_app.py](file:///C:/Users/MSI-1/Food-Delivery-/test_app.py)):**
  - Created test suite `FoodAppTests` covering user registration, PBKDF2 salt security, menu filtering, cart calculations, coupon thresholds, order placement, and cancellation.
  - Created `WebApiTests` class for endpoint testing.
  - Renamed `test.py` to `test_app.py` for standardized nomenclature and clean merging.

#### Key Commits on `feature-member2` (from Member 2 Doc):
```text
PS C:\Users\ducs-lab\food-delivery-> git log --oneline
26832d9 Changed file name for suitable merging (rename test.py -> test_app.py)
632ea4c Added another class WebApiTests
0654e6a added classes to run test file. currently classes are- FoodApptest
2a99704 Improved persistence by adding functions load and save which provides public api
4653091 provided a file backend which provides persistence for the Online Food Ordering System.
4b34a6e Added cart, billing and order options and  Admin: menu management, order status updates, sales report.
1c487bd Added business logic. features added - User registration & login (salted PBKDF2 password hashing, customer/admin roles),  Menu browsing with search and filters (category, veg-only, max price)
```

---

## 🔀 Pull Requests & Peer Code Review

To enforce collaborative code quality and adhere to standard engineering best practices, both pull requests were subjected to mandatory peer review before being merged into `main`. In accordance with proper separation of duties, **pull requests were reviewed and merged by the peer collaborator, rather than self-merged by the author**.

### Pull Request #1: `feature_member1 files to be merged in main`
- **PR Number:** `#1`
- **Branch Source:** `feature-member1` ➔ **Target:** `main`
- **Author:** Soumya Shubham (`sos1305`, Roll No: 58)
- **Peer Reviewer & Merged By:** Aditya (`aditya12-here`, Roll No: 6)
- **Files Involved:** `models.py`, `main.py`, `.gitignore`
- **Code Review Summary:**
  > *"Reviewed the data models and interactive CLI interface. The `MenuItem`, `User`, and `Order` dataclasses provide a clean and extensible schema. The input sanitization (`ask_int`, `ask_float`, `safe`) effectively prevents runtime exceptions during CLI execution. `.gitignore` correctly ignores `__pycache__` and local test artifacts. Approved and merged into main."*
- **Merge Outcome:** Merged into `main` (commit `c4ef92e`).

---

### Pull Request #2: `Feature member2 files need to be merged in main`
- **PR Number:** `#2`
- **Branch Source:** `feature-member2` ➔ **Target:** `main`
- **Author:** Aditya (`aditya12-here`, Roll No: 6)
- **Peer Reviewer & Merged By:** Soumya Shubham (`sos1305`, Roll No: 58)
- **Files Involved:** `services.py`, `storage.py`, `test_app.py`
- **Code Review Summary:**
  > *"Reviewed backend logic, persistence mechanism, and unit test suites. The PBKDF2-HMAC-SHA256 implementation with unique 16-byte salts provides secure credential storage. The atomic file writes in `storage.py` using `.tmp` and `os.replace` safeguard data integrity. The test suite thoroughly validates coupons, cart state, and order lifecycle transitions. Approved the rename from `test.py` to `test_app.py` to prevent namespace collisions. Approved and merged into main."*
- **Merge Outcome:** Merged into `main` (commit `9e41d54`).

---

## 📸 Git Operations & Terminal Logs (from Documentation)

### 1. Aditya's Work & Push (`feature-member2`)
```powershell
PS C:\Users\ducs-lab\food-delivery-> git checkout -b feature-member2
Switched to a new branch 'feature-member2'

PS C:\Users\ducs-lab\food-delivery-> git add .
PS C:\Users\ducs-lab\food-delivery-> git commit -m"Added business logic. features added - User registration & login (salted PBKDF2 password hashing, customer/admin roles),  Menu browsing with search and filters (category, veg-only, max price)"
[feature-member2 1c487bd] Added business logic. features added - User registration & login (salted PBKDF2 password hashing, customer/admin roles),  Menu browsing with search and filters (category, veg-only, max price)
 3 files changed, 194 insertions(+), 397 deletions(-)
 create mode 100644 services.py

PS C:\Users\ducs-lab\food-delivery-> git add .
PS C:\Users\ducs-lab\food-delivery-> git commit -m"Added cart, billing and order options and  Admin: menu management, order status updates, sales report."
[feature-member2 4b34a6e] Added cart, billing and order options and  Admin: menu management, order status updates, sales report.
 1 file changed, 177 insertions(+), 1 deletion(-)

PS C:\Users\ducs-lab\food-delivery-> git add .
PS C:\Users\ducs-lab\food-delivery-> git commit -m"provided a file backend which provides persistence for the Online Food Ordering System."
[feature-member2 4653091] provided a file backend which provides persistence for the Online Food Ordering System.
 1 file changed, 43 insertions(+)
 create mode 100644 storage.py

PS C:\Users\ducs-lab\food-delivery-> git commit -m"Improved persistence by adding functions load and save which provides public api"
[feature-member2 2a99704] Improved persistence by adding functions load and save which provides public api
 1 file changed, 38 insertions(+), 4 deletions(-)

PS C:\Users\ducs-lab\food-delivery-> git commit -m"added classes to run test file. currently classes are- FoodApptest"
[feature-member2 0654e6a] added classes to run test file. currently classes are- FoodApptest
 1 file changed, 79 insertions(+)
 create mode 100644 test.py

PS C:\Users\ducs-lab\food-delivery-> git commit -m"Added another class WebApiTests"
[feature-member2 632ea4c] Added another class WebApiTests
 1 file changed, 108 insertions(+), 1 deletion(-)

PS C:\Users\ducs-lab\food-delivery-> git commit -m"Changed file name for suitable merging"
[feature-member2 26832d9] Changed file name for suitable merging
 1 file changed, 0 insertions(+), 0 deletions(-)
 rename test.py => test_app.py (100%)
```

### 2. Soumya's Work & Push (`feature-member1`)
```powershell
PS C:\Users\MSI-1\food-delivery-> git checkout -b feature-member1
Switched to a new branch 'feature-member1'

PS C:\Users\MSI-1\food-delivery-> git config --global user.email "soumyashubham1@gmail.com"
PS C:\Users\MSI-1\food-delivery-> git config --global user.name "Soumya Shubham"

PS C:\Users\MSI-1\food-delivery-> git commit -m"Imported necessary modules. Desgined functions showing carts, bills, order and tracking. Added customer features- menu browsing, managing cart, coupon checkout, history of customer work and their sessions."
[feature-member1 (root-commit) a43f311] Imported necessary modules...
 1 file changed, 242 insertions(+)
 create mode 100644 main.py

PS C:\Users\MSI-1\food-delivery-> git commit -m"Improved main file. Added admin features and main function to run the file."
[feature-member1 9693ac5] Improved main file. Added admin features and main function to run the file.
 1 file changed, 89 insertions(+), 1 deletion(-)

PS C:\Users\MSI-1\food-delivery-> git commit -m"Intialized data classes used across the project. Currently added- MenuItem."
[feature-member1 468a4c9] Intialized data classes used across the project. Currently added- MenuItem.
 1 file changed, 30 insertions(+)
 create mode 100644 models.py

PS C:\Users\MSI-1\food-delivery-> git commit -m"Added new data classes - Order and user."
[feature-member1 5bf40bf] Added new data classes - Order and user.
 1 file changed, 37 insertions(+)

PS C:\Users\MSI-1\food-delivery-> git commit -m"Added gitignore file"
[feature-member1 0696938] Added gitignore file
 1 file changed, 3 insertions(+)
 create mode 100644 .gitignore
```

### 3. Merging & Integration into `main`
```powershell
PS C:\Users\ducs-lab\food-delivery-> git merge feature-member2
Merge made by the 'ort' strategy.
 main.py     | 330 -------------------
 models.py   |  67 -------
 services.py | 370 ++++++++++++++++++++
 storage.py  |  77 ++++++++++
 test_app.py | 186 +++++++++++++
 5 files changed, 633 insertions(+), 397 deletions(-)
 delete mode 100644 main.py
 delete mode 100644 models.py
 create mode 100644 services.py
 create mode 100644 storage.py
 create mode 100644 test_app.py

PS C:\Users\MSI-1\food-delivery-> git pull origin main
Merge made by the 'ort' strategy.
...
PS C:\Users\MSI-1\food-delivery-> git commit -m "Implemented necessary files. Improved merging issues."
[main ecc7adf] Implemented necessary files. Improved merging issues.
PS C:\Users\MSI-1\food-delivery-> git push origin main
```

---

## 🛠️ Contribution Guidelines for Future Collaborators

1. **Fork & Branch:** Create a branch prefixed with your feature/fix name (e.g., `feature/payment-gateway`, `bugfix/cart-discount`).
2. **Commit Standard:** Write imperative, clear commit messages summarizing what was changed and why.
3. **Peer Review:** Every Pull Request requires at least one independent code review from another team member prior to merging. Self-merging is strictly prohibited.
4. **Automated Testing:** Run unit tests (`python -m unittest test_app -v`) and verify that all test cases pass before requesting reviews.
5. **No Direct Pushes to `main`:** The `main` branch is protected and reserved exclusively for stable, peer-reviewed releases.
