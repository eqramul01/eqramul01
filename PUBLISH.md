# Publishing your GitHub profile — step by step

Everything below runs in your terminal. You already have `git` + `gh` authenticated,
so this is a clean path. Run the blocks in order.

The folder `github-profile-eqramul01/` contains:
- `README.md`     — your profile landing page
- `assets/banner.png` — the "Building Bots, With Justice" banner

GitHub shows a special repo named exactly after your username (`eqramul01/eqramul01`)
as your profile landing page. That is the repo we are creating.

---

## Step 0 — Check the profile repo doesn't already exist

```bash
gh repo view eqramul01/eqramul01 >/dev/null 2>&1 \
  && echo "EXISTS — use Step 3B" \
  || echo "DOES NOT EXIST — use Step 3A"
```

---

## Step 1 — Go to the folder

```bash
cd ~/GLOBAL_Resume/github-profile-eqramul01
```

## Step 2 — Initialize the repository

```bash
git init -b main
git add README.md assets/banner.png
git commit -m "Profile README: lawyer-developer landing page"
```

## Step 3A — Create the profile repo and push  (if Step 0 said DOES NOT EXIST)

```bash
gh repo create eqramul01 \
  --public \
  --source=. \
  --remote=origin \
  --push \
  --description "Profile landing page — Eqramul Chowdhury, J.D."
```

## Step 3B — Push to the existing profile repo  (if Step 0 said EXISTS)

```bash
git remote add origin https://github.com/eqramul01/eqramul01.git
git push -u origin main --force-with-lease
```

---

## Step 4 — Update your profile sidebar (bio, website, "available for hire")

The sidebar next to your avatar is set on your account, not in the repo.
Set it from the CLI:

```bash
gh api --method PATCH /user \
  -f bio="Lawyer-developer (J.D.). I build private, multimodal AI/RAG systems for legal operations and litigation document management." \
  -f blog="https://chowdhuryselfrep.com" \
  -f location="Broward County, FL" \
  -F hireable=true
```

## Step 5 — Confirm your pinned repositories

Pinning is the one thing GitHub does **not** expose to the CLI — it is a web action.
Your three repos are already pinned. To match the order in the README's pipeline table:

1. Open https://github.com/eqramul01
2. In the "Pinned" section, click **Customize your pins**
3. Confirm exactly these three, in this order:
   1. `Desktop-Organization-ChowdhurySelfRep`   (intake & organize)
   2. `GLOBAL-Old_Firm_RAG_Query`               (index the matter archive)
   3. `GLOBAL-email-RAG-gemini`                 (search the correspondence)
4. Save. Drag to reorder if needed.

This keeps the 600+ forks off your landing page and makes the three real
projects the story.

## Step 6 — Verify

```bash
open https://github.com/eqramul01
```

Check: banner image loads, the pipeline table links resolve, the bio and
website show in the sidebar, and the three pinned repos appear in order.
