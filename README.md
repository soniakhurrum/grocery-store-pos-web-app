# Grocery Store Point of Sale (POS) Web Application
**Name:** Sonia Khurrum  
**Document:** UI Design Specification Document (Web Application)

---

## 1. Introduction

### 1.1 Purpose
This UI Design Specification Document provides a detailed and comprehensive description of every screen, interface component, and user interaction within the Grocery Store Point of Sale (POS) Web Application. The document serves as the definitive reference for developers, testers, and evaluators to understand the visual structure and behavioral logic of the application's user interface.

It covers all screens accessible to both user roles: Admin and Cashier along with navigation flow, component inventory, interaction rules, and visual design standards. This document directly complements the project proposal submitted.

### 1.2 Scope
The Grocery Store POS System is a web-based application built using a modern web technology stack (e.g., React.js frontend, Node.js/Java Spring Boot backend, and MySQL database). The UI Design Specification covers the following:
* All 10 application screens across both Admin and Cashier roles 
* All UI components (inputs, buttons, tables, cards, modals, menus) 
* Full interaction behaviors including validation, role-based access, error handling, and state changes 
* Navigation flow between all screens 
* Visual design standards including color palette, typography, and dark mode support 

### 1.3 Audience
This document is intended for:
* **Development Team** – to implement the UI consistently using web technologies 
* **Testers** – to verify interface behavior against specifications 

### 1.4 Design Tools
The wireframes and interface diagrams referenced in this document are to be created using:
* **Figma** – for high-fidelity web wireframes 
* **Draw.io / diagrams.net** – for navigation flow diagrams 
* **Browser DevTools / React UI Builder** – for implementation testing 

### 1.5 Technology Context
The entire user interface is implemented as a Single Page Application (SPA) using web technologies.
* **Frontend:** React.js (or similar component-based framework) 
* **Backend:** Node.js / Express or Spring Boot REST API 
* **Database:** MySQL 
* **Communication:** REST APIs (JSON-based) 

All screens are rendered within a single web application shell using routing (React Router or equivalent) instead of JFrame/CardLayout.

---

## 2. UI Design Principles and Style Guide

### 2.1 Design Philosophy
The Grocery Store POS Web Application is designed for operational efficiency in a browser-based environment. Cashiers must process transactions quickly, and Admins require clear dashboards and data visibility.

**Core principles:**
* **Clarity** – Each page has a single purpose 
* **Efficiency** – Frequent actions accessible in one or two clicks 
* **Consistency** – Shared layout (header, sidebar, spacing system) 
* **Error Prevention** – Real-time validation + confirmation modals 
* **Accessibility** – Responsive design, readable fonts, proper contrast 

### 2.2 Color Palette
The application uses a consistent color scheme implemented through CSS variables.

| Theme State | UI Element | Color Name | Hex Code |
| :--- | :--- | :--- | :--- |
| **Light Mode** | Headers, Sidebar, Primary Buttons | Blue | `#1F4E79` |
| | Success Messages | Green | `#4CAF50` |
| | Low Stock Alerts | Amber | `#FFC107` |
| | Errors & Delete Actions | Red | `#D32F2F` |
| | Main App Background | Light Gray | `#F5F7FA` |
| | Primary Typography | Dark Gray | `#212121` |
| **Dark Mode** | Main App Background | Dark UI | `#1E1E1E` |
| | Primary Typography | Light Text | `#F5F5F5` |

### 2.3 Typography
* **Primary font:** Inter / Roboto / Segoe UI 
* **Base font size:** 14px 
* **Minimum size:** 12px for labels 
* **Headings:** Bold, hierarchical scale (H1–H4) 

### 2.4 Button Standards
* **Primary actions:** Solid blue (`#1F4E79`) 
* **Danger actions:** Red (`#D32F2F`) 
* **Secondary actions:** Outline buttons 
* *Note: All buttons should feature hover effects with smooth CSS transitions.*

### 2.5 Layout Standards
* **Top Header Bar:** Fixed, full width (Left: App name/logo | Right: Username, role badge, logout)
* **Sidebar Navigation (Admin only):** Fixed left panel (240px width) 
* **Content Area:** Responsive main container (flex/grid layout) 
* **Forms:** Two-column responsive layout (stacks on mobile screens) 
* **Tables:** Full-width with striped rows 
* **Modals:** Centered overlay dialogs (max-width 600px) 

