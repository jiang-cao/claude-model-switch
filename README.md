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
When you switch models with `cms`, the selected model automatically appears in Claude Code's built-in interactive `/model` selection menu:
```bash
# First switch model with cms
cms kimi
# ✅ Switches to: kimi-k2.6

# Now run /model in Claude Code CLI
/model
# The menu will show:
#  5. kimi-k2.6              Custom model
# ❯6. doubao-seed-2.0-pro ✔  Current model
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
- The tool updates `~/.claude/settings.json` automatically
- For changes to apply immediately in your current shell, run the export command shown after switching
- Install `jq` for safer JSON editing (recommended)
