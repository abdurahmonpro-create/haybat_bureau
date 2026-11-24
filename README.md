# haybat.bureau — Visual Archive

A dark, minimal image portfolio with a public gallery, individual shareable image pages, and a password-protected admin area.

## Included
- Responsive black / off-white editorial design
- Public gallery at `/`
- Individual image pages at `/image/<slug>`
- Admin login and image upload at `/admin`
- Copyable individual image links
- Supabase database + public image storage
- Netlify single-page routing

## 1. Create the database and storage
1. Create a project at https://supabase.com/
2. Open **SQL Editor** and run `supabase/schema.sql`.
3. Before running the SQL, replace both occurrences of `ADMIN_EMAIL` with the exact email address you will use as the site administrator.
4. In Supabase → Authentication → Users, create your admin user with that email and a strong password. Disable public sign-ups in Authentication settings.

## 2. Connect the website
1. In Supabase → Project Settings → API, copy the **Project URL** and **anon/public key**.
2. Copy `.env.example` to a new file named `.env` in the project root.
3. Fill in `VITE_SUPABASE_URL` and `VITE_SUPABASE_ANON_KEY`.
4. Never put a Supabase `service_role` key in this website. It must remain private.

## 3. Run locally
Install Node.js (LTS), then in this folder run:

```bash
npm install
npm run dev
```

Open the local URL printed by Vite. The admin page is `/admin`.

## 4. Publish on Netlify
1. Push this folder to a private GitHub repository, or upload the project to Netlify.
2. In Netlify, set build command to `npm run build` and publish directory to `dist`.
3. Add the two environment variables from `.env` in Netlify → Site configuration → Environment variables.
4. Deploy the site.

## 5. Connect a custom domain
Buy a domain from a supported registrar, then add it in Netlify → Domain management → Add a domain. Follow Netlify's DNS instructions at your registrar. Check availability and price before purchasing: `haybat.bureau` may or may not be available.

## How image sharing works
After you upload an image in `/admin`, it appears in the public gallery. Each image has its own URL such as `https://your-domain.com/image/quiet-geometry`. In the admin list, choose **COPY LINK** and send it to anyone. The image page is public and does not require a visitor account.

## Security notes
- Row-level security policies restrict uploads and deletes to the admin email configured in `supabase/schema.sql`.
- The public gallery and image pages are intentionally viewable by anyone with the URL (and the gallery itself is public).
- Use a unique, strong admin password and keep your Supabase project credentials private.
- Do not change the anon key to a service-role key in frontend environment variables.
- Demo images appear until Supabase is configured.
