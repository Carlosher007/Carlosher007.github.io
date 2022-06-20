---
layout: single
title: Configuración de Visual Studio Code
excerpt: 'Recursos y Configuración'
date: 2022-04-24
classes: wide
header:
  teaser: /assets/images/ejercicios-c++.png
  teaser_home_page: true
  icon: https://symbols.getvecta.com/stencil_25/38_java.bc46b9254c.png
categories:
  - Personalización y Configuración
tags:
  - Visual Studio Code
---

## Plugins

- Better C++ Syntax
- Better Comments
- C/C++
- C++ Intellisense
- Code Runner
- Color Picker
- Comunity Material Theme
- GitLens
- indent-rainbow
- Material Icon Theme
- Material Theme
- One dark pro
- Prettier
- Reload
- Spanish Language

## Fuentes usadas
- [Fira Code](https://fonts.google.com/specimen/Fira+Code)
- [Meslo NF](https://eng.m.fontke.com/font/23395516/download/)

## Settings.json

- En configuracion escribes **setting.json**, bajas y le das __Edit in settings.json__

```json
{
  // Numero de tabs
  "editor.tabSize": 2,
  // Salto de linea automatico
  "editor.wordWrap": "on",
  // Para que emmet funcione en codigo jsx
  "emmet.includeLanguages": {
    "javascript": "javascriptreact"
  },
  // Otras..
  "workbench.settings.editor": "json",
  "editor.formatOnPaste": true,
  "editor.formatOnSave": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "files.autoSave": "afterDelay",
  "workbench.iconTheme": "material-icon-theme",
  // "editor.fontFamily": "CaskaydiaCove Nerd Font",
  "editor.fontFamily": "Fira Code",
  "editor.fontLigatures": true,
  "editor.fontSize": 18,

  // "editor.fontWeight": "300", // Light
  "editor.fontWeight": "400", // Regular
  // "editor.fontWeight": "500", // Medium
  // "editor.fontWeight": "600", // Bold

  "editor.lineHeight": 38,
  "editor.letterSpacing": 0.4,
  "files.trimTrailingWhitespace": true,
  "prettier.eslintIntegration": true,
  "editor.cursorStyle": "line",
  "editor.cursorWidth": 0,
  "editor.cursorBlinking": "phase",
  "editor.renderWhitespace": "all",

  "prettier.arrowParens": "always",
  "prettier.bracketSpacing": true,
  "prettier.embeddedLanguageFormatting": "auto",
  "prettier.htmlWhitespaceSensitivity": "css",
  "prettier.insertPragma": false,
  "prettier.jsxBracketSameLine": false,
  "prettier.jsxSingleQuote": false,
  "prettier.printWidth": 80,
  "prettier.proseWrap": "preserve",
  "prettier.quoteProps": "as-needed",
  "prettier.requirePragma": false,
  "prettier.semi": true,
  "prettier.singleQuote": true,
  "prettier.tabWidth": 2,
  "prettier.trailingComma": "es5",
  "prettier.useTabs": false,
  "prettier.vueIndentScriptAndStyle": false,
  "terminal.integrated.sendKeybindingsToShell": true,
  "terminal.integrated.fontFamily": "MesloLGSDZ NF",
  "terminal.integrated.fontSize": 15,
  "terminal.integrated.fontWeight": "normal",
  "workbench.colorTheme": "Material Theme Palenight High Contrast",
  "workbench.editorAssociations": {
    "*.ipynb": "jupyter-notebook"
  },
  "tabnine.experimentalAutoImports": true,
  "editor.linkedEditing": true,
  "todo-tree.tree.showScanModeButton": false,
  "liveServer.settings.donotVerifyTags": true,
  "gitlens.defaultDateFormat": null,
  "gitlens.hovers.currentLine.over": "line",
  "gitlens.defaultDateShortFormat": null,
  "gitlens.defaultTimeFormat": null,
  "gitlens.defaultDateStyle": "absolute",
  "explorer.confirmDragAndDrop": false,
  "notebook.cellToolbarLocation": {
    "default": "right",
    "jupyter-notebook": "left"
  },
  "editor.suggestSelection": "first",
  "vsintellicode.modify.editor.suggestSelection": "automaticallyOverrodeDefaultValue",
  "files.exclude": {
    "**/.classpath": true,
    "**/.project": true,
    "**/.settings": true,
    "**/.factorypath": true
  },
  "liveServer.settings.ChromeDebuggingAttachment": false,
  "liveServer.settings.AdvanceCustomBrowserCmdLine": "",
  "javascript.updateImportsOnFileMove.enabled": "always",
  "[python]": {
    "editor.defaultFormatter": "ms-python.python"
  },
  "[cpp]": {
    "editor.defaultFormatter": "ms-vscode.cpptools"
  },
  // "C_Cpp.updateChannel": "Insiders",
  "bracketPairColorizer.depreciation-notice": false,
  "code-runner.runInTerminal": true,
  // "code-runner.executorMap": {
  //   "cpp": "echo \"Muslos supremacy\" && cd $dir && g++ *.cpp -o $fileNameWithoutExt  && $dir$fileNameWithoutExt && rm $fileNameWithoutExt.exe"
  // },
  // "code-runner.customCommand": "echo \"Muslos Supremacy\" && cd $dir && g++ $fileName -o $fileNameWithoutExt  && $dir$fileNameWithoutExt && rm $fileNameWithoutExt.exe"
  "code-runner.executorMap": {
    "cpp": "echo \"Executing...\" && cd $dir && g++ \"$fileName\" -o  main && .\\main.exe && rm \"main.exe\""
  },
  "code-runner.customCommand": "echo \"Executing...\" && cd $dir && g++ (Get-ChildItem -recurse *.cpp) -o main  && .\\main.exe && rm \"main.exe\"",
  // "code-runner.customCommand": "echo \"Executing Custom Command...\" && cd $dir && g++ (Get-ChildItem -recurse *.cpp) -o $fileNameWithoutExt  && $dir$fileNameWithoutExt && rm $fileNameWithoutExt.exe",
  "editor.bracketPairColorization.enabled": true,
  "editor.guides.bracketPairs": true,
  "editor.guides.bracketPairsHorizontal": true,
  "editor.guides.highlightActiveBracketPair": true,
  "security.workspace.trust.untrustedFiles": "open"
}
```
