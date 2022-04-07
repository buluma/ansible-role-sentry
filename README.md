# [sentry](#sentry)

Sentry installation with Python.

|GitHub|GitLab|Quality|Downloads|Version|Issues|Pull Requests|
|------|------|-------|---------|-------|------|-------------|
|[![github](https://github.com/buluma/ansible-role-sentry/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-sentry/actions)|[![gitlab](https://gitlab.com/buluma/ansible-role-sentry/badges/master/pipeline.svg)](https://gitlab.com/buluma/ansible-role-sentry)|[![quality](https://img.shields.io/ansible/quality/)](https://galaxy.ansible.com/buluma/sentry)|[![downloads](https://img.shields.io/ansible/role/d/)](https://galaxy.ansible.com/buluma/sentry)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-sentry.svg)](https://github.com/buluma/ansible-role-sentry/releases/)|[![Issues](https://img.shields.io/github/issues/buluma/ansible-role-sentry.svg)](https://github.com/buluma/ansible-role-sentry/issues/)|[![PullRequests](https://img.shields.io/github/issues-pr-closed-raw/buluma/ansible-role-sentry.svg)](https://github.com/buluma/ansible-role-sentry/pulls/)|

## [Example Playbook](#example-playbook)

This example is taken from `molecule/default/converge.yml` and is tested on each push, pull request and release.
```yaml
---
- name: Converge
  hosts: all
  become: yes
  gather_facts: yes

  roles:
    - role: buluma.sentry
```


## [Role Variables](#role-variables)

The default values for the variables are set in `defaults/main.yml`:
```yaml
---
# defaults var for role_sentry

docker_sh_url: "https://get.docker.com"
getsentry_url_v20_12_1: "https://codeload.github.com/getsentry/onpremise/tar.gz/20.12.1"

getsentry_domain_url: "sentry.testonpremise.com"
gensentry_local_port: 9000

# SSL
self_signed_certs:
  - key: /etc/ssl/private/{{ getsentry_domain_url }}.key
    cert: /etc/ssl/certs/{{ getsentry_domain_url }}.crt

# Nginx
nginx_snippets_ssl: "/etc/nginx/snippets"
nginx_site_default: "/etc/nginx/sites-available"


host_delay_time: 20

# Sentry Admin User [UPATE ADMIN USER EMAIL AND PASSWORD]
sentry_admin_email: "admin@sentry.com"
sentry_admin_password: "ADMIN"

```

## [Requirements](#requirements)

- pip packages listed in [requirements.txt](https://github.com/buluma/ansible-role-sentry/blob/main/requirements.txt).


## [Context](#context)

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://buluma.co.ke/) for further information.

Here is an overview of related roles:

![dependencies](https://raw.githubusercontent.com/buluma/ansible-role-sentry/png/requirements.png "Dependencies")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/buluma):

|container|tags|
|---------|----|
|ubuntu|bionic|
|el|7|
|debian|all|

The minimum version of Ansible required is 2.7, tests have been done to:

- The previous version.
- The current version.
- The development version.



If you find issues, please register them in [GitHub](https://github.com/buluma/ansible-role-sentry/issues)

## [License](#license)

Apache-2.0

## [Author Information](#author-information)

[Michael Buluma](https://buluma.github.io/)
