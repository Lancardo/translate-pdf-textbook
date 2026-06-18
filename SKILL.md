---
name: translate-pdf-textbook
description: End-to-end translation of English PDF textbooks, monographs, papers, and technical books into complete Chinese LaTeX/PDF editions. Use when Codex needs to translate long technical PDFs, preserve every chapter/appendix/front/back matter item, rebuild figures/tables/equations/references/index in LaTeX, add Chinese terminology with English originals in parentheses, compile the final PDF, and audit coverage, visual placement, and translation quality.
---

# PDF Textbook Translation

## Operating Standard

Produce a usable Chinese edition, not a rough text dump. Preserve the source structure, equations, figures, tables, captions, references, appendices, answers, index, and front/back matter. Do not append the original PDF behind the translation unless the user explicitly asks for a bilingual/source appendix.

Treat the source PDF as authoritative. OCR and extracted text are aids; inspect rendered pages when formulas, captions, tables, or figure placement are ambiguous.

## Workflow

1. **Inventory the source and project.**
   - Locate source PDFs, existing LaTeX files, figure folders, build commands, and progress notes.
   - Identify the book structure: title pages, contents, preface, chapters, appendices, answers, further reading, references, and index.
   - Extract per-page text and full-layout text when possible. Keep source page numbers visible in working files, for example with `\sourcepage{...}` markers or an equivalent audit map.

2. **Build a coverage map before translating deeply.**
   - Map every nonblank/non-placeholder source page to a destination section.
   - Create inventories for figure numbers, table numbers, equations, appendices, bibliography entries, and index sections.
   - Keep a `PROGRESS.md` or equivalent record that says what is translated, what is audited, what remains uncertain, and the last verified PDF build.

3. **Translate in structural passes.**
   - First create a complete LaTeX skeleton that mirrors the source.
   - Translate chapter by chapter, including captions, problems, answers, footnotes, front matter, back matter, and appendices.
   - Preserve equation numbering, symbols, references, and mathematical meaning. Never "simplify" formulas unless correcting a verified OCR or transcription error; record such corrections.

4. **Handle terminology deliberately.**
   - Prefer standard Chinese technical terms, followed by the English original in parentheses at definitions and other useful learning points.
   - Preserve acronyms as Chinese term + English original + acronym, for example `二次谐波产生（second-harmonic generation, SHG）`.
   - Distinguish nearby concepts instead of flattening them into one Chinese word, especially in optics: susceptibility vs polarisability, phase velocity vs group velocity, GVD/GTD/GTDD/GVM, wave vector, phase matching, birefringence, non-centrosymmetric media, polarisation/ionisation spelling, Raman/Stokes/anti-Stokes terms.
   - Keep the source's spelling convention for English originals when it is consistent, unless the user asks for another convention.

5. **Make the Chinese read naturally.**
   - Avoid mechanical translations such as overusing "显然", "事实上", "当然", "容易证明", and English-like sentence order.
   - Recast long English clauses into clear Chinese while preserving technical causality.
   - Do not delete authorial nuance, examples, warnings, or pedagogical asides.

6. **Place figures and tables inline.**
   - Extract or crop every source figure/table asset that is not already available.
   - Place each figure/table near its corresponding translated discussion, not as a dump at the end.
   - Translate captions and table headings. Recreate tables in LaTeX when feasible; use image crops only when the table is graphical or too risky to reconstruct quickly.
   - Audit for missing crop files, stale references, duplicated figure numbers, and empty figure regions in the compiled PDF.

7. **Verify repeatedly, not just at the end.**
   - Compile with the project's build command after meaningful batches.
   - Scan logs strictly for LaTeX errors, missing characters, undefined references, rerun requests, and fatal stops.
   - Extract text from the generated PDF and search for untranslated prose, missing terminology, old/incorrect terms, and representative corrected passages.
   - Render representative pages or contact sheets to visually check figure/table placement, blank pages, clipping, overlap, and whether the source PDF was accidentally appended.

8. **Close only with evidence.**
   - Before claiming completion, prove coverage for all source pages with content, all expected figures/tables, all major structural sections, and the current generated PDF.
   - Update progress notes with the exact output PDF path, page count, creation time, checks run, and remaining risks.
   - If a broad full-book semantic review is requested, do not mark the goal complete until the current-state evidence covers the full book.

## Resource

Read `references/verification-checklist.md` when approaching a milestone, auditing a final PDF, or recovering from a long interrupted translation project.
