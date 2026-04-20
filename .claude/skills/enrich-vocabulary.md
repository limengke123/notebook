---
description: Read words/phrases from input.md, detect language and part of speech, enrich with translations (EN↔ZH↔FR) and examples, append to the correct category file under vocabulary/, clear input.md, and push to git.
---

# Enrich Vocabulary

Process words and phrases from `input.md`, enrich each one with translations and examples, save to the correct category file, clear input, and push to git.

## Trigger

User runs `/enrich-vocabulary` or says "enrich vocabulary", "process my words", "process input".

## Steps

### 1. Read Input

Read `input.md`. Extract all non-empty lines under `## Words to Process`. If empty, tell the user and stop.

### 2. Detect Language, Part of Speech, and Target File

For each entry, determine:
- **Language**: English / Mandarin / French
- **Part of speech** (for English and French): noun, verb, adjective, adverb, phrase/idiom
- **Target file** (see routing table below)

#### File Routing

**English entries:**
| Part of speech | File |
|---|---|
| noun | `vocabulary/english/nouns.md` |
| verb | `vocabulary/english/verbs.md` |
| adjective | `vocabulary/english/adjectives.md` |
| adverb | `vocabulary/english/adverbs.md` |
| phrase, idiom, phrasal verb, expression, or multi-word | `vocabulary/english/phrases.md` |
| ambiguous / multiple (e.g. "verb / noun") | use the first/primary part of speech |

**French entries:**
| Part of speech | File |
|---|---|
| noun (nom) | `vocabulary/french/nouns.md` |
| verb (verbe) | `vocabulary/french/verbs.md` |
| adjective (adjectif) | `vocabulary/french/adjectives.md` |
| adverb (adverbe) | `vocabulary/french/adverbs.md` |
| phrase, expression | `vocabulary/french/phrases.md` |

**Mandarin entries:**
| Type | File |
|---|---|
| 成语 (4-character classical idiom) | `vocabulary/mandarin/chengyu.md` |
| all other expressions | `vocabulary/mandarin/expressions.md` |

### 3. Generate Enriched Content

---

**If English:**

Generate:
- Word/phrase as a level-2 heading with part of speech
- Date added
- Mandarin translation(s) — brief, primary meaning(s)
- French translation(s) — brief form, matches the part of speech
- Clear English definition
- 3 example sentences — one each in 🇺🇸 English, 🇨🇳 Mandarin, 🇫🇷 French
- 2–4 common collocations or related phrases with Mandarin gloss

Format:
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

The user knows this concept in Mandarin but wants to express it naturally in English (primary) and French. Prioritize idiomatic, native-sounding English — avoid word-for-word literal translations.

Generate:
- Expression as heading
- Date added
- English equivalents ranked most-idiomatic → most-literal (3–5 options, each with a register/context note)
- French equivalents (2–3 options with notes)
- Context explanation in Simplified Chinese
- 3 example usages

Format:
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

Generate:
- Word/phrase as heading with part of speech and grammatical gender if a noun
- Date added
- Mandarin translation(s)
- English translation(s) — brief, matches part of speech
- Usage note or definition
- 3 example sentences — French 🇫🇷, English 🇺🇸, Mandarin 🇨🇳
- Register note (formal / informal / neutral / slang / literary)

Format:
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

Append the enriched entry to the file determined in Step 2. If the file doesn't exist, create it with the appropriate language/category header first.

If the mkdocs.yml nav does not yet include the new file, add it under the correct section.

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

- Use today's actual date for "Added" fields.
- For Mandarin → English: think like a native speaker. What would someone actually say? Avoid translationese.
- Keep example sentences natural and varied in structure.
- The user's mother language is Mandarin Simplified Chinese. Context explanations for Mandarin entries should be written in Simplified Chinese.
- Cross-references are built into the format: English entries always include a French field, French entries always include an English field — keep these brief (just the form, not a full entry).
