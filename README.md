# Azul Online

Static frontend (`public/`) + one Vercel serverless function (`api/act.js`) + Supabase (Postgres + Realtime).
Every move is validated on the server by the same rules engine (`public/engine.js`), which the browser only uses for highlighting.

## Deploy
1. **Supabase**: create a project, open SQL Editor, run `supabase.sql`.
2. **GitHub**: `git init && git add . && git commit -m "Azul" && git remote add origin <your repo> && git push -u origin main`
3. **Vercel**: Import the repo (framework "Other"). Add environment variables:
   - `SUPABASE_URL` = your project URL
   - `SUPABASE_SERVICE_ROLE_KEY` = service_role key (Project Settings > API). Server only; never put it in `config.js`.
4. Edit `public/config.js` with `SUPABASE_URL` and the **anon** key for instant Realtime updates, commit and push. (Without it the game still works, updating every 4 seconds.)
5. Open your site, create a room, copy the invitation link (`/?room=CODE`) and send it.

Local test: `npm i && npx vercel dev`. Rules tests: add `runTests()` call in the console of any page importing `/engine.js`, or `node -e "import('./public/engine.js').then(m=>m.runTests())"`.
