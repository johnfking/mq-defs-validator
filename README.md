# mq-defs-validator

Validates [mq-definitions](https://github.com/macroquest/mq-definitions) LuaCATS annotations against the live MacroQuest runtime type system.

## What It Does

Compares every member of every MQ datatype (as registered in a running game instance) against the `@field` annotations in mq-definitions. Reports:

- **Missing** — members that exist at runtime but have no `@field` in the definitions
- **Stale** — `@field` entries in the definitions not found at runtime
- **Matched** — fully documented types

## Files

| File | Purpose |
|---|---|
| `gen_validate_script.py` | Generates the in-game Lua script with defs baked in; also generates markdown reports from results |
| `validate-defs.lua` | Auto-generated Lua script — run in-game to produce result JSON |
| `validation/` | Per-type markdown reports + `_summary.md` |

## Usage

### 1. Generate & run the in-game script

```bash
python gen_validate_script.py \
  --defs "C:/path/to/mq-definitions" \
  --lua  "C:/path/to/MacroQuest/lua"
```

Then in MacroQuest:
```
/lua run validate-defs
```

### 2. Generate markdown reports

```bash
python gen_validate_script.py --report --lua "C:/path/to/MacroQuest/lua"
```

Reports are written to `validation/`. See `validation/_summary.md` for the full overview.

## Requirements

- Python 3.9+ (no third-party packages needed)
- MacroQuest running in-game
- [mq-definitions](https://github.com/macroquest/mq-definitions) — clone it or install via the [zenithcodeforge.mq-defs](https://marketplace.visualstudio.com/items?itemName=zenithcodeforge.mq-defs) VS Code extension
