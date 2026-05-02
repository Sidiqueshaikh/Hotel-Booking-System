# HomelyHUB

HomelyHUB is a full-stack property rental platform built with a React frontend and a Node.js/Express backend. The application supports user authentication, property listings, booking management, payment/order creation simulation, and image uploads via ImageKit.

## Project Structure

- `backend/` - Node.js API server
  - `src/index.js` - Express app setup and route registration
  - `src/controllers/` - Auth, property, and booking controllers
  - `src/routes/` - API routers for users, properties, and bookings
  - `src/Models/` - Mongoose models for users, properties, and bookings
  - `src/utils/` - Database connection, ImageKit configuration, mail helper, and API filtering helpers

- `Frontend/` - React + Vite client application
  - `src/` - React app source files
  - `src/components/` - Page and UI components
  - `src/store/` - Redux store and slices
  - `src/utils/axios.js` - Axios instance configured for frontend API requests

## Key Features

- User signup/login/logout with JWT authentication
- Password reset flow via email
- Profile update and password change
- Create and manage property accommodations
- Browse available properties with search, filters, and pagination
- View detailed property pages and embedded maps
- Booking flow with order creation and payment verification simulation
- Manage user bookings and booking details
- Image uploads for property listings and avatar updates via ImageKit

## Tech Stack

- Frontend: React, Vite, React Router DOM, Redux Toolkit, Ant Design, Leaflet, Axios
- Backend: Node.js, Express, MongoDB, Mongoose, JWT, bcrypt, ImageKit, Nodemailer

## Getting Started

### 1. Backend Setup

```bash
cd backend
npm install
```

Create a `.env` file inside `backend/` with at least the following values:

```env
MONGO_URI=<your-mongodb-connection-string>
JWT_SECRET=<your-jwt-secret>
JWT_EXPIRES_IN=90d
JWT_COOKIE_EXPIRES_IN=90
ORIGIN_ACCESS_URL=http://localhost:5173
IMAGEKIT_PUBLICKEY=<your-imagekit-public-key>
IMAGEKIT_PRIVATEKEY=<your-imagekit-private-key>
IMAGEKIT_URLENDPOINT=<your-imagekit-url-endpoint>
MAILTRAP_SMTP_HOST=<smtp-host>
MAILTRAP_SMTP_PORT=<smtp-port>
MAILTRAP_SMTP_USER=<smtp-user>
MAILTRAP_SMTP_PASS=<smtp-password>
NODE_ENV=development
PORT=8080
```

> Note: The frontend Vite proxy uses `http://localhost:8080` by default. Set `PORT=8080` in the backend env or update `Frontend/vite.config.js` if you want to use another port.

Run the backend server:

```bash
npm run dev
```

### 2. Frontend Setup

```bash
cd Frontend
npm install
npm run dev
```

The frontend is served by Vite and will proxy API requests from `/api` to the backend.

## Running the App

- Backend default API base path: `/api/v1/rent`
- Frontend proxy path: `/api`

Open the Vite development URL shown in the terminal (usually `http://localhost:5173`).

## Available Backend Endpoints

### Auth & User

- `POST /api/v1/rent/user/signup` - Create a new user
- `POST /api/v1/rent/user/login` - Login and receive JWT cookie/token
- `GET /api/v1/rent/user/logout` - Logout user
- `GET /api/v1/rent/user/me` - Check current authenticated user
- `PATCH /api/v1/rent/user/updateMe` - Update user profile
- `PATCH /api/v1/rent/user/updateMyPassword` - Change password
- `POST /api/v1/rent/user/forgotPassword` - Request password reset email
- `PATCH /api/v1/rent/user/resetPassword/:token` - Reset password
- `POST /api/v1/rent/user/newAccommodation` - Create a new property listing
- `GET /api/v1/rent/user/myAccommodation` - Get properties created by current user

### Properties

- `GET /api/v1/rent/listing` - Get all properties with search/filter/pagination
- `GET /api/v1/rent/listing/:id` - Get property details by ID

### Bookings & Payments

- `GET /api/v1/rent/user/booking` - Get current user's bookings
- `GET /api/v1/rent/user/booking/:bookingId` - Get details for a specific booking
- `POST /api/v1/rent/user/booking/create-order` - Create a booking order
- `POST /api/v1/rent/user/booking/verify-payment` - Verify booking payment and save booking

## Notes

- The backend uses `cookie-parser` and JWT-based auth for protected routes.
- Image uploads are handled through ImageKit using the `backend/src/utils/ImagekitIO.js` helper.
- Password reset emails are generated using Mailgen and sent via Nodemailer.
- The frontend assumes API traffic is proxied through Vite; if backend runs on a different port, update `Frontend/vite.config.js`.

## Recommended Improvements

- Add tests for backend controllers and frontend components
- Add form validation and better error handling in the UI
- Add deployment scripts for production builds
- Secure mail and image service credentials in production

## Contact

If you need help configuring or deploying HomelyHUB, review the backend and frontend source folders or ask for support.
