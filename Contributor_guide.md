# NeuroMiner Manual – Contributor Guide

This short guide shows **exactly** how to add or edit pages in the NeuroMiner manual using only the **GitHub web editor**. No command line, no git installed. Every change is reviewed via **Pull Request (PR)** and a **built preview** is attached automatically.

---

## Ground rules

* You will **not** edit the `main` (or release) branch directly. Create a **feature branch** and open a **Pull Request** (PR).
* Keep PRs **small and focused** (one page or one topic).
* Put images in `docs/_static/` and reference them with MyST’s `{figure}` directive (see below).
* Use clear headings and consistent terminology. See the style snippets at the end.

---

## One‑time: Access & where to edit

1. Make sure you have a **GitHub account** and access to the repository.
2. Navigate to the repo → open the **`docs/`** folder. This is where the book content lives.

---

## Create a branch (web UI)

There are two easy ways:

**Method A (from the branch switcher):**

1. On the repo’s main page, click the branch dropdown (shows `main`).
2. Type a new branch name, e.g. `add-installation-notes`.
3. Click **Create branch: add-installation-notes from main**.

**Method B (while editing a file):**

1. Open a file under `docs/` (e.g., `docs/index.md`).
2. Click the **✏️ Edit** icon (top right of the file view).
3. Make your change. At the bottom, under **Commit changes**, select **Create a new branch for this commit** and type a branch name.
4. Click **Propose changes**.

> Either method creates a branch and takes you to the **Open a pull request** screen.

---

## Edit an existing page

1. In your new branch, navigate to the page, e.g., `docs/getting-started.md`.
2. Click **✏️ Edit**, make changes, and add a short commit message ("Fix typos in Getting Started").
3. Choose **Commit directly to the `your-branch` branch** → **Commit changes**.

---

## Add a new page

1. Go to `docs/` → **Add file** → **Create new file**.
2. Name it (kebab‑case), e.g. `docs/data-preparation.md`.
3. Paste your content.
4. **Commit** to your feature branch.
5. **Update the Table of Contents** (`docs/_toc.yml`) to include the new page (see next section), otherwise it won’t appear in the built book.

---

## Update the Table of Contents (`_toc.yml`)

Open `docs/_toc.yml` and add the file path under the right section. Example:

```yaml
format: jb-book
root: index
chapters:
  - file: getting-started
  - file: data-preparation    # ← your new page
```

Commit the change to your feature branch.

---

## Add images

1. Go to `docs/_static/` → **Add file** → **Upload files** → select your image(s) (PNG/JPG/SVG).
2. In your Markdown page, reference with MyST’s figure directive:

````md
```{figure} _static/example.png
:alt: Short description for screen readers
:height: 360px

Caption text shown under the image.
````

````

---

## Open a Pull Request (PR)
If GitHub didn’t already take you there:
1. Click **Pull requests** → **New pull request**.
2. **base** = `main` (or the target writing branch), **compare** = your feature branch.
3. Add a descriptive title and a short summary of what changed.
4. Click **Create pull request**.

---

## Check the built preview of your PR
1. Open your PR → **Checks** (or **Show all checks**).
2. Click **PR Preview (Jupyter Book)** → **Details**.
3. On the run page, download the **`site-preview`** artifact (right side).
4. Unzip it and open `index.html` in your browser to navigate the built manual.

> If your browser blocks local file assets, run from the unzipped folder: `python -m http.server 8000` and open http://localhost:8000.

---

## Address review comments & merge
- Reviewers may leave **comments** or request changes. Reply and push fixes to the **same branch**.
- When the preview check is **green**, and your PR is **approved**, click **Merge pull request** (or a maintainer will merge for you).

---

## Troubleshooting
**Checks didn’t run:**
- Ensure your PR’s **base** is `main` (or the configured target) and the workflow file exists in your branch.

**Preview failed to build:**
- Make sure `docs/_config.yml`, `docs/_toc.yml`, and at least `docs/index.md` exist.
- If you added a new page, confirm it’s listed in `_toc.yml`.
- Check image paths (e.g., `_static/name.png`) and headings formatting.

**New page doesn’t show up in sidebar:**
- You likely forgot to add it to `_toc.yml`.

---

## MyST/Markdown quick snippets
**Admonition (tip box):**
```md
```{admonition} Tip
- Keep sections short.
- Prefer descriptive figure captions.
````

````

**Code block:**
```md
```{code-block} bash
pip install neurominer
````

````

**Cross‑reference a figure:**
```md
See {numref}`fig:data-flow` for the pipeline.

```{figure} _static/data-flow.svg
:alt: Data flow
:name: fig:data-flow
A simplified data flow.
````

```

---

## Glossary
- **Branch**: A workspace for your changes. Keeps `main` clean until review.
- **Pull Request (PR)**: A request to merge your branch into the target branch.
- **Checks**: Automated jobs (build, preview) that must pass before merging.
- **Review**: Another person approves your change (may request edits).

---

**That’s it!** If anything is unclear, ping the maintainers in the PR and we’ll help you through your first edit.
```
