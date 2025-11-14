# Troubleshooting: ERR_CONNECTION_REFUSED

## ✅ Backend Server Status
The backend server IS running and responding correctly:
- Server is listening on port 4000
- API endpoints are working
- 50 products are available in the database
- All products have image URLs

## The Problem
Your browser is showing `ERR_CONNECTION_REFUSED` even though the server is running. This is typically caused by:

1. **Browser Cache** - The browser cached the connection failure
2. **CORS Preflight Issues** - Browser security blocking the request
3. **Network/Firewall** - Something blocking browser connections specifically

## Solutions

### Solution 1: Clear Browser Cache (Most Common Fix)

**Chrome/Edge:**
1. Press `Ctrl + Shift + Delete`
2. Select "Cached images and files"
3. Select "All time"
4. Click "Clear data"
5. Refresh the page with `Ctrl + F5`

**Or use Hard Refresh:**
- Press `Ctrl + Shift + R` or `Ctrl + F5` to force reload

### Solution 2: Check Browser Console for CORS Errors

1. Open DevTools (F12)
2. Go to Console tab
3. Look for CORS-related errors
4. If you see CORS errors, the server CORS config has been updated

### Solution 3: Verify Backend is Running

Run this command to test:
```bash
cd backend
node test-connection.js
```

You should see:
```
✅ Connection successful!
✅ Received 50 products
```

### Solution 4: Restart Both Servers

1. **Stop the backend** (if running):
   - Find the terminal running the backend
   - Press `Ctrl + C`

2. **Restart the backend**:
   ```bash
   cd backend
   npm run dev
   ```

3. **Restart the frontend**:
   ```bash
   cd frontend
   npm run dev
   ```

4. **Clear browser cache** and refresh

### Solution 5: Check Windows Firewall

If the above doesn't work:
1. Open Windows Defender Firewall
2. Check if Node.js is allowed through firewall
3. If not, allow it for both private and public networks

### Solution 6: Try Different Browser

Test in a different browser (Chrome, Firefox, Edge) to rule out browser-specific issues.

## Verification

After applying fixes, you should see:
- ✅ Products loading on the home page
- ✅ Images displaying correctly
- ✅ No errors in browser console
- ✅ Network tab shows successful API calls (status 200)

## Still Not Working?

1. Check if MongoDB is running:
   ```bash
   netstat -an | findstr ":27017"
   ```
   Should show `LISTENING`

2. Check backend logs for errors
3. Verify both servers are on the same machine
4. Check if any antivirus is blocking Node.js



