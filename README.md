Ansible Role - Dotfiles
========================

[![Ansible Galaxy](https://img.shields.io/badge/ansible--galaxy-dotfiles-blue)](https://galaxy.ansible.com/acimadamore/dotfiles)

Install dotfiles from a Git repository in any UNIX like system.

This role links all files and directories of the given repository(see below how to exclude files). Directories are not linked recursively, given a directory _dir_ a directory _.dir_ is created and all the regular files inside of it are linked.

Requirements
------------

Git must be installed on the managed host.

Role Variables
--------------

Available variables are listed below, along with default values (see `defaults/main.yml`):

    dotfiles_repository: ''

This variable is **required**. The git respository of the dotfiles to retrieve.

    dotfiles_repository_version: master

Tag, branch or commit of the git repository to use.

    dotfiles_repository_path: "~/dotfiles"

The local path where the `dotfiles_repository` will be cloned.

    dotfiles_home: "~"

The directory where dotfiles will be linked. Keep in mind that the existing files on this directory are deleted before linking with dotfiles in `rdotfiles_repository_path`. Back up this files previously if necessary.

    dotfiles_exclude:
      - README.md
      - LICENSE.md

A list of dotfiles that will be skipped from being linked. Regular expressions can be used. For files inside a directory, the pattern should be prefixed with the directory's name separated by a slash, for instance the pattern `vim/^not-link-\w*.conf$` excludes from linking all files from _vim_ directory that begin with _not-link_ and end with _.conf_.


Dependencies
------------

None.

Example Playbook
----------------

Basic usage example:

```yaml
---
- hosts: localhost
  connection: local
  vars:
    dotfiles_repository: 'https://github.com/acimadamore/dotfiles'
  roles:
    - acimadamore.dotfiles
```

Full example:

```yaml
- hosts: localhost
  connection: local
  roles:
    - role: acimadamore.dotfiles
      vars:
        dotfiles_repository: 'https://github.com/acimadamore/dotfiles'
        dotfiles_repository_version: 1.1
        dotfiles_repository_path: '~/projects/dotfiles'
        dotfiles_home: '~'
        dotfiles_exclude:
          - README.md
          - LICENSE.md
          - \w*.rc
          - ssh/config
```

License
-------

MIT

Author Information
------------------

This role was created in 2021 by Andres Cimadamore.
