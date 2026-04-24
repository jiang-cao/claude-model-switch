# claude-model-switch (cms)
🔁 Tiny Bash utility to quickly switch models in Claude Code CLI via multi-term fuzzy search.

## Usage
Run `cms <search-terms...>` to switch models. The tool will match models that contain **all** your search terms.

### Examples:

```bash
# Exact match (or unique search term)
cms deepseek
# ✅ Switches to: deepseek-v3.2

# Single search: match models with "glm"
cms glm
# ❌ Multiple matches: glm-5.1, glm-4.7 (add more terms to narrow down)

# Double search: match models with both "doubao" and "pro"
cms doubao pro
# ✅ Switches to: doubao-seed-2.0-pro
```

### Integration with Claude Code's `/model` command
When you switch models with `cms`:
1. **New/restarted Claude CLI sessions**: Automatically use the new model by default
2. **Active (already running) CLI sessions**: The new model appears in the `/model` selection list, and you can select it to switch immediately in the current session

```bash
# First switch model with cms
cms kimi
# ✅ Switches to: kimi-k2.6 (updates ~/.claude/settings.json persistently)

# Now run /model in an active Claude Code CLI session
/model
# The menu will show your selected model:
#  5. kimi-k2.6              Custom model
# Select it to activate immediately in the current session
```

## Available Models
```
doubao-seed-2.0-code
doubao-seed-2.0-pro
minimax-m2.7
glm-5.1
glm-4.7
deepseek-v3.2
kimi-k2.6
```

## Updating Model List
The available models depend on the coding plan you have purchased. Please check your vendor's documentation for the exact model names. To update the model list, simply edit the `MODELS` array in the `claude-model-switch` script.

## Notes
- The tool updates `~/.claude/settings.json` automatically, so changes are persistent across system restarts
- For changes to apply immediately in your current shell, you can either run the export command shown after switching, or use the `/model` command in Claude Code CLI to select the new model
- Install `jq` for safer JSON editing (recommended)
