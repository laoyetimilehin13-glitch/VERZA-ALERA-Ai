# VERZA-ALERA AI — External Deployment Build

Production-oriented foundation for the VERZA-ALERA AI data annotation workspace.

## What this build supports
- Email/password authentication with persistent browser sessions
- Email confirmation redirect to the deployed site
- Automatic workspace creation through the Supabase trigger
- Organizations and member roles
- Projects and batches
- Private image storage with signed URLs
- Bounding-box annotation workspace
- Task assignment/status workflow
- Review queue
- JSON / CSV / YOLO / COCO export builders
- Dataset version records
- Audit logs and usage events
- Human-in-the-loop AI pre-labeling placeholder
- Row Level Security policies
- SPA deployment configuration for Vercel and Netlify

## Before deployment
1. Create/configure the Supabase project.
2. Run `supabase/schema.sql` in the Supabase SQL Editor.
3. In Supabase Authentication → URL Configuration, set your deployed dashboard URL as the Site URL and add it to Redirect URLs.
4. Copy `.env.example` to `.env.local` for local development.
5. Set `VITE_SUPABASE_URL` and `VITE_SUPABASE_PUBLISHABLE_KEY`.
6. Run `npm install` and `npm run build`.

## Deploy with Vercel
- Import this project into Vercel.
- Framework preset: Vite.
- Build command: `npm run build`.
- Output directory: `dist`.
- Add the two VITE environment variables in the Vercel project settings.
- Redeploy after adding environment variables.

`vercel.json` is included so direct visits to dashboard routes are handled by the SPA.

## Deploy with Netlify
`netlify.toml` is included with the Vite build command, `dist` output, and SPA fallback. Add the same two VITE environment variables in Netlify.

## Security
The browser must use only the Supabase publishable/anon key. Never place a Supabase secret/service-role key in Vite environment variables or client-side code. The private image bucket relies on authenticated access and RLS policies.

Before accepting real customer data, test RLS with multiple accounts/roles, configure backups, monitoring, rate limits, abuse controls, email settings, privacy/terms, and a server-side job system for large files and AI/export processing.

## Build check
Run `npm run build`. A successful build creates the `dist/` directory.
