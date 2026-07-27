# Repository instructions

This is a GitHub Pages site built with Jekyll and the custom Manifold Royal Dark theme, which inherits its structure from the Midnight theme. It does not use a project-local package manager or application build.

This website tries to follow this graph:

Exploration
        ↓
System
        ↓
Lesson (implicit)
        ↓
Principle

## Systems guidance for Systems menu item

Systems are living documents, not project pages. They capture the evolution of my understanding as I build. Each system starts with a question, explores different ideas, and gradually expresses the principles that emerged along the way. Rather than documenting features or releases, I document why the system exists, the architectural decisions behind it, the trade-offs I made, what changed my mind, and what I would design differently today. As my understanding evolves, so do the systems.

## Exploration guidance

Explorations are not tutorials, product reviews, or opinion pieces. They begin with a genuine question rather than a predetermined answer. Their purpose is to challenge assumptions, explore first principles, and develop understanding through reasoning and, when appropriate, building.

An exploration should ask “What if…?”, “Should…?”, “Why…?”, or “Does…?” rather than immediately presenting a conclusion. The goal is not to defend an opinion but to discover one.

Prefer timeless questions over technology-specific commentary. Use current technologies as examples, but explore the underlying concepts instead. An article about AI gateways, Kubernetes, Git, or LLMs should ultimately be about broader ideas such as engineering freedom, agency, trustworthy autonomy, simplicity, modularity, opinionated software, or human-centered system design.

Whenever possible, conclude an exploration by building something. Building is not the goal—it is the mechanism for transforming borrowed knowledge into personal understanding. The resulting prototype may be small, incomplete, or intentionally opinionated. Its purpose is to test an idea rather than compete with existing products.

### Choosing exploration questions

An exploration begins with a question that the author genuinely wants to answer, regardless of whether it becomes popular or widely read. The primary audience is the author’s own curiosity. The purpose is to deepen understanding, not to maximize engagement.

Before accepting a question, challenge it:

* Is this the real question, or is there a deeper one underneath?
* What assumption does this question take for granted?
* Can the assumption itself be questioned?
* Does the question explore a timeless concept rather than a specific technology?
* Would the author still spend weeks exploring this question if nobody ever read the result?
* Is this question likely to change how the author thinks?
* Can the question be explored through building rather than only reasoning?

Prefer questions that challenge assumptions over questions that ask for opinions. A strong exploration often begins with What problem…, When…, Who…, Why…, Can…, or Should…, and invites genuine discovery rather than defending a predetermined conclusion.

Weak examples:

* Does everyone need an AI platform?
* Should there be one strategy for AI pull request reviews?

Stronger versions:

* What problem is an AI platform actually solving?
* Who actually needs an AI platform?
* What is the smallest AI platform that could possibly work?
* What makes a code review strategy effective?
* Should AI reviews optimize for consistency or diversity?

The goal is not to find the most interesting title. The goal is to discover the most interesting question. A good exploration should leave both the author and the reader thinking differently than when they started.

Good exploration questions include:

* What if AI gateways optimized for engineering freedom instead of vendor integration?
* What should an AI agent leave behind after completing a task?
* Does every platform need configuration?
* When does complexity stop paying for itself?
* Should software optimize for agency over convenience?
* What makes an autonomous engineer trustworthy?
* Can engineering freedom be measured?
* What would Git look like if it were designed in the age of AI agents?

A successful exploration often leads to one of three outcomes:

* A principle – a new insight that becomes part of the site’s philosophy.
* A system – a prototype or implementation that explores the idea in practice.
* A changed opinion – discovering that the original assumption was incomplete or wrong.

The purpose of an exploration is not to prove that an idea is correct. Its purpose is to understand the problem deeply enough to develop an informed point of view. Sometimes the most valuable outcome is discovering that the original question was the wrong one.

### Post structure

Every post published in Explorations (`_explorations/`) must follow this
sequence:

```text
Question
    ↓
Exploration
    ↓
Prototype
    ↓
Conclusion
    ↓
Principle (eventually)
```

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
