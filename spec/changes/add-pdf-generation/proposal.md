# Proposal: Add PDF Generation Support

## Why

**Context**:
- The Quarto-FH-SWF-Theme currently supports HTML (documents and RevealJS presentations) but lacks PDF output capability
- FH staff need PDF documents for formal submissions, printing, and archival purposes
- CI/CD pipelines at FH require automated document generation in multiple formats

**Current state**: Only `html` and `revealjs` formats are configured in `_quarto.yml`. No PDF-specific theming or CI workflow exists.

**Desired state**: Users can generate professional PDF documents with FH-SWF branding automatically via CI, alongside HTML outputs.

## What Changes

- Add `pdf` format configuration in `_quarto.yml` using Typst engine (Quarto 1.6+)
- Create `styles/fhswf-pdf.scss` with PDF-specific styling (page margins, typography, logo placement)
- Configure `_brand.yml` with PDF-specific settings (paper size, fonts embedding)
- Create GitHub Actions workflow `.github/workflows/pdf-ci.yml` for automated PDF generation
- Add `examples/document-pdf.qmd` demonstrating PDF-specific features
- Document PDF generation in `README.md`

## Impact

### Affected Specifications
- This is a new capability, no existing specs affected

### Affected Code
- `_quarto.yml` - Add pdf format block
- `_brand.yml` - Extend with pdf-specific configuration
- `styles/fhswf-pdf.scss` - New file for PDF styling
- `.github/workflows/pdf-ci.yml` - New CI workflow
- `examples/document-pdf.qmd` - Example document
- `README.md` - Documentation update

### User Impact
- Users gain ability to generate branded PDF documents
- CI pipelines can produce PDFs automatically on push/PR
- PDF output includes FH-SWF logo, corporate colors, and typography

### API Changes
- None (configuration-only change)

### Migration Required
- [ ] None for existing users (opt-in feature)
- [ ] Documentation updates for new PDF features

## Timeline Estimate

Medium (~3-5 days): PDF theming is straightforward, CI workflow is well-established pattern.

## Risks

- **Risk**: Typst vs LaTeX backend choice could limit compatibility
  - **Mitigation**: Use Typst (modern, faster, better font handling) with LaTeX fallback documented
- **Risk**: PDF fonts may not embed correctly across systems
  - **Mitigation**: Use Google Fonts with open licenses, embed subset fonts
