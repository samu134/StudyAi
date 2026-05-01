# StudyAI - Quick Setup Guide

Get your StudyAI application running in 5 minutes!

## Prerequisites

Before you begin, make sure you have:
- Node.js 18+ installed
- A PostgreSQL database (local or cloud)
- An OpenAI API key

## Step 1: Install Dependencies

```bash
npm install
```

## Step 2: Configure Environment Variables

1. Copy the example environment file:
   ```bash
   cp .env.example .env
   ```

2. Edit the `.env` file with your credentials:
   ```env
   DATABASE_URL="postgresql://user:password@localhost:5432/studyai"
   OPENAI_API_KEY="sk-your-actual-openai-key"
   ```

### Getting an OpenAI API Key

1. Go to [platform.openai.com](https://platform.openai.com/)
2. Sign up or log in
3. Navigate to API Keys section
4. Create a new API key
5. Copy and paste it into your `.env` file

### Database Options

#### Option 1: Local PostgreSQL

```bash
# Install PostgreSQL (macOS)
brew install postgresql
brew services start postgresql

# Create database
createdb studyai
```

#### Option 2: Docker PostgreSQL

```bash
docker run --name studyai-db \
  -e POSTGRES_PASSWORD=password \
  -e POSTGRES_DB=studyai \
  -p 5432:5432 \
  -d postgres:15
```

#### Option 3: Cloud Database (Recommended for Production)

Free tier options:
- [Supabase](https://supabase.com/) - Free tier available
- [Neon](https://neon.tech/) - Free tier available
- [Railway](https://railway.app/) - Free trial

After creating a database, copy the connection string to your `.env` file.

## Step 3: Set Up the Database

Generate Prisma client and create database tables:

```bash
npx prisma generate
npx prisma db push
```

## Step 4: Run the Application

Start the development server:

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

## Verify Installation

1. You should see the StudyAI landing page
2. Click "Upload Material" to test file upload
3. Upload a sample PDF, DOCX, or TXT file
4. Check that questions are generated successfully
5. Start a study session to test the full workflow

## Common Issues

### Database Connection Error

**Error**: `Can't reach database server`

**Solution**:
- Verify PostgreSQL is running: `pg_isready`
- Check your DATABASE_URL in `.env`
- Ensure the database exists: `createdb studyai`

### OpenAI API Error

**Error**: `Invalid API key`

**Solution**:
- Verify your API key is correct (starts with `sk-`)
- Check you have credits at [platform.openai.com](https://platform.openai.com/)
- Ensure no extra spaces in `.env` file

### Prisma Client Error

**Error**: `PrismaClient is unable to be run in the browser`

**Solution**:
```bash
npx prisma generate
npm run dev
```

### Port Already in Use

**Error**: `Port 3000 is already in use`

**Solution**:
```bash
# Kill the process using port 3000
lsof -ti:3000 | xargs kill -9

# Or use a different port
PORT=3001 npm run dev
```

## Next Steps

Once your app is running:

1. **Upload Study Materials**: Navigate to `/upload` and add your first document
2. **Start Studying**: Go to `/study` to begin an AI-powered study session
3. **Track Progress**: View your performance on the `/dashboard`

## Development Tools

### View Database

```bash
npx prisma studio
```

Opens a GUI at http://localhost:5555 to browse your database.

### Reset Database

```bash
npx prisma db push --force-reset
```

Warning: This will delete all data!

## Production Deployment

For deployment instructions, see the main README.md file.

Quick deploy options:
- [Vercel](https://vercel.com/) - Easiest for Next.js apps
- [Railway](https://railway.app/) - Includes database hosting
- [Render](https://render.com/) - Free tier available

## Need Help?

- Check the full README.md for detailed documentation
- Review the troubleshooting section
- Ensure all prerequisites are installed correctly

---

Happy studying! 🎓
