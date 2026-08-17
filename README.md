# Student Mark Record

A single-file web app for building Half-Semester and Final Results mark reports from an institutional marksheet (Google Sheets, Google Drive, Dropbox, GitHub, OneDrive, or a plain uploaded file). Everything runs in your browser — no backend, no data ever sent to a server other than the Google Sheets/Drive link you point it at and, if you use the email feature, Gmail's own API.

Open `index.html` locally and it mostly works, with one exception: pasting a **Link** to fetch a marksheet requires the page to be loaded from a real `https://` address, not opened directly from your file system. Deploying this repo (see below) fixes that, and is also required for the Gmail sending feature.

## Deploying (recommended: Vercel)

1. Push this repo to GitHub (or use GitHub's web UI to create a repo and upload `index.html` + this `README.md` directly — no command line needed).
2. Go to [vercel.com](https://vercel.com), sign in with your GitHub account.
3. **Add New... → Project**, import this repo.
4. Vercel auto-detects it as a static site — no configuration needed. Click **Deploy**.
5. You'll get a URL like `https://your-repo-name.vercel.app`. That's your app, live, permanently, for free.

Every time you push a change to this repo, Vercel redeploys automatically.

### Alternative: GitHub Pages

Repo **Settings → Pages → Source: Deploy from a branch → main / (root)**. Your app will be live at `https://yourusername.github.io/repo-name/`.

## Using the email feature

Sending emails needs a one-time Google Cloud setup (so the app can send from your own Gmail/Google Workspace account, rather than through a third-party relay). Once you have your Vercel/Pages URL from above:

1. Open the app at that URL, go to **4. Send by email**.
2. Click **"Show me how to set this up"** for the full step-by-step Google Cloud Console walkthrough (built into the app itself, so it's there whenever you need it).
3. You'll register your deployed URL as an **Authorized JavaScript origin** during that setup — this is exactly why the app needs to be hosted before this feature can work.

## What's in this repo

- `index.html` — the entire app. Everything (styles, logic, PDF generation, Google sign-in) is in this one file.
- `README.md` — this file.

There's nothing else to install or configure to run it locally or host it.
