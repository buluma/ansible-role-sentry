# Ansible role [sentry](https://galaxy.ansible.com/ui/standalone/roles/buluma/sentry/documentation)

Sentry installation with Python.

|GitHub|Version|Issues|Pull Requests|Downloads|
|------|-------|------|-------------|---------|
|[![github](https://github.com/buluma/ansible-role-sentry/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-sentry/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-sentry.svg)](https://github.com/buluma/ansible-role-sentry/releases/)|[![Issues](https://img.shields.io/github/issues/buluma/ansible-role-sentry.svg)](https://github.com/buluma/ansible-role-sentry/issues/)|[![PullRequests](https://img.shields.io/github/issues-pr-closed-raw/buluma/ansible-role-sentry.svg)](https://github.com/buluma/ansible-role-sentry/pulls/)|[![Ansible Role](https://img.shields.io/ansible/role/d/buluma/sentry)](https://galaxy.ansible.com/ui/standalone/roles/buluma/sentry/documentation)|

## [Example Playbook](#example-playbook)

This example is taken from [`molecule/default/converge.yml`](https://github.com/buluma/ansible-role-sentry/blob/master/molecule/default/converge.yml) and is tested on each push, pull request and release.

```yaml
---
- name: Converge
  hosts: all
  become: yes
  gather_facts: yes
  tasks:
    - name: Enable EPEL repo on EL for Redis role
      yum: pkg=epel-release state=present
      when: ansible_os_family == 'RedHat'
    - name: Flush handlers so services are restarted before Sentry installation
      meta: flush_handlers
    - import_role:
        name: buluma.sentry
      vars:
        sentry_db_user: 'sentry'
        sentry_secret_key: 'SAFE'
        sentry_extra_pip_packages:
          - 'sentry-plugins==9.0.0'
```

The machine needs to be prepared. In CI this is done using [`molecule/default/prepare.yml`](https://github.com/buluma/ansible-role-sentry/blob/master/molecule/default/prepare.yml):

```yaml
---
- name: Prepare
  hosts: all
  become: yes
  gather_facts: no

  roles:
    - role: buluma.bootstrap
    - role: buluma.buildtools
    - role: buluma.cron
    - role: duologic.postgresql_repository
    - role: geerlingguy.redis
    - role: geerlingguy.postgresql
    - role: duologic.sentry
```

Also see a [full explanation and example](https://buluma.github.io/how-to-use-these-roles.html) on how to use these roles.

## [Role Variables](#role-variables)

The default values for the variables are set in [`defaults/main.yml`](https://github.com/buluma/ansible-role-sentry/blob/master/defaults/main.yml):

```yaml
---
sentry_version: '21.6.3'
sentry_install_dir: '/srv/sentry'
sentry_system_user: 'sentry'
sentry_system_group: 'sentry'
sentry_system_cron_hour: 4
sentry_system_cron_minute: 0
sentry_extra_pip_packages: ['petname']

# config.yml settigs
sentry_mail_backend: 'dummy'
sentry_mail_host: 'localhost'
sentry_mail_port: 25
sentry_mail_username: ''
sentry_mail_password: ''
sentry_mail_use_tls: false
sentry_mail_from: 'root@localhost'
sentry_mail_enable_replies: false
sentry_mail_reply_hostname: ''
sentry_mail_mailgun_api_key: ''

sentry_secret_key: 'UNSAFE'
sentry_url_prefix: ''

sentry_redis_clusters:
  default:
    hosts:
      0:
        host: 127.0.0.1
        port: 6379

sentry_filestore_backend: 'filesystem'
sentry_filestore_options:
  location: '/tmp/sentry-files'

# sentry.conf.py settings
sentry_db_name: 'sentry'
sentry_db_user: 'sentry'
sentry_db_password: ''
sentry_db_host: ''
sentry_db_port: ''
sentry_broker_url: 'redis://localhost:6379'
sentry_behind_ssl_proxy: false
sentry_web_host: '0.0.0.0'
sentry_web_port: 9000
sentry_auth_register: true
# Extra configuration options, should be valid Python code
sentry_extra_conf_py: ''

# Cleanup
sentry_schedule_cleanup: true
sentry_cleanup_days: 30
```

## [Requirements](#requirements)

- pip packages listed in [requirements.txt](https://github.com/buluma/ansible-role-sentry/blob/master/requirements.txt).

## [State of used roles](#state-of-used-roles)

The following roles are used to prepare a system. You can prepare your system in another way.

| Requirement | GitHub | Version |
|-------------|--------|--------|
|[buluma.bootstrap](https://galaxy.ansible.com/buluma/bootstrap)|[![Ansible Molecule](https://github.com/buluma/ansible-role-bootstrap/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-bootstrap/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-bootstrap.svg)](https://github.com/shadowwalker/ansible-role-bootstrap)|
|[duologic.postgresql_repository](https://galaxy.ansible.com/buluma/duologic.postgresql_repository)|[![Ansible Molecule](https://github.com/buluma/duologic.postgresql_repository/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/duologic.postgresql_repository/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/duologic.postgresql_repository.svg)](https://github.com/shadowwalker/duologic.postgresql_repository)|
|[geerlingguy.redis](https://galaxy.ansible.com/buluma/geerlingguy.redis)|[![Ansible Molecule](https://github.com/buluma/geerlingguy.redis/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/geerlingguy.redis/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/geerlingguy.redis.svg)](https://github.com/shadowwalker/geerlingguy.redis)|
|[geerlingguy.postgresql](https://galaxy.ansible.com/buluma/geerlingguy.postgresql)|[![Ansible Molecule](https://github.com/buluma/geerlingguy.postgresql/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/geerlingguy.postgresql/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/geerlingguy.postgresql.svg)](https://github.com/shadowwalker/geerlingguy.postgresql)|
|[duologic.sentry](https://galaxy.ansible.com/buluma/duologic.sentry)|[![Ansible Molecule](https://github.com/buluma/duologic.sentry/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/duologic.sentry/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/duologic.sentry.svg)](https://github.com/shadowwalker/duologic.sentry)|
|[buluma.buildtools](https://galaxy.ansible.com/buluma/buildtools)|[![Ansible Molecule](https://github.com/buluma/ansible-role-buildtools/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-buildtools/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-buildtools.svg)](https://github.com/shadowwalker/ansible-role-buildtools)|
|[buluma.cron](https://galaxy.ansible.com/buluma/cron)|[![Ansible Molecule](https://github.com/buluma/ansible-role-cron/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-cron/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-cron.svg)](https://github.com/shadowwalker/ansible-role-cron)|

## [Context](#context)

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://buluma.github.io/) for further information.

Here is an overview of related roles:

![dependencies](https://raw.githubusercontent.com/buluma/ansible-role-sentry/png/requirements.png "Dependencies")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/buluma):

|container|tags|
|---------|----|
|[Ubuntu](https://hub.docker.com/repository/docker/buluma/ubuntu/general)|bionic|
|[EL](https://hub.docker.com/repository/docker/buluma/enterpriselinux/general)|7|
|[Debian](https://hub.docker.com/repository/docker/buluma/debian/general)|all|

The minimum version of Ansible required is 2.7, tests have been done to:

- The previous version.
- The current version.
- The development version.

If you find issues, please register them in [GitHub](https://github.com/buluma/ansible-role-sentry/issues)

## [Changelog](#changelog)

[Role History](https://github.com/buluma/ansible-role-sentry/blob/master/CHANGELOG.md)

## [License](#license)

[Apache-2.0](https://github.com/buluma/ansible-role-sentry/blob/master/LICENSE)

## [Author Information](#author-information)

[Shadow Walker](https://buluma.github.io/)


Template inspired by [Robert de Bock](https://github.com/robertdebock)
