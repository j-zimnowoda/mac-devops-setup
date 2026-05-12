# 💻 DevOps Mac OS automated setup 

This ansible playbook install and setup most of softwares and utilities for my DevOps environment.

## 🚥 Installation 

First of all clone or download this repository on you mac.

## 🚀 Usage

Create a `.env` file from `.env.example`, update values, then run:

```sh
set -a
source .env
set +a
ansible-playbook setup-my-mac.yml -i inventory -K
```

To run only the GPG role:

```sh
set -a
source .env
set +a
ansible-playbook setup-my-mac.yml -i inventory --tags gpg
```

To run only the SSH role:

```sh
set -a
source .env
set +a
ansible-playbook setup-my-mac.yml -i inventory --tags ssh
```

To run only the GitHub key upload role:

```sh
set -a
source .env
set +a
ansible-playbook setup-my-mac.yml -i inventory --tags github_keys
```

To preview changes without applying them (dry-run):

```sh
set -a
source .env
set +a
ansible-playbook setup-my-mac.yml -i inventory -K --check --diff
```

You can customize setup editing `config.yml` config file.


## ✨What this playbook do

The complete list of softwares installed is in `config.yml` , but in summary here what the playbook do.

- Install homebrew and cask and install applications, utilities and quick look plugins. 

    Docker, Vagrant, slack, 1password, postman,...

- Manage dotfiles from this repository into $HOME/dotfiles and symlink them into $HOME.

- Generate a GPG key (with passphrase from `.env`) and store the passphrase in macOS Keychain.

- Generate an SSH key (with passphrase from `.env`) and add it to the macOS Keychain.

- Upload generated GPG and SSH public keys to GitHub using the `gh` CLI.

- Configure terminal

    Install iTerm2 (Solarized Dark theme, font-inconsolata)
    Install Zsh and configure options with oh-my-zsh

- Configure Mac OS 

    Show icons for hard drives, servers, and removable media on the desktop
    Avoid creating .DS_Store files on network volumes
    Finder: show status bar
    Save screenshots in PNG format
    Save screenshots to the Desktop/Screenshots folder

## Improvements

Configure iTerm2 Profile with Solarized theme.
Add config for sync settings VScode and Brave
Configure VPN

## Testing the Playbook

Use Mac virtualbox https://github.com/geerlingguy/macos-virtualbox-vm

## See also

- https://blog.vandenbrand.org/2016/01/04/how-to-automate-your-mac-os-x-setup-with-ansible/
- http://www.nickhammond.com/automating-development-environment-ansible/
- https://github.com/simplycycling/ansible-mac-dev-setup/blob/master/main.yml
- https://github.com/mas-cli/mas
- https://github.com/geerlingguy/mac-dev-playbook
- https://github.com/osxc
- https://github.com/MWGriffin/ansible-playbooks/blob/master/sourcetree/sourcetree.yaml   
- https://github.com/sindresorhus/quick-look-plugins