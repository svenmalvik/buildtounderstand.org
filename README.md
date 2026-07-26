# Build to Understand

This repository contains the source for a GitHub Pages site about engineering
freedom. GitHub's built-in Jekyll support turns the Markdown into a site using
the custom **Manifold Royal Dark** theme. It inherits its structure from
Jekyll's Midnight theme; no application build, package manager, or Actions
workflow is required.

The `theme: jekyll-theme-midnight` setting in `_config.yml` intentionally names
the underlying Jekyll gem. The site's theme identity and custom palette are
Manifold Royal Dark.

## Publish from `main`

In the GitHub repository:

1. Open **Settings → Pages**.
2. Under **Build and deployment**, choose **Deploy from a branch**.
3. Select the **`main`** branch and the **`/ (root)`** folder.
4. Save the setting.

GitHub Pages will rebuild the site whenever content is pushed to `main`.

## Content structure

```text
.
├── _config.yml              # GitHub Pages and collection configuration
├── index.md                 # Home page
├── essays/index.md          # Generated essay listing
├── experiments/index.md     # Generated experiment listing
├── _essays/                 # Published long-form essays
├── _experiments/            # Published experiment notes
└── _templates/              # Unpublished authoring templates
```

Principles are written directly in the `## Principles` section of `index.md`.
Files in the two content collections are published automatically. Their file
names become their URLs:

```text
_essays/engineering-freedom.md
→ /essays/engineering-freedom/
```

## Add content

Copy the matching template into its collection, give the file a short
lowercase name with hyphens, and replace the template text:

```sh
cp _templates/essay.md _essays/engineering-freedom.md
cp _templates/experiment.md _experiments/remove-the-approval-gate.md
```

Every document needs YAML front matter at the top. `title` and `summary`
control how it appears on its collection page. Essays and experiments are
listed newest first by `date`.

The files under `_templates/` are excluded from the published site.
