# dotfiles

Machine-as-code for this Mac. `Brewfile` is the source of truth for every app and CLI tool installed; this file explains what each one is *for* and how to actually use it. (Folder/repo layout conventions live separately in `~/Developer/README.md`.)

## Bootstrapping a new Mac

```sh
git clone <this-repo-url> ~/Developer/personal/dotfiles
brew bundle --file ~/Developer/personal/dotfiles/Brewfile
```

Idempotent — safe to re-run any time. It only installs what's missing, never reinstalls or upgrades what's already there. `HOMEBREW_BUNDLE_FILE` is set in `~/.zshrc`, so a bare `brew bundle` works from any directory.

---

## Day one

### Raycast
**Purpose:** Spotlight replacement — launcher, clipboard history, window management, snippets.
**Usage:** ⌘Space to open. Type an app name, do math (`24*7`), or search clipboard history.
**Tutorial:** Raycast → Settings → Extensions → enable "Clipboard History" and "Window Management," then set your own hotkeys.

### Bitwarden
**Purpose:** password manager + SSH agent (keys unlock with Touch ID, never paid for it).
**Usage:** Settings → Unlock with Touch ID. Settings → SSH Agent → Enable, then add keys as vault items.
**Tutorial:**
```sh
# ~/.zshrc or ~/.ssh/config
export SSH_AUTH_SOCK=~/Library/Containers/com.bitwarden.desktop/Data/.bitwarden-ssh-agent.sock
```
Then `ssh-add -l` should list your vault's keys.

### Ghostty
**Purpose:** terminal.
**Usage:** config is one plain-text file: `~/.config/ghostty/config`. No GUI settings maze.
**Tutorial:** theme + font + blur setup:
```ini
theme = catppuccin-mocha
font-family = JetBrainsMono Nerd Font
background-opacity = 0.92
background-blur-radius = 20
```

### VS Code / Zed / PyCharm CE
**Purpose:** VS Code for the extension ecosystem, Zed for fast/native editing, PyCharm CE (optional) for full Python IDE features.
**Usage:** `code .` or `zed .` from any project directory opens it there.
**Tutorial:** if `code` isn't found in the terminal, VS Code Command Palette → "Shell Command: Install 'code' command in PATH." Zed installs its CLI automatically.

### Obsidian
**Purpose:** local-first markdown knowledge base — architecture notes, ADRs, decision logs.
**Usage:** vault lives at `~/Documents/Architecture`, already synced by iCloud (no paid Obsidian Sync needed).
**Tutorial:** File → Open Vault → `~/Documents/Architecture`. Use `[[wikilinks]]` to connect notes.

---

## Containers

### Colima + docker + docker-compose + docker-buildx
**Purpose:** Docker Desktop replacement — fully open source, no commercial-use license needed.
**Usage:**
```sh
colima start              # boots the VM (first run downloads it)
docker ps                 # works exactly like Docker Desktop from here
docker compose up -d
colima stop                # frees RAM/CPU when you're done
```
**Tutorial:** `colima start --cpu 4 --memory 8` to size the VM; `colima status` to check it.

---

## Diagrams

### draw.io Desktop
**Purpose:** formal architecture diagrams — every AWS/Azure/GCP/k8s icon set built in.
**Usage:** File → New, or open a `.drawio` / `.drawio.png` (renders as an image, stays fully editable).

### d2
**Purpose:** diagrams-as-code, best for larger/complex diagrams.
**Usage:**
```sh
echo 'x -> y: hello' > diagram.d2
d2 diagram.d2 diagram.svg    # render to SVG
d2 --watch diagram.d2        # live preview while editing
```

