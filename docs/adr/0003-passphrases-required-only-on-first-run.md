# Passphrases are required only when keys or Keychain entries are absent

`gpg_key_passphrase` and `ssh_key_passphrase` are validated conditionally: GPG passphrase only when the secret key is missing or the Keychain entry is absent; SSH passphrase only when the private key file does not exist. On subsequent runs against a provisioned machine both variables can be absent from `config.local.yml` entirely.

This makes `ansible-vault encrypt config.local.yml` practical: the vault password is entered once at initial setup, and re-runs that don't need to generate keys can omit the passphrase variables from the encrypted file rather than requiring it on every execution. The trade-off is that the conditional asserts are less obvious than a flat validation block — see ADR-0001 for why validation lives in the roles rather than in `pre_tasks`.
