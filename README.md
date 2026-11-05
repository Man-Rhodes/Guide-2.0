# EduGuide Gauteng

Static multi-page site for GitHub Pages, backed by Supabase (logins, database) and one Edge Function that keeps your Anthropic API key secret.

## Setup
1. Create a free project at supabase.com. Run `supabase/schema.sql` in the SQL Editor.
2. Authentication > URL Configuration: set Site URL to `https://man-rhodes.github.io/Edu-Guide/`.
3. Put your Project URL and anon key in `js/config.js`.
4. Deploy the AI function (Supabase CLI): `supabase functions deploy chat` then `supabase secrets set ANTHROPIC_API_KEY=sk-ant-...`
5. Make yourself admin: `insert into admins select id from auth.users where email='you@example.com';`
6. Upload these files to your repo root (replace the old ones). Settings > Pages > Deploy from branch `main` / root.

## Backups
Users can export JSON from My profile. For the database, use Supabase dashboard backups (daily on paid plans) or run `supabase db dump -f backup.sql` on a schedule; keep copies outside Supabase.

## Security notes
Never put the Anthropic key or Supabase service_role key in any file here. Row Level Security limits each user to their own rows; the database enforces question length, so client checks can’t be bypassed.
