![Dryft Software Production](docs/assets/banner.png)

# Software Production

A [Dryft](https://usedryft.com) stack for taking software projects from a brief to working code. It
provides skills and templates for project onboarding, planning, implementation
and handoffs, plus optional project rules and pre-commit privacy review. Work
stays in your linked source repository, with questions handled in chat or [Dryft](https://usedryft.com) UI.

## Release status

Candidate version: **0.2.0**. Canonical source: [1one8/dryft-software-production](https://github.com/1one8/dryft-software-production).
The registry commands below are the planned public installation path; production
listing and installation are still awaiting release verification.

Local acceptance is on Linux x86_64 with Python 3.12 and Claude/Codex. macOS
and native Windows are unverified. The constitution setup helper currently requires POSIX.
Agent-directed work follows the linked project instructions and user authorization;
source edits, Git operations and external services are disclosed in the usage guide.

## Install

With [Dryft](https://usedryft.com) installed and a workspace initialized, ask your agent to install
`dryft-software-production` using `/dryft-install-stack` (Claude) or
`$dryft-install-stack` (Codex). The skill finds the stack in the marketplace,
shows the selected release for review and installs it from the registry.

Or use the CLI, replacing the workspace path with your own:

Run the path-based examples from a parent directory containing `workspace` and
the stack source directories. Paths are relative to that directory; adjust them
to your layout. Commands without `--workspace` run from the workspace root.

```sh
dryft stack install dryft-software-production --inspect
dryft --workspace ./workspace stack install dryft-software-production
```

Review the inspected release and any prerequisites before running the install command.
Restart Claude or Codex in your
[Dryft](https://usedryft.com) workspace to load the skills, then start with
`/dryft-software-production-add` for existing source or
`/dryft-software-production-brief` for a new project. In Codex, use `$` instead
of `/`, or select the skill from the picker.

See the [usage guide](docs/usage.md) for the full workflow and available skills.

## License

Licensed under the [Apache License 2.0](LICENSE). Copyright 1one8 (Pty) Ltd.
