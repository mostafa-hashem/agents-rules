# AI Agent Rules

A shared rule set for Flutter, Rust desktop, web frontends, and backend integration. Use it across projects with different stacks or combine the relevant rules in a monorepo.

`rules.mdc` is the always-applied entry point. It tells the agent which files to read for the task. The other rules have descriptions for relevance-based selection in Cursor, so platform and provider guidance loads when it applies.

## Start here

| Working on | Rules to apply |
| --- | --- |
| Flutter on Windows, macOS, or Linux | [Flutter](flutter.mdc), [Desktop UX](desktop-ux.mdc), [Flutter Desktop](flutter-desktop.mdc) |
| Flutter on Android or iOS | [Flutter](flutter.mdc), [Flutter Mobile](mobile-flutter.mdc) |
| Rust native desktop | [Desktop UX](desktop-ux.mdc), [Rust Desktop](rust-desktop.mdc) |
| Tauri desktop | [Rust Desktop](rust-desktop.mdc), [Desktop UX](desktop-ux.mdc), [Web Frontend](web-frontend.mdc) |
| Flutter with a Rust bridge | The Flutter rules for the target platform plus the FFI section in [Rust Desktop](rust-desktop.mdc) |
| REST, GraphQL, gRPC, Firebase, or a custom backend | [Backend Integration](backend-integration.mdc), [Data Sync and Security](data-sync-and-security.mdc) |
| Supabase | The backend rules plus [Supabase](supabase.mdc) |
| Browser frontend | [Web Frontend](web-frontend.mdc) for HTML/webview stacks, or [Flutter](flutter.mdc) and applicable browser guidance for Flutter Web |

[Engineering Quality](engineering-quality.mdc) and [Architecture and State](architecture-and-state.mdc) cover implementation across stacks. For UI work, also read [Design System](mandatory-design.mdc) and [Interaction and UX](interaction-ux.mdc). [English Comments](english-comments-only.mdc) and [Git Commits](git-commits.mdc) cover source comments and commit messages. The full task-to-rule map lives in [the entry point](rules.mdc).

For example, a Flutter desktop feature backed by Supabase uses the Flutter, desktop, design, UX, and backend rules together. Its verification can include keyboard and resize behavior in the packaged app, expired sessions, and authorization for the affected Supabase resources.

## Install in Cursor

Keep the entire set of `.mdc` files in `.cursor/rules/` so the relative links resolve.

### Use a Git submodule

Run this from the consuming project's repository root when `.cursor/rules` is available as a new submodule path:

```sh
git submodule add https://github.com/mostafa-hashem/agents-rules.git .cursor/rules
```

Commit `.gitmodules` and the submodule reference in the consuming repository. Other contributors can initialize it with:

```sh
git submodule update --init --recursive
```

To adopt a newer rules revision, run the following, review the update, and commit the new submodule reference in the consuming repository:

```sh
git submodule update --remote .cursor/rules
```

### Copy the rules into the project

Copy every root-level `.mdc` file from this repository into the consuming project's `.cursor/rules/` directory. Review overlapping filenames before replacing existing project rules. Keep the filenames together so the entry point can find them.

### Use another coding agent

Use the agent's project-instructions mechanism to point it to `rules.mdc` and its companion files. If the agent does not understand MDC metadata, include an explicit instruction to read the entry point and follow its task-to-rule map.

## Extend the set

- Add a clearly named `.mdc` file with a task-specific `description` and `alwaysApply: false`.
- Register it in [the entry point](rules.mdc). Keep shared guidance in its existing file and link to it where needed.
- Document project-specific target OS versions, toolkit, design components, backend contracts, and release commands in the consuming project.
- Customize the reply preferences in `rules.mdc` for the project owner.

References: [Cursor rule activation](https://cursor.com/docs/rules), [Flutter desktop](https://docs.flutter.dev/platform-integration/desktop), [Cargo CI](https://doc.rust-lang.org/cargo/guide/continuous-integration.html), and [Tauri capabilities](https://v2.tauri.app/security/capabilities/).
