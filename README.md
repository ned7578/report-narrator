# Report narrator — deployment guide

This turns the prototype into a real, shareable link. No coding required beyond copy/paste — takes about 10 minutes.

## What's in this folder
- `index.html` — the app itself (upload/paste CSV, view summary, ask follow-ups)
- `api/summarize.js` — a small backend function that holds your API key and talks to Claude, so the key is never exposed in the browser
- `vercel.json` — tells Vercel how to deploy both pieces together

## Step 1 — Get an Anthropic API key
1. Go to https://console.anthropic.com and sign up / log in
2. Go to "API Keys" and create a new key
3. Add a small amount of credit to the account (a few dollars covers a lot of testing — each summary costs a fraction of a cent to a few cents depending on data size)
4. Copy the key somewhere safe — you'll paste it once in Step 3

## Step 2 — Create a free Vercel account
1. Go to https://vercel.com and sign up (GitHub login is easiest)

## Step 3 — Deploy
**Easiest path (drag and drop, no GitHub needed):**
1. Go to https://vercel.com/new
2. Look for the option to deploy without Git — drag this whole folder in, or use the Vercel CLI (below)
3. When it asks for environment variables, add:
   - Name: `ANTHROPIC_API_KEY`
   - Value: (paste the key from Step 1)
4. Deploy — Vercel gives you a live URL like `report-narrator-yourname.vercel.app`

**If you're comfortable with a terminal instead:**
```
npm install -g vercel
cd report-narrator
vercel
```
Follow the prompts, then when asked for env vars run:
```
vercel env add ANTHROPIC_API_KEY
```
paste your key, then redeploy with `vercel --prod`.

## Step 4 — Test it
Open your live URL, upload a CSV, hit "Generate summary." This time it'll actually work, because the API key lives safely on Vercel's server, not in the page itself.

## Sharing it with people
The live URL is what you post in analytics communities or send to people for feedback — not the HTML file. Anyone can use it without needing their own API key, since your backend handles that.

## Cost note
You're paying per API call, not a flat fee. Keep an eye on usage in the Anthropic console if you share this link widely — a public link with no rate limiting could run up a bill if it gets a lot of traffic. Worth adding basic rate limiting later if this gets real usage.
