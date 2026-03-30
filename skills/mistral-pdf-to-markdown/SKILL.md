---
name: mistral-pdf-to-markdown
description: Convert PDFs to Markdown using Mistral OCR API with image extraction. Use when you need to extract structured text and images from PDFs, especially for scanned documents or documents with complex formatting. Outputs Markdown with embedded images.
---

# Mistral PDF to Markdown Converter

Convert PDF documents to Markdown format using Mistral's OCR API. Automatically extracts text, formatting, and images.

## When to Use

- Converting research papers or documents to Markdown
- Extracting text from scanned PDFs (OCR capability)
- Preserving document structure with headers and formatting
- Extracting embedded images from PDFs

## Quick Start

**Always run from the project root** (where `.env` lives). Use `python3` (system Python), not `uv run` --- the conversion script has no project-specific dependencies beyond what it declares inline.

```bash
# Convert entire PDF
python3 ~/vscodeproject/ResearchHub/skills/mistral-pdf-to-markdown/scripts/convert_pdf_to_markdown.py \
  input.pdf output.md

# Convert specific pages
python3 ~/vscodeproject/ResearchHub/skills/mistral-pdf-to-markdown/scripts/convert_pdf_to_markdown.py \
  input.pdf output.md --pages "1-5"
```

## Project Type Detection

| Project type | PDF location | Output location |
|---|---|---|
| Research project | `Literature/` | `Literature/Extracted/<paper_folder>/` |
| Reading project | `Literature/` | `Extracted/<paper_folder>/` |

Each paper gets its own subfolder to avoid image filename collisions.

## Output Structure

```
<output_folder>/
├── Author_Year.md          # Markdown with text and image references
└── images/
    ├── img-0.jpeg          # Extracted images
    ├── img-1.jpeg
    └── ...
```

## Key Features

- **Markdown formatting**: Preserves headers, lists, and structure
- **Image extraction**: Saves images to `images/` subfolder automatically
- **Page selection**: Extract specific pages or ranges
- **Scanned PDF support**: True OCR capability for image-based PDFs
- **Relative paths**: Image references use `![...](images/img-X.jpeg)`

## Requirements

The script requires:
- Mistral API key in `.env` at project root (`mistral_api_key=...`)
- Python packages: `mistralai`, `python-dotenv`, `pypdf` (install with `pip3 install mistralai python-dotenv pypdf`)

## Common Use Cases

### Convert Research Paper
```bash
python3 ~/vscodeproject/ResearchHub/skills/mistral-pdf-to-markdown/scripts/convert_pdf_to_markdown.py \
  "Literature/Author_Year.pdf" \
  "Literature/Extracted/author_year/author_year.md"
```

### Extract Specific Sections
```bash
python3 ~/vscodeproject/ResearchHub/skills/mistral-pdf-to-markdown/scripts/convert_pdf_to_markdown.py \
  "paper.pdf" "output.md" --pages "10-20"
```

### Extract Figures Only
```bash
python3 ~/vscodeproject/ResearchHub/skills/mistral-pdf-to-markdown/scripts/convert_pdf_to_markdown.py \
  "paper.pdf" "figures.md" --pages "25,27,30,35"
```

## Error Handling

**API Key Not Found:**
```
Error: Mistral API key not found in .env
```
-> Add `mistral_api_key=YOUR_KEY` to `.env` at the project root

**Page Out of Range:**
```
Warning: Page 100 out of range, skipping
```
-> Check PDF page count and adjust page selection

**API Rate Limit:**
-> Wait a moment and retry, or reduce page count per request

## Notes

- Images are saved as JPEG files in `images/` subfolder
- Markdown image references are automatically updated to `images/img-X.jpeg`
- Large PDFs may take longer to process due to API limits
- For simple text extraction without OCR, consider using the `pdf` skill instead

## See Also

- `pdf` skill - For local PDF manipulation without API calls
- `reference.md` in the skill directory - Additional details about the Mistral OCR API
