# Dynasty Gallery - Local Development Setup

## Quick Start

### 1. Install Dependencies
```bash
npm install
```

### 2. Set Up Database

You need a PostgreSQL database. Choose one option:

#### Option A: Use Neon (Cloud - Free & Easy)
1. Go to https://neon.tech
2. Sign up for a free account
3. Create a new project
4. Copy the connection string (it will look like: `postgresql://user:password@host.neon.tech/dbname`)
5. Add it to your `.env` file as `DATABASE_URL`

#### Option B: Use Local PostgreSQL
1. Install PostgreSQL on your machine
2. Create a database: `createdb dynastygallery`
3. Use connection string: `postgresql://localhost:5432/dynastygallery`

### 3. Create .env File

Copy `.env.example` to `.env` and fill in your values:
```bash
cp .env.example .env
```

Edit `.env` and add your `DATABASE_URL` and `SESSION_SECRET`:
```
DATABASE_URL=your-database-connection-string
SESSION_SECRET=any-random-string-for-sessions
PORT=5000
```

### 4. Run Database Migrations

```bash
npm run db:push
```

### 5. Start Development Server

```bash
npm run dev
```

The app will be available at `http://localhost:5000`

## Troubleshooting

- **"DATABASE_URL must be set"**: Make sure you've created a `.env` file with `DATABASE_URL`
- **Database connection errors**: Check that your database is running and the connection string is correct
- **Port already in use**: Change `PORT` in `.env` to a different port (e.g., 5001)

