# Full-Stack Node.js & pure JS Application: From Scratch to Production-Ready

A project by **Adnan Dar** • [GitHub](https://github.com/AdnanMohi) • [LinkedIn](https://www.linkedin.com/in/adnanmohi/)

This project is a complete full-stack web application built from the ground up using **only the native Node.js `http` module**, intentionally bypassing frameworks like **Express.js** to demonstrate a deep, foundational understanding of server-side JavaScript. It serves as a comprehensive demonstration of professional web development principles by implementing a sophisticated **Single-Page Application (SPA)** architecture without a frontend framework.

The application's core is a dynamic **User Management Dashboard**. This dashboard functions as a full **CRUD (Create, Read, Update, Delete)** system, driven by a secure, stateless RESTful API with JWT-based authentication. The SPA behavior is achieved through a dynamic sidebar navigation system that fetches and injects HTML page content and its corresponding JavaScript modules on the fly, creating a seamless user experience without full page reloads.

Every aspect, from the custom server and middleware engine to the highly interactive and responsive frontend table, has been meticulously crafted to showcase a deep understanding of how modern web applications are built.

---

## ✨ Features

### Core Backend & Architecture

- **Zero Frameworks:** Built entirely on the native Node.js `http` module to showcase a deep understanding of server fundamentals.
- **JWT-Based Authentication:** Secure, stateless session management using JSON Web Tokens stored in `HttpOnly`, `Secure`, and `SameSite=Strict` cookies.
- **Custom Middleware Engine:** A clean, middleware-based architecture handles security rules for both API and page routes.
- **Dynamic API Router:** A custom "Smart Router" that correctly handles static paths, dynamic path parameters (e.g., `/api/users/:id`), and query strings.
- **Password Hashing:** Uses `bcryptjs` to securely hash and verify user passwords, following industry best practices.
- **Centralized Route Management:** All application routes and their security policies are defined in a single, easy-to-manage configuration file.

### 🚀 Feature Spotlight: Advanced User Management UI

The centerpiece of this application is a production-ready user management interface engineered for performance, usability, and professional polish.

- **Full CRUD Operations:** Create, Read, Update, and Delete users with professional UI modals, data validation, and clear toast notifications for user feedback.

- **Advanced Data Controls:**

  - **Server-Side Search:** Instantly find users by name or email with a debounced, real-time search that efficiently queries the database.
  - **Dynamic Sorting:** Click any column header to sort the data. The UI is jiggle-free thanks to a fixed table layout, and visual indicators (↑/↓) clearly show the active sort column and direction.
  - **Customizable Pagination:** A complete pagination system with icon-based "Previous/Next" buttons, an informative "Showing X to Y of Z results" label, and a "Rows per page" dropdown to give users full control over data density.

- **Professional & Responsive UI/UX:**
  - **Flicker-Free Experience:** All data operations (sorting, searching, paging) trigger a smooth loading overlay instead of a jarring page refresh, ensuring a stable and pleasant user experience.
  - **Sticky Header & Scrolling Body:** The table is contained within a fixed-height panel. The table body scrolls independently while the header remains "sticky" at the top, so column context is never lost.
  - **Responsive Design:** On smaller screens, the table gracefully enables horizontal scrolling with a `min-width`, preventing layout breaks and ensuring all data is accessible.
  - **Polished "Empty State":** When a search yields no results, a helpful, vertically-centered message with an icon is displayed instead of a blank space.

---

## ⚙️ Technology Stack

- **Backend:** Node.js, `mysql2`
- **Authentication:** `jsonwebtoken`, `bcryptjs`
- **Frontend:** JavaScript, HTML5, Tailwind CSS
- **Environment:** `dotenv`
- **Development:** `nodemon` for automatic server restarts

---

## 🚀 Getting Started

Follow these steps to get the project running on your local machine.

### 1. Prerequisites

- Node.js (v18 or later recommended)
- npm
- A running MySQL database server

### 2. Installation & Setup

1.  **Clone the repository:**

    ```
    git clone <your-repository-url>
    cd <your-project-directory>
    ```

2.  **Install dependencies:**

    ```
    npm install
    ```

3.  **Set up the database:**
    Connect to your MySQL server and run the following SQL command to create the `users` table:

    ```
    CREATE TABLE users (
      id INT AUTO_INCREMENT PRIMARY KEY,
      name VARCHAR(255) NOT NULL,
      email VARCHAR(255) NOT NULL UNIQUE,
      password VARCHAR(255) NOT NULL,
      created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
    );
    ```

4.  **Configure Environment Variables:**
    Create a `.env` file in the root of the project and add your configuration.

    ```
    # .env file

    # A strong, long, random string for signing JWTs
    JWT_SECRET=your_super_secret_and_long_random_string
    JWT_EXPIRES_IN=1h

    # Your database connection details
    DB_HOST=localhost
    DB_USER=your_db_user
    DB_PASSWORD=your_db_password
    DB_NAME=your_db_name
    ```

### 3. Running the Application

For production, use the `start` command.

For development, it is highly recommended to use the `dev` command, which uses `nodemon` for automatic server restarts on file changes.

The server will start running at `http://localhost:3000`.

---

## 📁 Project Structure

.
├── controllers/
│ ├── authController.js # Handles register, login, logout logic
│ └── usersController.js # Handles user-related API logic
├── middleware/
│ └── auth.js # Contains authMiddleware & redirectIfLoggedIn
├── public/
│ ├── components/ # Reusable client-side JS modules
│ │ ├── mainContentLoader.js
│ │ ├── sideBarToggle.js
│ │ └── toast.js
│ ├── js/ # Page-specific client-side scripts
│ │ ├── loginScript.js
│ │ ├── logoutScript.js
│ │ ├── mainScript.js
│ │ ├── registerScript.js
│ │ └── usersScript.js
│ ├── dashboard.html # HTML for the dashboard view
│ ├── index.html # Main application shell (with sidebar)
│ ├── login.html # Public login page shell
│ ├── profile.html # HTML for the user profile view
│ ├── public.html # A generic public-facing HTML page
│ ├── register.html # Public registration page shell
│ ├── setting.html # HTML for the settings view
│ └── users.html # HTML for the user list view
├── routes/
│ └── index.js # Centralized definition of all routes & pages
├── utils/
│ ├── bodyParser.js # Helper to parse request bodies
│ ├── cookieUtils.js # Helper to parse cookies
│ └── responseHelpers.js # Helpers for sending JSON, errors, etc.
├── .env # (Local) Environment variables
├── .gitignore
├── db.js # Database connection helper
├── package.json
└── index.js # Main server entry point (The Dispatcher)

## 🗺️ API Endpoints

| Method   | Endpoint              | Security      | Description                                                 |
| :------- | :-------------------- | :------------ | :---------------------------------------------------------- |
| `GET`    | `/`                   | Public-Only   | Serves the main login page for logged-out users.            |
| `GET`    | `/login`              | Public-Only   | Serves the `login.html` page.                               |
| `GET`    | `/register`           | Public-Only   | Serves the `register.html` page.                            |
| `GET`    | `/dashboard`          | **Protected** | Serves the main application shell for logged-in users.      |
| `GET`    | `/users`              | **Protected** | Serves the `users.html` page within the application shell.  |
| `POST`   | `/api/register`       | Public-Only   | Creates a new user account (self-registration).             |
| `POST`   | `/api/users/register` | **Protected** | Creates a new user (admin-only action from user dashboard). |
| `POST`   | `/api/login`          | Public-Only   | Authenticates a user and returns a session cookie.          |
| `GET`    | `/api/logout`         | **Protected** | Logs the user out by clearing the session cookie.           |
| `GET`    | `/api/users`          | **Protected** | Gets a list of users. Supports search, sort, & pagination.  |
| `GET`    | `/api/users/:id`      | **Protected** | Gets the details of a single user by their ID.              |
| `PUT`    | `/api/users/:id`      | **Protected** | Updates the details of a single user.                       |
| `DELETE` | `/api/users/:id`      | **Protected** | Deletes a single user.                                      |

**Query Parameters for `GET /api/users`:**

- `search`: A string to search against user `name` and `email`.
- `sortBy`: The column to sort by (`name`, `email`, `created_at`).
- `sortOrder`: The direction to sort (`asc` or `desc`).
- `page`: The page number for pagination.
- `limit`: The number of items per page (e.g., 5, 10, 20).

**Example:** `GET /api/users?search=john&sortBy=email&sortOrder=desc&page=2&limit=20`

---
