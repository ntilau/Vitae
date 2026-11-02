# Vitae: CV and Cover Letter Repository

This repository contains the Markdown source files for Laurent "Enzo" Ntibarikure's CV and
cover letter, along with the tooling that turns them into PDFs.

## Contents

| Path | Purpose |
|---|---|
| `CV.md` | CV content in Markdown — the source of truth (generalized; not tailored to a specific job) |
| `CL.md` | Cover letter content in Markdown — the source of truth (generalized; not tailored to a specific job) |
| `compile` | Builds `CV.pdf` and `CL.pdf` with Pandoc |
| `setup` | Verifies Pandoc and WeasyPrint are installed |
| `.github/workflows/pdf-generation.yml` | CI that builds the PDFs on GitHub |

`CV.md` and `CL.md` are the single source of truth. They are intentionally general — position- or
company-specific targeting has been removed so they can be reused for any application. The PDFs are
derived artifacts — regenerate them rather than editing them.

## Building the PDFs

```bash
./compile        # generate CV.pdf and CL.pdf
./setup          # verify pandoc + WeasyPrint are installed
./compile clean  # remove generated PDFs
```

A single document without the compile script:

```bash
pandoc CV.md -f markdown+autolink_bare_uris --pdf-engine=weasyprint -c pdf.css -o CV.pdf
pandoc CL.md -f markdown+autolink_bare_uris --pdf-engine=weasyprint -c pdf.css -o CL.pdf
```

The `-f markdown+autolink_bare_uris` flag is required: without it, bare URLs are not turned into
clickable links.

Local generation needs Pandoc and WeasyPrint. Run `./setup` to see what is missing.

## Continuous integration

`.github/workflows/pdf-generation.yml` builds both PDFs on every push to `main` and every
pull request that touches `CV.md` or `CL.md`. It installs its own Pandoc and WeasyPrint
toolchain and uploads `CV.pdf` and `CL.pdf` as build artifacts; it does not commit them.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
