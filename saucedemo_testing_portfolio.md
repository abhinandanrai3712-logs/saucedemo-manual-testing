# Level 1 Manual Testing Portfolio Project: SauceDemo

## Project Overview
**Application Under Test:** SauceDemo (Swag Labs) - an e-commerce demonstration website.
**Testing Goal:** To perform comprehensive Functional and UI validation of core e-commerce workflows to ensure reliability, usability, and correctness before simulated release. The focus is on verifying critical user journeys from authentication through product selection and order completion.

## Test Plan (Light)
* **Scope:** Login, Inventory (Product Catalog), Shopping Cart, and Checkout modules.
* **Out of Scope:** Performance testing, Security testing, Backend database validation.
* **Test Environment:** Google Chrome (Version 120.0+) / Windows 11.
* **Test Methodology:** Black-box manual testing, Exploratory testing.

## Test Case Suite

| Test Case ID | Feature | Scenario | Steps | Expected Result | Priority |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-001** | Login | Happy Path: Successful login with valid credentials | 1. Navigate to SauceDemo URL.<br>2. Enter Username: `standard_user`.<br>3. Enter valid password.<br>4. Click 'Login' button. | User is authenticated and redirected to the Inventory page. | High |
| **TC-002** | Login | Negative: Attempt login with locked-out account | 1. Navigate to SauceDemo URL.<br>2. Enter Username: `locked_out_user`.<br>3. Enter valid password.<br>4. Click 'Login' button. | Login fails. Error message displayed: "Epic sadface: Sorry, this user has been locked out." | High |
| **TC-003** | Login | Negative: Attempt login with empty credentials | 1. Navigate to SauceDemo URL.<br>2. Leave Username and Password fields blank.<br>3. Click 'Login' button. | Login fails. Error message displayed requiring username/password. | Medium |
| **TC-004** | Inventory | Happy Path: Add single product to cart | 1. Login successfully.<br>2. On Inventory page, click 'Add to cart' for "Sauce Labs Backpack".<br>3. Verify cart badge. | Button changes to 'Remove'. Cart badge updates to '1'. | High |
| **TC-005** | Inventory | Functional: Sort items by Price (Low to High) | 1. Login successfully.<br>2. Click on the sorting dropdown.<br>3. Select 'Price (low to high)'. | Products are re-ordered and displayed in ascending order based on price. | Medium |
| **TC-006** | Cart | Functional: Remove product from cart | 1. Add item to cart.<br>2. Navigate to Cart page.<br>3. Click 'Remove' button for the item. | Item is removed from the cart list. Cart badge counter decreases. | High |
| **TC-007** | Cart | Happy Path: Navigate to Checkout from Cart | 1. Ensure at least 1 item is in cart.<br>2. Navigate to Cart page.<br>3. Click 'Checkout' button. | User is redirected to 'Checkout: Your Information' page. | High |
| **TC-008** | Checkout | Negative: Proceed without required information | 1. Navigate to Checkout page.<br>2. Leave First Name, Last Name, and Zip Code blank.<br>3. Click 'Continue'. | Progression blocked. Error message displayed indicating missing required fields. | High |
| **TC-009** | Checkout | Happy Path: Complete checkout process successfully | 1. Navigate to Checkout page.<br>2. Enter valid First Name, Last Name, Zip.<br>3. Click 'Continue'.<br>4. On Overview page, click 'Finish'. | User is redirected to 'Checkout: Complete!' page. Success message is displayed. | High |
| **TC-010** | Checkout | Functional: Cancel checkout process | 1. Navigate to 'Checkout: Overview' page.<br>2. Click the 'Cancel' button. | User is redirected back to the Inventory page. Cart contents remain intact. | Medium |

## Defect Report

### BUG-001: Missing Field Validation in Checkout
* **Summary:** The checkout information form allows progression when the 'First Name' field contains only whitespace characters.
* **Severity:** Medium
* **Steps to Reproduce:**
  1. Login and add an item to the cart.
  2. Navigate to Cart and click 'Checkout'.
  3. Enter whitespace (spacebar) in the 'First Name' field.
  4. Enter valid data for 'Last Name' and 'Zip/Postal Code'.
  5. Click 'Continue'.
* **Expected Result:** The system should trim whitespace, recognize the field as practically empty, and display a validation error blocking progression.
* **Actual Result:** The system accepts the whitespace as a valid string and proceeds to the Checkout Overview page.

### BUG-002: Sorting Functionality - Price (High to Low) Incorrect
* **Summary:** Selecting the 'Price (high to low)' sorting option does not arrange the products in descending price order.
* **Severity:** High
* **Steps to Reproduce:**
  1. Login with valid credentials (`standard_user`).
  2. On the Inventory page, locate the sorting dropdown menu.
  3. Select the option 'Price (high to low)'.
  4. Observe the order of the product prices displayed.
* **Expected Result:** Products should be immediately re-rendered, displaying the most expensive item first, descending to the least expensive.
* **Actual Result:** The product list order remains unchanged or sorts randomly, failing to reflect the selected descending price order.

### BUG-003: UI Misalignment - Cart Badge Overlap on Mobile View
* **Summary:** When the cart contains more than 9 items (e.g., displaying "10"), the red cart notification badge text overflows its container on screens smaller than 400px width.
* **Severity:** Low (Cosmetic)
* **Steps to Reproduce:**
  1. Open Chrome DevTools and set the device view to 'iPhone SE' (or width < 400px).
  2. Login to the application.
  3. Add 10 or more items to the shopping cart.
  4. Observe the shopping cart icon in the top right corner.
* **Expected Result:** The red badge should dynamically resize to elegantly contain double-digit numbers without text overflow.
* **Actual Result:** The numbers spill outside the red circular badge, causing a visually unappealing UI overlap.

## Test Summary Report

**Execution Cycle:** 1 (Initial Release Validation)
**Environment:** Chrome 120 / Windows 11

| Metric | Count | Percentage |
| :--- | :--- | :--- |
| **Total Test Cases Planned** | 10 | 100% |
| **Total Test Cases Executed** | 10 | 100% |
| **Total Passed** | 8 | 80% |
| **Total Failed** | 2 | 20% |
| **Blocked/Not Run** | 0 | 0% |

**Executive Summary:**
The core functional paths (Login, Add to Cart, Checkout) are generally stable. However, validation issues in the checkout flow and critical sorting logic failures (as documented in the Defect Report) require development attention before a production release. The overall pass rate stands at 80%, indicating a solid foundation but necessitating a bug-fix cycle and subsequent regression testing.
