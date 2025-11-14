# Products Not Showing - Troubleshooting Guide

If products are not showing in the browser, follow these steps:

## ✅ Products Have Been Seeded

**50 products** have been successfully seeded to the database:
- 10 American Style Pizzas
- 10 Italian Style Pizzas
- 5 Noodles
- 5 Salads
- 10 Burgers
- 10 Finger Foods

## Quick Fixes

### 1. Make Sure Backend is Running

```bash
cd backend
npm run dev
```

You should see:
- `Connected to MongoDB`
- `Backend listening on http://localhost:4000`

### 2. Make Sure Frontend is Running

```bash
cd frontend
npm run dev
```

You should see:
- `Local: http://localhost:5173`

### 3. Check Browser Console

Open browser DevTools (F12) and check:
- **Console tab:** Look for:
  - `All products loaded: 50` (should show 50)
  - `Products loaded for [category]: X` (should show number of products)
  - Any error messages

- **Network tab:** Check:
  - Request to `/api/products` should return status 200
  - Response should contain an array of products

### 4. Verify Database Connection

Make sure MongoDB is running:
- **Windows:** Check Services for MongoDB
- **Mac/Linux:** Run `mongod` or check with `brew services list`

### 5. Check API Endpoint

Test the API directly:
- Open: `http://localhost:4000/api/products`
- Should return JSON array of products

Or test with category:
- Open: `http://localhost:4000/api/products?category=American Style Pizza`
- Should return products in that category

## Common Issues

### Issue: "No response received. Backend may not be running."

**Solution:**
1. Start the backend server: `cd backend && npm run dev`
2. Wait for "Backend listening on http://localhost:4000"
3. Refresh the browser

### Issue: "Cannot connect to server"

**Solution:**
1. Check if backend is running on port 4000
2. Check `frontend/.env` has: `VITE_API_BASE=http://localhost:4000/api`
3. Restart frontend after changing `.env`

### Issue: Products show as empty array `[]`

**Solution:**
1. Check if products exist in database:
   ```bash
   # Connect to MongoDB
   mongosh
   use american_pizza
   db.products.count()
   ```
2. If count is 0, run seed again:
   ```bash
   cd backend
   npm run seed
   ```

### Issue: Products load but images don't show

**Solution:**
- Images are from Unsplash (external URLs)
- Check internet connection
- Images should load automatically
- Fallback images are configured

## Verify Products in Database

To check if products are in the database:

```bash
# Connect to MongoDB
mongosh

# Use the database
use american_pizza

# Count products
db.products.count()

# List all products
db.products.find().pretty()

# Count by category
db.products.aggregate([
  { $group: { _id: "$category", count: { $sum: 1 } } }
])
```

## Re-seed Products (if needed)

If products are missing:

```bash
cd backend
npm run seed
```

You should see:
```
Connected to MongoDB
Seeded products: 50
```

## Still Not Working?

1. **Clear browser cache** and refresh
2. **Check browser console** for specific errors
3. **Check backend console** for errors
4. **Verify MongoDB connection** in backend logs
5. **Test API directly** in browser: `http://localhost:4000/api/products`
6. **Restart both servers** (backend and frontend)

## Expected Behavior

When everything is working:
1. Home page loads with hero section
2. Category buttons appear
3. Products grid shows products for selected category
4. Each product shows:
   - Image
   - Name
   - Price
   - Category badge
5. Clicking a product navigates to detail page
6. Search functionality works

If you see "Loading delicious items..." forever, the API call is failing.