---

## 3. Screen Inventory and Navigation Flow

### 3.1 Complete Screen List
The application includes the following 10 core screens:
1. **SCR-01:** Login Screen
2. **SCR-02:** Admin Dashboard
3. **SCR-03:** Product Management Screen
4. **SCR-04:** Inventory Management Screen
5. **SCR-05:** Customer Management Screen
6. **SCR-06:** Sales Reports Screen
7. **SCR-07:** Billing / POS Screen
8. **SCR-08:** Receipt Generation Screen
9. **SCR-09:** Discount Coupon Dialog
10. **SCR-10:** Low Stock Alert Panel

### 3.2 Navigation Flow Diagram
The diagram below illustrates how all screens connect based on user role and actions.

> <img width="432" height="245" alt="image" src="https://github.com/user-attachments/assets/55091be3-6c66-4f49-8c96-6cf28f4a508b" />


---

## 4. Detailed Screen Specifications

### 4.1 SCR-01: Login Screen
* **Purpose:** Authenticate user and redirect based on role.

#### 4.1.1 Interface Layout (Web Version)
The login screen is a centered login card inside a responsive web page.
* Full-screen background gradient 
* Centered login container (card UI) 
* Logo + title at top 
* Username + password inputs 
* "Remember Me" checkbox 
* Login button 
* Error message space below button 

**Responsive behavior:**
* **Mobile:** Full-width card 
* **Desktop:** Fixed 450px card
<img width="228" height="372" alt="image" src="https://github.com/user-attachments/assets/921d5ca8-388e-4972-acda-e4422725a2f4" />

#### 4.1.2 Components
Implemented cleanly as React controlled inputs (`LGN-01` through `LGN-08`).

#### 4.1.3 Interactive Behaviors
* **On application launch:** Focus is automatically placed on the Username Field (`LGN-03`).
* **Keypress Event:** Pressing `Enter` in either field triggers the Login action (same as clicking the Login Button).
* **Validation:** Login Button click (`LGN-07`) validates both fields are non-empty. If either is empty, `LGN-08` shows *"Username and Password cannot be empty."* in red text.
* **Authentication Workflow:** If fields are filled, the system queries the backend REST API. The password is compared securely using hashed values (`SHA-256` or `BCrypt`).
  * **Success — Admin:** Login screen closes; Admin Dashboard (`SCR-02`) opens in full screen.
  * **Success — Cashier:** Login screen closes; Billing/POS Screen (`SCR-07`) opens in full screen.
  * **Failure:** `LGN-08` displays *"Invalid username or password. Please try again."* Login button re-enables, password field is cleared, and cursor returns to the username field.
* **Security Rate Limiting:** After 5 consecutive failed attempts, the login button is disabled for 30 seconds. `LGN-08` shows *"Too many failed attempts. Please wait 30 seconds."*
* **Remember Me (`LGN-06`):** If checked and login succeeds, the username is cached securely in the browser. On the next launch, `LGN-03` is pre-filled.

---

### 4.2 SCR-02: Admin Dashboard
* **Screen ID:** SCR-02
* **Accessible By:** Admin only
* **Triggered By:** Successful login with Admin role
* **Purpose:** Provide a high-level operational overview including today's sales summary, inventory alerts, and quick navigation to all admin modules.

#### 4.2.1 Interface Layout
The Admin Dashboard uses a three-zone master layout:
* **Zone 1 — Top Header Bar** (Full width, 60px height): Contains the system logo/name on the left, and on the right shows the logged-in admin's username, their role badge ('ADMIN'), and a Logout button.
* **Zone 2 — Left Navigation Sidebar** (200px wide, full height minus header): Contains vertically stacked navigation menu items with icons — Dashboard (active), Products, Inventory, Customers, Reports. The active item is highlighted.
* **Zone 3 — Main Content Area** (Remaining space): Divided into two rows. Row 1 shows four KPI summary cards side by side. Row 2 shows a Recent Transactions table on the left and a Low Stock Alerts panel on the right.
  <img width="432" height="298" alt="image" src="https://github.com/user-attachments/assets/2ea7a635-5776-45db-b686-d9f6da0c86a5" />


