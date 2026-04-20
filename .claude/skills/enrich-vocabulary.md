---
description: Read words/phrases from input.md, enrich each with translations (EN↔ZH↔FR), definitions, and examples, append to the matching vocabulary file, clear the input, and push to git. Supports English, Mandarin, and French input.
---

# Enrich Vocabulary

Process words and phrases from `input.md`, enrich each one with translations and examples, append to the appropriate vocabulary file, clear the input, and push to git.

## Trigger

User runs `/enrich-vocabulary` or says something like "enrich vocabulary", "process my words", "process input".

## Steps

### 1. Read Input

Read `input.md`. Extract all lines under the `## Words to Process` section that are non-empty and not comment lines. If the section is empty, tell the user and stop.

### 2. Detect Language and Enrich

For each entry, detect the source language and generate the enriched content:

---

**If the entry is in English** (English word, phrase, or idiom):

Generate:
- Word/phrase as a level-2 heading with part of speech
- Date added
- Mandarin translation(s)
- French translation(s)
- Clear English definition
- 3 example sentences — one each in English 🇺🇸, Mandarin 🇨🇳, French 🇫🇷
- 2–4 common collocations or related phrases with Mandarin gloss

Use this format:
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

**If the entry is in Mandarin** (Chinese characters or a Chinese concept written in pinyin):

This means the user knows the concept in Mandarin but doesn't know how to express it naturally in English or French. Prioritize finding the most idiomatic, native-sounding English — avoid word-for-word literal translations.

Generate:
- Expression as heading
- Date added
- **English equivalents** ranked from most native/idiomatic to more literal (list 3–5 options, explain register differences)
- **French equivalents** (2–3 options)
- Context note explaining nuance, when/where to use it
- 3 example usages — Mandarin 🇨🇳, English 🇺🇸 (use the most natural expression), French 🇫🇷

Use this format:
```
## [expression]
> *Added: [YYYY-MM-DD]*

**English Equivalents** *(most idiomatic → more literal)*
1. [most native English expression] — [brief note on register/context]
2. [second option] — [note]
3. [third option] — [note]

**French Equivalents:**
- [French expression] — [note]
- [French expression] — [note]

**Context:** [When/how this expression is used; any cultural nuance]

**Examples:**
- 🇨🇳 [Mandarin sentence]
- 🇺🇸 [English — using the most natural expression]
- 🇫🇷 [French example]

---
```

---

**If the entry is in French** (French word or phrase):

Generate:
- Word/phrase as heading with part of speech and grammatical gender if a noun
- Date added
- Mandarin translation(s)
- English translation(s)
- Usage note or definition (can be in English)
- 3 example sentences — French 🇫🇷, English 🇺🇸, Mandarin 🇨🇳
- Register note (formal / informal / neutral / slang / literary)

Use this format:
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

### 3. Append to the Correct Vocabulary File

- English entries → append to `vocabulary/english.md`
- Mandarin entries → append to `vocabulary/mandarin.md`
- French entries → append to `vocabulary/french.md`

If the vocabulary file doesn't exist yet, create it with the appropriate header first.

### 4. Clear Input

Reset `input.md` to this exact content (preserve header, clear processed words):

```
# Vocabulary Input

Add words, phrases, or expressions you want to learn below — one per line.
Supported input languages: **English**, **Mandarin (中文)**, **French**.

Run the `enrich-vocabulary` skill to process this file.

---

## Words to Process

```

### 5. Git Commit and Push

Run the following commands:
```bash
git add -A
git commit -m "vocab: add $(echo '[comma-separated list of words processed]')"
git push
```

If `git push` fails because no remote is configured, commit the changes and tell the user they need to add a remote with `git remote add origin <url>` before pushing.

## Notes for the AI

- Use today's actual date for "Added" fields.
- For English equivalents of Mandarin, think like a native speaker — what would a native actually say? Avoid translationese.
- Keep example sentences natural and varied — don't repeat the same sentence structure.
- The user's mother language is Mandarin (Simplified Chinese). Mandarin explanations should be in Simplified Chinese.
