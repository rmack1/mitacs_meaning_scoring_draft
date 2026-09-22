# Meaning Test Coder

A single-file, no-backend scoring tool for the pre/intermediate/post meaning tests,
matching the same style as the Spelling & Story Coder. Everything runs client-side in the
browser — data is stored in `localStorage`, and you export CSV/JSON when you're ready.

This is a **separate site** from the Spelling & Story Coder — set it up as its own GitHub
repo (or its own folder within a repo, with its own GitHub Pages URL), since it uses
different data and its own browser storage.

## ⚠️ Before you use this for real data: fill in your rubric

I don't have your actual scoring rubric (the specific definitions and examples for scores
0/1/2/3 for each of your 12 words), so the tool currently ships with **placeholder text**,
clearly flagged with a ⚠️ warning icon in the interface. You have two options:

1. **Send me your rubric** (definition + example for each score 0–3, for each word) and
   I'll fill it in and give you an updated file.
2. **Edit it yourself** — open `index.html` in a text editor, find the `RUBRIC` object near
   the top of the `<script>` section (search for `RUBRIC_LEVELS` won't exist, search for
   `const RUBRIC = {}` instead), and replace each `definition` / `example` placeholder
   string. Every word already has an entry for scores 0–3 ready to fill in — for example:
   ```js
   RUBRIC["Sedan"] = [
     { score: 0, definition: "Your criteria for 0", example: "Your example response" },
     { score: 1, definition: "Your criteria for 1", example: "Your example response" },
     { score: 2, definition: "Your criteria for 2", example: "Your example response" },
     { score: 3, definition: "Your criteria for 3", example: "Your example response" }
   ];
   ```

## What it captures

- **Participant ID**
- **Pre-Meaning Test:** all 12 words, click each to see the rubric and select a score (0–3)
- **Intermediate Test — Story 1 / Story 2:** pick up to 4 target words per story, then for
  each: score against the rubric (0–3) and tick whether the participant remembered the
  target word from the story
- **Post-Meaning Test:** all 12 words, rubric score (0–3), plus a "Seen in PVT" checkbox
  and — if checked — which picture (1–4) the participant selected

## Publishing to GitHub Pages

1. Create a new GitHub repo (e.g. `meaning-test-coder`).
2. Add `index.html` to it.
3. In the repo settings, enable **GitHub Pages** for the `main` branch (root folder).
4. Your tool will be live at `https://<your-username>.github.io/<repo-name>/`

## Using it

1. Enter a Participant ID and click **Load / start participant**.
2. Score words in each section — click a word, review the rubric, click **Select** next
   to the score that fits.
3. For Story 1/2, pick your 4 target words first, then score just those.
4. For Post-Meaning, tick "Seen in PVT" and choose the picture number if applicable.
5. Export:
   - **Export this participant (CSV)** — one row for the current participant
   - **Export ALL participants (CSV)** — one row per participant, all combined
   - **Download full backup (JSON)** — everything in browser storage
   - **Restore from backup** — reload a JSON backup

## Notes

- Data lives only in the browser tied to the exact URL you use — always enter data through
  your one published GitHub Pages link, not downloaded local copies of the file, or data
  can appear to "go missing" across different local copies.
- The "Participants saved in this browser" panel shows exactly which participant IDs are
  currently stored, so you can verify nothing's missing before exporting.
- CSV export includes fixed columns for all 12 words across every section (blank where a
  word wasn't selected as a Story 1/2 target), so every participant's row lines up the
  same way for analysis.
