# File-Organizer-Addon

Cross-platform CLI that organizes messy folders by file type — recursive, duplicate detection, dry-run preview, and full undo. Works on Windows, macOS, and Linux.

## Install

pip install file-organizer-cli

Requires Python 3.8+. No other dependencies.

## Basic usage

file-organizer organize ~/Downloads

This sorts every loose file in the folder into category subfolders — Documents, PDFs, Images, Videos, Audio, Archives, Code, Executables, Text, Fonts, Spreadsheets, Presentations, and Other for anything unrecognized.

## Common options

| Command | What it does |
|---|---|
| `file-organizer organize ~/Downloads --recursive` | Also organizes every subfolder's own files, in place — keeps your folder structure, just tidies each level |
| `file-organizer organize ~/Downloads --flatten` | Pulls files from the entire folder tree up into category folders at the top |
| `file-organizer organize ~/Downloads --dry-run` | Shows exactly what would move, without touching anything |
| `file-organizer organize ~/Downloads --dedupe` | Detects duplicate files by content (not just filename) and moves extras into a Duplicates folder |
| `file-organizer organize ~/Pictures --by-date` | Further sorts each category into Year/Month subfolders |
| `file-organizer organize ~/Downloads --ignore '*.tmp'` | Skips files matching a pattern (repeatable flag) |
| `file-organizer organize ~/Downloads --config my-categories.json` | Uses your own custom categories on top of the defaults |
| `file-organizer undo` | Puts everything from the most recent run back exactly where it was |

You can combine flags:

file-organizer organize ~/Downloads --recursive --dedupe --dry-run

## Undo

Every real run writes a log to ~/.file-organizer/logs/. If you don't like the result:

file-organizer undo

This restores every moved file to its exact original location and cleans up any category folders it emptied along the way.

## Custom categories

Create a small JSON file:

{
  "Screenshots": [".png", ".jpg"],
  "Books": [".epub", ".mobi", ".azw3"]
}

Then run:

file-organizer organize ~/Downloads --config my-categories.json

## Optional: custom folder icons

Add --icons to any organize command to color-code the category folders it creates. Windows works out of the box; macOS needs fileicon (brew install fileicon); Linux needs gio (ships with GNOME). If the tool isn't present, this flag just does nothing — organizing still works normally.

## Optional: native right-click integration

The repo's integrations/ folder has a full Windows Explorer right-click add-on, a Linux Nautilus script, and macOS Automator instructions.
