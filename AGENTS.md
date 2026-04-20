# Vocabulary Enrichment Agent

This repository is a personal vocabulary learning notebook. The primary workflow:

1. User adds words/phrases to `input.md` under `## Words to Process`
2. Agent enriches each entry and saves it to the correct category file in `vocabulary/`
3. Agent clears `input.md` and pushes the changes
4. GitHub Actions auto-builds the MkDocs site and deploys to GitHub Pages

---

## When the User Asks to Enrich Vocabulary

### Step 1 — Read `input.md`

Extract all non-empty lines under `## Words to Process`. If empty, say so and stop.

### Step 2 — Detect Language, Part of Speech, and Target File

**English entries — file routing by part of speech:**
| Part of speech | File |
|---|---|
| noun | `vocabulary/english/nouns.md` |
| verb | `vocabulary/english/verbs.md` |
| adjective | `vocabulary/english/adjectives.md` |
| adverb | `vocabulary/english/adverbs.md` |
| phrase, idiom, phrasal verb | `vocabulary/english/phrases.md` |

**French entries — same mapping under `vocabulary/french/`**

**Mandarin entries:**
| Type | File |
|---|---|
| 成语 (4-character idiom) | `vocabulary/mandarin/chengyu.md` |
| all other expressions | `vocabulary/mandarin/expressions.md` |

### Step 3 — Generate Content

**English** → `vocabulary/english/[pos].md`
```
## [word] ([part of speech])
> *Added: [YYYY-MM-DD]*

**Mandarin:** [translation]
**French:** [translation]

**Definition:** [concise English definition]

**Examples:**
- 🇺🇸 [English sentence]
- 🇨🇳 [Mandarin sentence]
- 🇫🇷 [French sentence]

**Phrases & Collocations:**
- [collocation]: [Mandarin gloss]
- [collocation]: [Mandarin gloss]

---
```

**Mandarin** → `vocabulary/mandarin/[type].md`

User knows this in Chinese; wants to express it naturally in English (primary) and French. Prioritize idiomatic over literal English.
```
## [expression]
> *Added: [YYYY-MM-DD]*

**English Equivalents** *(most idiomatic → more literal)*
1. [most native expression] — [register note]
2. [second option] — [note]
3. [third option] — [note]

**French Equivalents:**
- [expression] — [note]
- [expression] — [note]

**Context:** [用中文解释使用场景和语气]

**Examples:**
- 🇨🇳 [Mandarin sentence]
- 🇺🇸 [English — most natural]
- 🇫🇷 [French example]

---
```

**French** → `vocabulary/french/[pos].md`
```
## [word] ([part of speech][, gender])
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

### Step 4 — Append to Target File

Append to the correct file. If the file doesn't exist, create it with an appropriate header.

### Step 5 — Reset `input.md`

```
# Vocabulary Input

Add words, phrases, or expressions you want to learn below — one per line.
Supported input languages: **English**, **Mandarin (中文)**, **French**.

Run the `enrich-vocabulary` skill to process this file.

---

## Words to Process

```

### Step 6 — Git Commit and Push

```bash
git add -A
git commit -m "vocab: add [comma-separated list of words]"
git push
```

---

## User Context

- Mother language: Mandarin Simplified Chinese
- Learning: English (primary) and French (secondary)
- Context notes for Mandarin entries must be in Simplified Chinese
- For Mandarin → English: always use what a native speaker would naturally say, not literal translations
- Cross-references are built into every entry: English entries always include a `**French:**` line; French entries always include an `**English:**` line (brief form only, not a full entry)
