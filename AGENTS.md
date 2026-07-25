# Repository instructions

This is a GitHub Pages site built with Jekyll and the Midnight theme. It does
not use a project-local package manager or application build.

## Local preview with Docker

Create and start the preview container from the repository root:

```sh
docker run -d \
  --name buildtounderstand-preview \
  -p 127.0.0.1:4000:4000 \
  -v "$PWD":/srv/jekyll:ro \
  jekyll/jekyll:4.2.2 \
  sh -lc 'gem install jekyll-theme-midnight webrick --no-document &&
    jekyll serve \
      --source /srv/jekyll \
      --destination /tmp/buildtounderstand-site \
      --host 0.0.0.0 \
      --port 4000 \
      --watch \
      --force_polling \
      --disable-disk-cache'
```

The site is available at <http://127.0.0.1:4000/>.

Once the container exists, use these commands:

```sh
docker start buildtounderstand-preview
docker stop buildtounderstand-preview
docker logs -f buildtounderstand-preview
```

If the container must be recreated, stop and remove only this named container
before running the creation command again:

```sh
docker stop buildtounderstand-preview
docker rm buildtounderstand-preview
```

## Publish with Git

Publish directly to `main` with ordinary Git commands. Do not require the
GitHub CLI.

Inspect and validate the pending changes first:

```sh
git fetch origin main
git status -sb
git diff
git diff --check
```

Stage only the intended files, then commit and push:

```sh
git add <file> [<file> ...]
git commit -m "<concise description>"
git push origin main
```

Pushing `main` triggers the GitHub Pages rebuild. Never use `git add -A` when
the working tree contains changes outside the current task.
