# SEO audit and release checks

Audit date: 2026-10-24. Base commit: 43184399bd12dd520749b2620770b47ece916e90.

## Structure and hosting

Small Jekyll site, Gemfile pins Jekyll ~> 3.10.0. No custom plugins, JavaScript rendering or external theme. Main pages are /, /research/, /cv/; the shared default layout renders all three. Configured origin is https://gianmarcocariola.github.io with empty baseurl. No CNAME or .nojekyll exists. Documentation and LaTeX CV source are excluded from the generated site.

GitHub Actions records a successful dynamic "pages build and deployment" run on main at this base commit:
https://github.com/gianmarcocariola/gianmarcocariola.github.io/actions/runs/37233381640
The Pages settings API is unavailable through the connector; source directory and HTTPS enforcement could not be independently read. Confirm Settings > Pages uses main / (root).

## Changes

- Shared head includes unique titles/descriptions, absolute HTTPS canonicals and Open Graph metadata with the existing portrait.
- Homepage title identifies Gianmarco Cariola as Economist, Bank of Italy.
- Person JSON-LD appears only on the homepage. Name, position, employer, research interests and profile URLs come exclusively from existing homepage/CV/profile data. No biographical claims added.
- robots.txt allows crawling and advertises the sitemap.
- sitemap.xml is rendered by core Jekyll/Liquid, listing default-layout pages except the error page and pages explicitly marked sitemap: false. No plugin required; no invented lastmod dates.
- Only /404.html receives noindex, follow; this is intentional and does not block the real pages.

## URL and content review

Navigation consistently links to /, /research/ and /cv/. Research section anchors match their section IDs. PDF, stylesheet, favicon and portrait paths match tracked files. Root HTML sources with explicit permalinks generate /research/index.html and /cv/index.html rather than additional /research.html and /cv.html output. Canonicals collapse index.html aliases to directory URLs. PDF CV remains a separate useful format and is unchanged; research listings repeated within CV are intentional, with distinct page purposes and self-canonicals. No duplicate source pages found.

No pre-existing noindex, robots blocks or crawler-specific code was found in the shared layout/config/main page sources. HTTP headers, live redirects, status codes and Google-selected canonicals remain unverified.

## Validation and limitations

Static checks confirm valid YAML config, unchanged layout body, unique expected titles/descriptions, absolute canonical/sitemap targets and parseable JSON-LD after substitution of existing profile values. No scientific content, CV, CSS, image or research record changed.

Full Jekyll build and browser comparison could not run: Ruby/Bundler are absent and the execution environment's configured proxy refuses connections. Web access to the public site also failed. This does not establish a site outage. Do not treat this audit as proof of live HTTP reachability or Google indexing.

Before merging, run bundle install and bundle exec jekyll build using Ruby and inspect _site/robots.txt, _site/sitemap.xml and the head of all three generated pages. Compare rendered page bodies with the base version.

After merge and successful Pages deployment:
1. Confirm /, /research/, /cv/, /robots.txt and /sitemap.xml return HTTP 200, without X-Robots-Tag: noindex on real pages. Check an unknown URL returns 404.
2. Confirm robots.txt contains the production sitemap URL and the sitemap contains exactly the three canonical page URLs.
3. Check /index.html, /research/index.html and /cv/index.html share the canonical of their directory URL; inspect HTTP-to-HTTPS behavior.
4. Check navigation, section anchors, portrait, CSS, favicon and CV download in desktop/mobile views.

## Google Search Console (owner action)

Add a URL-prefix property for https://gianmarcocariola.github.io/ (the owner does not control DNS for github.io).
Select HTML file verification, download Google's exact verification file, commit it at the repository root unchanged (no Jekyll front matter), deploy and confirm its exact public URL before clicking Verify. Keep the file after verification. No verification token is invented or included in this PR.

Once deployed and verified, submit sitemap.xml in Sitemaps. Inspect each canonical URL with URL Inspection, use Test live URL, review crawling/indexing eligibility and request indexing. Monitor Page indexing and Google's selected canonical. A successful live test or indexing request is not proof that Google has indexed the URL; only Search Console's indexed status establishes that observation. Ranking for name/employer queries is not guaranteed.
