---
layout: post
title: Helix Text Editor Setup
date: 2023-09-21 00:00 +0800
categories:
- Blogging
tags:
- dev-environment
- modal-text-editing
---
# What is Helix?
Helix is a modal text editor based on Kakoune. It's builtin tree sitter integration, LSP support, and other modern features make it stand out.

# Configuration
Helix prides itself on its easy configuration. 

Take my two configuration files for example

This sets up text editor preferences, like having relative line numbers, configuring the status line, and having a bar cursor shape in insert mode. 
```toml
theme = "dracula"

[editor]
line-number = "relative"
bufferline = "multiple"
color-modes = true

[editor.auto-pairs]
'(' = ')'
'{' = '}'
'[' = ']'
'"' = '"'
"'" = "'"
'`' = '`'

[editor.statusline]
left = ["mode", "spinner", "file-name", "file-modification-indicator"]
right = ["version-control", "diagnostics", "selections", "position", "file-encoding", "file-line-ending", "file-type"]
separator = "│"
mode.normal = "NORMAL"
mode.insert = "INSERT"
mode.select = "SELECT"

[keys.normal]
esc = ["collapse_selection", "keep_primary_selection"]

[editor.cursor-shape]
insert = "bar"

[editor.file-picker]
hidden=false
```
{: file='.config/helix/config.toml'}

The language.toml file sets up LSP with their language.
```toml
[[language]]
name = "go"
formatter = { command = "goimports" }
auto-format = true
text-width = 80

[[language]]
name = "html"
file-types = ["html", "gohtml"]
indent = { tab-width = 2, unit = "\t" }
language-server = { command = "emmet-ls", args = ["--stdio"] }
formatter = { command = 'prettier', args = ["--parser", "html"] }
auto-format = true

[[language]]
name = "yaml"
indent = { tab-width = 2, unit = "  " }

[[language]]
name = "make"
file-types = ["Makefile"]
indent = { tab-width = 4, unit = "\t" }

[[language]]
name = "python"
formatter = { command = "black", args=["--stdio"] }
auto-format = true
```
{: file='.config/helix/languages.toml'}

