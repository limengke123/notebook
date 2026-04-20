# Brady's Vocabulary Notebook

Learning **English** and **French**, with Mandarin as the base.
Entries are organized by language and month — browse from the sidebar or use the search bar above.

---

## English 🇺🇸

Monthly files under the **English** section.
Each entry includes: Mandarin translation, French form, definition, example sentences, and collocations.

## French 🇫🇷

Monthly files under the **French** section.
Each entry includes: Mandarin translation, English form, usage notes, and register.

## Mandarin 🇨🇳

Monthly files under the **Mandarin** section.
Each entry lists native English equivalents (idioms-first) and French equivalents, with context notes in Chinese.

---

## Workflow

1. Add words to `input.md` — one per line, any language
2. Run `/enrich-vocabulary` in Claude Code (or ask Cursor / Codex)
3. Each entry is enriched and saved to the **current month's file** for that language
4. `input.md` is cleared and changes are pushed automatically
5. This site rebuilds via GitHub Actions on every push
