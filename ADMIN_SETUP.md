# Admin Setup Guide

This guide explains how to set up and use the admin system for the American Pizza application.

## Becoming an Admin

### Method 1: Make First User Admin (Recommended for Initial Setup)

The first user created in the system can be automatically granted admin access:

```bash
cd backend
npm run make-admin
```

This script will:
- Find the first user (oldest by creation date)
- Grant them admin role
- Display confirmation message

### Method 2: Grant Admin via Another Admin

If you already have an admin account:

1. Log in as an existing admin
2. Navigate to **Users** in the admin panel (👑 Users link in navbar)
3. Find the user you want to make admin
4. Click **⬆️ Grant Admin** button
5. Confirm the action

## Admin Features

### User Management (`/admin/users`)

As an admin, you can:

- **View All Users**: See a list of all registered users with their details
- **Search Users**: Search by email or name
- **Grant Admin**: Promote any user to admin role
- **Revoke Admin**: Remove admin role from users (except yourself)
- **Edit User Info**: Update user name, phone, and address
- **Delete Users**: Remove users from the system (with safety checks)

### Product Management (`/admin/products`)

- Create, edit, and delete products
- Manage product categories, prices, and images

### Statistics Dashboard

View admin statistics:
- Total users count
- Total admins count
- Regular users count

## Security Features

### Admin Protection

- **Self-Protection**: Admins cannot:
  - Revoke their own admin status
  - Delete their own account
  - Modify their own role

- **Last Admin Protection**: The system prevents:
  - Deleting the last admin account
  - Revoking admin from the last admin

### Access Control

- Admin routes are protected with `requireAdmin` middleware
- Only users with `role: 'admin'` can access admin endpoints
- Frontend checks admin status before showing admin links

## API Endpoints

### Admin Routes (All require admin authentication)

- `GET /api/admin/users` - List all users
- `GET /api/admin/users/:id` - Get single user
- `POST /api/admin/users/:id/grant-admin` - Grant admin role
- `POST /api/admin/users/:id/revoke-admin` - Revoke admin role
- `PUT /api/admin/users/:id` - Update user info
- `DELETE /api/admin/users/:id` - Delete user
- `GET /api/admin/stats` - Get admin statistics

## Frontend Admin Pages

1. **Admin Users** (`/admin/users`): User management interface
2. **Admin Products** (`/admin/products`): Product management interface

## Navigation

When logged in as admin, you'll see:
- **⚙️ Products** - Product management
- **👑 Users** - User management

These links only appear for admin users.

## Troubleshooting

### I can't see admin links

1. Make sure you're logged in
2. Check if your account has admin role:
   - Go to `/login` page
   - If logged in, you should see "👑 Admin" in your account info
3. If not admin, ask an existing admin to grant you access

### Can't access admin pages

- Make sure you're logged in with an admin account
- Check browser console for error messages
- Verify your JWT token includes the admin role

### Need to reset admin access

If you've lost all admin access:

1. Connect to MongoDB directly
2. Find a user document
3. Set `role: 'admin'` manually
4. Or create a new user and run `npm run make-admin`

## Database Schema

User model includes:
```javascript
{
  email: String,
  password: String (hashed),
  name: String,
  phone: String,
  address: String,
  role: String ('user' | 'admin'), // Default: 'user'
  createdAt: Date,
  updatedAt: Date
}
```

## Notes

- Admin role is stored in JWT token for quick access checks
- Role is verified server-side for all admin operations
- Frontend role checks are for UI only - server always validates
- Admin status persists across sessions until manually changed




