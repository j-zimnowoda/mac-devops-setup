# 💻 DevOps Mac OS automated setup

This Ansible playbook installs and configures software and utilities for a DevOps environment on macOS.

## 🚥 Installation

Clone this repository on your Mac, then install Ansible:

```sh
brew install ansible
```

## 🚀 Usage

### 1. Configure

Copy the example config and fill in your values:

```sh
cp config.local.yml.example config.local.yml
```

Edit `config.local.yml`. Passphrases (`gpg_key_passphrase`, `ssh_key_passphrase`) are only required on first run — once keys are generated and stored in macOS Keychain, they can be removed. It is recommended to encrypt the file:

```sh
ansible-vault encrypt config.local.yml
```

### 2. Run

```sh
ansible-playbook setup-my-mac.yml -i inventory
```

With an encrypted `config.local.yml`:

```sh
ansible-playbook setup-my-mac.yml -i inventory --ask-vault-pass
```

To preview changes without applying them (dry-run):

```sh
ansible-playbook setup-my-mac.yml -i inventory --check --diff
```

Use `-K` only when running tasks that require privilege escalation.

### Selective runs

Run only the GPG role:

```sh
ansible-playbook setup-my-mac.yml -i inventory --tags gpg
```

Run only the SSH role:

```sh
ansible-playbook setup-my-mac.yml -i inventory --tags ssh
```

Run only the GitHub key upload role:

```sh
ansible-playbook setup-my-mac.yml -i inventory --tags github_keys
```

Uploading keys to GitHub requires extra `gh` CLI token scopes:

```sh
gh auth refresh -h github.com -s write:gpg_key
gh auth refresh -h github.com -s admin:public_key
```

For GitHub Enterprise, replace `github.com` with your enterprise hostname.

## ✨ What this playbook does

The full list of packages is in `config.yml`. In summary:

- **Homebrew** — installs packages, casks and taps (Docker, Slack, VSCode, iTerm2, …)

- **Dotfiles** — renders templates from `roles/setup_dotfiles/templates/` into `~/dotfiles` and symlinks them into `$HOME`. Add a template file there and it is deployed automatically.

- **GPG key** — generates an ed25519 GPG key using `gpg_key_name` and `gpg_key_email` from `config.local.yml`. Passphrase is stored in macOS Keychain on first run. `gitconfig_signingkey` in `.gitconfig` is resolved automatically from the keyring — no manual fingerprint copy required.

- **SSH key** — generates a key at `~/.ssh/{{ ssh_key_name }}`. Passphrase is added to macOS Keychain on first run. Set `ssh_key_name` in `config.local.yml` to choose the filename.

- **GitHub keys** — uploads GPG and SSH public keys to GitHub using the `gh` CLI. Enable `configure_github_enterprise_keys` and set `github_enterprise_hostname` to also upload to a GitHub Enterprise instance.

- **Terminal** — installs oh-my-zsh.

- **macOS preferences** — sets system defaults (Finder, screenshots, Dock, etc.).

## Testing the Playbook

Use Mac VirtualBox: https://github.com/geerlingguy/macos-virtualbox-vm

## See also

- https://github.com/geerlingguy/mac-dev-playbook
- https://github.com/mas-cli/mas
- https://github.com/sindresorhus/quick-look-plugins
