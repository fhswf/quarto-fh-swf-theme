# Implementation Tasks

## Phase 1: Configuration

1. Extend `_brand.yml` with PDF-specific settings (paper size A4, margins, font embedding)
2. Add `pdf` format block to `_quarto.yml` using Typst engine

## Phase 2: PDF Theme

3. Create `styles/fhswf-pdf.scss` with PDF-specific styling (page geometry, typography overrides)
4. Configure FH-SWF logo placement for PDF (header/footer)
5. Set up PDF color scheme (primary blue `#39569F` for headings)

## Phase 3: CI Workflow

6. Create `.github/workflows/pdf-ci.yml` with automated PDF generation on push
7. Configure artifact storage for generated PDFs
8. Add job for both document and slides PDF generation

## Phase 4: Examples & Documentation

9. Create `examples/document-pdf.qmd` demonstrating PDF-specific features
10. Update `README.md` with PDF generation instructions and CI setup
11. Add troubleshooting section for common PDF issues

## Phase 5: Validation

12. Verify PDF output matches corporate design (colors, logo, typography)
13. Test CI workflow execution
14. Validate PDF accessibility (tagged PDF, document structure)

---

**Notes**:
- Tasks 1-2 can run in parallel with tasks 3-5
- Task 6-8 require GitHub repo; document as manual steps if needed
- Final validation should include visual comparison against HTML output
