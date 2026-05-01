# Study AI - AI-Powered Study Companion

Transform your study materials into personalized, AI-generated quizzes and track your learning progress.

## Features

### MVP (Current Implementation)

- **File Upload & Processing**
  - Support for PDF, DOCX, and TXT files
  - Automatic text extraction
  - AI-powered content analysis

- **AI-Generated Content**
  - Automatic extraction of key concepts
  - Generation of multiple question types:
    - Multiple choice questions
    - Short answer questions
    - Flashcard-style questions
  - Difficulty ratings for each question

- **Study Sessions**
  - Timed study sessions (25 minutes default)
  - Adaptive question selection based on weak areas
  - Real-time progress tracking
  - Instant feedback and explanations

- **Progress Tracking**
  - Performance analytics
  - Weakness identification
  - Automatic topic-based scoring
  - Study streak tracking

- **Dashboard**
  - Overview of all study materials
  - Quick access to study sessions
  - Daily study plans
  - Recent activity feed

## Tech Stack

- **Frontend**: Next.js 15, React, TypeScript, Tailwind CSS
- **Backend**: Next.js API Routes
- **Database**: PostgreSQL with Prisma ORM
- **AI**: OpenAI GPT-4o
- **File Processing**: pdf-parse, mammoth

## Prerequisites

- Node.js 18+ and npm
- PostgreSQL database
- OpenAI API key

## Installation

1. **Install dependencies**
   ```bash
   npm install
   ```

2. **Set up environment variables**

   Copy the example environment file:
   ```bash
   cp .env.example .env
   ```

   Edit `.env` and add your credentials:
   ```env
   # Database
   DATABASE_URL="postgresql://user:password@localhost:5432/studyai"

   # OpenAI API
   OPENAI_API_KEY="sk-your-openai-api-key-here"
   ```

3. **Set up the database**

   Generate Prisma client:
   ```bash
   npx prisma generate
   ```

   Push the schema to your database:
   ```bash
   npx prisma db push
   ```

   (Optional) Open Prisma Studio to view your database:
   ```bash
   npx prisma studio
   ```

4. **Run the development server**
   ```bash
   npm run dev
   ```

   Open [http://localhost:3000](http://localhost:3000) in your browser.

## Usage Guide

### 1. Upload Study Materials

1. Navigate to the Upload page
2. Select a file (PDF, DOCX, or TXT)
3. Click "Upload & Generate Questions"
4. Wait for AI to process and generate questions

### 2. Start a Study Session

1. Go to the Dashboard
2. Click "Start Study Session"
3. Answer questions within the time limit
4. Review your results and feedback

### 3. Track Your Progress

- View your overall performance on the Dashboard
- Check weak topics in the Analytics section
- Follow daily study recommendations

## Project Structure

```
studyai/
├── app/
│   ├── api/
│   │   ├── upload/
│   │   │   └── route.ts          # File upload and processing
│   │   └── session/
│   │       ├── start/
│   │       │   └── route.ts      # Start study session
│   │       └── submit/
│   │           └── route.ts      # Submit answers
│   ├── dashboard/
│   │   └── page.tsx              # Main dashboard
│   ├── upload/
│   │   └── page.tsx              # File upload page
│   ├── study/
│   │   └── page.tsx              # Study session page
│   └── page.tsx                  # Landing page
├── lib/
│   ├── prisma.ts                 # Prisma client
│   ├── file-processor.ts         # File extraction utilities
│   └── ai-service.ts             # OpenAI integration
├── prisma/
│   └── schema.prisma             # Database schema
└── package.json
```

## Database Schema

### Main Models

- **User**: Student profiles with exam info and study preferences
- **Material**: Uploaded study materials
- **Concept**: AI-extracted key concepts from materials
- **Question**: Generated questions (MCQ, short answer, flashcard)
- **StudySession**: Individual study sessions
- **Answer**: User responses to questions
- **Weakness**: Tracked weak topics per user
- **StudyPlan**: Generated study schedules

## API Endpoints

### POST `/api/upload`
Upload and process a study material file.

**Body**: FormData with `file` and `userId`

**Response**:
```json
{
  "success": true,
  "materialId": "...",
  "conceptsCount": 5,
  "questionsCount": 10
}
```

### POST `/api/session/start`
Start a new study session.

**Body**:
```json
{
  "userId": "...",
  "materialIds": ["..."],
  "questionCount": 10
}
```

**Response**:
```json
{
  "sessionId": "...",
  "questions": [...]
}
```

### POST `/api/session/submit`
Submit answers for a study session.

**Body**:
```json
{
  "sessionId": "...",
  "answers": [
    {
      "questionId": "...",
      "userAnswer": "...",
      "timeSpent": 45
    }
  ]
}
```

**Response**:
```json
{
  "success": true,
  "score": 85,
  "correctCount": 8,
  "totalQuestions": 10,
  "results": [...]
}
```

## Configuration

### Adjusting Study Session Settings

Default settings based on user input:
- Session Duration: 25 minutes
- Questions Per Session: 10
- Weak Topic Threshold: 60%
- AI Model: gpt-4o

To customize, edit the relevant files:
- Session duration: `app/study/page.tsx`
- Question count: `app/api/session/start/route.ts`
- Weak topic threshold: `app/api/session/start/route.ts`

## Troubleshooting

### Database Connection Issues

```bash
# Test connection
npx prisma db push

# View database
npx prisma studio
```

### OpenAI API Errors

- Verify your API key is correct
- Check you have sufficient credits
- Ensure you're using a supported model (gpt-4o)

### File Upload Failures

- Check file size (max 10MB recommended)
- Ensure supported file format (.pdf, .docx, .txt)
- Verify file is not corrupted

## Security Notes

- Never commit `.env` file
- Rotate API keys regularly
- Use strong database passwords
- Implement rate limiting for production
- Add CORS configuration for API routes

## Future Enhancements

1. **Authentication** - User registration and login
2. **Study Plan Generator** - AI-powered study schedules
3. **Advanced Analytics** - Performance trends and insights
4. **Mobile App** - React Native implementation
5. **Social Features** - Study groups and shared materials

## License

MIT License - feel free to use for personal or educational purposes.

---

Built with ❤️ for students everywhere 🎓
