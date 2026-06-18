# Verification Checklist

Use this checklist as a menu. Match the commands to the local project and available tools.

## Source Coverage

- Count source PDF pages with `pdfinfo`.
- Extract per-page text with `pdftotext` or a PDF library.
- Classify pages as translated, blank, intentionally blank, figure-only, table-heavy, or unresolved.
- Confirm every nonblank source page maps to translated LaTeX content or an explicit preserved artifact.

Useful checks:

```sh
pdfinfo source.pdf
pdftotext -layout source.pdf source-extract/full-layout.txt
```

## Figure And Table Audit

- Build an expected list from source captions: figures, tables, appendices, and special front-matter tables.
- Build an actual list from LaTeX `\includegraphics`, `\caption`, and table environments.
- Confirm every source figure/table number appears in the generated PDF text or rendered page.
- Render contact sheets for visual inspection, especially around dense figures, tables, and appendices.

Useful checks:

```sh
rg -n '\\includegraphics|\\caption|表 [0-9A-Z]|图 [0-9A-Z]' translation *.tex
pdftotext output.pdf - | rg -n '图 [0-9]|表 [0-9]|附录'
```

## Build Log Gate

Run the project build command, then scan the log. Treat the following as blockers unless they are already understood and harmless.

```sh
latexmk -xelatex -interaction=nonstopmode main.tex
rg -n -i '(^! |LaTeX Error|Package .* Error|Missing character|Fatal error|Emergency stop|Undefined control sequence|undefined references|Citation .* undefined|Rerun to get)' main.log
pdfinfo output.pdf
```

Warnings such as small overfull boxes may be acceptable for long equations or technical parentheticals, but inspect visible layout if they occur near tables, captions, or section headings.

## Translation Quality Gate

Search both TeX and generated PDF text for:

- Long English prose that should have been translated.
- Chinese-only specialized terms that would benefit from an English original.
- Abbreviation-only parentheticals.
- Mechanical phrases: `显然`, `事实上`, `当然`, `容易证明`, `很容易`.
- Known false friends in the domain, for example `susceptibility` vs `polarisability`, `group delay` vs `group velocity`, `phase matching` vs `index matching`.
- Source spelling conventions for English originals, such as British `polarisation` and `ionisation` when the source uses them.

Useful checks:

```sh
rg -n '显然|事实上|当然|容易证明|很容易|polarization|ionization|TODO|待翻译' translation
pdftotext output.pdf - | rg -n 'TODO|待翻译|polarization|ionization|显然|事实上|当然|容易证明|很容易'
```

## Final Progress Note

Record:

- Source PDF path and generated PDF path.
- Build command.
- Generated PDF page count and creation time.
- What source pages/sections are covered.
- Figure/table audit status.
- Log scan result.
- PDF text audit result.
- Visual inspection scope.
- Any remaining risks or intentionally deferred items.
