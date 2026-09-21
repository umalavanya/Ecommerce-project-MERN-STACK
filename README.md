# 🛒 MERN Stack E-Commerce Platform

A feature-rich, full-stack E-Commerce application built using the **MERN** stack (**MongoDB, Express.js, React, Node.js**) with Redux Toolkit for state management, JWT authentication, and a modern responsive user interface.

---

## 🌟 Key Features

### 👤 User Authentication & Management
- **Registration & Login**: Secure authentication powered by JSON Web Tokens (JWT) and `bcryptjs` password hashing.
- **Persistent Sessions**: User state & authentication token persisted in `localStorage` and synchronized via Redux state.
- **Profile Management**: View logged-in user credentials and personal account details.

### 🛍️ Product Browsing & Filtering
- **Dynamic Catalog**: Paginated grid view of available products with real-time stock statuses and star ratings.
- **Advanced Search & Filtering**:
  - Search by keyword/product title.
  - Filter by category (Electronics, Clothing, Accessories, etc.).
  - Filter by price range slider.
  - Filter by minimum rating.
  - Sort by price (low to high, high to low), rating, or newest additions.
- **Detailed Product Page**: Full product description, high-resolution preview images, stock status indicator, rating breakdown, and quantity selector.

### 🛒 Shopping Cart & Checkout Workflow
- **Interactive Cart**: Add/remove items, adjust quantities, and calculate subtotal, tax, and shipping costs dynamically.
- **Checkout Process**: Step-by-step checkout workflow including shipping address selection and payment method setup (Cash on Delivery, PayPal, Credit Card).
- **Order Placement**: Real-time order calculation and order creation saved directly to MongoDB.

### 📦 Order Tracking & History
- **Order History**: View past orders placed by the authenticated user with order status, dates, and total amounts.
- **Order Details**: Comprehensive breakdown of itemized prices, delivery address, payment status, and shipping updates.

### 🛠️ Developer & CLI Tools
- **Data Seeder Utility**: Command-line script to populate MongoDB database with mock product data and test user accounts or destroy existing datasets easily.

---

## 🏗️ Tech Stack

