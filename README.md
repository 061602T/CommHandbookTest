# Committee Handbook Assistant — Live Test Build (matches the real click-through demo)

Built directly on the `committee-handbook-clickthrough` file you uploaded — same amber
hero, teal section bars, real NYC Bar logo/favicon, same accordion layout, same launcher
and chat panel design. Two things changed from that original file:

1. The widget's `<script>` block — the hardcoded PRESETS click-through answers are gone,
   replaced with a real, grounded call to the Anthropic API.
2. The static accordion text itself — updated to match the current handbook, so the page
   and the live chatbot no longer contradict each other. Specifically:
   - Every "Stephanie Glazer" contact → **Committee Membership** (committeemembership@nycbar.org)
   - **Maria Cilenti** → **Mary Margulis-Ohnuma**, Senior Policy Counsel (mmargulis-ohnuma@nycbar.org, 212-382-6767)
   - Removed the stale AV/room-setup contact (events@nycbar.org); folded catering billing
     questions into Linda Kemble's existing line
   - "Program Reservation Form" → **Event Reservation Request Form**
   - "CLE Program Questionnaire" → **CLE Proposal Form** (updated URL)
   - Op-ed limit 650 → **750 words**; letter to the editor 150 → **250 words**
   - CLE on-demand retention "about one year" → **approximately two years**
   - CLE Program Approval section rewritten to match the current 6-step planning process
     (4–6 months out for CLE programs, ~1 year for conferences) — the old May/Oct/April
     seasonal-deadline structure no longer exists in the handbook
   - Removed the now-nonexistent $499/$399 CLE pricing tiers (the handbook now just says
     the City Bar reserves the right to set CLE fees)
   - City Bar Center Accreditations corrected: NY is an accredited provider for
     live/livestream/on-demand specifically; CA/NJ/PA are "fully accredited" — a real
     distinction in the current handbook text

   Left alone, confirmed still accurate: the $15 gift-law threshold, the 25-person
   "widely attended event" threshold, the $75/hr four-hour-minimum recording fee, the
   two-week recording-request lead time, and the "10 days" vs "10 business days" catering
   wording (both genuinely appear that way in two different sections of the source
   handbook — not an inconsistency I introduced).

Internal QA tool only. Not connected to NYC Bar's production system.

## What this is
Two files:
- `index.html` — the full branded handbook page (hero, accordions, footer, the launcher
  button and chat panel), content current, with the live-API widget script embedded
- `handbook.md` — the full updated handbook content, fetched by the widget on page load
  and sent as grounding context on every question

## Setup (GitHub Pages)

1. Create a **new repository** on GitHub. Recommend private if your plan supports Pages
   on private repos (GitHub Pro/Team/Enterprise) — on GitHub Free, Pages only works on
   public repos, so the site is reachable by anyone with the URL even if unlisted.
2. Add both files to the repo root — "Add file → Upload files" in the GitHub web UI, or:
   ```
   git init
   git add index.html handbook.md
   git commit -m "Add live handbook test build"
   git branch -M main
   git remote add origin https://github.com/<your-username>/<repo-name>.git
   git push -u origin main
   ```
3. Repo → **Settings → Pages** → Source: "Deploy from a branch" → Branch: `main`,
   folder `/ (root)` → Save.
4. You'll get a URL like `https://<your-username>.github.io/<repo-name>/`. Takes a
   minute or two to go live the first time.

## Using it
1. Open the URL — the amber hero, handbook accordions, and a teal "Ask the Handbook"
   button (bottom-right) render immediately.
2. Click the launcher, paste an Anthropic API key into the field under the disclaimer,
   click "Use key."
3. Ask questions, or click one of the four starter chips. Each question is a live,
   grounded call using that key's usage. "New chat" clears conversation memory. The key
   is never written to the page or the repo — closing the tab clears it.

## Cost note
Every question run through this — including all 500 in the test set — uses real,
billed API usage on whatever key you enter. There's no free tier here.

## Security note
Never commit an API key into this repo or hardcode it into the page. Anything in a
GitHub Pages site is visible to anyone with the URL. The key-prompt design is
intentional — keep it that way.
