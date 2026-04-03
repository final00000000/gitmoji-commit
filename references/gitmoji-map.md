# Gitmoji Map

Canonical gitmoji catalog for this skill.

Use this file as the single source of truth for emoji selection when the user explicitly asks for gitmoji / emoji output.
Default output mode is Conventional Commit. When emoji mode is enabled, prepend the selected gitmoji to the Conventional Commit title. Fall back to ASCII-only Conventional Commit output when UTF-8 is unsafe or the user asks for ASCII-only text.

## Preferred title patterns

Default:

```text
type[optional scope]: <summary>
```

Emoji mode when the user explicitly asks for gitmoji / emoji output:

```text
<emoji> <type>[scope]: <summary>
```

## Selection rules

- Pick one primary gitmoji based on the dominant intent of the change.
- Prefer the most specific matching emoji over broad defaults like `✨` or `🔧`.
- If multiple emojis fit, use the one that best explains why the change exists; put secondary nuance in the body.
- Use the Conventional Commit column as guidance only. It is not a strict one-to-one mapping.
- `semver` reflects upstream gitmoji guidance when provided.

## Full catalog

| Emoji | Code | Meaning | Recommended use | Conventional Commit analog | Semver |
|------|------|---------|-----------------|----------------------------|--------|
| 🎨 | `:art:` | Improve structure / format of the code. | Formatting cleanup, structural polish, code organization. | `style` / `refactor` | — |
| ⚡️ | `:zap:` | Improve performance. | Performance tuning, latency reduction, render/query optimization. | `perf` | patch |
| 🔥 | `:fire:` | Remove code or files. | Delete obsolete files, remove dead modules, cleanup. | `chore` / `refactor` | — |
| 🐛 | `:bug:` | Fix a bug. | Standard bug fix. | `fix` | patch |
| 🚑️ | `:ambulance:` | Critical hotfix. | Urgent production or release-blocking fix. | `fix` | patch |
| ✨ | `:sparkles:` | Introduce new features. | New user-visible features and capabilities. | `feat` | minor |
| 📝 | `:memo:` | Add or update documentation. | Docs, guides, READMEs, inline docs. | `docs` | — |
| 🚀 | `:rocket:` | Deploy stuff. | Deployment flow changes, publish/release operations. | `chore` / `release` | — |
| 💄 | `:lipstick:` | Add or update the UI and style files. | Visual polish, styling-only UI updates. | `style` | patch |
| 🎉 | `:tada:` | Begin a project. | Initial commit, project bootstrap, first public scaffold. | `chore` / `init` | — |
| ✅ | `:white_check_mark:` | Add, update, or pass tests. | Add or improve passing tests. | `test` | — |
| 🔒️ | `:lock:` | Fix security or privacy issues. | Security fix, privacy hardening, secret exposure remediation. | `fix` / `security` | patch |
| 🔐 | `:closed_lock_with_key:` | Add or update secrets. | Secret wiring, secret rotation references, credentials plumbing. | `chore` / `security` | — |
| 🔖 | `:bookmark:` | Release / Version tags. | Version tags, release labeling, tag-only flows. | `chore(release)` | — |
| 🚨 | `:rotating_light:` | Fix compiler / linter warnings. | Lint cleanup, static analysis warnings, compiler warnings. | `fix` / `chore` | — |
| 🚧 | `:construction:` | Work in progress. | Draft/WIP checkpoint when explicitly desired. | `wip` / `chore` | — |
| 💚 | `:green_heart:` | Fix CI Build. | Repair broken CI pipelines or build verification. | `ci` / `fix` | — |
| ⬇️ | `:arrow_down:` | Downgrade dependencies. | Pin or roll back to older dependency versions. | `build` / `chore` | patch |
| ⬆️ | `:arrow_up:` | Upgrade dependencies. | Upgrade dependencies or platform versions. | `build` / `chore` | patch |
| 📌 | `:pushpin:` | Pin dependencies to specific versions. | Lock exact dependency versions. | `build` / `chore` | patch |
| 👷 | `:construction_worker:` | Add or update CI build system. | CI pipelines, workflow config, build automation. | `ci` | — |
| 📈 | `:chart_with_upwards_trend:` | Add or update analytics or track code. | Analytics, telemetry, metrics instrumentation. | `feat` / `chore` | patch |
| ♻️ | `:recycle:` | Refactor code. | Internal refactor without intended behavior change. | `refactor` | — |
| ➕ | `:heavy_plus_sign:` | Add a dependency. | Introduce a new dependency. | `build` | patch |
| ➖ | `:heavy_minus_sign:` | Remove a dependency. | Remove an unnecessary dependency. | `build` | patch |
| 🔧 | `:wrench:` | Add or update configuration files. | App config, tool config, environment config. | `chore` / `build` | patch |
| 🔨 | `:hammer:` | Add or update development scripts. | Dev scripts, local tooling automation, helper scripts. | `chore` | — |
| 🌐 | `:globe_with_meridians:` | Internationalization and localization. | Translations, locale files, i18n support. | `feat` / `docs` | patch |
| ✏️ | `:pencil2:` | Fix typos. | Small wording fixes and typo cleanup. | `docs` / `fix` | patch |
| 💩 | `:poop:` | Write bad code that needs to be improved. | Deliberately temporary ugly hack. Use sparingly. | `chore` / `wip` | — |
| ⏪️ | `:rewind:` | Revert changes. | Revert a previous commit or behavior. | `revert` | patch |
| 🔀 | `:twisted_rightwards_arrows:` | Merge branches. | Merge commit or integration merge. | `merge` | — |
| 📦️ | `:package:` | Add or update compiled files or packages. | Bundles, compiled assets, distributables, package artifacts. | `build` | patch |
| 👽️ | `:alien:` | Update code due to external API changes. | External API breakage, SDK contract updates. | `fix` / `feat` | patch |
| 🚚 | `:truck:` | Move or rename resources (e.g.: files, paths, routes). | Rename files, move routes, relocate modules. | `refactor` / `chore` | — |
| 📄 | `:page_facing_up:` | Add or update license. | License file or licensing terms update. | `docs` / `legal` | — |
| 💥 | `:boom:` | Introduce breaking changes. | Intentional breaking change, incompatible API change. | `feat!` / `refactor!` | major |
| 🍱 | `:bento:` | Add or update assets. | Images, icons, fixtures, static assets. | `feat` / `chore` | patch |
| ♿️ | `:wheelchair:` | Improve accessibility. | Accessibility fixes and WCAG improvements. | `feat` / `fix` | patch |
| 💡 | `:bulb:` | Add or update comments in source code. | Comment-only changes. | `docs` / `chore` | — |
| 🍻 | `:beers:` | Write code drunkenly. | Joke / novelty commit only when explicitly desired. | `chore` | — |
| 💬 | `:speech_balloon:` | Add or update text and literals. | UX copy, labels, messages, text literals. | `feat` / `docs` | patch |
| 🗃️ | `:card_file_box:` | Perform database related changes. | Schema, migrations, data model updates. | `feat` / `fix` / `refactor` | patch |
| 🔊 | `:loud_sound:` | Add or update logs. | Add logging or increase observability output. | `chore` / `feat` | — |
| 🔇 | `:mute:` | Remove logs. | Remove noisy logs or sensitive logging. | `chore` / `refactor` | — |
| 👥 | `:busts_in_silhouette:` | Add or update contributor(s). | Contributor metadata and acknowledgements. | `docs` / `chore` | — |
| 🚸 | `:children_crossing:` | Improve user experience / usability. | UX improvements without major new functionality. | `feat` / `fix` | patch |
| 🏗️ | `:building_construction:` | Make architectural changes. | Large-scale architecture and module boundary updates. | `refactor` / `chore` | — |
| 📱 | `:iphone:` | Work on responsive design. | Mobile/responsive layout improvements. | `feat` / `style` | patch |
| 🤡 | `:clown_face:` | Mock things. | Test mocks, stubs, fake services. | `test` | — |
| 🥚 | `:egg:` | Add or update an easter egg. | Easter egg or hidden delight. | `feat` | patch |
| 🙈 | `:see_no_evil:` | Add or update a .gitignore file. | Ignore rules and repo hygiene. | `chore` | — |
| 📸 | `:camera_flash:` | Add or update snapshots. | Snapshot tests and snapshot fixtures. | `test` | — |
| ⚗️ | `:alembic:` | Perform experiments. | Experimental prototypes, spikes, trials. | `chore` / `experiment` | patch |
| 🔍️ | `:mag:` | Improve SEO. | SEO metadata, structured data, crawler improvements. | `feat` / `perf` | patch |
| 🏷️ | `:label:` | Add or update types. | Types, schemas, interface declarations. | `refactor` / `feat` | patch |
| 🌱 | `:seedling:` | Add or update seed files. | Seed data and dev bootstrap records. | `chore` / `feat` | — |
| 🚩 | `:triangular_flag_on_post:` | Add, update, or remove feature flags. | Feature flag config or rollout gating. | `feat` / `chore` | patch |
| 🥅 | `:goal_net:` | Catch errors. | Error boundaries, exception handling, guardrails. | `fix` | patch |
| 💫 | `:dizzy:` | Add or update animations and transitions. | Motion and transitions. | `style` / `feat` | patch |
| 🗑️ | `:wastebasket:` | Deprecate code that needs to be cleaned up. | Deprecation markers and pending removal. | `refactor` / `chore` | patch |
| 🛂 | `:passport_control:` | Work on code related to authorization, roles and permissions. | RBAC, permissions, authz flows. | `feat` / `fix` | patch |
| 🩹 | `:adhesive_bandage:` | Simple fix for a non-critical issue. | Small safe bug fix. | `fix` | patch |
| 🧐 | `:monocle_face:` | Data exploration/inspection. | Exploratory data work, inspection, audit scripts. | `chore` / `analysis` | — |
| ⚰️ | `:coffin:` | Remove dead code. | Remove unreachable or abandoned code. | `refactor` / `chore` | — |
| 🧪 | `:test_tube:` | Add a failing test. | Reproduce a bug with a failing test first. | `test` | — |
| 👔 | `:necktie:` | Add or update business logic. | Domain rules and application business logic. | `feat` / `fix` | patch |
| 🩺 | `:stethoscope:` | Add or update healthcheck. | Health endpoints, readiness/liveness checks. | `feat` / `chore` | — |
| 🧱 | `:bricks:` | Infrastructure related changes. | Infra, platform, deployment substrate. | `chore` / `ops` | — |
| 🧑‍💻 | `:technologist:` | Improve developer experience. | DX, tooling UX, local workflow quality. | `chore` / `feat` | — |
| 💸 | `:money_with_wings:` | Add sponsorships or money related infrastructure. | Funding links, billing/sponsorship plumbing. | `chore` / `feat` | — |
| 🧵 | `:thread:` | Add or update code related to multithreading or concurrency. | Concurrency primitives, async orchestration, threading. | `perf` / `feat` | — |
| 🦺 | `:safety_vest:` | Add or update code related to validation. | Validation, guard clauses, schema checks. | `fix` / `feat` | — |
| ✈️ | `:airplane:` | Improve offline support. | Offline mode, cache-first behavior, sync resilience. | `feat` | — |
| 🦖 | `:t-rex:` | Code that adds backwards compatibility. | Compatibility shims and upgrade bridges. | `fix` / `feat` | — |

## Quick picks

- New feature: `✨`
- Standard bug fix: `🐛`
- Critical hotfix: `🚑️`
- Docs: `📝`
- Refactor: `♻️`
- Performance: `⚡️`
- Tests: `✅` or `🧪`
- CI/workflows: `👷` or `💚`
- Dependencies: `⬆️` `⬇️` `➕` `➖` `📌`
- Security/privacy fix: `🔒️`
- Move/rename: `🚚`
- Breaking change: `💥`
- Accessibility: `♿️`
- Validation: `🦺`

## Examples

Default gitmoji-native style:

- `✨ add token refresh handling`
- `🐛 fix missing workspace path handling`
- `🚚 rename skill references to canonical paths`
- `💥 remove legacy commit title fallback`
- `👷 refresh release workflow automation`

Compatibility mode on request:

- `✨ feat(auth): add token refresh handling`
- `🐛 fix(config): handle missing workspace path`
- `🔒️ fix(auth): harden token verification`
- `💥 feat(api)!: remove legacy v1 response shape`
