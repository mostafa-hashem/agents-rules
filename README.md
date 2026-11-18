# Universal AI Agent Rules (`.mdc`)

A battle-tested, stack-agnostic suite of **10 mandatory `.mdc` rule files** designed to enforce production-grade engineering, UX polish, security, performance, and clean architecture across AI coding agents (Cursor, Antigravity, and compatible `.mdc` rule runners).

Every file sets `alwaysApply: true`, binding the entire suite automatically across **any application, framework, state management pattern, backend, or database**.

---

## Why This Rule Suite?

Most AI agent rule sets either stay too vague or lock you into one framework. This collection encodes hard-won production lessons into concrete, non-negotiable constraints while staying adaptable to your codebase:

- **Any Frontend / Client:** Flutter (iOS/Android), Next.js, React, TypeScript, or native/cross-platform clients.
- **Any Architecture:** Feature-First, Clean Architecture, BLoC/Cubit, Riverpod, Provider, Redux, Zustand, MVVM.
- **Any Backend & Database:** Supabase, Firebase, REST, GraphQL, gRPC, WebSockets, PostgreSQL, MySQL, MongoDB, SQLite, Drift, Hive, Isar, IndexedDB.

---

## Core Non-Negotiables

The rules force the AI agent to inspect your project before editing and strictly enforce five core pillars on every task:

1. **0ms Optimistic UI First (with Rollback):** User actions update in-memory state and UI synchronously before awaiting encryption, media uploads, or network/DB calls, capturing a snapshot to roll back cleanly on failure.
2. **Live / Decrypted State Priority Over Stale Cache:** In-memory decrypted caches and live realtime snapshots always win over local persistence (SQLite, IndexedDB, Drift, Hive) unless `cache.timestamp >= server.timestamp`.
3. **Custom Feedback & Toast Exclusivity:** User-facing feedback must go through centralized toast helpers (`showSuccessToast`, `showErrorToast`, etc.) and shared confirmation dialogs—raw snackbars (`ScaffoldMessenger.showSnackBar`) and `window.alert` are forbidden.
4. **Design Tokens, Shared Primitives & 100% Localization:** Zero hardcoded UI strings, zero raw hex or framework colors in features, script-aware bidirectional text (`ContentDirectionality` / `dir="auto"`), unified icons, skeleton loaders instead of full-page spinners, and structured logging (`appLog`).
5. **Zero N+1 Queries & Scoped UI Rebuilds:** Resolve encryption keys and sender lookups once per batch, peek synchronous in-memory caches first, and isolate list/timeline rebuilds (`buildWhen`, `BlocSelector`, selectors, revision counters).

---

## Rule Files Reference

| # | File | Scope & Enforcement |
| --- | --- | --- |
| 1 | `rules.mdc` | Master index, mandatory pre-edit inspection, 5 core non-negotiables, layer mapping, priority hierarchy, and reply formatting |
| 2 | `git-commits.mdc` | English-only commit messages focused on *why*; forbids AI/tool `Co-authored-by` trailers |
| 3 | `english-comments-only.mdc` | English-only developer comments/docstrings/`TODO`s; zero hardcoded UI strings |
| 4 | `engineering-quality.mdc` | Minimal diffs, analyzer/lint zero-warning enforcement, `context.mounted` safety, lazy controllers, viewport list purity, Windows PowerShell `;` syntax |
| 5 | `mandatory-design.mdc` | Semantic color tokens, typography scale (no fixed `Text` heights), script-aware bidi & fonts, unified icon pack, no ScreenUtil, shared primitives |
| 6 | `interaction-ux.mdc` | Destructive-action confirmations, custom toasts, skeletons, scoped mutation loading, 0ms optimistic UI, tap guards, keyboard/system insets, active-tab re-tap rules |
| 7 | `architecture-and-state.mdc` | Feature-first folders (`State / Data / UI`), thin screens (`~150–250` lines), zero business logic or direct service calls in UI, scoped rebuilds, in-memory cache retention |
| 8 | `data-sync-and-security.mdc` | Backend/DB abstraction, `AES-256-GCM` & isolate/worker crypto, authoritative stream/cache reconciliation, preview priority, zero N+1, speed-critical push notification tray hot paths |
| 9 | `mobile-flutter.mdc` | Flutter mobile entry binding `#1–8` + `TabBar.onTap` trap guard + Crashlytics & native release checklist |
| 10 | `web-frontend.mdc` | Next.js/React/TS architecture, CSS design tokens, Web Workers for crypto, SSR auth & RLS security, cross-platform sync parity |

