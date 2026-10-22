# Self-hosting an open-source agent workspace

An open-source agent workspace can run in two shapes. The first is a desktop app on your machine, the shape Nimbalyst, Orca, and Emdash use. The second is a server you operate for your team, the shape Kortix ships as `kortix self-host`. This guide walks the second one, because it is the path a developer takes when the agents have to run off a laptop and the data has to stay inside the network.

## What the two shapes mean for you

A desktop workspace keeps everything local: the app, the git worktrees, the agent sessions. It is fast to start and easy to leave. A self-hosted workspace puts one stack on a server you control, so sessions run in the background, several people share the same configuration, and nothing leaves your infrastructure. Kortix does both. You can run it on Kortix Cloud, in your VPC, or on your own on-prem network, and self-host is free ([kortix.com/docs](https://kortix.com/docs), [self-hosting guide](https://kortix.com/docs/host)).

## What you need before you start

The self-hosting guide lists the requirements plainly. You need a Linux server with a public IP, DNS records for your domain and its `api.` subdomain pointing at that server before the first start, and ports 80 and 443 open inbound. You also need a sandbox provider key (Platinum or the legacy Daytona fallback) and a model provider key, which you add in the web app after the first sign-in. The instance has to be reachable from the internet so the sandboxes can call back to its API.

## Install and start

On a server that already has Docker and the Compose plugin, install the CLI and bring the stack up:

```sh
curl -fsSL https://kortix.com/install | bash
kortix self-host init --domain kortix.example.com --admin-email you@example.com
kortix self-host start
```

`kortix self-host init` writes `docker-compose.yml`, `.env`, a `Caddyfile`, and `updater.sh` into `~/.config/kortix/self-host/<instance>/`. The first interactive run asks every setup question; `--yes`, or a shell with no terminal, keeps the defaults. If the sandbox key is missing at that point, `init` and `start` print a warning and continue, and you can add the key later.

If a bootstrap script already installed Docker and the CLI for you (the guide covers that path too), the remaining steps are the same. If it added your user to the `docker` group, open a new shell first, then answer the setup questions:

```sh
kortix self-host configure
kortix self-host start
```

`configure` asks for your admin email, your sandbox provider key, and the preview domain, and writes the answers to the files. `start` applies them. Then check the instance and fix every failing check:

```sh
kortix self-host doctor
```

## Try it first with a tunnel

If you want to evaluate Kortix before you point DNS at a server, the tunnel mode needs no domain:

```sh
kortix self-host init --tunnel cloudflare
kortix self-host start
```

The web app opens at `http://localhost:13737`, and `cloudflared` publishes the API on a temporary HTTPS URL. That URL changes each time the tunnel restarts, so for a stable one you create a named tunnel and set two values with `kortix self-host env set`, then start again. The self-hosting guide has the exact keys.

## What runs where

`kortix self-host start` runs one Compose project, `kortix-<instance>`, that holds the frontend, `kortix-api` at `/v1`, the standalone `llm-gateway`, a one-shot database migration job, a daily updater, and the Supabase distribution for Postgres, auth, storage, and the rest. In domain mode, Caddy terminates TLS on ports 80 and 443.

Not everything is on the server. Sessions run on a sandbox provider, not on the host, so keep a provider key ready. The stack pulls its images from Docker Hub and calls the model providers your projects connect.

## After the first start

Open your domain and sign up with the admin email, connect GitHub, create a team account and a project, and add a model key. Do this as soon as the stack starts: until you set `EMAIL_URL` or `DISABLE_SIGNUP=true`, anyone who reaches the instance can create a confirmed account. Restricting account creation is on by default in `configure`, and `kortix self-host doctor` is the check to trust before you hand the URL to anyone else.

Two decisions decide most of a self-host deploy: whether the work should leave your laptop at all, and whether the configuration should belong to a server you own or to an app you install. Kortix answers both the same way, with the open-source AI Operating System running the whole control plane inside your network.
