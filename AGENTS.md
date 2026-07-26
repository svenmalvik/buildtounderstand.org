# Repository instructions

This is a GitHub Pages site built with Jekyll and the custom Manifold Royal
Dark theme, which inherits its structure from the Midnight theme. It does not
use a project-local package manager or application build.

## Exploration post structure

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

## System page structure

Every page published in Systems (`_systems/`) must illustrate one or more
principles rather than merely describe a project. It must follow this sequence:

```text
System
    ↓
Problem
    ↓
Principles
    ↓
Architecture
    ↓
Lessons
```

## Private editorial guidance

The notes in this section are a private idea backlog for AI-assisted planning.
Use them to help the author choose, develop, and structure future content. Do
not copy or publish this backlog, its category descriptions, or its coaching
language on the site.

### Exploration guidance

Explorations are not tutorials. They are questions explored through thinking
and eventually building.

#### Reimagining Systems

- What if AI gateways optimized for engineering freedom?
- What if Kubernetes were designed today?
- What if Git had been invented in the age of AI agents?
- What if every AI system left a trail?
- What if software prioritized agency over convenience?

#### First Principles

Break an assumption and rebuild from scratch.

- Do AI gateways need to be gateways?
- Does every platform need configuration?
- What is the smallest useful AI platform?
- What if AI memory belonged to the engineer?
- Should AI platforms be model-agnostic?

#### Engineering Freedom

This becomes the author's philosophy.

- Why Engineering Freedom Matters
- Every Dependency Is a Trade-off
- Designing Escape Hatches
- Open Beats Closed
- Vendor Lock-in Is a Design Decision
- Measuring Engineering Freedom

#### Opinionated Software

These articles should become uniquely the author's.

- Opinionated, Never Restrictive
- Why I Prefer Opinionated Systems
- Building My Own Interpretation
- Simplicity Creates Freedom
- Complexity Is a Tax

#### Build to Understand

Personal reflections:

- Why I Build Instead of Study
- Reading vs Building
- Why Building Changes My Thinking
- The Difference Between Knowing and Understanding
- Building Is How I Think

#### AI & Autonomous Engineering

This is where the author's current interests naturally fit.

- Trust Before Autonomy
- Delegation Requires Confidence
- Evidence Over Assertions
- AI Platforms Through the Lens of Engineering Freedom
- What Makes an Autonomous Engineer Trustworthy?

### System guidance

Every system should illustrate one or more principles. Do not frame a system
as merely "here's my project"; connect its problem, principles, architecture,
and lessons.

#### Manifold

Principles demonstrated:

- Build to Understand
- Opinionated Software
- Engineering Freedom

Topics:

- Why I built it
- What I learned
- What I'd redesign today
- Architecture
- Trade-offs

#### AI Gateway

Do not present this as merely "AI Gateway." Frame it as "Engineering Freedom
Applied to AI Gateways."

Topics:

- Why another gateway?
- Design philosophy
- Vendor independence
- Model independence
- Escape hatches
- Opinionated defaults

#### Future Platform

Maybe later:

- Identity
- Agent Runtime
- Planner
- Memory
- Evidence Engine

#### Small Systems

Tiny explorations, each demonstrating one principle:

- Prompt Router
- MCP Explorer
- AI Planner
- Git Experiment
- Configuration Engine

#### Reference Architectures

Treat these as architectures, not products:

- AI Gateway
- Agent Platform
- Trustworthy Agent
- Evidence Pipeline
- Autonomous Engineering Platform

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
