# Context

## Glossary

**GPG signing key**
The fingerprint of the GPG key used to sign git commits. Auto-resolved at dotfiles render time by querying the local keyring with `gpg_key_name` — does not need to be set manually in `config.local.yml`.

**SSH key name**
The filename of the SSH keypair under `~/.ssh` (e.g. `id_ed25519`, `id_work`). Set via `ssh_key_name` in `config.local.yml`; the full path is derived from it. Distinct from the SSH key comment, which identifies the key to remote services.