#### 4.2.2 Interactive Behaviors
* **On load:** Dashboard fetches today's sales total, product count, low-stock count, and customer count dynamically from the database.
* **KPI Card Actions:** * Clicking *Today's Sales* navigates to Sales Reports Screen (`SCR-06`) filtered to today's date.
  * Clicking *Low Stock Items* navigates to Inventory Management Screen (`SCR-04`) with the low-stock filter active.
* **Nav Menu Items (`ADM-07`):** Clicking any item loads the corresponding screen dynamically into the main content area via client routing.
* **Recent Transactions Table (`ADM-09`):** Double-clicking any row opens a read-only Sale Detail modal showing the full itemized bill for that transaction.
* **Low Stock Alerts panel (`ADM-10`):** Automatically refreshes every 5 minutes. Clicking any item in the list navigates to `SCR-04` with that product pre-selected.
* **Logout Button (`ADM-05`):** Shows a confirmation modal: *"Are you sure you want to logout?"*. Confirming clears the active session tokens and returns to the Login Screen (`SCR-01`).

---

### 4.3 SCR-03: Product Management Screen
* **Screen ID:** SCR-03
* **Accessible By:** Admin only
* **Triggered By:** Clicking 'Products' in the Admin navigation sidebar
* **Purpose:** Allow the admin to view, add, edit, delete, and search all products in the store's inventory catalog.

#### 4.3.1 Interface Layout
* **Header Bar and Sidebar:** Shared across all Admin screens (`Products` active).
* **Content Area Row 1 — Search & Filter Bar:** Spans full content width. Contains a search text field (search by name, ID, or category), a category filter dropdown, a price range filter (min/max fields), a Search button, and a Reset Filters button.
* **Content Area Row 2 — Product Table:** Full-width web data grid listing all products. Columns: *Product ID, Product Name, Category, Price (Rs.), Stock Quantity, Low Stock Threshold, Actions.*
* **Content Area Bottom — Action Toolbar:** Below the table. Contains 'Add New Product' button on the left and 'Export to CSV' on the right.
* **Add/Edit Product Panel:** Opens cleanly as a centered modal dialog.
<img width="432" height="280" alt="image" src="https://github.com/user-attachments/assets/2632c0e1-65fa-497a-ab3f-9adbe87f12a8" />


#### 4.3.2 Component Inventory
* Search Field (`PRD-01`), Category Dropdown (`PRD-02`), Price Range Fields (`PRD-03`, `PRD-04`), Search Button (`PRD-05`), Reset Filters Button (`PRD-06`)
* Product Table Grid (`PRD-07`), Inline Edit Button (`PRD-08`), Inline Delete Button (`PRD-09`)
* Add New Product Button (`PRD-10`), Export to CSV Button (`PRD-11`), Add/Edit Modal Form (`PRD-12`)

#### 4.3.3 Interactive Behaviors
* **Search Execution (`PRD-05`):** Queries database with a filtered matching pattern. Table re-renders with live data. If no results match, the table displays *"No products found."*
* **Reset Filters (`PRD-06`):** Clears all input filter fields and reloads the absolute catalog.
* **Edit Action (`PRD-08`):** Opens the Form Modal pre-populated with data. On Save, inputs are validated (Name is required, price must be a positive decimal, stock bounds must be integers).
* **Delete Action (`PRD-09`):** Triggers a warning modal: *"Delete [Product Name]? This cannot be undone."* If the product contains historical sales records, the action blocks with an alert: *"Cannot delete product with existing sales history. Deactivate instead."*
* **Low Stock Highlight:** If any product's `Stock Quantity` drops below its `Low Stock Threshold`, the corresponding table cell highlights in amber (`#FFC107`).

---

### 4.4 SCR-04: Inventory Management Screen
* **Screen ID:** SCR-04
* **Accessible By:** Admin only
* **Triggered By:** Clicking 'Inventory' in the Admin navigation sidebar
* **Purpose:** Monitor real-time stock levels across all products, adjust stocks manually, and review automatic transaction log adjustments.

