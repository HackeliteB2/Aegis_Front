# Demo Mode Instructions

## Overview
Authentication has been temporarily disabled for demo purposes. All auth-related functionality is bypassed when `DEMO_MODE = true`.

## What's Changed

### 1. AuthContext (`src/contexts/AuthContext.tsx`)
- Added `DEMO_MODE = true` flag at the top
- Modified to automatically create a mock admin user in demo mode
- Login function accepts any credentials and returns a mock user
- Logout function simply clears state without API calls

### 2. ProtectedRoute (`src/components/ProtectedRoute.tsx`)
- Added `DEMO_MODE = true` flag at the top
- Bypasses all authentication and authorization checks in demo mode
- Always renders children components without redirects

## Demo User Details
When in demo mode, a mock user is automatically created with:
- **Username**: `demo_admin` (or whatever is entered in login)
- **Email**: `admin@demo.com`
- **Name**: `Demo Administrator`
- **Role**: `admin` (if username is "admin", otherwise "user")
- **Status**: `active`

## Current State
- ✅ All authentication is disabled
- ✅ Admin pages are accessible without login
- ✅ User pages are accessible without login
- ✅ No API calls are made to authentication endpoints
- ✅ All protected routes are accessible

## How to Revert (Enable Authentication Again)

### Quick Method:
1. In `src/contexts/AuthContext.tsx`, change:
   ```typescript
   const DEMO_MODE = true;
   ```
   to:
   ```typescript
   const DEMO_MODE = false;
   ```

2. In `src/components/ProtectedRoute.tsx`, change:
   ```typescript
   const DEMO_MODE = true;
   ```
   to:
   ```typescript
   const DEMO_MODE = false;
   ```

### Complete Cleanup (Remove Demo Code):
If you want to completely remove the demo code:
1. Remove the `DEMO_MODE` constant and all demo-related if statements
2. Restore the original authentication logic
3. Remove this instruction file

## Testing the Demo
- Navigate to `/Admin` - should work without login
- Navigate to `/Admin/Users` - should work without login
- Navigation should work seamlessly
- No login redirects should occur

## Notes
- The demo uses mock data, so no real authentication is performed
- API calls to the backend are bypassed in demo mode
- LocalStorage is not used for authentication in demo mode
- All users appear as admin users for demo purposes
