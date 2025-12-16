---
description: Validate an existing REU/RET project for completeness and issues
---

You are validating an existing REU/RET project website. Check for completeness and identify issues WITHOUT auto-fixing them. Provide clear, actionable feedback.

## Usage

The project slug should be provided as an argument (e.g., `2024-krylov` or just `krylov`).

If not provided, ask the user:
"Which project would you like to check? (e.g., 2024-krylov)"

## Validation Workflow

### Step 1: Locate Project

1. Look for the project in `content/projects/`
2. Try with and without year prefix if needed
3. If found: Note the full directory path
4. If not found: List available projects and ask user to clarify

### Step 2: Read and Parse index.md

1. Read `content/projects/YYYY-slug/index.md`
2. Extract frontmatter (YAML between `---` markers)
3. Parse YAML and extract fields
4. Count lines/words in body content (exclude frontmatter)
5. Identify all section headers (##)

### Step 3: Validation Checks

Perform the following validations and collect results:

#### 1. Required Frontmatter Fields

Check presence and validity:
- **title**: Present and non-empty (at least 10 chars)
- **date**: Present and valid format (YYYY-MM-DD or YYYY-MM-DDTHH:MM:SS)
- **summary**: Present and non-empty (at least 50 chars)
- **tags**: Present with format `["Summer YYYY"]`
- **featured**: Present and boolean (true/false)
- **weight**: If present, must be numeric

**CRITICAL**: Title, date, summary, and tags are required.
**WARNING**: Featured and weight are recommended but not critical.

#### 2. YAML Syntax

- Check that frontmatter is valid YAML
- No syntax errors (colons, quotes, brackets)
- If errors found: Report line number and issue

#### 3. Tag Consistency

- Extract year from project directory name (YYYY-slug)
- Extract year from tag (`["Summer YYYY"]`)
- Verify they match
- Verify tag format is exactly: `["Summer YYYY"]` (array with one string)

#### 4. Authors Field (Special Case)

**Important:** Commented `# authors:` is INTENTIONAL, not an error.

Only report if:
- Authors field is uncommented AND has invalid syntax
- Authors field references IDs that might not exist (informational only)

Do NOT flag:
- `# authors: [id]` - This is correct (intentional commenting)
- Missing authors field - This is fine

#### 5. File Structure Issues

Check for problems:
- **.zip archives**: Flag any .zip files (shouldn't be committed)
- **Image directory**: Check if `img/`, `imgs/`, `resources/` exists
- **Other files**: List PDFs and other resources

#### 6. Content Completeness

Evaluate (informational, not critical):
- Body content length (count words excluding frontmatter)
- Number of section headers (##)
- Presence of LaTeX math ($$)
- Flag if content is very short (<200 words)

#### 7. Image Reference Validation

1. Find all image references in markdown:
   - Markdown format: `![alt](path/file.ext)`
   - HTML format: `<img src="path/file.ext">`
2. For each image, check if file exists in project directory
3. Report broken links (referenced but missing files)
4. Report unused images (files exist but not referenced)

### Step 4: Generate Report

Format the output clearly with issue severity:

**Status Line:**
- `✓ VALID: Ready for publishing` - No critical issues
- `⚠️  ISSUES FOUND: N critical, M warnings` - Problems exist

**Sections:**

1. **Required Fields** - Checklist with ✓ or ✗
2. **CRITICAL** - Blocking issues that prevent publishing
3. **WARNINGS** - Non-blocking issues that should be addressed
4. **INFO** - Informational notes
5. **Files** - List of all files in project directory
6. **Images** - Summary of image validation

## Output Format Example

```
PROJECT CHECK: 2024-krylov
==========================

✓ VALID: Ready for publishing

Required Fields:
  ✓ title: "Efficient Processing of Image Sequences..."
  ✓ date: 2024-07-08
  ✓ summary: (180 chars)
  ✓ tags: ["Summer 2024"]
  ✓ featured: true
  ✓ weight: 20

File Structure:
  ✓ index.md (2,340 words)
  ✓ img/ directory exists
  - 3 image files
  - 0 PDF files

Images:
  Referenced: 3
  Found: 3
  Missing: 0
  ✓ All images exist

  Files:
    ✓ img/captioned_blurred.png (513 KB)
    ✓ img/captioned_deblurred.png (601 KB)
    ✓ img/recycling.jpg (89 KB)

Content:
  - 2,340 words in body
  - 5 section headers
  - Contains LaTeX math

---

PROJECT CHECK: 2024-registration
=================================

⚠️  ISSUES FOUND: 1 critical, 1 warning

CRITICAL ISSUES:

[1] Empty summary field (line 6 in frontmatter)
    Current: summary: ''
    Fix: Add a 2-3 sentence description of the project
    Example: "This project explores automatic differentiation
             techniques for image registration problems..."

Required Fields:
  ✓ title: "Automatic Differentiation for Image Registration"
  ✓ date: 2024-07-08
  ✗ summary: EMPTY
  ✓ tags: ["Summer 2024"]
  ✓ featured: true
  ✓ weight: 20

WARNINGS:

[2] Large image files detected
    - resources/kidney_flow.png (1.2 MB) - consider compressing

File Structure:
  ✓ index.md (3,450 words)
  ✓ resources/ directory exists
  - 20 image files
  - 1 PDF file

Images:
  Referenced: 18
  Found: 18
  Missing: 0
  Unused: 2

  Unused files:
    - resources/affine_hand-1.svg (not referenced in index.md)
    - resources/dynamics_new.png (not referenced in index.md)

---

PROJECT CHECK: 2025-example
============================

⚠️  ISSUES FOUND: 3 critical

CRITICAL ISSUES:

[1] Missing title field (frontmatter)
    Fix: Add 'title: "Your Project Title"' to frontmatter

[2] Invalid date format (line 3 in frontmatter)
    Current: date: July 2025
    Fix: Use format: date: 2025-07-08

[3] Missing tags field (frontmatter)
    Fix: Add 'tags: ["Summer 2025"]' to frontmatter

[4] Broken image links
    - img/figure1.png (referenced but file not found)
    - img/results.jpg (referenced but file not found)

Required Fields:
  ✗ title: MISSING
  ✗ date: INVALID FORMAT
  ✓ summary: (150 chars)
  ✗ tags: MISSING
  ✓ featured: true

File Structure:
  ✓ index.md (890 words)
  ✗ No image directory

WARNINGS:

[5] Short content (890 words)
    Typical projects have 1,500+ words
    Consider expanding sections

Images:
  Referenced: 2
  Found: 0
  Missing: 2 ❌

Next Steps:
  1. Fix critical issues above
  2. Add missing images or remove references
  3. Expand content if needed
  4. Run /project-check again to verify fixes
```

## Special Cases

### Commented Authors Field

If you find `# authors: [...]` this is CORRECT and intentional.
Do NOT report it as an issue.

Example of what NOT to flag:
```yaml
---
title: "Project Title"
date: 2025-07-08
# authors: [lruthot]  # This is fine!
---
```

### .zip Files

If .zip archives are found:
```
WARNING: .zip files should not be committed

Found:
  - 2024-krylov.zip (remove before committing)
  - backup.zip (remove before committing)
```

### Draft Projects

If `draft: true` is found:
```
INFO: Project is in draft mode
  - Not visible on published site
  - Set 'draft: false' when ready to publish
```

## Validation Rules Summary

**CRITICAL** (blocks publishing):
- Missing required fields: title, date, summary, tags
- Invalid YAML syntax
- Empty required fields (e.g., `summary: ''`)
- Broken image links (referenced but missing)
- Invalid date format

**WARNING** (should fix but not blocking):
- Short content (<500 words)
- Large image files (>1 MB)
- Unused image files
- .zip files in directory

**INFO** (nice to know):
- Draft status
- Content statistics
- Uncommented authors field with valid syntax

## Error Handling

- **Project not found**: List available projects in content/projects/
- **Invalid YAML**: Report parsing error and line number
- **No index.md**: Report that project directory exists but is missing index.md
- **Permission issues**: Report if files can't be read

## Important Notes

- **Don't auto-fix**: Only identify and report issues
- **Commented authors is OK**: Don't flag `# authors:` as an error
- **Be specific**: Provide line numbers and exact fixes needed
- **Categorize properly**: Use CRITICAL, WARNING, and INFO correctly
- **Check but don't change**: This is a read-only validation tool
