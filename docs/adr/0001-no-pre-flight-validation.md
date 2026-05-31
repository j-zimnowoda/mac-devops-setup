# No centralised pre-flight validation in pre_tasks

This playbook is designed to run incrementally on a blank machine: Homebrew installs GPG and other prerequisites, and individual roles both install tools and consume configuration for those tools. A `config.local.yml` that is only partially filled in is a normal and expected state — the user populates it progressively as they enable features via the `configure_*` flags.

Centralising config assertions in `pre_tasks` would fail the entire playbook run whenever any enabled feature lacks its variables, even when the user intends to run only unrelated roles (e.g. install packages before setting up GPG). The per-role `assert` tasks at the top of each role are the right validation seam: they fire at the moment the role actually needs the variable, with a message that names exactly what is missing and where to set it.
