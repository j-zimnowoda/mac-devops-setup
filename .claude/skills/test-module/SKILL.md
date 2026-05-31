---
name: test-module
description: Run an Ansible module dry-run test in this mac-devops-setup repo using --check --diff. Use when the user wants to test a module, run ansible tags, check ansible config, or says "test module", "test tag", "dry run".
---

# Test Module

## Quick start

1. **Copy config if missing**
   ```bash
   [ -f config.local.yml ] || cp config.local.yml.example config.local.yml
   ```

2. **Ask the user which tags to test** (e.g. `homebrew`, `zsh`, `git`)

3. **Run the dry-run**
   ```bash
   ansible-playbook setup-my-mac.yml -i inventory --check --diff --tags <tags>
   ```

## Sudo note

Add `-K` **only** when running privileged tasks that require sudo. Do not add it by default.

```bash
ansible-playbook setup-my-mac.yml -i inventory --check --diff --tags <tags> -K
```

## Workflow

- [ ] Check `config.local.yml` exists; copy from example if not
- [ ] Confirm tags with user
- [ ] Run playbook with `--check --diff`
- [ ] Report any failures or diffs to the user
- [ ] Offer to re-run with `-K` if sudo-requiring tasks fail with permission errors
