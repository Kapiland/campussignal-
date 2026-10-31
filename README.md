# CampusSignal AI

**CampusSignal AI is a campus opportunity intelligence workspace for college students.** It turns scattered WhatsApp forwards, circulars, posters, and PDFs into structured opportunities students can review, track, and act on. It also helps students find collaborators through profiles that explicitly opt in to discovery.

## The problem it addresses

Internships, hackathons, scholarships, workshops, and campus events are often announced across class groups, posters, and department channels. Students must manually find the important details, remember deadlines, track applications, and search for teammates. Notices can be missed, and the same details are difficult to compare or share.

CampusSignal brings those steps into one student workspace: understand a notice, review the extracted information, save an opportunity, track application status, and find opted-in collaborators.

## What the prototype does

- **Notice intelligence:** Paste a notice or upload a poster/PDF. Google AI extracts fields such as organization, eligibility, skills, deadline, location, and application link into a typed draft. Students can review and edit the draft before saving it.
- **Opportunity radar:** Search and filter database-backed opportunities, open their source links, and track each saved opportunity as Interested, Applied, or Completed.
- **Deadline reminders:** Show upcoming deadlines for tracked opportunities and offer browser notifications two days and one day beforehand. Browser alerts require permission and work while the app is open.
- **Team matcher:** Compare a project description with student skills, interests, experience, and preferred roles. Only signed-in students whose profiles opt in to discovery appear in matches. AI can provide a readable explanation for a match.
- **Student profiles:** Save course, college, skills, interests, experience, and preferred roles to support matching.
- **Authentication and privacy:** Supabase Auth protects student features. Supabase Row Level Security scopes profile changes and saved-opportunity records to their owner; public discovery is opt-in.

## How a student uses it

1. Create an account and confirm the email address.
2. Complete a profile; opt in to discovery only if you want to be found by teammates.
3. Paste a campus notice or upload its poster/PDF.
4. Check and edit the AI-extracted fields against the original notice.
5. Save the opportunity to Radar and update its application status.
6. Review deadline reminders or describe a project to find opted-in teammates.

## Intended benefits

- Spend less time retyping details from unstructured announcements.
- Keep deadlines and application status visible in one place.
- Make opportunities easier to search and compare.
- Help students form project teams around complementary skills.
- Give students control over whether their profile appears in discovery.

These are intended benefits; the prototype has not yet measured student outcomes in a campus pilot.

## Prototype scope and limitations

- Opportunities come from the connected database and student-submitted notices. The prototype does **not** continuously crawl every college, so it cannot promise a complete or always-current campus feed.
- AI extraction and explanations can be wrong. Review extracted information against the original notice before acting on it.
- Browser deadline alerts require notification permission and the app to be open; they are not email or SMS reminders.
- Team matches require other students to have completed profiles and opted in. Match scores are recommendations, not guarantees of team success.
- The repository contains no seeded demo accounts or sample opportunities. Supabase and Google AI must be configured for the corresponding live features.

## Technology

- Next.js App Router, React, TypeScript, and Tailwind CSS
- Supabase Auth and PostgreSQL with Row Level Security
- Google AI API for notice extraction and natural-language opportunity/team explanations
- Zod schemas for request validation and extracted opportunity fields

## Set up locally

1. Install packages and create the local environment file:

   ```powershell
   npm install
   Copy-Item .env.example .env.local
   ```

2. Set your own Supabase project URL, anon/publishable key, and Google AI Studio key in `.env.local`. The app does not need a Supabase service-role key.

3. In Supabase **SQL Editor**, run [`supabase/schema.sql`](supabase/schema.sql). This creates the account-linked tables, profile-on-signup trigger, and owner-scoped RLS policies. It does not add sample accounts or opportunities.

4. In Supabase **Authentication → URL Configuration**, allow the local callback URL `http://localhost:3001/auth/callback` (or `http://localhost:3000/auth/callback` if using the default port) and your deployed callback URL. Enable Email sign-in and keep email confirmation enabled.

5. Start the app:

   ```powershell
   npm run dev -- --port 3001
   ```

   Open `http://localhost:3001`, create an account, confirm the email, then complete your profile. Set profile discovery on only if you want to appear in Team Matcher.

## Set up locally

1. Install packages and create the local environment file:

   ```powershell
   npm install
   Copy-Item .env.example .env.local
   ```

2. Set your own Supabase project URL, anon/publishable key, and Google AI Studio key in `.env.local`. The app does not need a Supabase service-role key.

3. In Supabase **SQL Editor**, run [`supabase/schema.sql`](supabase/schema.sql). This creates the account-linked tables, profile-on-signup trigger, and owner-scoped RLS policies. It does not add sample accounts or opportunities.

4. In Supabase **Authentication → URL Configuration**, allow the local callback URL `http://localhost:3001/auth/callback` (or `http://localhost:3000/auth/callback` if using the default port) and your deployed callback URL. Enable Email sign-in and keep email confirmation enabled.

5. Start the app:

   ```powershell
   npm run dev -- --port 3001
   ```

   Open `http://localhost:3001`, create an account, confirm the email, then complete your profile. Set profile discovery on only if you want to appear in Team Matcher.

## Environment variables

```env
GEMINI_API_KEY=your-google-ai-studio-api-key
GEMINI_MODEL=gemini-3.5-flash
GEMMA_MODEL=gemini-3.5-flash
NEXT_PUBLIC_SUPABASE_URL=https://your-project-ref.supabase.co
NEXT_PUBLIC_SUPABASE_ANON_KEY=your-supabase-anon-or-publishable-key
NEXT_PUBLIC_APP_URL=http://localhost:3001
```

Keep `.env.local` private. Never put a service-role key or an AI key in a `NEXT_PUBLIC_` variable.

## Commands

```powershell
npm run dev
npm run lint
npm run build
```

The model IDs above are example configuration values. Use model IDs enabled for your Google AI project and update them in `.env.local` if needed.

## Judge presentation

The editable slide deck includes the product pitch, end-to-end prototype flow, live demo walkthrough, current limitations, roadmap, speaker notes, and prepared judge Q&A: [`deliverables/CampusSignal_Judge_Pitch.pptx`](deliverables/CampusSignal_Judge_Pitch.pptx).
