# Machine-as-code: `brew bundle` rebuilds this Mac from scratch.
# HOMEBREW_BUNDLE_FILE in ~/.zshrc points here, so `brew bundle` works from anywhere.

# ── Day one ──────────────────────────────────────────────────
cask "raycast"              # launcher, clipboard history, window mgmt, snippets
cask "bitwarden"            # passwords + SSH agent (Touch ID)
cask "ghostty"              # terminal
cask "visual-studio-code"
cask "zed"
cask "obsidian"             # vault lives in ~/Documents/Architecture (iCloud-synced)

# ── Containers: Docker without Docker Desktop ────────────────
brew "colima"               # container runtime VM — `colima start`
brew "docker"               # docker CLI (client only)
brew "docker-compose"       # `docker compose` (symlinked into ~/.docker/cli-plugins)
brew "docker-buildx"        # modern image builder (same symlink treatment)

# ── Diagrams ──────────────────────────────────────────────────
cask "drawio"                # draw.io Desktop — formal architecture diagrams
brew "d2"                    # diagrams-as-code, nicer output for big diagrams
brew "mermaid-cli"           # diagrams-as-code, renders natively in GitHub markdown

# ── Engineering toolbelt — desktop apps ───────────────────────
cask "bruno"                 # API client, collections as files
cask "dbeaver-community"     # universal DB GUI
cask "utm"                   # VMs (QEMU UI)
cask "mitmproxy"             # HTTP/S debugging proxy (free Proxyman replacement)

# ── Engineering toolbelt — CLI belt ───────────────────────────
brew "gh"                    # GitHub from the terminal
brew "fzf"                   # fuzzy finder
brew "fd"                    # faster, friendlier find
brew "bat"                   # cat with syntax highlighting
brew "eza"                   # ls replacement, icons/git-aware
brew "zoxide"                # smarter cd, learns your habits
brew "git-delta"             # readable git/diff output
brew "lazygit"               # git TUI
brew "btop"                  # resource monitor TUI
brew "tldr"                  # simplified man pages
brew "yq"                    # yaml/json/xml processor (jq's sibling)
brew "hyperfine"             # command-line benchmarking

# ── Runtimes & package managers ────────────────────────────────
brew "mise"                  # one version manager: node/python/go/everything, per-project pins
brew "uv"                    # fast Python package/venv manager
brew "pnpm"                  # fast Node package manager
brew "bun"                   # JS/TS runtime, bundler, test runner, package installer

# ── Terminal aesthetics ────────────────────────────────────────
brew "starship"              # minimal, fast cross-shell prompt
brew "fastfetch"             # system info flex screen
cask "font-jetbrains-mono-nerd-font"   # ligatures + icons for eza/starship

# ── macOS quality of life ─────────────────────────────────────
cask "shottr"                # screenshots, annotation, OCR
cask "alt-tab"               # Windows-style window switcher
cask "jordanbaird-ice"       # menu bar manager (cask token is NOT "ice")
cask "stats"                 # menu bar system monitor
cask "appcleaner"            # uninstaller that removes leftovers
cask "keepingyouawake"       # prevent sleep during builds/demos

# ── Principal-engineer side ───────────────────────────────────
cask "fathom"                # AI meeting notes/transcription
brew "herdr"                  # terminal workspace manager for AI coding agents (sessions/worktrees/panes)

# ── Security ──────────────────────────────────────────────────
cask "lulu"                  # outbound firewall

# ── Optional — uncomment when wanted ─────────────────────────
# cask "secretive"          # Secure Enclave SSH keys (hardware-grade, keys never leave Mac)
# cask "pycharm-ce"         # free Python IDE
# cask "rancher"            # Rancher Desktop: container GUI + built-in k8s (alternative to colima)
