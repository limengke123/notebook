# Brady's Vocabulary Notebook

Learning **English** and **French**, with Mandarin as the base.

---

## English 🇺🇸

| Category | Description |
|---|---|
| [Adjectives](english/adjectives.md) | Describing words |
| [Adverbs](english/adverbs.md) | Modifiers |
| [Nouns](english/nouns.md) | People, places, things |
| [Verbs](english/verbs.md) | Actions and states |
| [Phrases & Idioms](english/phrases.md) | Multi-word expressions |

## French 🇫🇷

| Category | Description |
|---|---|
| [Adjectives](french/adjectives.md) | Adjectifs |
| [Adverbs](french/adverbs.md) | Adverbes |
| [Nouns](french/nouns.md) | Noms |
| [Verbs](french/verbs.md) | Verbes |
| [Phrases](french/phrases.md) | Expressions |

## Mandarin 🇨🇳

| Category | Description |
|---|---|
| [Expressions](mandarin/expressions.md) | 日常表达 — how to say a Chinese concept natively in English/French |
| [Idioms (成语)](mandarin/chengyu.md) | 4-character classical idioms |

---

## Workflow

1. Add words to `input.md` — one per line, any language
2. Run `/enrich-vocabulary` in Claude Code (or ask Cursor / Codex to "enrich vocabulary")
3. Each entry is enriched with translations and examples, saved to the right category file
4. `input.md` is cleared and changes are pushed automatically
5. This site rebuilds via GitHub Actions on every push
