# 👥 User & Admin Role Functionalities

This document details the exact capabilities, permissions, features, and workflows available to each role in the **MERN Stack E-Commerce Platform**.

---

## 📊 1. Roles & Permissions Comparison Matrix

| Feature / Action | Guest (Unauthenticated) | Customer (Authenticated) | Administrator (Admin) |
| :--- | :---: | :---: | :---: |
| **Browse Product Catalog** | ✅ | ✅ | ✅ |
| **Search, Filter & Sort Products** | ✅ | ✅ | ✅ |
| **View Product Details** | ✅ | ✅ | ✅ |
| **Add / Remove Items in Cart** | ✅ | ✅ | ✅ |
| **User Account Registration & Login** | ✅ | ❌ *(Already Logged In)* | ❌ *(Already Logged In)* |
| **View Personal Profile** | ❌ | ✅ | ✅ |
| **Proceed through Checkout** | ❌ *(Redirects to Login)* | ✅ | ✅ |
| **Place Orders** | ❌ | ✅ | ✅ |
| **View Personal Order History** | ❌ | ✅ | ✅ |
| **Manage Store Products (Create/Edit/Delete)** | ❌ | ❌ | ✅ |
| **Manage All User Accounts & Roles** | ❌ | ❌ | ✅ |
| **View & Fulfill System Orders** | ❌ | ❌ | ✅ |

---

## 👤 2. Guest User (Unauthenticated)

A **Guest User** accesses the platform without logging in. Guests are primarily restricted to discovery and browsing functions.

### 🌟 Key Capabilities & Features:
1. **Catalog Exploration**:
   - View the paginated home page product grid with high-resolution images, titles, star ratings, and prices.
2. **Search & Discovery**:
   - Search products by title or description keywords.
   - Filter products by **Category** (e.g., Electronics, Wearables, Audio, Footwear).
   - Adjust price range filters using min/max inputs or price sliders.
   - Filter products by minimum star rating.
   - Sort products by price (Low to High / High to Low), highest rating, or newest items.
3. **Product Information**:
   - Open individual product detail pages to inspect descriptions, stock status, ratings, and image previews.
4. **Local Shopping Cart**:
   - Add items to the cart and adjust item quantities up to available inventory limits (`countInStock`).
   - Remove items from the cart.
5. **Account Access**:
   - Access the Login and Registration forms to create an account or sign in.

---

## 🛍️ 3. Registered Customer (Authenticated User)

A **Registered Customer** is a logged-in user with standard access. Customers enjoy a complete online shopping experience.

### 🌟 Key Capabilities & Features (Includes all Guest capabilities plus):
1. **Session & Profile Management**:
   - Secure stateless authentication using JSON Web Tokens (JWT).
   - Persistent login state synchronized with Redux and `localStorage`.
   - Access user profile details and logout button via the user menu.
2. **Checkout & Payment Workflow**:
   - Transition seamlessly from the shopping cart into the step-by-step Checkout process.
   - Input and save shipping address details (Address, City, Postal Code, Country).
   - Select payment method (Cash on Delivery, PayPal, Credit Card).
   - Dynamic real-time calculation of items subtotal, tax rate (15%), shipping fees, and grand total.
   - Submit order placement directly into the database.
3. **Order History & Tracking**:
   - View personal order history list (`/orders`) showing order IDs, order placement dates, total amounts, payment status, and delivery status.
   - View itemized breakdown of past orders (`/order/:id`) including delivery address, items ordered, and fulfillment states.

---

## 🛡️ 4. Administrator (Admin Role)

An **Administrator** is a privileged user whose account has `isAdmin: true`. Admins have complete control over store inventory, customer accounts, and order fulfillment.

### 🌟 Key Capabilities & Features (Includes all Customer capabilities plus):

### 👑 4.1 Admin Navigation Menu
- Access to an exclusive **Admin** dropdown menu in the top navigation bar with quick links to:
  - 📦 **Manage Products** (`/admin/productlist`)
  - 🛒 **Manage Orders** (`/admin/orderlist`)
  - 👥 **Manage Users** (`/admin/userlist`)

### 📦 4.2 Product Catalog Administration (`ProductListPage.jsx`)
- **View Product Inventory Table**: Comprehensive table displaying item thumbnail, name, category, brand, price, and exact stock count.
- **Create New Product**: One-click creation of new product entries (`POST /api/products`) pre-populated with customizable defaults.
- **Delete Product**: Instantly remove outdated or discontinued products from the store catalog (`DELETE /api/products/:id`).
- **Inventory & Stock Management**: Monitor real-time stock levels with color-coded inventory badges (Green for in-stock, Red for out-of-stock).

### 🛒 4.3 System Order Fulfillment (`OrderListPage.jsx`)
- **System-wide Order Tracking**: View all orders placed across the platform by all customers (`GET /api/orders`).
- **Inspect Order Details**: Access full buyer details, delivery addresses, and itemized receipts (`GET /api/orders/:id`).
- **Update Fulfillment Status**: Mark pending orders as **Delivered** (`PUT /api/orders/:id/deliver`), which updates delivery status badges and records exact timestamp (`deliveredAt`).

### 👥 4.4 User & Role Management (`UserListPage.jsx`)
- **User Roster Overview**: View list of all registered platform users (`GET /api/users`), including User IDs, full names, emails, and role badges.
- **Role Promotion & Demotion**: Toggle user roles between standard Customer and Administrator (`PUT /api/users/:id`).
- **Account Deletion**: Delete user accounts from the database (`DELETE /api/users/:id`), with built-in safety protection preventing admins from accidentally deleting their own active session.

---

## 🔒 5. Security & Access Control Enforcement

- **Backend Route Guarding**: Administrative endpoints are protected by both `protect` (token verification) and `admin` (role verification) Express middlewares.
- **Frontend Route Guarding**: Admin pages under `/admin/*` are wrapped by [`AdminRoute.jsx`](file:///d:/Resume%20Projects/Ecommerce-project-MERN-STACK/frontend/src/components/AdminRoute.jsx). Non-admin users attempting direct URL access are automatically redirected to `/login`.
