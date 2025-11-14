# Quick Fix: Cannot Login After Logout

## Immediate Solutions

### Solution 1: Clear Browser Data
1. Open browser DevTools (F12)
2. Go to **Application** tab (Chrome) or **Storage** tab (Firefox)
3. Click **Local Storage** → `http://localhost:5174`
4. Click **Clear All** or delete individual items
5. Refresh page (Ctrl + Shift + R)

### Solution 2: Clear via Console
Open browser console (F12) and run:
```javascript
localStorage.clear();
location.reload();
```

### Solution 3: Check Rate Limiting
If you see "Too many authentication attempts":
- Wait 15 minutes
- OR restart backend server to reset rate limit

### Solution 4: Restart Backend
```bash
# Stop backend (Ctrl+C in backend terminal)
cd backend
npm run dev
```

## What Was Fixed

1. ✅ **Logout now clears form fields** - Email/password reset
2. ✅ **Login status properly updates** - Component re-renders correctly
3. ✅ **Rate limit increased** - 10 attempts per 15 minutes (was 5)
4. ✅ **Better error messages** - Shows rate limit errors clearly
5. ✅ **Old token cleared** - Removes old token before new login

## Test Login Flow

1. **Logout:**
   - Click logout button
   - Should see "Logged out successfully"
   - Form should reset

2. **Login:**
   - Enter email: `kenkeswary11@icloud.com`
   - Enter your password
   - Click "Sign In"
   - Should see "Logged in successfully"

3. **If Still Fails:**
   - Check browser console for errors
   - Check backend console for errors
   - Verify credentials are correct
   - Clear browser cache completely

## Common Error Messages

- **"Too many authentication attempts"** → Wait 15 min or restart backend
- **"Invalid email or password"** → Check credentials
- **"Cannot connect to server"** → Backend not running
- **"Validation failed"** → Check email format




