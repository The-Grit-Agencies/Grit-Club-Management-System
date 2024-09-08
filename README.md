

---

# Grit-Club Management System

**Grit-Club Management System** is an all-in-one platform designed to help clubs manage their operations seamlessly. It includes user role management (waiters, managers, and inventory managers), inventory tracking, order logging, and payment processing. The system streamlines club operations, allowing for efficient inventory management, customer order tracking, and real-time monitoring of activities by managers and administrators.

---

## Table of Contents

- [Features](#features)
- [Technologies](#technologies)
- [System Architecture](#system-architecture)
- [Setup and Installation](#setup-and-installation)
- [Usage](#usage)
- [Database Schema](#database-schema)
- [Roles and Access](#roles-and-access)
  - [Admin](#admin)
  - [Manager](#manager)
  - [Inventory Manager](#inventory-manager)
  - [Waiter](#waiter)
- [Order Management Workflow](#order-management-workflow)
- [Inventory Management Workflow](#inventory-management-workflow)
- [REST API Endpoints](#rest-api-endpoints)
- [Future Enhancements](#future-enhancements)
- [Contributing](#contributing)
- [License](#license)

---

## Features

### User and Role Management
- **Admin Panel**: Admins can view the total number of users, categorized by their roles (e.g., waiters, managers, inventory managers).
- **Role-Based Access Control**: Different functionalities are available based on the user's role. Admins have full access, while managers, waiters, and inventory managers have limited access based on their responsibilities.
  
### Inventory Management
- **Item Categorization**: Inventory items can be categorized into club-related categories like beers, wine, gin, water, juice, etc.
- **Bulk Item Addition**: Inventory managers can add multiple items at once, specifying quantities and prices.
- **Real-Time Updates**: Inventory automatically updates when customer orders are placed, preventing overselling.

### Order Tracking and Status Management
- **Waiter Order Logging**: Waiters can log customer orders into the system with specific statuses (unpaid, pending, served, paid) and attach Mpesa payment codes.
- **Manager Monitoring**: Managers can monitor all orders, track order statuses, and know which waiter is responsible for each order.

### Payment Processing
- **Mpesa Integration**: When logging orders, waiters can input Mpesa transaction codes to confirm payments.
- **Order Status**: Orders are updated to reflect payment status (e.g., unpaid, pending, served, paid).

### Reporting and Statistics
- **Admin Dashboard**: Admins can view detailed statistics about club operations, including user roles, inventory levels, orders processed, and financial data.

---

## Technologies

- **Backend**: Flask (Python)
- **Frontend**: HTML, CSS, JavaScript (with Jinja2 for templating)
- **Database**: SQLite (can be configured to use MySQL, PostgreSQL)
- **Payment Gateway**: Mpesa (or similar) integration for processing payments
- **Authentication**: Flask-Login (with role-based access control)
- **API**: RESTful API for interaction with the frontend and external services
- **Other Libraries**: Flask-SQLAlchemy, Flask-Migrate for database management

---

## System Architecture

1. **User Authentication**: Using Flask-Login, users authenticate based on their role (admin, manager, waiter, inventory manager).
2. **Inventory Management**: The inventory is managed through a CRUD system where the inventory manager can add, update, and delete stock items.
3. **Order Management**: Orders are tracked in a centralized database, and status updates occur in real-time, automatically affecting the inventory.
4. **Admin Dashboard**: Admins can access a summary of club operations, including user activity, inventory levels, and order statuses.

---
## Waiter Dashboard

Below is a screenshot of the **Waiter Dashboard** in the Grit-Club system:

![Waiter Dashboard](https://i.postimg.cc/XvwvkPF2/Screenshot-from-2024-09-08-20-03-25.png "Grit-Club Waiter Dashboard")

---

## Manager Dashboard

Here’s the **Manager Dashboard** interface in the Grit-Club system:

![Manager Dashboard](https://i.postimg.cc/1RW3BwnZ/Screenshot-from-2024-09-08-20-05-12.png "Grit-Club Manager Dashboard")

## Setup and Installation

### Prerequisites

- **Python 3.x** installed on your machine
- **Flask** installed via `pip install Flask`
- A virtual environment for Python dependencies is recommended

### Installation Steps

1. Clone the repository:

   ```bash
   git clone grit-club
   cd grit-club
   ```

2. Set up and activate a virtual environment:

   ```bash
   python3 -m venv venv
   source venv/bin/activate
   ```

3. Install required dependencies:

   ```bash
   pip install -r requirements.txt
   ```

4. Initialize the database:

   ```bash
   flask db init
   flask db migrate
   flask db upgrade
   ```

5. Start the Flask server:

   ```bash
   flask run
   ```

6. Access the app at `http://127.0.0.1:5000/`.

---

## Usage

- **Admins**: Manage users and monitor all club activities.
- **Managers**: View waiter activities, track orders, and monitor inventory.
- **Waiters**: Log customer orders and update order statuses.
- **Inventory Managers**: Add, update, and delete stock items, and monitor inventory levels.

---

## Database Schema

### User Table
- `id`: Integer (Primary Key)
- `name`: String
- `email`: String
- `password`: String (hashed)
- `role`: Enum (admin, manager, waiter, inventory_manager)

### Inventory Table
- `id`: Integer (Primary Key)
- `name`: String
- `category`: String (e.g., beer, wine, gin)
- `quantity`: Integer
- `price`: Float
- `added_by`: Foreign Key (references inventory manager)

### Order Table
- `id`: Integer (Primary Key)
- `waiter_id`: Foreign Key (references waiter)
- `status`: Enum (unpaid, pending, served, paid)
- `items`: Text (list of ordered items)
- `total_price`: Float
- `transaction_code`: String (Mpesa transaction code)

---

## Roles and Access

### Admin
- Manage all users and their roles.
- View club-wide statistics and reports.

### Manager
- Manage orders placed by waiters.
- Monitor inventory levels and waiter activities.

### Inventory Manager
- Add, update, or delete inventory items.
- View inventory statistics.

### Waiter
- Log and manage customer orders.
- Update order statuses.

---

## Order Management Workflow

1. **Order Placement**: Waiters log an order in the system, adding items and order status.
2. **Order Status Update**: As orders are processed (e.g., unpaid -> pending -> served -> paid), the status is updated by waiters.
3. **Inventory Update**: When an order is paid, the inventory automatically updates, reducing the quantity of the ordered items.
4. **Manager Review**: Managers can monitor all orders and track which waiter handled each.

---

## Inventory Management Workflow

1. **Add Inventory**: Inventory managers can add new items in bulk with categories, quantities, and prices.
2. **Update Inventory**: Inventory is automatically updated as items are consumed through orders.
3. **View Inventory**: Managers can see a summary of all inventory items, including total quantities and prices.

---

## REST API Endpoints

- **POST** `/login`: User login
- **GET** `/dashboard`: Admin/Manager dashboard
- **POST** `/inventory/add`: Add inventory items
- **POST** `/order/log`: Log a new order
- **GET** `/orders`: Get all orders
- **PATCH** `/order/status`: Update order status

---

## Future Enhancements

- **Analytics Dashboard**: Add a detailed analytics page for admins to view trends, sales, and operational statistics.
- **Automated Notifications**: Notify managers or admins when inventory is running low.
- **Mobile App**: Develop a mobile version for waiters to log orders directly from their devices.

---

## Contributing

If you would like to contribute to this project, please fork the repository and submit a pull request. You can also open an issue for suggestions or bug reports.

---

## License

This project is licensed under the BSD-3-Clause license.

---

### Contact

For further information or support:

- **Email**: gritagencies@gmail.com
- **Website**: [Grit-Club](https://malixkorea.pythonanywhere.com/)

---

