# Ansible Role: Nginx

**Note:** Please consider using the official [NGINX Ansible role](https://github.com/nginxinc/ansible-role-nginx) from NGINX, Inc.

Installs Nginx on RedHat, Debian/Ubuntu OS.

This role installs and configures the latest version of Nginx from the Nginx RedHat-based and Debian-based systems package manager. This is not a production ready configuration and will need addtional configurations and settings to match your environment.

## Requirements

None.

## Dependencies

None.

## Example Playbook

    - hosts: server
      roles:
        - { role: nginx }

## License

MIT / BSD