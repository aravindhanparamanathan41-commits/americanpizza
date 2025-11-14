# Troubleshooting Guide - Project Not Running

## Common Issues and Solutions

### 1. Backend Server Not Running
**Error:** `ERR_CONNECTION_REFUSED` or `Failed to load resource`

**Solution:**
```bash
# Make sure you're in the backend directory
cd backend

# Install dependencies (if not done)
npm install

# Start the backend server
npm run dev

# You should see: "Backend listening on http://localhost:4000"
```

### 2. Frontend Not Starting
**Error:** Port already in use or build errors

**Solution:**
```bash
# Make sure you're in the frontend directory
cd frontend

# Install dependencies (if not done)
npm install

# Start the frontend
npm run dev

# You should see: "Local: http://localhost:5173"
```

### 3. MongoDB Not Running
**Error:** `MongoServerError` or connection timeout

**Solution:**
- **Windows:** Check if MongoDB service is running in Services
- **Mac/Linux:** Run `mongod` or `brew services start mongodb-community`
- **Alternative:** Use MongoDB Atlas (cloud) and update `MONGODB_URI` in `.env`

### 4. Missing Environment Variables
**Error:** API calls failing or undefined variables

**Solution:**
Create `backend/.env`:
```
MONGODB_URI=mongodb://localhost:27017/american_pizza
PORT=4000
JWT_SECRET=your-secret-key-here
CLIENT_ORIGIN=http://localhost:5173
```

Create `frontend/.env`:
```
VITE_API_BASE=http://localhost:4000/api
```

### 5. Dependencies Not Installed
**Error:** Module not found errors

**Solution:**
```bash
# Backend
cd backend
npm install

# Frontend
cd frontend
npm install
```

### 6. Port Already in Use
**Error:** `Port 4000 is already in use` or `Port 5173 is already in use`

**Solution:**
- Kill the process using the port:
  - Windows: `netstat -ano | findstr :4000` then `taskkill /PID <PID> /F`
  - Mac/Linux: `lsof -ti:4000 | xargs kill`
- Or change the port in `.env` files

### 7. Database Not Seeded
**Error:** No products showing in menu

**Solution:**
```bash
cd backend
npm run seed
```

### 8. Browser Cache Issues
**Error:** Old code showing or images not loading

**Solution:**
- Hard refresh: `Ctrl+Shift+R` (Windows) or `Cmd+Shift+R` (Mac)
- Clear browser cache
- Try incognito/private mode

## Quick Start Checklist

1. ✅ MongoDB is running
2. ✅ Backend dependencies installed (`cd backend && npm install`)
3. ✅ Frontend dependencies installed (`cd frontend && npm install`)
4. ✅ Environment variables set (`.env` files created)
5. ✅ Database seeded (`cd backend && npm run seed`)
6. ✅ Backend server running (`cd backend && npm run dev`)
7. ✅ Frontend server running (`cd frontend && npm run dev`)
8. ✅ Browser opened to `http://localhost:5173`

## Still Not Working?

1. Check browser console (F12) for errors
2. Check terminal for error messages
3. Verify all services are running:
   - MongoDB: `mongosh` or check services
   - Backend: `curl http://localhost:4000`
   - Frontend: Open `http://localhost:5173`

## Need Help?

Check the main README.md for detailed setup instructions.




