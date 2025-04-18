# Wuxia Cultivation Idle Game

Creator: Ronald C. Pancho

An immersive idle game exploring wuxia cultivation themes, offering players a strategic journey through mystical realms of energy manipulation and personal growth.

## Features

- Cultivation progression through multiple realms (Qi Condensation, Foundation Establishment, etc.)
- Combat system with various enemies and locations
- Herb gathering and utilization during combat
- Level-gated locations with progressive difficulty scaling
- Character attributes and skills development

## Deployment to Vercel

### Prerequisites

1. Create a [Vercel](https://vercel.com) account
2. Set up a PostgreSQL database (recommended: [Neon](https://neon.tech) or [Supabase](https://supabase.com))
3. Install the [Vercel CLI](https://vercel.com/docs/cli): `npm i -g vercel`

### Steps to Deploy

1. **Prepare Environment Variables**

   Create a `.env` file with the following variables (see `.env.example`):
   ```
   DATABASE_URL=your-postgres-connection-string
   SESSION_SECRET=your-session-secret
   NODE_ENV=production
   ```

2. **Login to Vercel CLI**

   ```bash
   vercel login
   ```

3. **Deploy to Vercel**

   ```bash
   vercel
   ```

4. **Set Environment Variables on Vercel**

   In the Vercel dashboard, go to your project settings and add the environment variables listed in your `.env` file.

5. **Run Database Migrations**

   ```bash
   npx drizzle-kit push
   ```

## Development

1. Clone the repository
2. Install dependencies: `npm install`
3. Start the development server: `npm run dev`

## Tech Stack

- Frontend: React, TypeScript, Tailwind CSS, Shadcn UI
- Backend: Express.js, Node.js
- Database: PostgreSQL with Drizzle ORM
- State Management: Zustand
- Routing: Wouter
