---
description: Read words/phrases from input.md, detect language (EN/ZH/FR), enrich with translations and examples, append to the current month's vocabulary file (e.g. vocabulary/english/2026-04.md), clear input.md, and push to git.
---

# Enrich Vocabulary

Process words and phrases from `input.md`, enrich each one with translations and examples, save to the current month's file for that language, clear input, and push to git.

## Trigger

User runs `/enrich-vocabulary` or says "enrich vocabulary", "process my words", "process input".

## Steps

### 1. Read Input

Read `input.md`. Extract all non-empty lines under `## Words to Process`. If empty, tell the user and stop.

### 2. Detect Language and Target File

For each entry, determine the language. All entries this month go into the same monthly file:

| Language | Target file |
|---|---|
| English | `vocabulary/english/[YYYY-MM].md` |
| French | `vocabulary/french/[YYYY-MM].md` |
| Mandarin | `vocabulary/mandarin/[YYYY-MM].md` |

Use today's actual date to determine `YYYY-MM` (e.g., April 2026 → `2026-04`).

If the target file doesn't exist yet, create it with the header:
`# English — [Month Year]` (or French / Mandarin equivalent, e.g. `# French — April 2026`, `# Mandarin — April 2026`)

### 3. Generate Enriched Content

---

**If English:**

```
## [word/phrase] ([part of speech])
> *Added: [YYYY-MM-DD]*

**Mandarin:** [translation]
**French:** [translation]

**Definition:** [concise definition]

**Examples:**
- 🇺🇸 [English sentence]
- 🇨🇳 [Mandarin sentence]
- 🇫🇷 [French sentence]

**Phrases & Collocations:**
- [collocation]: [Mandarin gloss]
- [collocation]: [Mandarin gloss]

---
```

---

**If Mandarin:**

The user knows this concept in Mandarin but wants to express it naturally in English (primary) and French. Prioritize idiomatic, native-sounding English — avoid literal translations.

```
## [expression]
> *Added: [YYYY-MM-DD]*

**English Equivalents** *(most idiomatic → more literal)*
1. [most native English expression] — [register/context note]
2. [second option] — [note]
3. [third option] — [note]

**French Equivalents:**
- [French expression] — [note]
- [French expression] — [note]

**Context:** [用中文解释：使用场景、语气、文化背景]

**Examples:**
- 🇨🇳 [Mandarin sentence]
- 🇺🇸 [English — most natural expression]
- 🇫🇷 [French example]

---
```

---

**If French:**

```
## [word/phrase] ([part of speech][, gender])
> *Added: [YYYY-MM-DD]*

**Mandarin:** [translation]
**English:** [translation]

**Note:** [usage note or definition]

**Examples:**
- 🇫🇷 [French sentence]
- 🇺🇸 [English sentence]
- 🇨🇳 [Mandarin sentence]

**Register:** [formal / informal / neutral / slang / literary]

---
```

---

### 4. Append to the Target File

Append the enriched entry to the monthly file determined in Step 2.

### 5. Clear Input

Reset `input.md` to this exact content:

```
# Vocabulary Input

Add words, phrases, or expressions you want to learn below — one per line.
Supported input languages: **English**, **Mandarin (中文)**, **French**.

Run the `enrich-vocabulary` skill to process this file.

---

## Words to Process

```

### 6. Git Commit and Push

```bash
git add -A
git commit -m "vocab: add [comma-separated list of words processed]"
git push
```

If push fails because no remote is configured, commit and tell the user to run `git remote add origin <url>`.

## Notes

- Use today's actual date for "Added" fields and to determine the monthly file name.
- For Mandarin → English: think like a native speaker. Avoid translationese.
- Keep example sentences natural and varied.
- Mandarin context explanations must be in Simplified Chinese.
- Cross-references are built into the format: English entries include a `**French:**` line; French entries include an `**English:**` line (brief form only, not a full entry).
