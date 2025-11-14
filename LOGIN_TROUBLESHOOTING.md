# Login Issues Troubleshooting

## Problem: Cannot Login After Logout

If you're experiencing issues logging in after logging out, here are the fixes applied and troubleshooting steps:

## Fixes Applied

### 1. **Improved Logout Function**
- Now clears all form fields (email, password, name, phone)
- Resets component state properly
- Forces component re-render
- Clears all localStorage items

### 2. **Rate Limiting Adjustments**
- Increased from 5 to 10 login attempts per 15 minutes
- Better error messages for rate limiting
- Successful logins don't count toward limit

### 3. **State Management**
- Login status now uses React state for proper re-rendering
- Listens for logout events to update UI immediately
- Periodic checks to ensure UI stays in sync

### 4. **Error Handling**
- Better detection of rate limiting errors (429 status)
- Detailed error logging for debugging
- Clear error messages for users

## Common Issues and Solutions

### Issue 1: Rate Limiting
**Symptom:** "Too many authentication attempts" error

**Solution:**
- Wait 15 minutes before trying again
- Rate limit is now 10 attempts per 15 minutes (increased from 5)
- Successful logins don't count toward the limit

**Check:**
- Look for 429 status code in browser console
- Check backend logs for rate limit messages

### Issue 2: Token Not Cleared
**Symptom:** Old token still being sent in requests

**Solution:**
- Clear browser cache and localStorage
- Open DevTools (F12) → Application → Local Storage → Clear all
- Or run in console: `localStorage.clear()`

### Issue 3: Form State Not Resetting
**Symptom:** Old email/password still in form after logout

**Solution:**
- Fixed: Form fields now clear on logout
- Refresh page if issue persists

### Issue 4: Component Not Updating
**Symptom:** Still shows "Account" view after logout

**Solution:**
- Fixed: Component now properly detects logout
- Refresh page if needed: `Ctrl + Shift + R`

## Debugging Steps

### 1. Check Browser Console
Open DevTools (F12) and check:
- Any error messages
- Network tab for failed requests
- Status codes (401, 429, 500, etc.)

### 2. Check Backend Logs
Look for:
- "Login attempt failed" messages
- Rate limiting messages
- Authentication errors

### 3. Clear Everything
```javascript
// Run in browser console
localStorage.clear();
sessionStorage.clear();
location.reload();
```

### 4. Test Login Directly
Try logging in with:
- Correct email and password
- Check if user exists in database
- Verify password is correct

### 5. Check Rate Limit Status
If you see 429 errors:
- Wait 15 minutes
- Or restart backend server (clears rate limit cache)

## Manual Rate Limit Reset

If you're blocked by rate limiting:

1. **Restart Backend Server:**
   ```bash
   # Stop backend (Ctrl+C)
   # Then restart
   cd backend
   npm run dev
   ```

2. **Clear Browser Data:**
   - Press `Ctrl + Shift + Delete`
   - Clear cookies and cached data
   - Refresh page

3. **Wait 15 Minutes:**
   - Rate limit resets automatically after 15 minutes

## Verification Steps

After fixes, verify:

1. **Logout works:**
   - Click logout button
   - Should see "Logged out successfully" message
   - Form should reset to login tab
   - No token in localStorage

2. **Login works:**
   - Enter email and password
   - Should see "Logged in successfully" message
   - Should redirect to home page
   - Token should be in localStorage

3. **Multiple login/logout cycles:**
   - Logout → Login → Logout → Login
   - Should work without issues

## Still Not Working?

1. **Check Backend:**
   - Is backend running? (`http://localhost:4000`)
   - Check backend console for errors
   - Verify MongoDB is connected

2. **Check Network:**
   - Open Network tab in DevTools
   - Try login and check request/response
   - Look for error status codes

3. **Check Credentials:**
   - Verify email is correct
   - Verify password is correct
   - Try creating a new account

4. **Clear Everything:**
   ```bash
   # Clear browser data
   # Restart backend
   # Restart frontend
   ```

## Error Messages Reference

- **"Invalid email or password"** → Wrong credentials or user doesn't exist
- **"Too many authentication attempts"** → Rate limited, wait 15 minutes
- **"Cannot connect to server"** → Backend not running
- **"Validation failed"** → Check email format and password requirements
- **"Token expired"** → Old token, need to login again
