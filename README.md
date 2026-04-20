# Vocabulary Notebook

A personal vocabulary learning repo for English and French, with Mandarin as the base language.
Add words to [`input.md`](./input.md), run the skill, and they land in structured vocabulary files with translations and examples.

---

## Workflow

```
input.md  ──(run skill)──▶  vocabulary/english.md
                        ├──▶  vocabulary/french.md
                        └──▶  vocabulary/mandarin.md
```

1. **Add words** to [`input.md`](./input.md) under `## Words to Process` — one per line, any language
2. **Run the skill** — Claude/Cursor/Codex detects the language, enriches each entry, and saves it
3. **`input.md` is cleared** automatically; enriched entries appear in the vocabulary files
4. Changes are **committed and pushed** automatically

---

## Language Handling

| Input language | What gets generated | Saved to |
|---|---|---|
| English | Mandarin (with pinyin) + French + definition + collocations | [`vocabulary/english.md`](./vocabulary/english.md) |
| 中文 Mandarin | Ranked native English expressions (idioms-first) + French + context notes in Chinese | [`vocabulary/mandarin.md`](./vocabulary/mandarin.md) |
| Français French | Mandarin + English + register notes | [`vocabulary/french.md`](./vocabulary/french.md) |

---

## Files

| File | Description |
|---|---|
| [`input.md`](./input.md) | Add words here, one per line |
| [`vocabulary/english.md`](./vocabulary/english.md) | English words with ZH + FR translations |
| [`vocabulary/french.md`](./vocabulary/french.md) | French words with ZH + EN translations |
| [`vocabulary/mandarin.md`](./vocabulary/mandarin.md) | Mandarin expressions with native EN + FR equivalents |
| [`.claude/skills/enrich-vocabulary.md`](./.claude/skills/enrich-vocabulary.md) | Skill definition for Claude Code |
| [`AGENTS.md`](./AGENTS.md) | Agent instructions for Codex |
| [`.cursor/rules/enrich-vocabulary.mdc`](./.cursor/rules/enrich-vocabulary.mdc) | Rule for Cursor |

---

## How to Run

**Claude Code**
```
/enrich-vocabulary
```
or just say: `process my words`

**Cursor** — open Agent mode and say:
```
enrich vocabulary
```

**Codex** — the agent picks up the workflow from `AGENTS.md` automatically.
