# Frontend Debugging Guide

## Issue: `npm run dev` command not found

### Problem
The error occurs because the `dev` script doesn't exist in `frontend/package.json`.

### Solution
I've added the `dev` script to your `package.json`. Now you can use either:
- `npm start` (standard React command)
- `npm run dev` (now available)

## Debugging Steps

### Step 1: Verify package.json
Check that the `dev` script exists:
```bash
cd frontend
cat package.json | grep -A 5 "scripts"
```

You should see:
```json
"scripts": {
  "start": "react-scripts start",
  "dev": "react-scripts start",
  ...
}
```

### Step 2: Check if node_modules are installed
```bash
cd frontend
ls node_modules
```

If `node_modules` is missing or incomplete:
```bash
npm install
```

### Step 3: Verify React Scripts is installed
```bash
npm list react-scripts
```

If not installed:
```bash
npm install react-scripts@5.0.1
```

### Step 4: Check for port conflicts
The default port is 3000. If it's in use:
- Change port in `.env` file: `PORT=3001`
- Or kill the process using port 3000:
  ```powershell
  # Windows
  netstat -ano | findstr :3000
  taskkill /PID <PID> /F
  ```

### Step 5: Clear cache and reinstall
If issues persist:
```bash
cd frontend
rm -rf node_modules package-lock.json
npm install
npm start
```

### Step 6: Check for TypeScript errors
```bash
npm run build
```

This will show any compilation errors.

### Step 7: Check environment variables
Ensure `.env` file exists in `frontend/` directory:
```env
REACT_APP_API_URL=http://localhost:5000/api
```

### Step 8: Verify Node.js version
React Scripts requires Node.js 14+:
```bash
node --version
```

### Common Issues and Fixes

#### Issue: "Module not found"
**Fix**: Delete `node_modules` and `package-lock.json`, then run `npm install`

#### Issue: "Port already in use"
**Fix**: 
- Use different port: `PORT=3001 npm start`
- Or kill the process using port 3000

#### Issue: "Cannot find module 'react-scripts'"
**Fix**: 
```bash
npm install react-scripts@5.0.1 --save-dev
```

#### Issue: "EADDRINUSE: address already in use"
**Fix**: 
```powershell
# Find process using port 3000
netstat -ano | findstr :3000
# Kill the process (replace <PID> with actual process ID)
taskkill /PID <PID> /F
```

#### Issue: TypeScript compilation errors
**Fix**: Check `tsconfig.json` and fix any type errors shown in the terminal

### Quick Start Commands

```bash
# Navigate to frontend
cd frontend

# Install dependencies (if not done)
npm install

# Start development server
npm start
# OR
npm run dev

# Build for production
npm run build

# Run tests
npm test
```

### Expected Output
When running `npm start` or `npm run dev`, you should see:
```
Compiled successfully!

You can now view attendance-frontend in the browser.

  Local:            http://localhost:3000
  On Your Network:  http://192.168.x.x:3000
```

### Still Having Issues?

1. **Check the full error log**:
   ```bash
   npm start 2>&1 | tee error.log
   ```

2. **Verify all dependencies are installed**:
   ```bash
   npm list --depth=0
   ```

3. **Check for conflicting global packages**:
   ```bash
   npm list -g --depth=0
   ```

4. **Try creating a fresh React app** (last resort):
   ```bash
   npx create-react-app test-app --template typescript
   # Compare package.json and scripts
   ```