#### 4.4.1 Interface Layout & Components
* **View Selector Tabs:** Interactive toggle states to quickly filter between *"All Products"*, *"Low Stock"*, and *"Out of Stock"*.
* **Main Data Grid:** Features columns for *Product ID, Product Name, Category, Current Stock, Threshold, Status Badge, Last Updated, and Action Link.*
* **Audit Trail Panel:** An expandable lower accordion menu listing recent structural deductions (*Sale ID, Product, Quantity Deducted, Date/Time*).
<img width="432" height="281" alt="image" src="https://github.com/user-attachments/assets/f7e77987-a658-4e1b-ac24-0e9c102fb68d" />

#### 4.4.2 Interactive Behaviors
* **Dynamic Views:** Switching tabs dispatches an asynchronous API filter payload (`/api/inventory?status=low_stock`) updating states smoothly without structural browser refreshing.
* **Debounced Search:** The product search input utilizes a `300ms` keystroke debounce layout to mitigate unnecessary performance spikes on backend data endpoints.
* **Stock Adjustments:** Clicking *"Adjust Stock"* pops up a modal form interface. Inputs require absolute numeric schemas prior to issuing a network `PATCH` request.

---

### 4.5 SCR-05: Customer Management Screen
* **Screen ID:** SCR-05
* **Accessible By:** Admin only
* **Triggered By:** Clicking 'Customers' in the Admin navigation sidebar

#### 4.5.1 Interface Layout & Behaviors
* **Top Layout Control:** Features a split container dividing a Customer Search bar (query by name/phone) from an **Add New Customer** workflow trigger button.
* **Data Fields Displayed:** *Customer ID, Name, Phone Number, Email, Total Purchases, Total Spent (Rs.), Registration Date, Action Panel.*
* **Interactive Validation Elements:** Phone numbers require strict 11-digit parameters matching Pakistani communication layouts. Emails validate against clean standard RegEx expressions.
* **Cascading Delete Handling:** If an admin selects to delete a customer profile holding an active ledger history, a system override intercepts: *"This customer has purchase history. Deleting will unlink their records from sales. Proceed?"*
<img width="379" height="264" alt="image" src="https://github.com/user-attachments/assets/fdf3a7a0-971b-4672-8080-a80b85e61f4d" />

---

### 4.6 SCR-06: Sales Reports Screen
* **Screen ID:** SCR-06
* **Accessible By:** Admin only
* **Purpose:** Provide operational metrics, dynamic date-ranged analytics charts, monthly margins, and bulk file downloads.

#### 4.6.1 Layout Configuration tabs
* **Daily Reports:** Native HTML5 Date Pickers linked to an analytics query processing engine. Displays summary metrics (Total Income, Transaction counts, Volume metrics).
* **Monthly Matrix:** Grouped parameters matching drop-down choices for simple year/month breakdowns.
* **Product Standings:** Ranks high-performing items during configurable time intervals showing categorical performance, volumetric sales, and calculated revenues.
* **Export Action Elements:** Fast access footer links parsing visual application screens into readable download structures (`Export to PDF` / `Export to CSV`).
* <img width="421" height="465" alt="image" src="https://github.com/user-attachments/assets/ea8c9ffb-f39b-4046-9f34-dd552c22b93e" />


---

### 4.7 SCR-07: Billing / POS Screen
* **Screen ID:** SCR-07
* **Accessible By:** Cashier only
* **Triggered By:** Successful login with Cashier role
* **Purpose:** Primary cashier workspace. Speed-optimized layout to search products, process shopping carts, handle coupons, compute taxes, and process checkout operations.

#### 4.7.1 Layout Architecture
Uses an optimized responsive split-pane screen structure:
* **Left Panel (55% Width) — Search & Scan Zone:** Features rapid focus barcode inputs and contextual category dropdown lookups driving a catalog grid. Double-clicking any item passes it into the active invoice.
* **Right Panel (45% Width) — Checkout Transaction Matrix:** High-visibility itemized data layout showing running balances, real-time discount parameters, configurable multi-tier tax percentages, coupon adjustments, and net calculations.
<img width="432" height="315" alt="image" src="https://github.com/user-attachments/assets/a92f86d3-8ae3-4be4-8c8a-2c5bf9931de3" />


