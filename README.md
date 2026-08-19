# Student Mark Record & Insights Dashboard

A single-file web app for building Half-Semester and Final Results mark reports from an institutional marksheet, plus a student-facing dashboard showing a six-axis "hexagon" competency breakdown once you choose to publish it. Everything runs in your browser — no backend server of ours; the only external services involved are Google Sheets/Drive (for loading your marksheet), Gmail's API (if you use the email feature), Anthropic's API (if you use AI-generated feedback), and Firebase (Authentication + Firestore, for the student dashboard).

**Important change: this app now requires a one-time Firebase setup before *anyone* — including you as admin — can get past the login screen.** Previously Firebase was optional and only needed for publishing; now the whole app sits behind a sign-in gate, so this is a hard requirement from the very first use, not an optional add-on.

## How it works

- **One shared login screen** — the only URL you give out, to anyone.
- **Students** sign in with **Google**. If they have published results, they see their own grade, marks breakdown, feedback, and hexagon chart. Nothing else — not other students' data, not the admin tool.
- **You (admin)** sign in with the **email + password** account you create in Firebase Authentication. This takes you to the full tool: load a marksheet, define assessments, tag hexagon competencies, generate feedback, send emails, and publish results live to the student dashboard.
- Nothing is visible to students until you explicitly click **Publish** from your own signed-in session.

## Deploying (recommended: Vercel)

1. Push this repo to GitHub (or use GitHub's web UI to create a repo and upload `index.html` + this `README.md` directly — no command line needed).
2. Go to [vercel.com](https://vercel.com), sign in with your GitHub account.
3. **Add New... → Project**, import this repo.
4. Vercel auto-detects it as a static site — no configuration needed. Click **Deploy**.
5. You'll get a URL like `https://your-repo-name.vercel.app`. That's your app, live, permanently, for free.

Every time you push a change to this repo, Vercel redeploys automatically.

### Alternative: GitHub Pages

Repo **Settings → Pages → Source: Deploy from a branch → main / (root)**. Your app will be live at `https://yourusername.github.io/repo-name/`.

## Required setup: Firebase (do this first)

Nobody can sign in — student or admin — until this is done, since the login screen itself needs to know which Firebase project to talk to.

1. Open `index.html` in a text editor, find the `FIREBASE_CONFIG` object near the top of the `<script>` section, and note it's currently empty.
2. Follow the full walkthrough (project creation, enabling Google + Email/Password sign-in, creating your admin account, Firestore security rules, getting your config values) — this is written out in full inside the app itself: open the login screen, expand **"Firebase isn't configured yet"**, and it's all there, including the exact security rules to paste into Firestore.
3. Paste your six config values into the `FIREBASE_CONFIG` object in the file, save, and push the change (Vercel/GitHub Pages redeploys automatically).

The Firestore security rules are what actually enforce "students only ever see their own results" — not anything in the page's own JavaScript, which anyone could inspect.

## Using the email feature

Sending emails needs a separate one-time Google Cloud setup (so the app can send from your own Gmail/Google Workspace account, rather than through a third-party relay).

1. Once signed in as admin, go to **5. Send by email**.
2. Click **"Show me how to set this up"** for the full step-by-step Google Cloud Console walkthrough (built into the app itself).
3. You'll register your deployed URL as an **Authorized JavaScript origin** during that setup — this is exactly why the app needs to be hosted, not opened as a local file.

## Using AI-generated feedback

Optional — under **3. Feedback wording per grade**, toggle "Use AI-generated feedback" and paste in your own Anthropic API key (not saved anywhere, session-only, unlike the Firebase/Google settings above which are meant to be public/embedded).

## What's in this repo

- `index.html` — the entire app: admin tool, student dashboard, and the login gate between them, all in this one file.
- `README.md` — this file.

There's nothing else to install or configure to run it locally or host it, beyond the Firebase setup above.

