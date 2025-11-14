🍕 American Pizza Shop - Online Ordering System
================================================

A full-stack web application for a pizza shop with online ordering, menu management, and customer reviews.

Tech stack
----------
- Frontend: React + Vite, React Router, Bootstrap, React-Bootstrap
- Backend: Node.js + Express
- Database: MongoDB (Mongoose)

Features
--------
- Menu with required pizzas and finger food, plus 5 burgers
- Click product to add directly to cart
- Cart: clear cart, print bill, Pay Now (QR code)
- Login via email (demo JWT) and admin product CRUD
- Monthly sales report
- Home category buttons (Home, American Style Pizza, Italian Style Pizza, Noodle, Salate, Burger, Finger Food)
- Route Map page (Google Maps embed)

Project structure
-----------------
- `backend/`: Express API, MongoDB models, seed script
- `frontend/`: React app with Bootstrap UI

Setup
-----
1) Requirements:
- Node.js 18+
- MongoDB running locally at `mongodb://localhost:27017`

2) Install dependencies:
```
cd backend
npm install
cd ../frontend
npm install
```

3) Environment:
- Backend reads:
  - `MONGODB_URI` (default: `mongodb://localhost:27017/american_pizza`)
  - `PORT` (default: `4000`)
  - `JWT_SECRET` (any string, default provided for dev)
  - `CLIENT_ORIGIN` (default: `http://localhost:5173`)
  - `SMS_ENABLED` (optional, set to `true` to enable SMS notifications)
  - `TWILIO_ACCOUNT_SID`, `TWILIO_AUTH_TOKEN`, `TWILIO_PHONE_NUMBER` (optional, for SMS)
- Frontend:
  - Create `frontend/.env` with:
```
VITE_API_BASE=http://localhost:4000/api
```

**SMS Notifications (Optional):**
- See `backend/SMS_SETUP.md` for detailed SMS configuration
- SMS notifications are sent automatically when order status changes
- Can be disabled by setting `SMS_ENABLED=false` or omitting Twilio credentials

4) Seed menu:
```
cd backend
npm run seed
```

5) Run apps (IMPORTANT: Start backend first!):
```
# Terminal 1 - Start Backend Server
cd backend
npm run dev
# You should see: "Backend listening on http://localhost:4000"

# Terminal 2 - Start Frontend (in a new terminal)
cd frontend
npm run dev
# You should see: "Local: http://localhost:5173"
```

**⚠️ IMPORTANT:** The backend server MUST be running before the frontend can load products. If you see `ERR_CONNECTION_REFUSED`, make sure the backend is running on port 4000.

Default URLs
------------
- Frontend: `http://localhost:5173`
- Backend: `http://localhost:4000`
- API base: `http://localhost:4000/api`

Notes
-----
- The Pay Now flow is a demo: it generates a QR code to a placeholder URL.
- Printing bill uses the browser print dialog from the cart panel.
- Login is email-only for demo purposes; it stores a JWT in localStorage.