#### 4.7.2 Operational Workflows & Hotkeys
* **Automated Scanner Handlers:** The screen boots prioritizing active focus on the Barcode field (`BIL-01`). Scanning exact numeric code strings automatically triggers cart calculations without secondary interface steps.
* **Stock Intercepts:** If an employee attempts to populate an item possessing zero quantities, a warning tooltip prevents checkout progression declaring an *"Out of stock"* state.
* **Payment Finalization Requirements:** The central Checkout trigger button (`BIL-14`) remains absolute disabled until the fields verifying `Cash Received` evaluate greater than or equal to the total calculation parameters.
* **Transaction Completion Actions:** Finalizing checkout dispatches payload arrays writing to backend logs, recalibrating current inventory values, updating customer reward parameters, and automatically routing the app state to the receipt rendering component.

---

### 4.8 SCR-08: Receipt Generation Screen
* **Screen ID:** SCR-08
* **Accessible By:** Cashier (auto-triggered post-checkout)

#### 4.8.1 Layout & Printing Directives
* Center-aligned layout modeling structural thermal paper configurations. Contains all metadata: store location, clerk identities, itemized lists, pricing schemas, and custom footer texts.
* **Web Printing Automation:** Upon successful initialization, the application invokes native user agent pipelines by issuing a standard `window.print()` programmatic hook. This triggers custom print-media CSS layouts formatting the transaction cleanly to standard POS thermal receipt printers.
<img width="280" height="523" alt="image" src="https://github.com/user-attachments/assets/344d3756-71f3-479b-a3bf-0086b6b1e93e" />


---

### 4.9 SCR-09: Discount Coupon Dialog
* **Screen ID:** SCR-09
* **Accessible By:** Cashier
* **Purpose:** Small modal popup contextually managing coupon checks. Checks rules for date eligibility bounds, active binary states, and total usage restrictions prior to adjusting invoice parameters.
<img width="270" height="266" alt="image" src="https://github.com/user-attachments/assets/946c27aa-5c7a-4519-939a-5ec088884713" />

---

### 4.10 SCR-10: Low Stock Alert Panel
* **Screen ID:** SCR-10
* **Accessible By:** Admin only

#### 4.10.1 Presentation States
1. **Dashboard Widget:** A running container inside screen `SCR-02` parsing entries with distinct text decorations highlighting deficient stocks.
2. **Real-time Popups:** Transient floating toast cards popping up in the bottom-right corner when an operational cashier checkout forces an item under safety margins. Cards dismiss automatically after an `8-second` layout cycle.
<img width="432" height="281" alt="image" src="https://github.com/user-attachments/assets/2022a37c-b59d-4fd2-a484-d104bbc4b061" />


---

## 5. Accessibility and Error Handling Standards

### 5.1 General Error Handling Patterns
* **Database Interventions:** If backend communication states fail, the UI restricts normal interface navigation paths by overlaying a persistent blocker reading: *"Cannot connect to database. Please check MySQL server is running and config.properties settings are correct."*
* **Empty States:** Empty arrays across data tables automatically render clean typographic substitutions reading *"No records found."* instead of dropping raw structural spaces.

### 5.2 Dark Mode Architecture
The application layout provides toggles activating alternative stylesheets across components. Selected user choices are set inside the browser's persistent `localStorage` cache engine, preventing jarring white screen transitions during application boot lifecycles.

---

## 6. Summary: Wireframes Required
The following is a complete reference list of all wireframe/mockup images that must be inserted into this document at the marked placeholders:
* [ ] **FIG-01:** Login Screen High-Fidelity Mockup
* [ ] **FIG-02:** Admin Dashboard Layout Specification
* [ ] **FIG-03:** Product Management Form Modal
* [ ] **FIG-04:** POS Split-Pane Interface Blueprint

---

## 7. Conclusion
This UI Design Specification Document provides a complete blueprint for the user interface of the Grocery Store POS Web Application. Every screen has been specified with its layout structure, full web component inventory, and comprehensive interaction behaviors covering all user actions, validation rules, error states, and asynchronous system responses.

Upon completion of the high-fidelity Figma web wireframes at the marked placeholders, this document will serve as the definitive guide for the frontend development team to implement the React.js single-page web interface consistently and correctly.
