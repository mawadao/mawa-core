# mawa-core

A lightweight agent runtime in Go, based on [PicoClaw](https://github.com/sipeed/picoclaw). It runs
an agent with tools, skills, memory and chat channels in a few megabytes of RAM, so it can run
on small, cheap hardware as well as in the cloud.

Part of [mawa](https://github.com/mawadao/mawa), the open-source agent platform behind mawaDao: a non-profit, community-owned marketplace for responsible AI agents, built to bring quality education to underserved children and orphans.

## What it does

- **Agent loop:** models from many providers, tools, skills (`workspace/skills/`), memory and scheduled jobs.
- **Channels:** Telegram, Discord, Slack, WhatsApp and more (`pkg/channels/`).
- **Launcher and web UI** (`web/`): configure and run the gateway from a browser.
- **Hosting:** each instance is a launcher (`:18800`) plus gateway (`:18790`). [`mawa-manager`](https://github.com/mawadao/mawa/tree/main/microservices/manager) runs and manages instances for members.

This is the next-generation runtime; it will replace [`mawa-gateway`](https://github.com/mawadao/mawa-gateway).
See the [architecture](https://github.com/mawadao/mawa/blob/main/docs/architecture.md).

## Run it locally

Requires Go (version in `go.mod`).

```bash
make build                       # binary in build/picoclaw
./build/picoclaw onboard         # create a config and workspace
./build/picoclaw gateway
```

Or with Docker: `docker build -f docker/Dockerfile .` and see `docker/docker-compose.yml`.
Checks: `make test`, and `golangci-lint` as in `.github/workflows/pr.yml`.

Full documentation, including configuration and channels, is in [`docs/`](docs/). Start with
[docs/picoclaw-README.md](docs/picoclaw-README.md).

## Upstream

This repository follows PicoClaw's `main` (forked at bbf6893c, 2026-08-19). Internal names (`picoclaw` binary,
Go module `github.com/sipeed/picoclaw`, config paths) are unchanged so upstream fixes merge
cleanly. To pull them in:

```bash
git remote add upstream https://github.com/sipeed/picoclaw.git   # once
git fetch upstream
git merge upstream/main
```

PicoClaw's README, CONTRIBUTING, LICENSE and release workflows were moved or replaced here. When
a merge conflicts on those files, keep mawaDao's version.

## Contributing

Read the [contributing guide](https://github.com/mawadao/mawa/blob/main/CONTRIBUTING.md) before opening a pull request.
Fixes that aren't mawaDao-specific are better sent upstream to PicoClaw first.
Work lands on `main`; releases are tagged `vX.Y.Z` as described in [RELEASING.md](https://github.com/mawadao/mawa/blob/main/RELEASING.md).

## Licence

Apache 2.0. See [LICENSE](LICENSE), and [NOTICE](NOTICE) for the MIT-licensed PicoClaw code it builds on.
