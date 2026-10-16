# ChainLink — Michigan Disc Golf Community

A Next.js 15 mobile-first community app: per-course chat, round invitations, lost-and-found posts, public email accounts, usernames, report and block controls. Hosted on Vercel with Supabase backend.

## Quick start

1. Install Node.js 20+.
2. `npm install`
3. `cp .env.example .env.local` (on Windows: `copy .env.example .env.local`)
4. `npm run dev` and open http://localhost:3000. Without Supabase keys, the UI runs in **preview mode**, but messages/accounts/posts are disabled.

## Activate public multi-user functionality

1. Create a project at https://supabase.com/dashboard.
2. Open **SQL Editor**, paste `supabase/schema.sql`, and run it once.
3. In **Project Settings → API**, copy the project URL and publishable/anon key into `.env.local` as `NEXT_PUBLIC_SUPABASE_URL` and `NEXT_PUBLIC_SUPABASE_ANON_KEY`. Never use a service-role key in a `NEXT_PUBLIC_` variable.
4. In **Authentication → Providers**, enable Email. Configure email confirmation and allowed site URLs in **Authentication → URL Configuration**. For production, configure reliable SMTP and anti-abuse protections.
5. Restart `npm run dev`. Register, confirm email if required, save a username, and test posting with two separate accounts.

## Deploy on Vercel

1. Create a GitHub repository, upload this folder, and push to the main branch. Do not commit `.env.local`.
2. Go to https://vercel.com/new, connect GitHub, and import the repository. Vercel detects Next.js.
3. Add the two `NEXT_PUBLIC_SUPABASE_*` environment variables in Vercel project settings for Production and Preview; use the publishable/anon key only.
4. Deploy. Copy the resulting Vercel URL and add it to Supabase Authentication → URL Configuration as the Site URL; add preview/localhost URLs to Redirect URLs as needed.
5. Redeploy after adding environment variables, then verify signup, login, two-person messaging, and posts from separate devices.

## Important launch notes

- Chat updates via 5-second polling; not WebSocket realtime yet.
- Course list contains 10 **starter Michigan courses**, not a comprehensive or verified directory.
- Posts support descriptions and optional public contact details, **not image uploads** yet.
- Public reading is enabled for course posts and messages. Avoid sharing phone numbers, email addresses, or precise location in public posts.
- Reporting and blocking are included, but there is **no moderation dashboard or automated enforcement**. Reports must be reviewed by an administrator through a secure backend workflow before wider public promotion.
- Before a broad public launch, add server-side rate limits, CAPTCHA/anti-spam, content moderation, a privacy policy, terms, account deletion workflow, and age-appropriate protections.
- Public profiles expose usernames. Messages and posts are readable by anyone; only authenticated users can write. Row-level security prevents users writing as another account.
- Supabase Free plan limits and Vercel plan limits may apply.
