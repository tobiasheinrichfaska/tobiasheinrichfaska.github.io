# CLAUDE.md — tobiasheinrichfaska.github.io (Personal Homepage)

> **For workspace conventions, see:** [`c:\skripte\private\general stuff\general_stuff_claude.md`](../../private/general\ stuff/general_stuff_claude.md)

This is the personal portfolio and homepage published at GitHub Pages. It serves as the public-facing index of Tobias Heinrich's open-source projects.

---

## When to Update This Homepage

Update `index.html` when:

1. **A new public project is released** — add an `app-card` div with project name, GitHub link, and description
2. **A project description changes** — update the paragraph in the existing card
3. **A project moves or is archived** — remove or update the card
4. **Contact information changes** — update the email or contact section
5. **Privacy policy changes** — update the policy section to reflect any data handling changes

## Active Projects to Display

These projects should appear on the homepage (currently 4/8 active projects listed):

### Currently Listed
- ✅ **Arbeitszeitplaner** (private) — React SPA, resource & time planner for iPad/web
- ✅ **VereinsKalender** (public) — React + React Native organization calendar
- ✅ **DigitalerUnterlagenOrdner** (private→public) — PDF organizer desktop app
- ✅ **Adobe Add In - Lesezeichen** (public) — Adobe Acrobat JS add-in

### Not Listed (Consider Adding?)
- ❌ **WindowsWartung** (public) — Windows maintenance utilities
- ❌ **TKD-Coach** (private) — Coaching methods (not a user app)
- ❌ **Zeitplaner** (private) — Zammad→Outlook automation (not public-facing)

---

## How to Add/Update a Project Card

### Add a New Project

Copy this template into the `<h2>Open-Source Projects</h2>` section:

```html
<div class="app-card">
    <h3><a href="https://github.com/tobiasheinrichfaska/ProjectName" style="color: #007aff; text-decoration: none;">Project Name</a></h3>
    <p>One-line description. Technology stack. Dual-licensed: AGPLv3 + commercial.</p>
</div>
```

### Update Existing Project

Modify the paragraph text inside the card's `<p>` tag. Keep it concise (1–2 sentences) with:
- What the app does
- Target user or platform
- Technology stack (if notable)
- License reminder

---

## File Structure

```
public/tobiasheinrichfaska.github.io/
├── index.html                 # Homepage (single-file bundle)
├── README.md                  # GitHub repo description
├── LICENSE                    # AGPLv3 full text
├── LICENSE_COMMERCIAL.md      # Commercial licensing terms
├── CONTRIBUTING.md            # Contributor guidelines
└── tobiasheinrichfaska_github_io_claude.md  # This file
```

---

## Deployment

**This homepage is published automatically by GitHub Pages:**

1. Push changes to the `main` branch
2. GitHub builds and publishes to `https://tobiasheinrichfaska.github.io`
3. Updates typically live within 1–2 minutes

No build step needed — `index.html` is served directly.

---

## Conventions

- Keep styling minimal and responsive (mobile-friendly)
- All external links use `https://`
- Contact info always points to `tobias.a.w.heinrich@gmail.com`
- Update the privacy policy effective date when changes are made
- Keep project descriptions under 2 sentences for clarity

---

*Last updated: 2026-05-30*
