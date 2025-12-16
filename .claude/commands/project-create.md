---
description: Create a new REU/RET project from student materials (folder or URL)
---

You are creating a new REU/RET project website for the Emory REU/RET Computational Mathematics program. Follow these steps to ingest student materials and create a properly structured project with minimal changes.

## Core Philosophy
1. **Start with student materials** - preserve their work
2. **Minimal changes** - only fix what's broken
3. **Interactive prompts** - only ask for missing required fields
4. **Don't auto-fix content** - ask the user instead

## Workflow

### Step 1: Get Source Materials

Ask the user for the source of student materials:
- **Folder path**: Local directory containing markdown files and images
- **Website URL**: Website to download and convert

If not provided as an argument, prompt:
"Please provide the source of student materials:
- Path to a folder containing markdown and images
- URL of a website to download and convert"

### Step 2: Process Materials

**If folder path:**
1. Check that the folder exists
2. List all files in the folder (recursively)
3. Identify markdown files (*.md, *.markdown)
4. Identify images (*.png, *.jpg, *.jpeg, *.gif, *.svg)
5. Identify PDFs and other resources

**If URL:**
1. Use `wget` or `curl` to download the website
2. Download with depth limit (1-2 levels)
3. Save to a temporary directory
4. Convert HTML to markdown using `pandoc` if available (or `html2text`)
5. Extract main content and preserve images
6. List all downloaded files

### Step 3: Analyze Existing Content

Look for markdown files and analyze:
1. Check if frontmatter already exists (YAML between `---` markers)
2. Extract existing fields: title, date, summary, tags
3. Count words in body content (exclude frontmatter)
4. Find all image references in markdown
5. Check for LaTeX/math content ($$ or $ delimiters)

### Step 4: Interactive Prompts for Missing Fields

Only prompt for fields that weren't found in existing content:

**Project year** (required):
- Prompt: "What year is this project? (e.g., 2025)"
- Validate: Must be 20XX format

**Project slug** (required):
- Prompt: "Short name for URL (e.g., 'model-aware', 'krylov', 'fast-and-fair'):"
- Validate: lowercase, hyphens only, no spaces
- This will create: `content/projects/YYYY-slug/`

**Title** (required if not found):
- Prompt: "Project title:"
- If markdown has a # heading, suggest: "Found title: [heading]. Use this? (y/n)"
- Validate: Not empty, reasonable length (10-150 chars)

**Date** (required if not found):
- Prompt: "Publication date (YYYY-MM-DD):"
- Default: Today's date
- Validate: YYYY-MM-DD format

**Summary** (required if not found):
- Prompt: "2-3 sentence summary describing the research question, approach, and key findings:"
- Validate: At least 50 characters
- This is critical for homepage display

**Featured** (optional):
- Prompt: "Feature this project on the homepage? (y/n)"
- Default: y (true)

**Weight** (optional):
- Prompt: "Sort order (lower number = higher priority, default 20):"
- Default: 20
- Validate: Numeric

### Step 5: Create Project Structure

Create the directory: `content/projects/YYYY-slug/`

Organize files:
```
content/projects/YYYY-slug/
├── index.md          # Frontmatter + student content
├── img/              # All images moved here
└── [other files]     # PDFs, etc. at root level
```

**File organization:**
1. Move all images to `img/` subdirectory
2. Keep PDFs at root level (posters, presentations, manuscripts)
3. Preserve any other files (videos, data files) at root

### Step 6: Construct index.md

**Build the frontmatter:**
```yaml
---
title: "[User-provided or extracted title]"
date: YYYY-MM-DD
featured: true
weight: 20
summary: "[User-provided or extracted summary]"
tags: ["Summer YYYY"]
# authors: []
---
```

**Important:** Always include `# authors: []` as a commented-out field at the end of frontmatter. This is intentional to prevent mentors from appearing on every project page.

**Process the body content:**
1. Take existing student markdown content
2. Fix image paths to reference `img/` subdirectory:
   - Change `![alt](image.png)` to `![alt](img/image.png)`
   - Change `<img src="image.png">` to `<img src="img/image.png">`
   - Preserve all other attributes (width, style, etc.)
3. Do NOT rewrite or edit student text
4. Preserve LaTeX math notation exactly as written
5. Preserve heading structure

**If content is sparse (<300 words):**
Add template sections with [TODO] placeholders at the end:
```markdown

## Introduction
[TODO: Add introduction describing the problem and motivation]

## Background
[TODO: Add relevant background and mathematical foundations]

## Our Approach
[TODO: Describe methodology and key contributions]

## Results
[TODO: Present findings with visualizations]

## Conclusion
[TODO: Summarize key takeaways and future directions]

## References
[TODO: List cited works]
```

### Step 7: Validation & Summary

**Validate the created project:**
1. Check all referenced images exist in `img/`
2. Verify frontmatter is valid YAML (proper syntax)
3. Check that required fields are non-empty: title, date, summary, tags
4. Report any .zip files found (user should remove them manually)

**Print summary:**
```
✓ Created project: content/projects/YYYY-slug/

Structure:
  ✓ index.md (XXX words)
  ✓ img/ (N images)
  ✓ [list other files]

Frontmatter:
  title: [title]
  date: YYYY-MM-DD
  summary: [first 60 chars...]
  tags: ["Summer YYYY"]
  featured: true
  weight: 20

Images: X referenced, X exist

Notes:
- Project will automatically appear in content/summerYYYY/projects.md via tag filtering
- No manual linking needed (uses Wowchemy pages widget)
[if .zip files found: - Remove .zip files before committing]
[if TODOs added: - Template sections added - please fill in [TODO] placeholders]

Next steps:
1. Review and edit content/projects/YYYY-slug/index.md
2. Fill in any [TODO] placeholders
3. Run: /project-check YYYY-slug
4. Build site with: hugo server
```

## Important Notes

- **Preserve student work**: Don't rewrite their content
- **Minimal changes**: Only fix broken image paths
- **Commented authors**: Always add `# authors: []` but commented out
- **Automatic cohort linking**: Tags handle this automatically
- **Ask don't assume**: If anything is unclear, ask the user

## Error Handling

- If source folder doesn't exist: Report error and ask for correct path
- If URL can't be downloaded: Report error and suggest checking URL or network
- If pandoc not available: Try html2text, or ask user to provide markdown manually
- If project directory already exists: Ask if user wants to overwrite or choose different slug
- If any step fails: Report the specific issue and ask user how to proceed
