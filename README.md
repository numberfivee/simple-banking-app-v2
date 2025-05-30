# Simple Banking App

The application can be accessed online by clicking this link: [lilok97085.pythonanywhere.com](https://lilok97085.pythonanywhere.com/login?next=%2F%3Ffbclid%3DIwY2xjawKeuqpleHRuA2FlbQIxMABicmlkETF6OE50dUZldjlhdlladUM5AR7aDbauSq8o53z1q-paTbf-pkpHcbj20L9ttgEkzsnJibC4SgzkELiDXVHFbg_aem_7ptzUu3w21F37NNFQrMRHw)

Project Presentation: https://youtu.be/BmAS4ojPM2A

## Group Members
- Member 1: Rigel Parco
- Member 2: Caren Joy Epres
- Member 3: Mark Wayne Cleofe

## Introduction

The Simple Banking App is a user-friendly and responsive Flask-based banking application designed for deployment on PythonAnywhere. This application allows users to create accounts, perform simulated money transfers between accounts, view transaction history, and securely manage their credentials.

## Objectives

- Provide a secure and intuitive online banking experience.
- Enable users to manage accounts, transfer funds, and view transaction history.
- Implement a hierarchical user role system (User, Admin, Manager).
- Integrate Philippine location data for accurate address management.
- Ensure the application is secure against common web vulnerabilities.

## Features

- **User Authentication**
  - Secure login with username/password
  - Registration of new users
  - Password recovery mechanism (email-based)

- **Account Management**
  - Display of account balance
  - View recent transaction history (last 10 transactions)

- **Fund Transfer**
  - Transfer money to other registered users
  - Confirmation screen before completing transfers
  - Transaction history updated after transfers

- **User Role Management**
  - Regular user accounts
  - Admin users with account approval capabilities
  - Manager users who can manage admin accounts

- **Location Data Integration**
  - Philippine Standard Geographic Code (PSGC) API integration
  - Hierarchical location data selection (Region, Province, City, Barangay)
  - Form fields pre-populated with location data

- **Admin Features**
  - User account approval workflow
  - Account activation/deactivation
  - Deposit funds to user accounts
  - Create new accounts
  - Edit user information

- **Manager Features**
  - Create and manage admin accounts
  - View admin transaction logs
  - Monitor all system transfers

- **Security**
  - Password hashing with bcrypt for secure storage
  - Secure session management
  - Token-based password reset
  - API rate limiting to prevent abuse
  - CSRF protection for all forms

## Security Assessment Findings

During the security assessment of the original application, the following vulnerabilities were identified:

- **Insecure Password Storage:** Passwords were not always hashed using a strong algorithm.
- **Session Management Issues:** Sessions were not properly invalidated on logout.
- **CSRF Vulnerabilities:** Some forms lacked CSRF protection.
- **Rate Limiting Gaps:** Critical endpoints lacked sufficient rate limiting.
- **Input Validation:** Insufficient validation on user input, leading to potential SQL injection and XSS.
- **Password Reset Flaws:** Token-based reset mechanism was not securely implemented.
- **Privilege Escalation:** Inadequate checks on user roles for sensitive actions.

## Security Improvements Implemented

To address the identified vulnerabilities, the following improvements were made:

- **Password Hashing:** All passwords are now hashed using bcrypt.
- **Session Security:** Sessions are securely managed and invalidated on logout.
- **CSRF Protection:** Flask-WTF CSRF protection is enforced on all forms.
- **Rate Limiting:** Flask-Limiter is configured for all sensitive endpoints.
- **Input Validation:** All user inputs are validated and sanitized using WTForms.
- **Password Reset:** Secure, time-limited tokens are used for password resets.
- **Role-Based Access Control:** Strict checks are implemented for all privileged actions.
- **API Security:** PSGC API integration is secured and rate-limited.

## Penetration Testing Report

**Summary of Vulnerabilities Identified:**
- SQL Injection via login and registration forms.
- Cross-Site Scripting (XSS) in user profile fields.
- CSRF on fund transfer and admin actions.
- Brute-force login attempts due to missing rate limiting.

**Exploitation Steps:**
1. Attempted SQL injection payloads in login and registration forms.
2. Injected script tags in profile fields to test for XSS.
3. Submitted forged POST requests to test CSRF.
4. Automated login attempts to test for brute-force protection.

**Recommendations:**
- Use parameterized queries and ORM for all database access.
- Sanitize and encode all user-generated content.
- Enforce CSRF tokens on all forms.
- Implement rate limiting on authentication and sensitive endpoints.

## Remediation Plan

- Refactored all database queries to use SQLAlchemy ORM.
- Added input validation and output encoding for all user inputs.
- Enabled CSRF protection globally via Flask-WTF.
- Configured Flask-Limiter for all critical routes.
- Reviewed and enforced role-based access checks throughout the application.
- Improved password reset flow with secure tokens and expiry.

## Getting Started

### Prerequisites
- Python 3.7+
- pip (Python package manager)
- MySQL Server 5.7+ or MariaDB 10.2+

### Database Setup

1. Install MySQL Server or MariaDB if you haven't already:
   ```
   # For Ubuntu/Debian
   sudo apt update
   sudo apt install mysql-server
   
   # For macOS with Homebrew
   brew install mysql
   
   # For Windows
   # Download and install from the official website
   ```

2. Create a database user and set privileges:
   ```
   mysql -u root -p
   
   # In MySQL prompt
   CREATE USER 'bankapp'@'localhost' IDENTIFIED BY 'your_password';
   GRANT ALL PRIVILEGES ON *.* TO 'bankapp'@'localhost';
   FLUSH PRIVILEGES;
   EXIT;
   ```

3. Update the `.env` file with your MySQL credentials:
   ```
   DATABASE_URL=mysql+pymysql://bankapp:your_password@localhost/simple_banking
   MYSQL_USER=bankapp
   MYSQL_PASSWORD=your_password
   MYSQL_HOST=localhost
   MYSQL_PORT=3306
   MYSQL_DATABASE=simple_banking
   ```

4. Initialize the database:
   ```
   python init_db.py
   ```

### Installation

1. Clone the repository:
   ```
   git clone https://github.com/lanlanjr/simple-banking-app.git
   cd simple-banking-app
   
   # Set up your own repository
   # First, create a new repository named 'simple-banking-app-v2' on GitHub
   
   # Then configure your local repository
   git remote remove origin
   git remote add origin https://github.com/yourusername/simple-banking-app-v2.git
   git remote set-url origin https://yourusername@github.com/yourusername/simple-banking-app-v2.git
   git branch -M main
   git push -u origin main
   
   # Note: Replace 'yourusername' with your actual GitHub username
   ```

2. Install the required packages:
   ```
   pip install -r requirements.txt
   ```

3. Run the application:
   ```
   python app.py
   ```

4. Access the application at `http://localhost:5000`

## Deploying to PythonAnywhere

1. Create a PythonAnywhere account at [www.pythonanywhere.com](https://www.pythonanywhere.com)

2. Upload your code using Git:
   ```
   git clone https://github.com/yourusername/simple-banking-app-v2.git
   ```

3. Install requirements:
   ```
   cd simple-banking-app-v2
   pip install -r requirements.txt
   ```

4. Set up MySQL database on PythonAnywhere:
   - Go to the Databases tab in your PythonAnywhere dashboard
   - Create a new MySQL database
   - Note the database name, username, and password
   - Update your .env file with these credentials

5. Initialize your database on PythonAnywhere:
   ```
   python init_db.py
   ```

6. Configure a new web app via the PythonAnywhere dashboard:
   - Select "Manual configuration"
   - Choose Python 3.8
   - Set source code directory to `/home/yourusername/simple-banking-app-v2`
   - Set working directory to `/home/yourusername/simple-banking-app-v2`
   - Set WSGI configuration file to point to your Flask app

7. Add environment variables in the PythonAnywhere dashboard for security

## Usage

### Registration
- Navigate to the registration page
- Enter username, email, and password
- Confirm your password
- Submit the form to create your account (pending admin approval)

### Login
- Enter your username and password
- Click "Sign In"

### Account Overview
- View your current balance
- See your recent transaction history

### Transfer Funds
- Navigate to the Transfer page
- Enter recipient's username or account number
- Enter the amount to transfer
- Confirm the transfer details on the confirmation screen
- Complete the transfer

### Password Reset
- Click "Forgot your password?" on the login page
- Enter your registered email address
- Follow the link in the email (simulated in this demo)
- Create a new password

### Admin Features
- Approve new user registrations
- Activate/deactivate user accounts
- Create new user accounts
- Make over-the-counter deposits to user accounts
- Edit user details including location information

### Manager Features
- Create new admin accounts
- Toggle admin status for users
- View all user transactions
- Monitor and audit admin activities

## User Roles

The system supports three types of user roles:

1. **Regular Users** - Can manage their own account, make transfers, and view their transaction history.

2. **Admin Users** - Have all regular user privileges plus:
   - Approve/reject new user registrations
   - Activate/deactivate user accounts
   - Create new user accounts
   - Make deposits to user accounts
   - Edit user information

3. **Manager Users** - Have all admin privileges plus:
   - Create and manage admin accounts
   - View admin transaction logs
   - Monitor all system transfers
   - System-wide oversight capabilities

## Address Management with PSGC API

The application integrates with the Philippine Standard Geographic Code (PSGC) API to provide standardized address selection for user profiles. The address system follows the Philippine geographical hierarchy:

- Region
- Province
- City/Municipality
- Barangay

This integration ensures addresses are standardized and validates location data according to the Philippine geographical structure.

## Technologies Used

- **Backend**: Python, Flask
- **Database**: MySQL (with SQLAlchemy ORM)
- **Frontend**: HTML, CSS, Bootstrap 5
- **Authentication**: Flask-Login, Werkzeug, Flask-Bcrypt
- **Forms**: Flask-WTF, WTForms
- **Security**: Flask-Limiter for API rate limiting, CSRF protection
- **External API**: PSGC API for Philippine geographic data

## Rate Limiting

The application uses Flask-Limiter to implement API rate limiting, which protects against potential DoS attacks and abusive bot activity. The rate limits are configured as follows:

- **Login**: 10 attempts per minute
- **Registration**: 5 attempts per minute
- **Password Reset**: 5 attempts per hour
- **Money Transfer**: 20 attempts per hour
- **API Endpoints**: 30 requests per minute
- **Admin Dashboard**: 60 requests per hour
- **Admin Account Creation**: 20 accounts per hour
- **Admin Deposits**: 30 deposits per hour
- **Manager Dashboard**: 60 requests per hour
- **Admin Creation**: 10 admin accounts per hour

By default, the rate limiting data is stored in memory. For production use, it's recommended to use Redis as a storage backend for persistence across application restarts. To enable Redis storage:

1. Install Redis server on your system
2. Update the `.env` file with your Redis URL:
   ```
   REDIS_URL=redis://localhost:6379/0
   ```

If Redis is not available, the application will automatically fall back to in-memory storage.

## License

This project is licensed under the MIT License - see the LICENSE file for details.