### **Frontend**
- **Library**: [React 18](https://react.dev/)
- **Build Tool**: [Vite](https://vitejs.dev/)
- **State Management**: [Redux Toolkit](https://redux-toolkit.js.org/) & `react-redux`
- **Routing**: [React Router v6](https://reactrouter.com/)
- **HTTP Client**: [Axios](https://axios-http.com/)
- **Icons**: [Lucide React](https://lucide.dev/)
- **Styling**: Vanilla CSS (Custom Design System with Glassmorphism & Responsive Grids)

### **Backend**
- **Runtime**: [Node.js](https://nodejs.org/)
- **Framework**: [Express.js](https://expressjs.com/)
- **Database**: [MongoDB](https://www.mongodb.com/) via [Mongoose ORM](https://mongoosejs.com/)
- **Security & Auth**: `jsonwebtoken` (JWT), `bcryptjs`, `cors`
- **Configuration**: `dotenv`

---

## 📁 Folder Structure

```
Ecommerce-project-MERN-STACK/
├── backend/
│   ├── config/             # Database connection setup (db.js)
│   ├── controllers/        # Route controllers (auth, product, order logic)
│   ├── middleware/         # Auth verification & error handling middlewares
│   ├── models/             # Mongoose Schemas (User, Product, Order)
│   ├── routes/             # Express API route endpoints
│   ├── utils/              # Helper utilities (generateToken.js)
│   ├── .env.example        # Environment variable blueprint
│   ├── seeder.js           # Database seeder script
│   └── server.js           # Express app entry point
│
├── frontend/
│   ├── src/
│   │   ├── components/     # Reusable UI components (Navbar, Footer, ProductCard, Filters, etc.)
│   │   ├── pages/          # Application views (HomePage, ProductDetailPage, CartPage, CheckoutPage, etc.)
│   │   ├── redux/          # Redux Store & Slices (authSlice, productSlice, cartSlice, orderSlice)
│   │   ├── index.css       # Global design system & component styling
│   │   ├── App.jsx         # Main router layout & container component
│   │   └── main.jsx        # App entry point with Redux Provider
│   ├── vite.config.js      # Vite dev configuration & API proxy setup
│   └── package.json
│
└── README.md
```

---

## 🔌 API Endpoints Summary

### **Authentication & User Admin Routes** (`/api/users`)
| Method | Endpoint | Access | Description |
| :--- | :--- | :--- | :--- |
| `POST` | `/api/users/register` | Public | Register a new user |
| `POST` | `/api/users/login` | Public | Authenticate user & get JWT token |
| `GET` | `/api/users/profile` | Protected | Get authenticated user profile |
| `GET` | `/api/users` | Admin | Fetch all registered users |
| `DELETE` | `/api/users/:id` | Admin | Delete a user account |
| `GET` | `/api/users/:id` | Admin | Fetch user details by ID |
| `PUT` | `/api/users/:id` | Admin | Update user details & toggle Admin role |

### **Product Routes** (`/api/products`)
| Method | Endpoint | Access | Description |
| :--- | :--- | :--- | :--- |
| `GET` | `/api/products` | Public | Fetch all products (supports query filters & pagination) |
| `GET` | `/api/products/:id` | Public | Fetch single product by ID |
| `POST` | `/api/products` | Admin | Create a new sample product |
| `PUT` | `/api/products/:id` | Admin | Update product details, price, & stock |
| `DELETE` | `/api/products/:id` | Admin | Remove product from store |

### **Order Routes** (`/api/orders`)
| Method | Endpoint | Access | Description |
| :--- | :--- | :--- | :--- |
| `POST` | `/api/orders` | Protected | Create a new order |
| `GET` | `/api/orders/myorders` | Protected | Fetch logged-in user's order history |
| `GET` | `/api/orders/:id` | Protected | Fetch order details by Order ID |
| `GET` | `/api/orders` | Admin | Fetch all platform customer orders |
| `PUT` | `/api/orders/:id/deliver` | Admin | Mark order fulfillment status as delivered |

---

## ⚙️ Environment Variables

Create a `.env` file inside the `backend` directory based on `.env.example`:

```env
PORT=5000
NODE_ENV=development
MONGO_URI=mongodb://127.0.0.1:27017/ecommerce_db
JWT_SECRET=supersecretjwtkey123456_ecommerce_app
```

---

## 🚀 Getting Started & Local Setup

### **Prerequisites**
- [Node.js](https://nodejs.org/) (v16.x or later)
- [MongoDB](https://www.mongodb.com/) (Local installation or MongoDB Atlas URI)

---

### **1. Clone the Repository**
```bash
git clone https://github.com/your-username/Ecommerce-project-MERN-STACK.git
cd Ecommerce-project-MERN-STACK
```

---

### **2. Backend Setup**
```bash
# Navigate to backend directory
cd backend

# Install dependencies
npm install

# Create environment config
cp .env.example .env

# (Optional) Seed the database with sample products and admin/user accounts
npm run data:import

# Start backend dev server with nodemon
npm run dev
```
The backend API server will run on `http://localhost:5000`.

---

### **3. Data Seeder Commands**
From the `backend` folder:
- **Import Sample Data**: `npm run data:import`
- **Destroy/Clear Data**: `npm run data:destroy`

---

### **4. Frontend Setup**
Open a new terminal window:
```bash
# Navigate to frontend directory
cd frontend

# Install dependencies
npm install

# Start Vite development server
npm run dev
```
The frontend app will launch at `http://localhost:5173`.

---

## 🧪 Testing the Application

1. **User Sign Up / Sign In**: Register a new account or use seeded demo user credentials.
2. **Product Filtering**: Navigate to the home page, search for products, adjust category and price filters.
3. **Shopping & Checkout**:
   - Add items to your cart.
   - Proceed to Checkout.
   - Enter shipping address and choose payment options.
   - Complete order placement.
4. **Order History**: Click on your user profile or orders tab to view order details and tracking status.

---

## 📜 License

This project is licensed under the **ISC License**. Feel free to use and adapt it for educational and portfolio purposes.
