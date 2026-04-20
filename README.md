# Vocabulary Notebook

A personal vocabulary learning repo for English and French, with Mandarin as the base language.
Add words to [`input.md`](./input.md), run the skill, and they land in structured vocabulary files with translations and examples.

The site is auto-built with MkDocs and published to **GitHub Pages** on every push.

> After forking or setting up: go to **Settings → Pages → Source** and select the `gh-pages` branch.

---

## Workflow

```
input.md  ──(run skill)──▶  vocabulary/english/adjectives.md
                        ├──▶  vocabulary/english/verbs.md
                        ├──▶  vocabulary/french/nouns.md
                        ├──▶  vocabulary/mandarin/expressions.md
                        └──▶  ... (routed by language + part of speech)
                                      │
                              git push to main
                                      │
                           GitHub Actions builds MkDocs
                                      │
                              GitHub Pages (gh-pages branch)
```

1. **Add words** to [`input.md`](./input.md) under `## Words to Process` — one per line, any language
2. **Run the skill** — AI detects language and part of speech, enriches each entry, saves to the right file
3. **`input.md` is cleared** automatically; enriched entries appear in the vocabulary files
4. Changes are **committed and pushed** automatically
5. **GitHub Actions** builds the MkDocs site and deploys to GitHub Pages

---

## Language Handling

| Input | What gets generated | Saved to |
|---|---|---|
| English | Mandarin + French (brief) + definition + collocations | `vocabulary/english/[pos].md` |
| 中文 Mandarin | Ranked native English expressions (idioms-first) + French | `vocabulary/mandarin/expressions.md` or `chengyu.md` |
| Français French | Mandarin + English (brief) + register notes | `vocabulary/french/[pos].md` |

Cross-references are built-in: English entries always include a `**French:**` line; French entries always include an `**English:**` line.

---

## File Structure

```
vocabulary/
  english/
    adjectives.md
    adverbs.md
    nouns.md
    verbs.md
    phrases.md
  french/
    adjectives.md
    adverbs.md
    nouns.md
    verbs.md
    phrases.md
  mandarin/
    expressions.md
    chengyu.md
  index.md            ← MkDocs home page
input.md              ← Add words here
mkdocs.yml            ← Site config
requirements.txt      ← mkdocs-material
.github/workflows/
  deploy.yml          ← Auto-build on push
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
