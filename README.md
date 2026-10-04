# Gianmarco Cariola — academic website

A minimal Jekyll website for GitHub Pages, with Home, Research and CV pages. Publications appear first; all working and occasional papers share the Working Papers section. VoxEU/lavoce.info/SUERF media coverage sits beneath its research project and appears separately in the CV. No tracking, external fonts or JavaScript dependencies. Publication on GitHub Pages is authorized. The local repository is prepared; remote setup and deployment must be verified before claiming the site is live.

## Local preview

Use a maintained Ruby installation (Ruby 3.2 or newer recommended) and Bundler. From this directory:

```sh
bundle config set --local path vendor/bundle
bundle install
bundle exec jekyll serve --host 127.0.0.1 --port 4001
```

Open http://127.0.0.1:4001 . Stop with Ctrl-C. A static build uses `bundle exec jekyll build` and writes `_site/`.

## GitHub Pages setup, when authorized

For a user site, create `USERNAME.github.io` and set `_config.yml` url to `https://USERNAME.github.io`, leaving baseurl empty. For a project site, set that url and baseurl to `/REPOSITORY`. All internal links use Jekyll's relative_url filter. Configure Pages to deploy from the root of the chosen branch. Jekyll 3.10 is deliberately used for GitHub Pages compatibility. No Pages configuration has been applied remotely.

## Content

- `_data/profile.json`: public name, position, interests, contact and profiles.
- `_data/research.json`: one record per research project; links group alternate versions. Categories control Publications / Working Papers / Work in Progress. Commentary records retain their own title, authors, outlet and date. Sources and verification date accompany each record.
- `cv/gianmarco-cariola-cv.tex`: standalone academic CV; update alongside research data.
- `assets/documents/gianmarco-cariola-cv.pdf`: compiled public CV, linked from Home and CV.
- `assets/images/profile.jpg`: optimized replacement photograph with original metadata removed.
- `docs/FACT_CHECK.md`: reconciliation decisions and remaining questions.

## CV

Open the standalone `.tex` in Codex's LaTeX editor to edit and preview. To generate the public PDF on a TeX-equipped machine:

```sh
pdflatex -interaction=nonstopmode -halt-on-error -output-directory=assets/documents cv/gianmarco-cariola-cv.tex
```

The current reviewed PDF is linked from Home and CV. `_config.yml` stores its path in `cv_pdf: /assets/documents/gianmarco-cariola-cv.pdf`. After editing the LaTeX source, re-export the PDF to that same path and rebuild the website; the PDF does not update automatically when the `.tex` changes. LaTeX auxiliary files are ignored.

## Privacy and publishing

Everything tracked in a public repository is public, even files excluded from the generated Jekyll website. Never add source input documents, the original photograph, restricted materials or private personal details. `.gitignore` excludes local dependencies/build products, not the public CV PDF. Inspect all files before committing. `docs/FACT_CHECK.md`, README and AGENTS are public repository documentation but are excluded from the rendered site. Keep unresolved private review notes outside the repository.
