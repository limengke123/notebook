# Vocabulary Notebook

A personal vocabulary learning repo for English and French, with Mandarin as the base language.
Add words to [`input.md`](./input.md), run the skill, and they land in the current month's vocabulary file.

The site is auto-built with MkDocs and published to **GitHub Pages** on every push.

> After setup: go to **Settings → Pages → Source** and select the `gh-pages` branch.

---

## Workflow

```
input.md  ──(run skill)──▶  vocabulary/english/2026-04.md
                        ├──▶  vocabulary/french/2026-04.md
                        └──▶  vocabulary/mandarin/2026-04.md
                                      │
                              git push to main
                                      │
                           GitHub Actions builds MkDocs
                                      │
                              GitHub Pages (gh-pages branch)
```

1. **Add words** to [`input.md`](./input.md) under `## Words to Process` — one per line, any language
2. **Run the skill** — AI detects language, enriches each entry, appends to this month's file
3. **`input.md` is cleared** automatically
4. Changes are **committed and pushed** automatically
5. **GitHub Actions** rebuilds the site and deploys to GitHub Pages

New month → new file created automatically. No config changes needed.

---

## Language Handling

| Input | What gets generated | Saved to |
|---|---|---|
| English | Mandarin + French (brief) + definition + collocations | `vocabulary/english/YYYY-MM.md` |
| 中文 Mandarin | Ranked native English expressions (idioms-first) + French | `vocabulary/mandarin/YYYY-MM.md` |
| Français French | Mandarin + English (brief) + register notes | `vocabulary/french/YYYY-MM.md` |

Cross-references are built-in: English entries always include a `**French:**` line; French entries always include an `**English:**` line.

---

## File Structure

```
vocabulary/
  english/
    2026-04.md      ← all English words added in April 2026
    2026-05.md      ← May (created automatically when needed)
  french/
    2026-04.md
  mandarin/
    2026-04.md
  index.md          ← MkDocs home page
input.md            ← Add words here
mkdocs.yml          ← Site config (nav auto-generated from files)
requirements.txt    ← mkdocs-material
.github/workflows/
  deploy.yml        ← Auto-build and deploy on push
```

---

## Running the Skill

**Claude Code:**
```
/enrich-vocabulary
```
or: `process my words`

**Cursor** (agent mode):
```
enrich vocabulary
```

**Codex:** picks up the workflow from `AGENTS.md` automatically.

---

## Local Preview

```bash
pip install -r requirements.txt
mkdocs serve
```

Then open `http://localhost:8000`.
