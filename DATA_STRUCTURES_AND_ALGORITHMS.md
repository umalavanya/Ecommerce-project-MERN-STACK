# 🧮 Data Structures & Algorithms (DSA) Analysis

This document provides a comprehensive breakdown of all **Data Structures** and **Algorithms** utilized throughout the frontend (React/Redux) and backend (Node.js/Express/MongoDB) of the **MERN Stack E-Commerce Platform**.

---

## 📦 1. Data Structures Used

### 1.1 Hash Maps / Hash Tables / Key-Value Objects
- **Where Used**:
  - **Redux State Slices** (`authSlice`, `productSlice`, `cartSlice`, `orderSlice`).
  - **Express Route Parameters & Query Objects** (`req.params`, `req.query`, `req.body`).
  - **JWT Tokens** (JSON payload storing user ID and claims).
  - **Environment Variables** (`.env` key-value mappings).
- **Time Complexity**:
  - **Access / Lookup**: $O(1)$ average time.
  - **Insertion / Deletion**: $O(1)$ average time.

---

### 1.2 Arrays / Dynamic Lists
- **Where Used**:
  - **Shopping Cart Items (`cartItems`)**: Stores selected products, quantities, and item prices.
  - **Product Catalog Grid (`products`)**: Stores fetched product objects for grid rendering.
  - **Order Items List (`orderItems`)**: Array of item snapshots stored inside each Order document.
  - **User Orders List (`orders`)**: Array of past orders returned from database queries.
- **Operations & Complexity**:
  - **Insertion**: $O(1)$ amortized (`push` / `unshift`).
  - **Traversal / Rendering**: $O(N)$ linear pass.
  - **Deletion / Filtering**: $O(N)$ linear scan (`filter` / `splice`).

---

### 1.3 Set Data Structure (Unique Collections)
- **Where Used**:
  - Extracting unique category lists for frontend filter dropdowns:
    - Backend: `Product.distinct('category')`
    - Frontend fallback: `Array.from(new Set(products.map(p => p.category)))`
- **Properties**:
  - Eliminates duplicate category strings in $O(N)$ time complexity.

---

### 1.4 B-Trees & B+ Trees
- **Where Used**:
  - **MongoDB Primary & Secondary Indexes**: MongoDB utilizes B-Trees / B+ Trees under the hood to index `_id` ObjectIDs and unique constraints (`email`).
- **Time Complexity**:
  - **Search / Insert / Delete**: $O(\log N)$.

---

### 1.5 Strings & Serialized Buffers
- **Where Used**:
  - **Password Hashes**: 60-character `bcrypt` Blowfish hash strings.
  - **JWT Security Tokens**: Signed Base64URL encoded strings (`Header.Payload.Signature`).
  - **LocalStorage Cache**: Serialized JSON strings (`JSON.stringify()` / `JSON.parse()`).

---

### 1.6 Stack Data Structure (LIFO)
- **Where Used**:
  - **Browser / React Router Navigation History**: Managed via `useNavigate()` stack.
  - **JavaScript Execution Call Stack**: Manages synchronous function calls and execution contexts.

---

### 1.7 Queue Data Structure (FIFO)
- **Where Used**:
  - **Node.js Event Loop Queues**: Microtask and Macrotask queues managing asynchronous HTTP I/O requests, database queries, and timer callbacks without blocking the main event thread.

---

## ⚙️ 2. Algorithms & Algorithmic Patterns Used

### 🔒 2.1 Cryptographic & Hashing Algorithms

#### A. Blowfish / bcrypt Password Hashing Algorithm
- **Usage**: Encrypting user passwords in `User.js` pre-save hook (`bcrypt.hash(password, salt)`).
- **Mechanism**: Generates a 128-bit salt and applies iterative Blowfish block cipher hashing (key expansion factor of 10) to prevent rainbow table and brute-force attacks.

#### B. HMAC-SHA256 Digital Signature Algorithm
- **Usage**: Signing and verifying JSON Web Tokens in `generateToken.js` and `authMiddleware.js`.
- **Mechanism**: Combines Base64URL encoded header and payload with secret key `JWT_SECRET` via SHA-256 hash function.

---

### 🔍 2.2 Search Algorithms

#### A. MongoDB Regex Pattern Matching Algorithm (`$regex`)
- **Usage**: Case-insensitive keyword search in `productController.js` (`getProducts`).
- **Complexity**: $O(N)$ text scanning / index search across `name`, `brand`, and `description` fields.

#### B. Linear Search Algorithm (`Array.prototype.find` / `findIndex`)
- **Usage**: Locating matching items in Redux cart state to update existing quantities rather than appending duplicate rows.
- **Complexity**: $O(N)$ worst-case comparison time.

---

### 📊 2.3 Sorting Algorithms

#### A. Multi-Criteria Sort Algorithm
- **Usage**: Sorting catalog products by price (ascending/descending), rating, or creation date (`createdAt: -1`).
- **Implementation**:
  - Backend: MongoDB B-Tree / QuickSort / MergeSort implementation.
  - Frontend fallback: V8 Engine **Timsort** algorithm (`Array.prototype.sort`).
- **Time Complexity**: $O(N \log N)$.

---

### 🧮 2.4 Aggregation & Accumulator Pattern (MapReduce / Filter-Reduce)

#### A. Accumulator / Reduction Algorithm (`Array.prototype.reduce`)
- **Usage**: Calculating real-time shopping cart metrics in `cartSlice.js` and `CartPage.jsx`:
```javascript
// Cart item count calculation
const totalCartCount = cartItems.reduce((acc, item) => acc + item.qty, 0);

// Items subtotal price calculation
const itemsPrice = cartItems.reduce((acc, item) => acc + (item.price * item.qty), 0);
```
- **Time Complexity**: $O(N)$ single-pass linear traversal.

---

### 📄 2.5 Offset Pagination Algorithm

- **Usage**: Paginating large product datasets in `productController.js`:
```javascript
const pageSize = 8;
const page = Number(req.query.pageNumber) || 1;

const skip = pageSize * (page - 1);
const totalPages = Math.ceil(count / pageSize);
```
- **Time Complexity**: $O(K)$ where $K$ is offset limit.

---

### 🌲 2.6 Virtual DOM Reconciliation Algorithm (React Fiber)

- **Usage**: React's core rendering engine updates the DOM efficiently by comparing current and previous Virtual DOM trees.
- **Complexity**: Optimized heuristic tree diffing algorithm running in $O(N)$ time.

---

## 📑 3. Summary Table of DSA Application

| Component / Feature | Primary Data Structure | Underlying Algorithm | Time / Space Complexity |
| :--- | :--- | :--- | :--- |
| **Password Auth** | String / Buffer | `bcrypt` (Blowfish Hashing) | $O(2^K)$ compute cost |
| **JWT Verification** | Base64 String | HMAC-SHA256 Hashing | $O(1)$ verification |
| **Product Search** | String / Array | Regex Pattern Matching (`$regex`) | $O(N)$ text scan |
| **Catalog Sorting** | Array | Timsort / QuickSort / MergeSort | $O(N \log N)$ |
| **Cart Price Totals** | Dynamic Array | Accumulator Pattern (`reduce`) | $O(N)$ time, $O(1)$ space |
| **Catalog Pagination** | Integer / Array | Offset Pagination Algorithm | $O(1)$ page math |
| **Unique Categories** | Set Data Structure | Hash Set Deduplication | $O(N)$ time, $O(N)$ space |
| **Database Indexing** | B-Tree / B+ Tree | Binary Tree Range Search | $O(\log N)$ search |
