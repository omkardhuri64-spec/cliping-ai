# ClipForge AI — Real App Starter

This is a deployable Next.js starter that upgrades the original demo into a real application architecture.

## Run locally

1. Install Node.js 20+.
2. Copy `.env.example` to `.env.local`.
3. Add `OPENAI_API_KEY` if you want AI responses.
4. Run:
   npm install
   npm run dev
5. Open http://localhost:3000

## Important production architecture

The current `/api/analyze` endpoint intentionally does NOT download YouTube videos. For a production service, connect a worker that processes media the user owns or is authorized to use.

Recommended pipeline:

authorized upload/source
-> object storage
-> FFmpeg worker
-> Whisper/transcription
-> transcript with timestamps
-> OpenAI clip scoring
-> FFmpeg 9:16 reframing/captions
-> object storage
-> signed download URL

Use Redis/BullMQ or a managed queue for long jobs. Add PostgreSQL for users/projects/clips.

## Required production additions

- Authentication
- PostgreSQL/Prisma
- S3-compatible storage
- Redis/BullMQ worker
- FFmpeg worker
- Speech-to-text
- Scene/face detection
- Signed URLs
- Rate limiting
- Usage limits/billing
- Automated cleanup
- Terms/copyright workflow

The UI and API are deliberately usable immediately in demo mode when no AI key is present.
