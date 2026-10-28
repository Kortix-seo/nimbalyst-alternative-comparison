# Nimbalyst alternative: Kortix, the open-source AI Operating System

Kortix is the open-source AI Operating System, and it is the alternative to reach for when a desktop coding workspace stops at your laptop. Your agents, their skills, your company memory, and every connector live in one git repo you own, and each session runs on its own cloud computer.

Nimbalyst is an open-source visual workspace for running coding agents. It runs Claude Code, Codex, and OpenCode sessions side by side on your desktop, with visual editors for markdown, mockups, diagrams, and data models, a session kanban board, and optional git-worktree isolation ([nimbalyst.com](https://nimbalyst.com), [features](https://nimbalyst.com/features), [source](https://github.com/nimbalyst/nimbalyst)). It fits one developer who wants to stay local and watch the artifacts as they change. This repo is for the point where you want the work to run somewhere other than your machine, land through a review you control, and sit on infrastructure you can keep.

## Why Kortix

Kortix is the open-source AI Operating System. A project is a git repo that is the company: agents, skills, memory, connector config, and triggers are files inside it, and `kortix.yaml` declares the machine image, the connectors, and the triggers. Five facts decide most of the choice.

- **One repo you own.** Agents, skills, memory, connector config, and triggers are files in one git repo. You can `grep` the whole company and diff any change.
- **A cloud computer per session.** One isolated sandbox per session. Each session has its own isolated machine and branch.
- **A reviewed path to `main`.** Session work reaches `main` through a change request. Merge is default-deny for agents.
- **Any model, your keys.** Any model provider with your own keys. Or the ChatGPT plan you already pay for.
- **Self-host for free.** Run it on Kortix Cloud, in your VPC, or on your own on-prem network. Self-host is free.

Kortix is also widely adopted: 20,000+ GitHub stars on [Kortix on GitHub](https://github.com/kortix-ai/suna) (checked October 2026).

## Kortix compared with Nimbalyst

| Dimension | Kortix | Nimbalyst |
| --- | --- | --- |
| Category | Open-source AI Operating System | Open-source visual workspace for coding agents |
| Where it runs | Kortix Cloud, your VPC, or on-prem | Desktop app for macOS, Windows, and Linux |
| A session runs on | Its own cloud computer and branch | Your machine, in a local git worktree |
| Configuration lives in | One git repo you own | Plain markdown files in your repo |
| Finished work arrives as | A change request a person reviews | A red/green diff you accept or reject |
| Models and agents | Any model with your keys; an open-source agent harness | Claude Code, Codex, OpenCode, and Copilot |
| Self-host | Self-host is free | Local desktop app |
| Open source | Yes | Yes |

## The three guides

- [Kortix vs Nimbalyst: a head-to-head](docs/kortix-vs-nimbalyst.md) works through the two products dimension by dimension, including where each one fits.
- [The Nimbalyst alternatives](docs/nimbalyst-alternatives.md) covers the parallel coding workspaces buyers weigh in 2026, each cell drawn from the tool's own page.
- [Self-hosting an open-source agent workspace](docs/self-hosting-agent-workspaces.md) walks the real `kortix self-host` setup on a server you control.

## Start here

If you want the work to run off your laptop and land through a review, start at **https://nimbalystalternative.com**, the reader-facing guide behind this comparison.

## About this repo

Every claim about another tool links to that tool's own page or repository, so you can check it at the source. The comparison pages concern developer tooling; they name no customer, no price you cannot verify, and no metric that is not published by the vendor. Kortix links point at [kortix.com](https://kortix.com), [kortix.com/docs](https://kortix.com/docs), and [Kortix on GitHub](https://github.com/kortix-ai/suna).
