# Audit Report — tobiasheinrichfaska.github.io

**Date:** 2026-05-31
**Project:** `c:\skripte\public\tobiasheinrichfaska.github.io`
**Type:** Static single-page GitHub Pages site (one `index.html`, no build, no JS, no dependencies)

---

## Scope & Context

This project is a personal developer homepage plus an embedded privacy policy, served
directly by GitHub Pages with no build step. There is no application code, no package
manager, no test suite, and no runtime backend. Consequently, most dynamic audit
dimensions (logic errors, injection, N+1 queries, dependency CVEs, build output) are
**not applicable**. The audit focuses on content correctness, consistency with the
workspace project state, accessibility, security headers, and documentation hygiene.

**Pre-flight checks:**
- Build: N/A (static HTML, served directly — confirmed by CLAUDE.md "No build step needed")
- Lint: N/A (no toolchain configured)
- Tests: N/A (no test suite)
- `FEATURES_REQUIRED.md`: **Missing** (see CRIT-1)
- Bash / PowerShell / WebFetch tools were denied in this session, so live link resolution
  and `git status` could not be performed; link findings are based on static cross-reference
  against CLAUDE.md.

---

## Findings

| # | Category | Severity | Finding | Location | Suggestion |
|---|----------|----------|---------|----------|------------|
| CRIT-1 | Features | Critical | No `FEATURES_REQUIRED.md` defining critical user paths. Cannot formally validate integration. | project root | For a one-page static site the only critical path is "page loads and all project/contact/license links resolve." Add a minimal `FEATURES_REQUIRED.md` documenting this, or mark the file intentionally N/A in CLAUDE.md. |
| H-1 | Consistency | High | Privacy Policy states it "applies to the **mobile application** published … on the Apple App Store and Google Play Store" (singular mobile app), but the page advertises 4 projects that are mostly **desktop/web** (PDF organizer = Python/Tkinter desktop, Arbeitszeitplaner = web SPA, Adobe add-in). The policy scope does not match the products shown. | index.html:48-62 | Reword the policy to cover the actual portfolio (web + desktop + mobile), or scope it explicitly to the named app(s). As written it is legally ambiguous and arguably inaccurate for store review. |
| H-2 | Consistency / Runtime | High | `Arbeitszeitplaner` card links to `https://github.com/tobiasheinrichfaska/Arbeitszeitplaner`, but CLAUDE.md marks Arbeitszeitplaner as **(private)**. A private repo link 404s for every public visitor. | index.html:29 ; CLAUDE.md:24 | Confirm the repo is actually public before linking. If it is private, remove the card or point to a public mirror. Same risk applies to any card whose repo is not yet public. |
| M-1 | Consistency | Medium | Repo-name mismatch: the Adobe card links to `adobe-acrobat-bookmarks-addon`, but the workspace project is named "Adobe Add In - Lesezeichen" / `adobe_add_in_lesezeichen`. The public GitHub repo slug is unverified and may not exist. | index.html:39 | Verify the live GitHub slug matches the link; align naming so the public repo name is discoverable from CLAUDE.md. |
| M-2 | Accessibility | Medium | Footer text uses `color: #888` on white (`#fff`) ≈ 3.5:1 contrast, below WCAG AA (4.5:1) for normal-size text. | index.html:13 | Darken to `#767676` or below (`#666`) to meet AA. |
| M-3 | Security | Medium | No security headers / meta hardening. No Content-Security-Policy `<meta>`, and `mailto:` exposes the address to scrapers (minor, by design). GitHub Pages cannot set most headers, but a CSP meta and `referrer` policy meta add defense-in-depth. | index.html `<head>` | Add `<meta http-equiv="Content-Security-Policy" content="default-src 'self'; style-src 'unsafe-inline'; img-src 'self' data:">` and `<meta name="referrer" content="strict-origin-when-cross-origin">`. Note inline `<style>` requires `'unsafe-inline'`. |
| L-1 | Code Quality | Low | Link styling (`style="color: #007aff; text-decoration: none;"`) is duplicated inline on all 4 project headings instead of using a CSS class. | index.html:24,29,34,39 | Move to a `.app-card h3 a { color:#007aff; text-decoration:none; }` rule in the existing `<style>` block. |
| L-2 | Consistency | Low | CLAUDE.md says "currently 4/8 active projects listed" and flags WindowsWartung (public) as a candidate not shown. Public portfolio is incomplete relative to documented public projects. | CLAUDE.md:21,30 | Decide whether WindowsWartung (public) should appear; update either the page or the CLAUDE.md note so they agree. |
| L-3 | Accessibility | Low | Heading hierarchy: `<h3>` project titles sit under an `<h2>`, which is correct, but the page has no `<main>` landmark and the single `<h1>` text "Open-Source Developer" duplicates the role conveyed by `<title>`. Minor semantic polish only. | index.html:16-21 | Wrap content in `<main>`; optionally make `<h1>` the site/owner name for clearer document outline. |
| L-4 | Documentation | Low | Privacy Policy "Effective Date: May 2026" has no day; CLAUDE.md convention says "Update the privacy policy effective date when changes are made." Ambiguous date weakens that convention. | index.html:49 | Use a full ISO date (e.g. 2026-05-31) for auditability. |
| L-5 | SEO / Meta | Low | No `<link rel="canonical">`, no Open Graph / Twitter card meta, no favicon. Harmless but reduces share/preview quality for a public portfolio. | index.html `<head>` | Add canonical URL, basic `og:title`/`og:description`, and a favicon. |

---

## Summary

**Findings by severity:** Critical 1 · High 2 · Medium 3 · Low 5 (Total 11)

### Top 3 Critical/High Fixes
1. **H-1 — Privacy policy scope mismatch.** The policy claims to cover a single mobile
   app while the page sells a desktop/web portfolio. This is the highest real-world risk
   (app-store review and legal accuracy). Reword to match the actual products.
2. **H-2 — Private repo link.** Verify `Arbeitszeitplaner` (and every card) points to a
   genuinely public repo; private links 404 for all visitors.
3. **CRIT-1 — Define critical paths.** Add a minimal `FEATURES_REQUIRED.md` ("page loads;
   all 4 project links, the mailto, and both license links resolve") or mark N/A in CLAUDE.md.

### Top 2 Architectural Improvements
1. **Extract repeated inline link styles into the `<style>` block** (L-1) — the only real
   structural cleanup available in a single-file site; keeps future card additions DRY.
2. **Add a small head-hardening + meta block** (M-3, L-5) — CSP/referrer/canonical/OG as a
   reusable template snippet documented in CLAUDE.md's "Add a New Project" section.

### Quick Wins (easy, high impact)
- M-2: change `#888` → `#666` for WCAG AA (one-line).
- L-4: full ISO effective date (one-line).
- L-1: dedupe link styling into one CSS rule.
- M-3: paste two meta tags into `<head>`.

### Pre-flight Results
Build / Lint / Tests: **N/A** (static HTML, no toolchain — expected and acceptable).
Runtime: page is valid, self-contained HTML; renders with no scripts and no external
runtime dependencies, so no blank-screen or console-error risk. The only runtime risk is
**dead links** (H-2/M-1), which could not be live-verified this session due to denied
network access.

---

*Report generated by /audit. Note: Bash, PowerShell, and WebFetch were unavailable this
session; link resolution findings are from static cross-reference with CLAUDE.md and should
be confirmed with a live link check.*
