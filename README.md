# BoodleBox Fall 2026 — Meeting Sign-up

A single-page sign-up sheet for the Fall 2026 BoodleBox faculty & staff meetings.
People add themselves as attendees under each date and can sign up to lead a
15-minute mini-session. Entries are stored in a Google Sheet you own.

Files:

- `index.html` — the page (Lake + Curiosity styling; no build step, no dependencies beyond Google Fonts)
- `Code.gs` — the Google Apps Script that saves and serves the sign-ups
- `README.md` — this guide

Setup takes about 10 minutes and is done once.

## Part 1 — The Google Sheet (where sign-ups are saved)

1. Go to <https://sheets.new> and create a blank spreadsheet. Name it something like
   **BoodleBox Fall 2026 Sign-ups**.
2. In the menu choose **Extensions → Apps Script**.
3. Delete the placeholder code in the editor, paste in the entire contents of `Code.gs`,
   and click the **Save** (disk) icon.
4. In the toolbar, pick the function **`setup`** from the dropdown next to "Debug" and click **Run**.
   - Google will ask you to authorize the script: choose your account, click **Advanced →
     Go to (project name)**, then **Allow**. This is normal for your own scripts.
   - Back in the spreadsheet you'll now see two tabs, **Attendance** and **Presenters**,
     with Sara Greenleaf already listed for Pair 1.
5. Click **Deploy → New deployment**.
   - Click the gear next to "Select type" and choose **Web app**.
   - Description: anything (e.g. "v1").
   - **Execute as:** Me
   - **Who has access:** **Anyone**  ← this is what lets people sign up without logging in
   - Click **Deploy**, then **Copy** the **Web app URL**. It ends in `/exec`.

## Part 2 — Put the URL in the page

1. Open `index.html` in any text editor (Notepad, TextEdit, VS Code).
2. Near the top, find:
   ```js
   window.SIGNUP_API_URL = "";
   ```
   and paste the URL between the quotes:
   ```js
   window.SIGNUP_API_URL = "https://script.google.com/macros/s/AKfycb.../exec";
   ```
3. Save the file.

## Part 3 — Publish on GitHub Pages

1. Sign in at <https://github.com> and click **New repository** (the + in the top right).
   Name it e.g. `boodlebox-signup`, keep it **Public**, and click **Create repository**.
2. On the empty repo page click **uploading an existing file**, drag in `index.html`
   (you can add `Code.gs` and `README.md` too — they're harmless), and click **Commit changes**.
3. Go to **Settings → Pages**. Under "Build and deployment", set **Source** to
   **Deploy from a branch**, **Branch** to `main` and folder `/ (root)`, then **Save**.
4. After a minute or two the page is live at
   `https://<your-github-username>.github.io/boodlebox-signup/`
   (the exact link is shown at the top of the Pages settings).

Share that link with faculty and staff. No login is needed to sign up.

## Everyday use

- **See who's coming:** open the Google Sheet. The **Attendance** tab has one row per
  person per date; the **Presenters** tab has one row per presenter sign-up.
- **Remove someone:** either hover their name on the page and click *remove* twice, or in
  the sheet set that row's `removed` cell to `TRUE`. (Rows are never deleted by the page,
  so you keep a full record.)
- **Add a presenter yourself:** add a row in the Presenters tab. `slot` must be one of
  `pair1`, `pair2`, `pair3`, `pair4`, `oct16`, `dec1`, `dec11`; `both_dates` is TRUE/FALSE;
  `format` is `inperson` or `video`. Put any unique text in `id`.
- **Change dates or wording:** edit `index.html` (the `SLOTS` list near the top of the
  script holds the dates) and re-upload it to GitHub. Sign-ups in the sheet are unaffected.
- Sign-up for a date closes automatically on the day of the meeting.

## If something isn't working

- *"This page isn't connected to its sign-up list yet"* — the URL in `index.html` is empty
  or wrong. Re-check Part 2; the URL must end in `/exec`.
- *Sign-ups don't save for other people but work for you* — the deployment's "Who has
  access" is not set to **Anyone**. Deploy → Manage deployments → edit → change it.
- *You edited `Code.gs` and nothing changed* — Apps Script needs a new deployment after code
  changes: **Deploy → Manage deployments → pencil icon → Version: New version → Deploy**.
  The URL stays the same.

