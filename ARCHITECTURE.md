# Architecture

## Detected stack

- Static website stack: HTML + CSS with no framework, bundler, or runtime build step.
  - Evidence: `index.html`, `styles/main.css`
- Asset-driven presentation layer with local image assets.
  - Evidence: `index.html` (`assets/...` references), `assets/`
- Planning and execution artifacts co-located under `ai/` (feature briefs, specs, task reports).
  - Evidence: `ai/README.md`, `ai/features/`
- Target deployment is static hosting on GitHub Pages.
  - Evidence: `ai/epic/web-design-brief.txt`

## Conventions

- Formatting and linting
  - No formatter/linter config is present.
  - Evidence: no `package.json`, no `.pre-commit-config.yaml`, no `Makefile`, no `justfile`
- Type checking
  - None configured (no typed language toolchain files).
  - Evidence: no `tsconfig.json`, no Python/Rust/Go/Java/.NET build manifests
- Testing
  - No automated test framework or test runner configured.
  - Evidence: no test config files or package scripts in repo root
- Documentation and planning
  - Architectural/planning documentation is maintained in markdown and structured task/spec folders.
  - Evidence: `ARCHITECTURE.md`, `ai/features/*/tasks/*/spec/`

## Linting and testing commands

- No single aggregator command exists.
  - Evidence: no `Makefile`, `justfile`, `package.json`, or CI workflow files
- No canonical lint/type-check/test commands are currently defined for this repo.
- Closest project-wide validation currently used is patch/whitespace validation:
  - `git diff --check`

## Project structure hotspots

- Main entry point
  - `index.html`: single-page site markup, semantic section flow, in-page anchor navigation.
- Styling system
  - `styles/main.css`: global tokens, section layout, breakpoints, CTA states, reduced-motion handling.
- Content/design source of truth
  - `ai/epic/web-design-brief.txt`: canonical product/design direction.
- Feature workflow artifacts
  - `ai/features/`: feature-level plan, task briefs, task specs, validation reports.
- Brand and visual assets
  - `assets/`: favicon and imagery used by homepage.

## Do and don't patterns

- Do use semantic section and heading structure with ARIA labels where appropriate.
  - Evidence: `index.html`
- Do use a single shared stylesheet with tokenized variables and section-scoped rules.
  - Evidence: `styles/main.css`
- Do keep planning/spec artifacts under `ai/features/.../tasks/.../spec/`.
  - Evidence: `ai/features/final-cta/tasks/`, `ai/features/about-preview/tasks/`
- Do not assume framework/build-tool abstractions (components, bundling, transpilation).
  - Evidence: absence of framework/toolchain manifests at repo root; direct HTML/CSS editing in `index.html` and `styles/main.css`
- Do not rely on automated CI/lint/test gates yet.
  - Evidence: no `.github/workflows/`, no project test/lint configuration files

## Open questions

- Will static deployment use repository root publishing (`index.html` at root) or a GitHub Actions workflow later?
- Should a minimal automated check baseline be introduced (for example HTML/CSS linting) once implementation scope grows?
