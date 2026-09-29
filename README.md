# VoxOnboard

### Say it once. Get it structured.

VoxOnboard swaps the sign-up questionnaire for a conversation. A new user simply answers a voice assistant out loud, and the app quietly converts what was said into a tidy JSON record with nine fields filled in, ready for whatever comes next in your pipeline.


---

## The problem

Long forms are tedious to complete, and the answers people type in are inconsistent and hard to clean up afterwards. Teams end up re-keying details by hand or chasing users for missing information.

## The idea

Speaking is faster and more natural than filling in boxes. VoxOnboard captures the conversation, hands the transcript to a language model, and returns only the details that matter, already organised into a fixed schema.

## What happens under the hood

| Step | What occurs |
| ---- | ----------- |
| 1. Access | The user logs in through Clerk, using email or their Google account. |
| 2. Conversation | A Vapi-powered voice agent asks the onboarding questions and listens to the replies. |
| 3. Processing | The finished transcript goes to a dedicated Next.js API endpoint, which prompts Llama 3.3 70B running on Groq. |
| 4. Output | The model responds with a nine-field JSON object that the app stores and displays. |

```
Speech -> Vapi -> Transcript -> Next.js API -> Groq (Llama 3.3 70B) -> JSON
```

## Highlights

- Hands-free onboarding driven entirely by voice
- Automatic conversion of free speech into nine defined data fields
- Secure accounts for multiple users, including Google sign-in
- Middleware that keeps private pages behind authentication
- Live production deployment on Vercel

## Built with

- **Next.js 14** with TypeScript and Tailwind CSS for the app and API layer
- **Vapi** for real-time voice interaction
- **Groq** serving **Llama 3.3 70B** for language understanding
- **Clerk** for user management and Google OAuth
- **Vercel** for hosting

## Folder layout

```
app/            routes, pages and API handlers
components/     shared interface pieces
lib/            utility functions
public/         images and static files
middleware.ts   authentication guard for protected routes
```

## Run it locally

You will need Node.js 18 or newer, plus API access to Clerk, Vapi and Groq.

```bash
git clone https://github.com/mohdfaiz98110/codeflex.ai.git
cd codeflex.ai
npm install
npm run dev
```

Before starting, create a `.env.local` file in the project root and fill in your credentials. The names below are typical, so match them to what the code expects:

```env
NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=
CLERK_SECRET_KEY=
NEXT_PUBLIC_VAPI_WEB_TOKEN=
GROQ_API_KEY=
```

Then visit http://localhost:3000. Keep your keys private and out of version control.

## Going live

Connect the GitHub repository to Vercel, copy the same environment variables into the project's settings, and trigger a deploy.

## Creator

Built by **MONU PATHAK** together with a collaborator.
[LinkedIn](https://www.linkedin.com/in/monu-pathak-89b394326/) | [GitHub](https://github.com/monupathak3122)
