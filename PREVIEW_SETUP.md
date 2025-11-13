# How to Preview Dynasty Gallery

## Step 1: Install Node.js (if not installed)

1. Go to https://nodejs.org/
2. Download the LTS version (recommended)
3. Install it (this will also install npm)
4. Restart your terminal/command prompt after installation

Verify installation:
```bash
node --version
npm --version
```

## Step 2: Install Project Dependencies

Open terminal in the project folder and run:
```bash
npm install
```

## Step 3: Set Up Database

You need a PostgreSQL database. **Easiest option: Neon (free cloud database)**

1. Go to https://neon.tech
2. Click "Sign Up" (free account)
3. Create a new project
4. Copy the connection string (looks like: `postgresql://user:pass@host.neon.tech/dbname?sslmode=require`)

## Step 4: Create .env File

Create a file named `.env` in the project root (same folder as `package.json`):

```env
DATABASE_URL=your-neon-connection-string-here
SESSION_SECRET=any-random-secret-string-here-make-it-long
PORT=5000
```

**Important:** Replace `your-neon-connection-string-here` with the actual connection string from Neon.

## Step 5: Set Up Database Tables

Run this command to create the database tables:
```bash
npm run db:push
```

## Step 6: Start the Development Server

```bash
npm run dev
```

## Step 7: Open in Browser

The server will start on port 5000. Open your browser and go to:
```
http://localhost:5000
```

## Troubleshooting

### "DATABASE_URL must be set"
- Make sure you created the `.env` file
- Check that `DATABASE_URL` is spelled correctly
- Make sure there are no spaces around the `=` sign

### "Port 5000 already in use"
- Change `PORT=5001` in your `.env` file
- Then go to `http://localhost:5001`

### "Cannot find module" errors
- Run `npm install` again
- Make sure you're in the project root directory

### Database connection errors
- Check your Neon connection string is correct
- Make sure the database is active in Neon dashboard
- Try copying the connection string again from Neon

## Quick Checklist

- [ ] Node.js installed
- [ ] `npm install` completed
- [ ] Neon database created
- [ ] `.env` file created with `DATABASE_URL`
- [ ] `npm run db:push` completed successfully
- [ ] `npm run dev` started without errors
- [ ] Browser opened to `http://localhost:5000`

