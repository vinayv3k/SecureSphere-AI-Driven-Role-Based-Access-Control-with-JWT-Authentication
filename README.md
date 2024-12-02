RBAC with JWT Authentication, Authorization & Role Management

This is an implementation of a secure backend system using Node.js, MongoDB, and JWT (JSON Web Token) to manage user authentication, role-based access control (RBAC), and various additional features like email verification, password reset, and two-factor authentication (2FA).

Features:
1.User Registration & Login: Users can register with credentials, login with JWT authentication, and perform secure operations.
2.RBAC (Role-Based Access Control): Role-based access for different levels (Admin, Moderator, User). Permissions are mapped to roles.
3.Secure Authentication: Passwords are securely hashed using bcrypt. JWT is used for session management.
4.Password Reset: Users can reset their password through a secure token sent to their email.
5.Email Verification: New users must verify their email before they can access the system.
6.2FA (Two-Factor Authentication): Users can enable and verify two-factor authentication using OTP.
7.Dynamic Role Management: Admins can dynamically update roles and permissions.
8.Rate Limiting: Protection against brute-force login attempts.

Tech Stack:
1.Backend: Node.js, Express.js
2.Database: MongoDB
3.Authentication: JWT (JSON Web Token)
4.Email Service: Nodemailer
5.2FA: speakeasy (for OTP generation)
6.Rate Limiting: express-rate-limit
7.Password Hashing: bcrypt

Prerequisites:
1.Node.js: v14.x or higher
2.MongoDB: Installed locally or use a cloud MongoDB service like MongoDB Atlas.
3.Postman: For testing API endpoints.
4.Nodemailer Configuration: For sending emails (email username & password needed).

Setup:
Clone the repository:
git clone https://github.com/your-username/rbac-jwt-system.git
cd rbac-jwt-system

Install dependencies:
npm install

Set up environment variables: Create a .env file in the root directory and add the following:

PORT=5000
MONGO_URI=mongodb://localhost:27017/rbac_db
JWT_SECRET=supersecuresecret
EMAIL_USER=your-email@gmail.com
EMAIL_PASS=your-email-password
FRONTEND_URL=http://localhost:3000

Run the application:
npm start
The server should be running on http://localhost:5000.

API Endpoints:

Authentication:
1.POST /auth/register
2.Register a new user.
3.Request body:
{ "email": "user@example.com", "password": "password", "role": "User" }

POST /auth/login:
1.Login to get a JWT token.
2.Request body:
{ "email": "user@example.com", "password": "password" }
3.Response:
{ "token": "JWT_TOKEN_HERE" }

POST /auth/forgot-password:
1.Request a password reset token via email.
2.Request body:
{ "email": "user@example.com" }

POST /auth/reset-password:
1.Reset the password using the reset token.
2.Request body:
{ "resetToken": "RESET_TOKEN", "newPassword": "new_password" }

GET /auth/verify-email;
1.Verify email using the token sent to the user.
2.Query parameter: ?token=VERIFICATION_TOKEN

POST /auth/enable-2fa:
1.Enable two-factor authentication (2FA).
2.Response contains OTP secret URL for use in an authenticator app.
3.Example response:
{ "message": "2FA enabled", "secret": "otpauth://totp/YourApp:email@example.com?secret=SECRET_HERE" }

POST /auth/verify-2fa:
1.Verify OTP for 2FA.
2.Request body:
{ "token": "OTP_TOKEN" }
Role-Based Access Control

GET /admin:
1.Only accessible by Admin role.

GET /moderator:
1.Only accessible by Moderator and Admin roles.

GET /user:
1.Accessible by User, Moderator, and Admin roles.

POST /auth/update-role:
1.Admins can update roles and permissions.
2.Request body:
{ "roleName": "Admin", "permissions": ["read", "write", "delete"] }

Security & Rate Limiting:
Rate Limiting: Prevents brute-force login attempts. Set limit for login attempts to 10 per 15 minutes.

Testing:
You can use Postman to test the following scenarios:
1.Registration: Test creating new users with different roles (Admin, Moderator, User).
2.Login: Verify correct JWT tokens are issued and that unauthorized users cannot access protected routes.
3.RBAC: Test different roles accessing /admin, /moderator, and /user routes.
4.Password Reset: Request a reset token and change the password successfully.
5.Email Verification: Ensure that users cannot log in until their email is verified.
6.2FA: Enable and verify OTP-based two-factor authentication.

Contributions:
Feel free to fork this project, contribute improvements, or report issues. You can contribute by following these steps:
1.Fork the repository
2.Create a feature branch (git checkout -b feature-name)
3.Commit your changes (git commit -am 'Add new feature')
4.Push to the branch (git push origin feature-name)
5.Create a new Pull Request
