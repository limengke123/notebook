# Vocabulary Enrichment Agent

This repository is a personal vocabulary learning notebook. The primary workflow is:

1. User adds words/phrases to `input.md` under `## Words to Process`
2. The agent enriches each entry and saves it to the appropriate file in `vocabulary/`
3. The agent clears `input.md` and pushes the changes

---

## When the User Asks to Enrich Vocabulary

Follow these steps exactly:

### Step 1 — Read `input.md`

Read `input.md` and extract all non-empty lines under `## Words to Process`. If the section is empty, say so and stop.

### Step 2 — Detect Language and Enrich Each Entry

**English entries** → `vocabulary/english.md`

For each English word or phrase, generate:
- Heading: `## [word] ([part of speech])`
- Date line: `> *Added: [YYYY-MM-DD]*`
- `**Mandarin:** [translation] ([pinyin])`
- `**French:** [translation]`
- `**Definition:** [concise English definition]`
- **Examples:** one sentence each in 🇺🇸 English, 🇨🇳 Mandarin, 🇫🇷 French
- **Phrases & Collocations:** 2–4 common collocations with Mandarin gloss
- Separator: `---`

**Mandarin entries** → `vocabulary/mandarin.md`

The user knows the concept in Chinese but wants to know how to say it naturally in English and French.

For each Mandarin word or expression, generate:
- Heading: `## [expression] ([pinyin])`
- Date line: `> *Added: [YYYY-MM-DD]*`
- **English Equivalents** — ranked most-idiomatic to most-literal, 3–5 options, each with a register/context note. Prioritize expressions a native English speaker would actually use.
- **French Equivalents** — 2–3 options with notes
- **Context:** nuance and usage explanation in Chinese (Simplified)
- **Examples:** 🇨🇳 Mandarin, 🇺🇸 English (most natural expression), 🇫🇷 French
- Separator: `---`

**French entries** → `vocabulary/french.md`

For each French word or phrase, generate:
- Heading: `## [word] ([part of speech][, gender if noun])`
- Date line: `> *Added: [YYYY-MM-DD]*`
- `**Mandarin:** [translation] ([pinyin])`
- `**English:** [translation]`
- `**Note:** [usage note or definition]`
- **Examples:** one sentence each in 🇫🇷 French, 🇺🇸 English, 🇨🇳 Mandarin
- `**Register:** [formal / informal / neutral / slang / literary]`
- Separator: `---`

### Step 3 — Append to Vocabulary Files

Append each enriched entry to the appropriate file. Do not overwrite existing entries.

### Step 4 — Reset `input.md`

Replace the content of `input.md` with:

```
# Vocabulary Input

Add words, phrases, or expressions you want to learn below — one per line.
Supported input languages: **English**, **Mandarin (中文)**, **French**.

Run the `enrich-vocabulary` skill to process this file.

---

## Words to Process

```

### Step 5 — Git Commit and Push

```bash
git add -A
git commit -m "vocab: add [comma-separated list of words]"
git push
```

If the push fails due to no remote, commit and notify the user.

---

## User Context

- Mother language: Mandarin (Simplified Chinese)
- Learning: English (primary) and French (secondary)
- Mandarin explanations should be in Simplified Chinese
- For English equivalents of Mandarin concepts, think like a native speaker — avoid translationese
