# Admin Access Fix Guide

This guide helps you diagnose and fix admin access issues.

## ✅ What Was Fixed

The following improvements have been made to the admin access system:

1. **Login Process**: Now always fetches fresh role from database before creating JWT token
2. **Signup Process**: Now always fetches fresh role from database before creating JWT token
3. **Error Logging**: Enhanced logging in `requireAdmin` middleware to show exactly why access is denied
4. **Diagnostic Tools**: New scripts to check and fix admin status
5. **Consistency**: All role checks now use the same logic and always check database

## Quick Fix Steps

### Step 1: Check Your Admin Status

Run this command to check if your user account has admin role:

```bash
cd backend
npm run check-admin <your-email>
```

Example:
```bash
npm run check-admin admin@example.com
```

Or check all users:
```bash
npm run check-admin
```

### Step 2: Make Yourself Admin

If you're not an admin, run one of these commands:

**Option A: Make first user admin**
```bash
cd backend
npm run make-admin
```

**Option B: Make specific user admin (by email)**
```bash
cd backend
npm run make-user-admin <your-email>
```

Example:
```bash
npm run make-user-admin admin@example.com
```

### Step 3: Log Out and Log Back In

**IMPORTANT:** After changing your role to admin, you MUST:
1. Log out completely
2. Clear your browser's localStorage (or use incognito mode)
3. Log back in

This is because the JWT token contains your role, and it only updates when you log in.

### Step 4: Verify Access

After logging back in:
1. Check the login page - you should see "👑 Admin" next to your role
2. Try accessing `/admin/products` or `/admin/users`
3. Check browser console for any errors

## Troubleshooting

### Issue: "Access Denied" even after making admin

**Solution:**
1. Verify your role in database:
   ```bash
   npm run check-admin <your-email>
   ```
2. Make sure you logged out and logged back in
3. Clear browser cache and localStorage
4. Check backend console logs for error messages

### Issue: Role shows as "user" in login page

**Solution:**
1. The role in localStorage might be stale
2. Log out completely
3. Clear localStorage: Open browser console and run:
   ```javascript
   localStorage.clear()
   ```
4. Log back in

### Issue: Backend shows "Admin check failed"

**Check backend console logs.** The error message will show:
- Your user ID
- Your current role
- What role was expected

**Solution:**
1. Run `npm run check-admin <your-email>` to verify database
2. If role is not 'admin', run `npm run make-user-admin <your-email>`
3. Log out and log back in

## Database Verification

You can also check directly in MongoDB:

```javascript
// Connect to MongoDB
use american_pizza

// Find your user
db.users.findOne({ email: "your-email@example.com" })

// Check the role field
// It should be: role: "admin"

// If not, update it:
db.users.updateOne(
  { email: "your-email@example.com" },
  { $set: { role: "admin" } }
)
```

## How the System Works

1. **User Model**: Stores `role` field with values: 'user', 'admin', or 'delivery'
2. **Login Process**: 
   - Fetches fresh role from database
   - Includes role in JWT token
   - Returns role to frontend
3. **Admin Middleware** (`requireAdmin`):
   - Verifies JWT token
   - Fetches user from database (always fresh)
   - Checks if `user.role === 'admin'`
4. **Frontend Check** (`isAdmin`):
   - Calls `/api/auth/me` to get current user
   - Checks if `user.role === 'admin'`

## Common Issues

### Issue: Role changed but still can't access

**Cause:** JWT token contains old role

**Fix:** Log out and log back in to get new token

### Issue: Database shows admin but access denied

**Possible causes:**
1. Token expired - log out and back in
2. Wrong user ID in token - log out and back in
3. Backend not reading from database - check logs

### Issue: Multiple users, unsure which is admin

**Solution:**
```bash
npm run check-admin
```
This lists all users and their roles.

## Verification Checklist

- [ ] User exists in database
- [ ] User's `role` field is set to `'admin'` (not `'Admin'` or `'ADMIN'`)
- [ ] Logged out completely
- [ ] Cleared localStorage/cache
- [ ] Logged back in
- [ ] Login page shows "👑 Admin"
- [ ] Can access `/admin/products`
- [ ] Can access `/admin/users`
- [ ] Backend logs show "Admin access granted"

## Still Having Issues?

1. Check backend console for detailed error messages
2. Check browser console for frontend errors
3. Verify JWT token contains role:
   - Open browser console
   - Run: `JSON.parse(atob(localStorage.getItem('token').split('.')[1]))`
   - Check the `role` field
4. Verify database directly using MongoDB shell
5. Try creating a fresh admin user:
   ```bash
   # Create new user via signup
   # Then make them admin
   npm run make-user-admin <new-email>
   ```

## Scripts Available

- `npm run check-admin` - Check admin status of all users
- `npm run check-admin <email>` - Check specific user
- `npm run make-admin` - Make first user admin
- `npm run make-user-admin <email>` - Make specific user admin

