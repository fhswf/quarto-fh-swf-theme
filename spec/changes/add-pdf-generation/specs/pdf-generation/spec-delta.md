# Spec Delta: PDF Generation Capability

This file contains specification changes for the new PDF generation feature.

## ADDED Requirements

### Requirement: PDF Format Configuration
WHEN a user renders a Quarto document with `format: pdf`,
the system SHALL produce a PDF file using Typst engine with FH-SWF branding.

#### Scenario: Document PDF Generation
GIVEN a document with `format: pdf` in frontmatter
AND `_brand.yml` is present with FH-SWF configuration
WHEN the user runs `quarto render document.qmd --to pdf`
THEN the system generates a PDF file
AND the PDF includes FH-SWF logo in header
AND the PDF uses primary blue `#39569F` for headings
AND the PDF uses Lato font family

#### Scenario: Presentation PDF Export
GIVEN a RevealJS presentation with `format: revealjs`
WHEN the user runs `quarto render slides.qmd --to pdf`
THEN the system generates a PDF of the presentation
AND the PDF uses landscape A4 paper size
AND the PDF includes FH-SWF logo centered on title slide

---

### Requirement: CI PDF Generation
WHEN code is pushed to the repository,
the CI SHALL automatically generate PDFs for all documents in `examples/` directory.

#### Scenario: Push Triggered PDF Generation
GIVEN a push event to main branch
AND documents exist in `examples/` directory with PDF format configured
WHEN the CI workflow runs
THEN the system generates PDF for each configured document
AND stores PDFs as build artifacts
AND uploads PDFs to artifact storage

#### Scenario: PR PDF Generation
GIVEN a pull request is opened
AND documents exist in `examples/` directory with PDF format configured
WHEN the CI workflow runs
THEN the system generates PDFs for each configured document
AND uploads PDFs as PR artifacts for review

---

### Requirement: PDF Brand Compliance
WHEN a PDF is generated with FH-SWF branding,
the system SHALL include corporate design elements per CD-Handbuch.

#### Scenario: Logo Placement
GIVEN a generated PDF document
THEN the FH-SWF Wort-Bildmarke SHALL appear in the header on the first page
AND the FH-SWF Bildmarke SHALL appear in the footer on subsequent pages
AND logo dimensions SHALL NOT exceed 25% of page width

#### Scenario: Color Compliance
GIVEN a generated PDF document
THEN headings SHALL use primary blue `#39569F`
AND body text SHALL use dark gray `#333333`
AND accent elements SHALL use secondary colors from `_brand.yml` palette

#### Scenario: Typography Compliance
GIVEN a generated PDF document
THEN body text SHALL use Lato font at 11pt
AND headings SHALL use Lato Semibold
AND code blocks SHALL use JetBrains Mono

---

### Requirement: PDF Quality Standards
WHEN a PDF is generated,
the system SHALL meet basic accessibility and archival standards.

#### Scenario: Document Structure
GIVEN a generated PDF
THEN the PDF SHALL contain proper heading structure (H1-H6)
AND paragraphs SHALL be tagged for accessibility
AND links SHALL be identifiable

#### Scenario: Font Embedding
GIVEN a generated PDF
THEN all fonts SHALL be embedded in the PDF
AND the PDF SHALL render correctly on systems without FH-SWF fonts installed

---

## MODIFIED Requirements

None.

---

## REMOVED Requirements

None.

---

## Notes

- Use Typst engine (Quarto 1.6+) as primary PDF generator
- Fallback to LaTeX/Pandoc if Typst unavailable
- PDF/A standard is aspirational but not required for initial release
