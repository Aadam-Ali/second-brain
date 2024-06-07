---
id: 20240523170514
tags: [ansible, nix]
---

# Refactoring development environment Ansible playbook

Currently, my Ansible role is a bit of a mess. Variables that have
values specific to an OS / distro might be set in the `vars/main.yml`
file. Instead what I'd like to do is for the variables that differ is
to default them to be empty and then overriden in the specific variable
file.

The other change that I'm making is the name of the variables, instead
of names like `common_pkgs` and `os_pkgs` they should really be
`cli_pkgs` and `gui_pkgs`.

This change should allow me to be a place where I can happily write up a
blogpost on automating my development environment. Just in time for me
to possibly start using `nix`, `flakes` and `home-manager` to achieve
the same thing in a reproducable way rather than a repeatable way but I
need to do some more learning and experimenting before I can migrate.

Related:
  * <https://github.com/Aadam-Ali/dotfiles/tree/main/ansible>
