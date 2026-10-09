# Daily Spend Tracker (GitHub Pages + auto CSV sync)

A responsive expense tracker (phone, tablet, desktop). Every change is saved to
your browser **and** auto-committed to a CSV file in a GitHub repo. On load, and
every minute, it fetches the latest CSV so all your devices show the same spend.

## 1. Host the website (GitHub Pages)

1. Create a repo, e.g. `spend-tracker`. Upload `index.html` to it.
2. Repo **Settings → Pages → Build and deployment → Source: Deploy from a branch**,
   choose `main` / `(root)` → Save.
3. Your site will be live at `https://<username>.github.io/spend-tracker/`.

> Free GitHub Pages needs a **public** repo. Do not store your spend data there.

## 2. Create a private data repo

1. Create a **private** repo, e.g. `spend-data`.
2. Upload `data/expenses.csv` to it (or leave it out; the app creates it).

## 3. Create an access token

1. GitHub → **Settings → Developer settings → Personal access tokens → Fine-grained tokens → Generate**.
2. Repository access: **Only select repositories → spend-data**.
3. Permissions: **Contents → Read and write**. Nothing else.
4. Copy the token (`github_pat_...`).

## 4. Connect

Open your site → **⚙️ GitHub** → enter owner, repo (`spend-data`), branch (`main`),
path (`data/expenses.csv`), paste the token → **Save & Connect**.
Repeat once on each device. The token stays in that browser only.

## How sync works

- Add/edit/delete → saved locally at once → pushed to GitHub ~1.5 s later (a commit per change).
- Opening the app, returning to the tab, or going back online → pulls the latest CSV.
- Offline changes are kept and pushed when you're back online.
- Rows added on another device are merged in; if the same row is edited on two devices, the device that syncs last wins.
- Without a token the app is read-only (works for public data repos).

## CSV format

`id,date,category,amount,note` — editable in any spreadsheet app or directly on GitHub.

## Auto-connect (no login page)

- Enter owner, repo, branch, path and token **once** and tap Save & Connect.
- They are saved in your browser and the app reconnects and fetches your CSV automatically every time you open it.
- Repeat the one-time setup on each device (phone, tablet, PC).
- To change repo or token, tap **GitHub** and save again, or **Disconnect** to remove them.
- The token is stored in your browser's local storage, so use a fine-grained token limited to the data repo (Contents: read/write) and keep the data repo private.
