# [atom](#atom)

|GitHub|GitLab|
|------|------|
|[![github](https://github.com/mullholland/ansible-role-atom/workflows/Ansible%20Molecule/badge.svg)](https://github.com/mullholland/ansible-role-atom/actions)|[![gitlab](https://gitlab.com/mullholland/ansible-role-atom/badges/master/pipeline.svg)](https://gitlab.com/mullholland/ansible-role-atom)|[![quality](https://img.shields.io/ansible/quality/unset)](https://galaxy.ansible.com/mullholland/atom)|

Installs and configures the editor from atom.io.
Allows to create the config an install packages.


## [Role Variables](#role-variables)

These variables are set in `defaults/main.yml`:
```yaml
---
# Install follows
# https://flight-manual.atom.io/getting-started/sections/installing-atom/#platform-linux
# Install and configres personal atom.io editor
atom_packages:
  - docker
  - linter
  - linter-ansible-linting
  - linter-terraform-syntax
  - linter-yaml
  - zentabs
  - pp-markdown
  - editorconfig
  - atom-python-virtualenv
  - terraform-fmt

atom_config:
  '*':
    autosave:
      enabled: true
    core:
      openEmptyEditorOnStart: false
      projectHome: '~/atom'
      telemetryConsent: "no"
    editor:
      showIndentGuide: true
      showInvisibles: true
      tabType: "soft"
    "exception-reporting":
      userId: "1ead1e75-512e-4162-bd55-4f3a5e5cd218"
    "linter-ansible-linting":
      ansibleLintExecutablePath: "/home/sebweiss/.virtualenvs/ansible/bin/ansible-lint"
      useProjectConfig: true
    "linter-yaml":
      useProjectConfig: ".yamllint"
      yamlLintExecutablePath: "/home/sebweiss/.virtualenvs/ansible/bin/yamllint"
    welcome:
      showOnStartup: false
    zentabs:
      neverCloseDirty: true
    terraform-fmt:
      binPath: "terraform"
      fmtOnSave: true

# By default the config file will not be overwritten
atom_config_overwrite: true
```


## [Example Playbook](#example-playbook)

This example is taken from `molecule/default/converge.yml` and is tested on each push, pull request and release.
```yaml
---
- name: Converge
  hosts: all
  become: true
  gather_facts: true
  # vars:
  #   example_var: "value"
  roles:
    - role: "mullholland.atom"
```

The machine needs to be prepared in CI this is done using `molecule/default/prepare.yml`:
```yaml
---
- name: Prepare
  hosts: all
  become: true
  gather_facts: true

  tasks:
    - name: Debian/Ubuntu | Install cron for Backupscript
      package:
        name:
          - "ca-certificates"
        state: latest
      when: ansible_os_family == "Debian"
```





## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/mullholland):

-   [fedora34](https://hub.docker.com/r/mullholland/docker-molecule-fedora34)
-   [fedora35](https://hub.docker.com/r/mullholland/docker-molecule-fedora35)

The minimum version of Ansible required is 2.10, tests have been done to:

-   The last 2 versions.
-   The current version.



## [Exceptions](#exceptions)

Some variations of the build matrix do not work. These are the variations and reasons why the build won't work:

| variation                 | reason                 |
|---------------------------|------------------------|
| debian9 | Not used as a Desktop OS by me |
| debian10 | Not used as a Desktop OS by me |
| debian11 | Not used as a Desktop OS by me |
| ubuntu1804 | Not used as a Desktop OS by me |
| ubuntu2004 | Not used as a Desktop OS by me |
| centos7 | Not used as a Desktop OS by me |
| centos8 | Not used as a Desktop OS by me |
| centos8-stream | Not used as a Desktop OS by me |
| ubi8 | Not used as a Desktop OS by me |
| rockylinux8 | Not used as a Desktop OS by me |
| almalinux8 | Not used as a Desktop OS by me |
| amazonlinux | Not used as a Desktop OS by me |
| fedora33 | EOL |


If you find issues, please register them in [GitHub](https://github.com/mullholland/ansible-role-atom/issues)

## [License](#license)

MIT


## [Author Information](#author-information)

[Mullholland](https://github.com/mullholland)

## [Special Thanks](#special-thanks)

Template inspired by [Robert de Bock](https://github.com/robertdebock)