---

## Priority Order When Rules Overlap

1. **`data-sync-and-security.mdc`** — Wins for data synchronization, cache reconciliation, encryption, push/tray hot paths, and security.
2. **`mandatory-design.mdc`** — Wins for colors, typography, icons, shared UI primitives, and localization/bidi.
3. **`english-comments-only.mdc`** — Wins for comment language and keeping UI copy localized.
4. **`engineering-quality.mdc`**, **`interaction-ux.mdc`**, and **`architecture-and-state.mdc`** — Govern code quality, UX behavior, and architectural separation.
5. **`mobile-flutter.mdc`** and **`web-frontend.mdc`** — Govern platform-specific requirements within their respective workspaces without cross-bleeding widget/DOM rules.

---

## How to Use in Your Projects

Place all 10 `.mdc` files inside your project's `.cursor/rules/` directory (or your AI IDE's global rules directory).

### Option 1: Add as a Git Submodule (Recommended)

Keeps your rules versioned and easy to update across projects.

**Bash / macOS / Linux:**

```bash
mkdir -p .cursor
git submodule add https://github.com/mostafa-hashem/agents-rules.git .cursor/rules
```

**Windows PowerShell:**

```powershell
New-Item -ItemType Directory -Force -Path .cursor; git submodule add https://github.com/mostafa-hashem/agents-rules.git .cursor/rules
```

To pull future rule updates in any project:

```bash
git submodule update --remote .cursor/rules
```

### Option 2: Copy Directly into a Repository

**Bash / macOS / Linux:**

```bash
git clone https://github.com/mostafa-hashem/agents-rules.git /tmp/agents-rules && mkdir -p .cursor/rules && cp /tmp/agents-rules/*.mdc .cursor/rules/
```

**Windows PowerShell:**

```powershell
git clone https://github.com/mostafa-hashem/agents-rules.git $env:TEMP\agents-rules; New-Item -ItemType Directory -Force -Path .cursor\rules; Copy-Item $env:TEMP\agents-rules\*.mdc .cursor\rules\
```

### Option 3: Global Agent Rules

If your AI editor supports global user rules, copy the contents of `rules.mdc` (and any satellite files you want active everywhere) into your global rules configuration so they apply across every workspace automatically.

---

## How the Agent Applies These Rules

Because every file uses `alwaysApply: true`:

1. **Automatic Full-Set Binding:** You do not need to `@`-mention individual `.mdc` files. Mentioning `rules.mdc` (or simply opening the workspace) activates all 10 files together.
2. **Project Adaptation:** Before writing code, the agent scans your repository to map canonical concepts in the rules (`appLog`, `AppException`, `showErrorToast`, semantic theme tokens, localization files, state controllers) onto your existing helpers—or creates clean centralized wrappers matching these patterns if your project is greenfield.
3. **Monorepo Ready:** Works seamlessly whether your repository is a single Flutter/Web app or a monorepo containing mobile, web, and shared database migrations.

---

## Customization

- **Assistant Reply Prefix & Length (`rules.mdc`):** By default, `rules.mdc` instructs the agent to start replies with the owner's name (`Mostafa, ` / `مصطفى، `), keep task-completion confirmations ultra-concise (2–3 words unless an explanation was requested), and format Arabic responses cleanly in RTL with separate LTR code blocks. Update the **Assistant Replies** section in `rules.mdc` to match your own name and preferred verbosity.
- **Tech-Specific Exceptions:** If a project intentionally uses a different UI kit or state manager, document the concrete class/helper names in your repo's `rules.mdc` mapping table so the agent resolves them immediately without guessing.
