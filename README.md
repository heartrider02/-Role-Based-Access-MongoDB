# User Authentication System with Role-Based Access and MongoDB
## Project Overview
This project is a **User Authentication System** built using **PHP** and **MongoDB**. It supports two types of users: **Normal User** and **Admin**, providing a role-based access control (RBAC) system. The system allows users to register and log in, manages sessions, and restricts access to pages based on user roles. 

Admins have access to specific administrative pages, while normal users are restricted to user-specific content.

## Features
- **User Registration** and **Login** APIs
- Secure password hashing using `password_hash` and `password_verify`
- Session management with session expiry and logout functionality
- Role-based access control (RBAC) for normal users and admins
- Error handling and validation for both APIs and MongoDB operations
- Simple frontend for admin and user dashboards
- MongoDB integration with the `auth_system` database
 Clone the repository
git clone https://github.com/yourusername/auth_system.git
cd auth_system

#Install dependencies:
You need to install the MongoDB PHP driver using Composer. Run the following command in the project root
composer install

##Run the PHP server
Start the PHP server using the following command
php -S localhost:8000

##API Endpoints
User Registration
POST /api/register.php

Accepts username, email, and password as inputs.
Stores user data in the MongoDB users collection with hashed passwords.
Response:

200 OK: Registration successful.
400 Bad Request: Invalid input or user already exists.

##User Login
POST /api/login.php

Accepts email and password as inputs.
Verifies credentials, starts a session on success, and assigns the correct user role.

##User Dashboard
GET /api/user.php

Accessible only to normal users.
Fetches user-specific details from the MongoDB users collection.
Admin Dashboard
GET /api/admin.php

Accessible only to admin users.
Fetches admin-specific details and user management functionality.
Logout
POST /api/logout.php

Logs out the user and destroys the session.

Session Management
Sessions are handled via PHP's $_SESSION superglobal.
Session expiry is set after 15 minutes of inactivity.
To log out, the session can be destroyed using /api/logout.php.

##Role-Based Access Control (RBAC)
Normal Users can only access the /templates/user.php dashboard.
Admin Users can access /templates/admin.php for managing user accounts.
Role-based pages are managed using PHP template inheritance:
base.php: Contains common elements like header, footer.
user.php and admin.php extend the base layout for role-specific content.

##Error Handling
Meaningful HTTP status codes and error messages are returned for invalid input or failed authentication.
MongoDB connection errors are handled gracefully.
Security Measures
Passwords are securely hashed using password_hash before storing them in MongoDB.
Authentication is handled with password_verify during login.
Sessions are securely managed to keep users logged in for a specified period.
