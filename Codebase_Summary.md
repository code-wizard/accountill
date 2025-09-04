# Accountill - MERN Stack Invoicing Application

Accountill is a full-stack invoicing web application built with the MERN stack (MongoDB, Express, React, and Node.js) designed for freelancers and small businesses. It enables users to create, send, and manage invoices, receipts, estimates, quotations, and bills, with features like PDF generation, email sending, payment tracking, and a comprehensive dashboard.

## Backend (Express REST API) - Located in server directory
Entry Point: server/index.js - Express application bootstrap with middleware setup
Main Configuration: server/package.json - Dependencies and scripts
URL Routing: server/index.js - Route definitions for invoices, clients, users, and profiles

App Structure - Express follows a modular architecture:
- Controllers (server/controllers/) - Business logic for handling requests (clients.js, invoices.js, profile.js, user.js)
- Models (server/models/) - Mongoose schemas for data modeling
  - InvoiceModel.js: Invoice data with items, payments, client info, and status tracking
  - ClientModel.js: Client information storage
  - userModel.js: User authentication data with password reset tokens
  - ProfileModel.js: Business profile information including logo and payment details
- Routes (server/routes/) - API endpoints for CRUD operations
- Middleware (server/middleware/) - Authentication middleware
- Documents (server/documents/) - PDF and email template generation

Key Features:
- JWT-based authentication system
- PDF invoice generation using html-pdf
- Email sending via Nodemailer with SMTP configuration
- MongoDB integration with Mongoose ODM

## Frontend (React SPA) - Located in client directory
Entry Point: client/src/index.js - React application bootstrap
Main Component: client/src/App.js - Root component with React Router setup
State Management: Redux store configuration (though store.js appears to contain sample data)

Architecture Pattern - Redux-based state management with action/reducer pattern:
- Actions (client/src/actions/) - API calls and state updates for auth, clients, invoices, and profiles
- Reducers (client/src/reducers/) - State management logic for different domains
- Components (client/src/components/) - Reusable UI components organized by feature (Dashboard, Invoice, Clients, etc.)
- Utils (client/src/utils/) - Utility functions

Key Libraries:
- Material UI for UI components
- Axios for API calls
- ApexCharts for data visualization
- React Router for navigation
- Redux Thunk for async actions

## Technologies Used
### Client
- React 17
- Redux & Redux Thunk
- React Router DOM
- Material UI & CSS Modules
- Axios
- ApexCharts
- React Google Login
- Cloudinary (for logo uploads)

### Server
- Express
- Mongoose
- JWT (authentication)
- bcryptjs (password hashing)
- Nodemailer (email sending)
- html-pdf (PDF generation)
- CORS

### Database
- MongoDB (MongoDB Atlas)

## Key Features
- Create and send invoices, receipts, estimates, quotations, and bills
- Generate and download PDF documents
- Email integration for sending documents
- Payment tracking with partial payment support
- Automatic status updates based on payments
- Dashboard with statistics (total received, pending, recent payments)
- Client management
- Multi-user registration
- JWT and Google OAuth authentication
- Business profile customization with logo upload

## Local Setup Instructions
Prerequisites:
- Node.js LTS (18.x or 20.x) and npm
- MongoDB Atlas account (or local MongoDB)
- Git

### Manual Setup:
1. Clone the repository and navigate to the project directory.

2. **Client Setup:**
   - Navigate to `client` directory
   - Create a `.env` file with:
     ```
     REACT_APP_GOOGLE_CLIENT_ID=your_google_client_id
     REACT_APP_API=http://localhost:5000
     REACT_APP_URL=http://localhost:3000
     ```
   - Install dependencies: `npm install`
   - Start the client: `npm start`

3. **Server Setup:**
   - Navigate to `server` directory
   - Create a `.env` file with:
     ```
     DB_URL=your_mongodb_connection_string
     PORT=5000
     SECRET=your_jwt_secret
     SMTP_HOST=your_smtp_host
     SMTP_PORT=your_smtp_port
     SMTP_USER=your_smtp_username
     SMTP_PASS=your_smtp_password
     ```
   - Install dependencies: `npm install`
   - Start the server: `npm start`

### Docker Setup:
- Use docker-compose.prod.yml for production deployment
- Configure .env files as above, adjusting DB_URL for Docker network (e.g., `mongodb://mongo:27017/accountill`)

## Verification:
- Backend API: http://localhost:5000
- Frontend: http://localhost:3000
- Test API: curl -sS http://localhost:5000/ | python -m json.tool

## Troubleshooting:
- For PDF generation issues, run:
  ```
  npm install html-pdf -g
  npm link html-pdf
  npm link phantomjs-prebuilt
  ```
- Ensure MongoDB connection string is correct
- For Google OAuth, configure credentials in Google Cloud Console with correct redirect URIs
- If encountering CORS issues, verify CORS middleware is properly configured

Note: The application uses JWT for API security, Nodemailer for email functionality, and follows a traditional REST API architecture with React frontend consuming Express API endpoints. PDF generation relies on html-pdf with PhantomJS.
