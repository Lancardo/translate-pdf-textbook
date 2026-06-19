# translate-pdf-textbook

`translate-pdf-textbook` is a reusable AI-agent skill for translating English PDF textbooks, monographs, papers, and technical books into complete Chinese LaTeX/PDF editions.

It was distilled from a full technical-book translation workflow where the hard parts were not only language translation, but also coverage auditing, figure/table placement, LaTeX reconstruction, terminology consistency, and final PDF verification.

## What It Does

- Translates long English technical PDFs into Chinese.
- Preserves front matter, chapters, appendices, answers, references, indexes, equations, figures, tables, and captions.
- Uses Chinese technical terms with English originals in parentheses, such as `二次谐波产生（second-harmonic generation, SHG）`.
- Places figures and tables inline near the corresponding translated discussion.
- Encourages natural Chinese technical prose instead of mechanical sentence-by-sentence translation.
- Uses a chapter-level acceptance gate before moving to the next major section.
- Requires evidence-based verification before calling a translation complete.

## Repository Structure

```text
translate-pdf-textbook/
  SKILL.md
  references/
    verification-checklist.md
```

`SKILL.md` contains the core operating workflow. `references/verification-checklist.md` contains milestone and final-audit checks for coverage, figures/tables, LaTeX logs, generated PDF text, and visual layout.

## Install In Codex

Copy this folder into your Codex user skills directory:

```sh
mkdir -p ~/.agents/skills
cp -R translate-pdf-textbook ~/.agents/skills/
```

Then invoke it in Codex:

```text
Use $translate-pdf-textbook to translate this English PDF textbook into a complete Chinese LaTeX/PDF edition.
```

You can also refer to it naturally:

```text
用 translate-pdf-textbook 这个 skill，把根目录里的英文 PDF 教材翻译成中文 PDF。
```

## Install In Claude Code

For personal use across all projects:

```sh
mkdir -p ~/.claude/skills
cp -R translate-pdf-textbook ~/.claude/skills/
```

For project-level sharing, put the folder inside a repository:

```text
your-project/
  .claude/
    skills/
      translate-pdf-textbook/
        SKILL.md
        references/
          verification-checklist.md
```

Then invoke it in Claude Code:

```text
/translate-pdf-textbook 翻译这个英文 PDF 教材，输出中文 LaTeX/PDF。
```

## Recommended Input Project Layout

A LaTeX template is optional. If you have one, the agent should reuse it; if not, the agent can create a basic Chinese LaTeX project.

```text
project/
  source.pdf
  latex-template/   # optional
  figures/          # optional
```

For batch work, keep a stable template and reuse the same project structure.

## Good Usage Prompt

```text
Use $translate-pdf-textbook. Translate the English PDF in this project into a complete Chinese LaTeX/PDF textbook. Preserve all figures, tables, equations, appendices, references, and index entries. Add English originals in parentheses for specialized terminology. Compile and verify the final PDF.
```

## Design Principles

- Build a source-page coverage map before deep translation.
- Translate structurally, not as a flat text stream.
- Keep source page numbers available for auditing.
- Use standard Chinese terminology, but preserve useful English originals.
- Recreate or place every figure and table.
- Require each chapter to pass source coverage, figure/table inventory, build/log, and PDF text gates before continuing.
- Compile early and often.
- Treat final completion as unproven until coverage, logs, PDF text, and visual layout are checked.

## Notes

This skill is intentionally domain-agnostic enough for technical PDFs outside optics, but it includes examples from optics because that was the source workflow. For another discipline, keep the same verification process and adapt the terminology checks.
