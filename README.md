# k3d-bin

AUR package for [k3d](https://github.com/k3d-io/k3d) — run [k3s](https://k3s.io) clusters in Docker. Pre-built upstream binary, multi-arch (x86_64, aarch64, armv7h).

[![AUR](https://img.shields.io/aur/version/k3d-bin?label=AUR&style=flat-square)](https://aur.archlinux.org/packages/k3d-bin)
[![CI](https://img.shields.io/github/actions/workflow/status/88plug/k3d-bin/auto-release.yml?label=auto-release&style=flat-square)](https://github.com/88plug/k3d-bin/actions)
[![License](https://img.shields.io/badge/license-MIT-blue?style=flat-square)](https://github.com/k3d-io/k3d/blob/main/LICENSE)

## Install

```bash
yay -S k3d-bin
```

Installs `/usr/bin/k3d`, bash/zsh/fish completions, and the upstream MIT license. Conflicts with `k3d` and `k3d-git`.

## Why -bin

Arch's official repos do **not** ship k3d. The AUR has only `k3d-git` (build-from-source, 1 vote, untrusted). This package:

- Pre-built binary from k3d's official GitHub release (~24MB, no Go toolchain needed)
- Multi-arch: x86_64, aarch64, armv7h
- SHA256-verified against upstream `checksums.txt`
- Auto-tracks upstream — new release on `k3d-io/k3d` lands on AUR within 24h via the auto-update workflow

## Verify

```bash
k3d version
```

## Usage

```bash
k3d cluster create test
k3d cluster list
k3d cluster delete test
```

For GPU-ready clusters, see [k3d-gpu](https://github.com/88plug/k3d-gpu).

## Automation

`auto-release.yml` runs daily at 06:00 UTC. When `k3d-io/k3d` publishes a new release:

1. Bump `pkgver` + recompute `sha256sums_{x86_64,aarch64,armv7h}` from the upstream `checksums.txt`
2. Commit, tag `vX.Y.Z`
3. Dispatch `aur-deploy.yml` → AUR receives the update within ~40s of the upstream release

No PAT required (uses GitHub-default `GITHUB_TOKEN` + `workflow_dispatch` chaining).

## Related

- [k3d-gpu](https://github.com/88plug/k3d-gpu) — GPU-passthrough wrapper for k3d
- [Upstream k3d](https://github.com/k3d-io/k3d)