### mermaid-cli (`mmdc`)
**Purpose:** diagrams-as-code that also renders natively inside GitHub markdown.
**Usage:**
```sh
echo 'graph TD; A-->B;' > diagram.mmd
mmdc -i diagram.mmd -o diagram.png
```
Or skip the CLI entirely — paste a ` ```mermaid ` fenced block into a README and GitHub renders it for you.

---

## Engineering toolbelt — desktop apps

### Bruno
**Purpose:** API client (Postman without the account nagging) — collections are plain files, diffable in PRs.
**Usage:** New Collection → point it at a folder inside a repo. Requests save as `.bru` files.

### DBeaver Community
**Purpose:** one GUI for every database — Postgres, MySQL, Redis, SQLite, etc.
**Usage:** New Database Connection → pick a driver → DBeaver fetches the JDBC driver automatically.

### UTM
**Purpose:** full virtual machines via QEMU — other OSes/architectures.
**Usage:** Create a New Virtual Machine → point at an ISO.

### mitmproxy
**Purpose:** inspect, modify, and replay HTTP(S) traffic from any app.
**Usage:**
```sh
mitmproxy    # terminal UI
mitmweb      # browser UI instead
```
Point a device's HTTP proxy at `localhost:8080`, then visit `mitm.it` while proxied to install the CA cert and see HTTPS traffic too.

---

## Engineering toolbelt — CLI belt

| Tool | Purpose | Try it |
|---|---|---|
| **gh** | GitHub from the terminal | `gh auth login` once, then `gh pr create`, `gh pr view --web`, `gh issue list` |
| **fzf** | fuzzy-filter any list | `Ctrl+R` for fuzzy history search (add `eval "$(fzf --zsh)"` to enable); or `git branch \| fzf` |
| **fd** | faster/friendlier `find` | `fd config` instead of `find . -iname "*config*"` — respects `.gitignore` automatically |
| **bat** | `cat` with syntax highlighting | already aliased — just `cat somefile.py` |
| **eza** | `ls` with icons + git status | already aliased — try `eza --tree --level=2` |
| **zoxide** | `cd` that learns your habits | already wired — after visiting a dir a few times, `z partial-name` jumps there from anywhere |
| **git-delta** | readable git diffs | set once: `git config --global core.pager delta`, then every `git diff`/`log -p` looks better |
| **lazygit** | full git workflow, one TUI | run `lazygit` in any repo — `space` stages, `c` commits, `p`/`P` pull/push, `?` for keybinds |
| **btop** | resource monitor | run `btop` — click a process for detail, `q` to quit |
| **tldr** | example-based cheat sheets | `tldr tar` (first run caches the pages) |
| **yq** | `jq` for YAML/JSON/XML | `yq '.spec.replicas' deployment.yaml`, or `yq -i '.spec.replicas = 3' deployment.yaml` |
| **hyperfine** | rigorous CLI benchmarking | `hyperfine 'old.sh' 'new.sh'` — reports mean/stddev, tells you which is actually faster |

---

## Runtimes & package managers

### mise
**Purpose:** one version manager for node/python/go/everything — replaces nvm/pyenv/rbenv/etc.
**Usage:**
```sh
mise use -g node@lts python@3.13   # global defaults
cd some-project
mise use node@20                    # pins THIS project to node 20 (writes mise.toml)
mise install                        # installs whatever a cloned repo's mise.toml/.tool-versions pins
```

### uv
**Purpose:** fast Python package/venv manager.
**Usage:**
```sh
uv init myproject && cd myproject
uv add django
uv run python manage.py runserver
```

### pnpm
**Purpose:** fast, disk-efficient Node package manager.
**Usage:** `pnpm install`, `pnpm add react`, `pnpm dlx create-next-app` — same mental model as npm/yarn.

### bun
**Purpose:** JS/TS runtime + bundler + test runner + package installer, one fast binary.
**Usage:** `bun install` (10–20x faster than npm for installs), `bun run script.ts` (runs TypeScript directly, no build step), `bun test`.

---

## Terminal aesthetics

### starship
**Purpose:** fast, minimal, informative shell prompt (git branch, language versions, exit codes).
**Usage:** already wired via `starship init` in `.zshrc`. Customize: `starship preset nerd-font-symbols -o ~/.config/starship.toml`.

### fastfetch
**Purpose:** system info splash screen.
**Usage:** just run `fastfetch`.

### JetBrains Mono Nerd Font
**Purpose:** coding font with icon glyphs — required for eza's icons and starship's symbols to render instead of showing empty boxes.
**Usage:** set as the font in Ghostty (`font-family = JetBrainsMono Nerd Font`) and in VS Code/Zed's editor font settings.

---

## macOS quality of life

Set-once-and-forget menu bar apps:

- **Shottr** — screenshots with annotation, OCR, scrolling capture. Output already redirected to `~/Pictures/Screenshots`.
- **AltTab** — Windows-style ⌘Tab showing every window. Needs Accessibility permission on first launch.
- **Ice** — menu bar manager; choose which icons stay hidden in its settings.
- **Stats** — CPU/RAM/network in the menu bar; enable the sensors you want, disable the rest.
- **AppCleaner** — drag an app onto it to remove it along with its leftover files.
- **KeepingYouAwake** — click the menu bar icon to block sleep during a long build/demo; click again to release.

---

## Principal-engineer side

### Fathom
**Purpose:** AI meeting notes and transcription.
**Usage:** connect your calendar in Fathom's settings — it joins scheduled calls automatically and produces a transcript + summary afterward.

### herdr
**Purpose:** terminal workspace manager for AI coding agents — persistent sessions, git worktrees, and panes so you can run/monitor multiple agents (Claude Code, etc.) side by side instead of juggling tabs.
**Usage:**
```sh
herdr                        # launch or attach to the persistent session
herdr status                 # check local client + running server status
herdr worktree --help        # git worktree helpers over the socket API
herdr session attach <name>  # jump back into a named session
```
**Tutorial:** run it as a background service so it survives reboots and reattaches instantly:
```sh
brew services start herdr
```
Or run it in the foreground when you just want it for this terminal session: `herdr server`.

---

## Security

### LuLu
**Purpose:** outbound firewall — alerts when something tries to phone home.
**Usage:** first launch walks you through allow/block rules. Approve your normal tools once; get alerted on anything new.

---

## Optional (commented out in the Brewfile)

- **Secretive** — SSH keys in the Secure Enclave, hardware-backed, keys never leave the Mac. Alternative to Bitwarden's SSH agent for maximum paranoia.
- **PyCharm CE** — full Python IDE if VS Code's Python support isn't enough.
- **Rancher Desktop** — GUI + built-in Kubernetes, alternative to Colima if you want a visual container manager.

Uncomment the relevant line in `Brewfile` and run `brew bundle` to install.

---

## Wiring notes — installed ≠ working

A handful of these do nothing until one line of config activates them. Already done in `~/.zshrc`:

```zsh
alias cat="bat"
alias ls="eza --icons"
eval "$(zoxide init zsh)"
eval "$(starship init zsh)"
eval "$(mise activate zsh)"
```

Still outstanding, once `git-delta` is actually installed:
```sh
git config --global core.pager delta
```
