## Plugin Submission Details
- **Plugin Name:** `YourPluginName`
- **Version:** `1.0.0`
- **Submission Type:**
  - [ ] New Plugin
  - [ ] Plugin Update
  - [ ] Bug Fix

## Description
Briefly describe what this plugin adds or changes in the mother program:

## Folder Structure Checklist
Make sure your files are placed inside `src/<YourPluginName>/` like this:
```text
src/
└── YourPluginName/
    ├── main.cpp        (or multiple .cpp/.h files)
    └── plugin.json
```

### Example `plugin.json`
```json
{
  "name": "YourPluginName",
  "version": "1.0.0",
  "author": "YourGitHubUsername",
  "description": "A short summary of what your plugin does."
}
```

## Security & Build Checklist
- [ ] My code is placed inside `src/<YourPluginName>/` and matches the plugin name.
- [ ] I have **not** included any pre-compiled binaries (`.exe`, `.dll`, `.so`) or scripts.
- [ ] My code does **not** spawn external processes (`CreateProcess`, `system`, `ShellExecute`, `fork`, etc.) or download external executables.
- [ ] My `plugin.json` contains valid JSON with `name`, `version`, `author`, and `description`.
- [ ] All automated GitHub Action checks pass on this Pull Request.
