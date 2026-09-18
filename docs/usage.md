# Using Software Production

Run the path-based examples from a parent directory containing `workspace` and
the stack source directories. Paths are relative to that directory; adjust them
to your layout. Commands without `--workspace` run from the workspace root.

Software Production adds project onboarding, briefs, planning, implementation,
project rules and privacy review to your [Dryft](https://usedryft.com) workspace. Your source stays in
its own directory; [Dryft](https://usedryft.com) stores the context needed to continue work across sessions.

## Install and start

Install [Dryft](https://usedryft.com) and initialize a workspace first. In your workspace's agent session,
invoke `/dryft-install-stack` in Claude or `$dryft-install-stack` in Codex and ask
to install `dryft-software-production`. The skill searches the marketplace,
inspects the selected release and guides installation after review.

For the same flow in the CLI:

```sh
dryft marketplace search "software production"
dryft stack install dryft-software-production --inspect
dryft --workspace ./workspace stack install dryft-software-production
dryft --workspace ./workspace stack list
```

Replace the workspace path with your own. Review the source, selected version,
prerequisites and any warnings from inspection before installing. Add
`--version VERSION` to both inspection and installation to select a particular
release. [Dryft](https://usedryft.com) downloads and validates the stack through the registry; no clone
or manual download is needed. Registry installation requires network access.

The stack installs skills, templates and guides. It registers no automatic hooks
and imports no brain knowledge. Optional project constitution setup creates
project-local startup hooks only when requested or accepted.

Restart Claude or Codex in your [Dryft](https://usedryft.com) workspace after installation. Invoke skills
with `/dryft-software-production-<action>` in Claude, or
`$dryft-software-production-<action>` in Codex. You can also use the host's skill
picker. Supply the project name or source path when needed to identify the project.

## Start a project

For existing source, invoke `/dryft-software-production-add` and give the source
path. The agent links the project, explains its structure and setup, and offers
onboarding and a brief. Linking alone leaves source files unchanged.

For a new project, invoke `/dryft-software-production-brief` and choose a source
directory outside your [Dryft](https://usedryft.com) workspace. Describe the problem, intended users,
scope, constraints and what successful delivery looks like. The agent uses what
you have already supplied and asks only for missing information.

Review the resulting brief and approve its contents. Then invoke
`/dryft-software-production-init` to create a bounded implementation plan and
initial work items. Changes to the brief require approval of the revised content
before planning continues.

## Build and continue work

Use `/dryft-software-production-tasks` to see ready work, then
`/dryft-software-production-build <task-id>` to implement a selected item. Review
the changes and observed checks, then use `/dryft-software-production-close
<task-id>` to complete or cancel it. Closure preserves the record unless you
explicitly request deletion.

Use `task` to add individual work items and `triage` to clarify priorities or
resolve dependencies. Implementation and closure update handoffs so a later
session can resume with the relevant decisions and next steps.

| Action | What it does |
| --- | --- |
| `add` | Link existing source and offer onboarding and a brief. |
| `brief` | Define the problem, users, scope, constraints and acceptance criteria. |
| `init` | Plan initial work from the approved brief. |
| `task <overview>` | Create one work item with a bounded outcome. |
| `tasks <status>` | List work; defaults to `ready`, with `all` for every state. |
| `triage` | Clarify, prioritize, resolve dependencies and group work. |
| `build <task-id>` | Implement selected work in the linked source directory. |
| `close <task-id>` | Complete or cancel selected work and save a handoff. |
| `constitution <project-id>` | Define project rules and configure local startup loading. |
| `pii <project-id>` | Review staged changes and the complete proposed commit message. |

Each action uses the `dryft-software-production-` prefix. For optional setup and
review, see [project constitution](constitution.md) and
[privacy review](privacy-review.md).

## Answer questions in chat or [Dryft](https://usedryft.com) UI

Say “use dui” to answer missing-input questions in a local browser page, or answer
in chat. A complete request can proceed without an interview. Submit the page to
send your answers; drafts and cancelled pages do not authorize work. Submitted
answers inform the brief or plan, which you can then review. UI responses remain
local until explicitly cleaned up.

## Files and preferences

Shared project configuration lives in `.dryft/project.json` inside the source
repository, alongside the brief and any internal work records. These files are
intended for version control. Private `.dryft/developer.json` holds local tool,
model and workflow preferences; it must be ignored and contain no credentials.
The default is direct, manual work with no predefined agent roles.

Internal Markdown is the default work tracker. If you select an external system,
it owns descriptions and status; local context contains references and
implementation notes. External workflows require your connected provider and
configured status mapping. The stack does not synchronize a duplicate local queue
or install dependencies for you.

Handoffs live in your workspace under
`.dryft/state/software-production/<project-id>/`. They are operational context,
separate from approved brain knowledge. See the [workflow reference](workflow.md)
for file formats, preservation rules, orchestration preferences and UI behavior.

## Update or remove

Inspect an available update before approving it:

```sh
dryft --workspace ./workspace stack update dryft-software-production --check
```

Approve the inspected plan through the CLI's interactive update flow or pass its
`approval_sha256` with `--approve` after reviewing it. Registry installations check the
recorded registry for an approved newer release. An update requires a higher version. Preserve any edits to
installed files and restore their recorded originals before retrying a blocked
update or removal.

To remove the stack:

```sh
dryft --workspace ./workspace stack remove dryft-software-production
```

Removal preserves project files, project-local constitution setup, workspace
handoffs and brain knowledge. Restart the host after an update or removal to
refresh loaded skills.
