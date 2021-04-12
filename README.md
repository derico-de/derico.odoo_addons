# derico.odoo

Ansible role to deploy and configure multiple Odoo addon's.
It also set's symbolic links from the checked out repositories to Odoo's addons directory, to activate specific addon's of a repository.

## Minimum Ansible Version:

2.9

## Supported versions and systems

| System / Odoo       | 12.0 | 13.0 |
|---------------------|------|------|
| Debian 10 (buster)  | yes  | yes  |

## Usage

### Play

```yaml
- name: Odoo
    hosts: odoo_servers
    become: yes
    environment:
    LC_ALL: en_US.UTF-8

    roles:
    - role: derico.odoo_addons
```

### host_vars/odoo01:

```yaml
odoo_setup:
    - name: 13.0
      odoo_user: odoo
      instances:
        - name: odoo_demo
          domain: demo.office.example.com
          config_http_port: 8000
          config_longpolling_port: 9000
      odoo_user: odoo
      odoo_addon_repos:
        - id: project
          url: https://github.com/OCA/project.git
          symlinks:
            - project/project_stage_closed
            - project/project_task_default_stage
            - project/project_task_add_very_high
            - project/project_parent_task_filter
        - id: project-agile
          url: https://github.com/OCA/project-agile.git
          symlinks:
            - project-agile/project_scrum
```
