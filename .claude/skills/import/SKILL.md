---
name: import
description: Import documents (PDF, DOCX, DOC, XLSX) into a project as Markdown. Use when the user provides documents for analysis.
argument-hint: "[file-path-or-glob] [project-name]"
---

# Document Import

Convert documents to Markdown and save them as project source material. This is a **conversion-only** step — requirement extraction happens later via `/elicit`.

## Step 1: Identify inputs

Parse the arguments:
- **File path(s)**: Can be a single file, multiple files, or a glob pattern (e.g., `*.pdf`, `docs/*.xlsx`)
- **Project name**: Which project to save under. If not specified, ask.

Supported formats: `.pdf`, `.docx`, `.doc`, `.xlsx`, `.xls`

If the user provided a file path that doesn't match a supported format, tell them and list what's supported.

## Step 2: Verify files exist

Check that the file(s) exist. If using a glob, expand it and show the list:

```
Found 3 files to import:
1. requirements-v2.pdf (2.4 MB)
2. meeting-notes.docx (156 KB)
3. data-model.xlsx (89 KB)
```

If no files match, say so and stop.

## Step 3: Convert each file

For each file, run the converter:

```bash
cd /home/nosjr/endgame/ba-brain && .venv/bin/python convert.py "{input_file}"
```

Capture the output (Markdown string).

## Step 4: Save to project sources

Create the output directory if it doesn't exist:
```
projects/{project}/sources/
```

Save each converted file as `projects/{project}/sources/{original-filename-without-ext}.md`.

Add a metadata header at the top of each saved file:

```markdown
<!-- Imported: {original filename} -->
<!-- Date: {YYYY-MM-DD HH:MM} -->
<!-- Converter: convert.py ({format}) -->

{converted markdown content}
```

## Step 5: Show summary

For each imported file, show:
- Original filename and size
- Output path
- Content preview: number of headings, tables, paragraphs found
- Any conversion warnings

Example output:
```
Imported 3 files into projects/acme/sources/:

| File | Format | Output | Headings | Tables |
|------|--------|--------|----------|--------|
| requirements-v2.pdf | PDF | sources/requirements-v2.md | 12 | 3 |
| meeting-notes.docx | DOCX | sources/meeting-notes.md | 5 | 0 |
| data-model.xlsx | XLSX | sources/data-model.md | 4 sheets | 4 |
```

## Step 6: Suggest next steps

After import, suggest:

1. **Read the imported files** to verify conversion quality
2. **Run `/elicit {project} document-analysis`** to extract requirements from the imported content
3. If multiple files were imported: "You might want to start with `{largest/most relevant file}` — it looks like the main document."

## Error handling

- If `convert.py` fails on a file, report the error but continue with remaining files
- If `.venv` doesn't exist or dependencies are missing, tell the user to run:
  ```bash
  cd /home/nosjr/endgame/ba-brain && python3 -m venv .venv && .venv/bin/pip install pymupdf4llm mammoth openpyxl
  ```
- If a file is too large (> 50 MB), warn before processing
