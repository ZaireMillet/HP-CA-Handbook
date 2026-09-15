# HP CA Handbook

A single-page reference tool for HP Client Advocates. It organizes job aids, cover
letters, and helpful SharePoint links into six categories so CAs can find what they
need without digging through SharePoint.

## What's in this repo

- `index.html` — the entire site. One self-contained file: all styling,
  behavior, and PDFs are embedded directly in it (no separate assets, no build step,
  no dependencies).

## Categories

1. **HP CA Production** — kit follow-up, kit processing, and the production workflow
2. **WTCHP POP and Applications** — application steps, hourly requirements, cover
   letters, and eligibility/route-mapping references
3. **WTCHP Enrollment/Certification** — certification flowcharts, program exams,
   clinic contacts, suspension/denial handling, and exposure forms
4. **Medical Records** — aerodigestive condition guidance, the medical record cheat
   sheet, the dynamic HIPAA ROI, and release-form references
5. **BMSP SOPs** — company-wide SOPs (onboarding, death notification, HIPAA ROI,
   disengagement)
6. **BPO - HIPAA ROI & EVL Assistance** — the BPO tasking job aid and release-form
   references

## How it works

- PDF job aids are embedded as base64 data directly in the HTML. Clicking one
  decodes it in the browser and opens it in a new tab — no external file requests.
- The **Dynamic HIPAA ROI** is an interactive, fillable PDF. Browsers' built-in PDF
  viewers don't run the Acrobat JavaScript that powers its dropdown, Run, and
  Finalize buttons, so clicking it **downloads** the file instead of opening a
  preview tab. Users should open the downloaded file with Adobe Acrobat or Adobe
  Reader for full functionality.
- All SharePoint/external links open in a new tab via `window.open`.

## Publishing to GitHub Pages

1. Create (or use) a repo and add `index.html` to it. Because it's already named
   `index.html`, it will load automatically at the Pages URL's root — no filename
   needed in the address bar.
2. Push to GitHub.
3. In the repo, go to **Settings → Pages**.
4. Under **Build and deployment → Source**, choose **Deploy from a branch**.
5. Pick the branch (e.g. `main`) and the folder (`/root` or `/docs`, depending on
   where you placed the file), then **Save**.
6. GitHub will publish the site at `https://<org-or-user>.github.io/<repo-name>/`.

No build step, no npm install, no server — it's a static file, so this is all
that's required.

## A few things worth knowing before you publish

- **File size:** this file is roughly 17 MB, almost entirely embedded PDF data.
  That's well under GitHub's 100 MB per-file limit, so a normal `git add` / `git
  commit` / `git push` works fine. If your org's repo has a stricter size policy or
  uses Git LFS rules that flag large files, check with whoever manages the repo
  before pushing.
- **Popup blockers:** clicking a PDF or link opens a new tab via JavaScript. Most
  browsers allow this when it happens directly from a click (which is how this site
  is built), but some locked-down corporate browser policies block all
  `window.open` calls regardless of trigger. If a user reports nothing happens when
  they click an item, that's the first thing to check.
- **Repo visibility:** if this repo is public, the embedded PDFs and all linked
  SharePoint URLs are visible to anyone who finds the Pages site or browses the
  repo's source. If the content should stay internal, use a private repo — note
  that GitHub Pages sites built from private repos are only free/available on
  paid GitHub plans (Pro, Team, or Enterprise); check your org's plan before
  relying on this.
- **Updating content:** to add or change a document/link, edit the `CATEGORIES`
  array and (for PDFs) the base64 data in the `<script>` block of `index.html`
  directly, or ask Claude to regenerate the file with the changes and re-upload it
  to the repo.

## Support

This handbook covers the documents and links available at the time it was built.
If you need information that isn't included here, direct your question to a
manager.
