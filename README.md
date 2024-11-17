# Hugo Webhost Role

This Ansible role deploys and manages Hugo-created websites on target hosts.

## Role Description

The `hugo_webhost` role automates the process of setting up and configuring a web server to host multiple Hugo-generated static websites. It handles package installation, user setup, Caddy web server configuration, and website deployment from Git repositories.

## Requirements

- Ansible 2.17.5 or higher
- Target hosts running EL 9 (AlmaLinux 9.4 tested)
- Git installed on the control node
- Internet access on target hosts for package installation and Git operations

## Dependencies
This role depends on `caddy_ansible.caddy_ansible`: Used for installing and configuring the Caddy web server

## Role Variables

### Default Variables

The site varialble contains a list of hugo websites to deploy to the target host. You can override these defaults or add more sites as needed.

These variables are defined in `defaults/main.yml`:

```yaml
sites:
  - name: alain.apigban.com
    local_path: /var/www/html
    repo_url: https://github.com/apigban/alain.apigban.com.git
    port: 10000
  - name: another-site.apigban.com
    local_path: /var/www/html
    repo_url: https://github.com/apigban/another-site.apigban.com.git
    port: 11000
```

### Other Variables
Additional variables are defined in `vars/main.yml`:

* `packages`: List of packages to be installed
* `hugo`: Configuration for Hugo commands and version

## Example Playbook
```yaml
- hosts: webservers
  roles:
    - role: hugo_webhost
```

## Role Structure
```
apigban.hugo_webhost
├── ansible.cfg
├── ansible-navigator.yml
├── defaults
│   └── main.yml
├── files
│   └── ...
├── handlers
│   └── main.yml
├── meta
│   └── main.yml
├── molecule
│   └── default    
|    └── ...
├── README.md
├── requirements.yml
├── tasks
│   ├── deploy-websites.yml
│   ├── hugo-operations.yml
│   ├── main.yml
│   ├── setup-caddy.yml
│   ├── setup-pkgs.yml
│   └── setup-users.yml
├── templates
│   └── ...
├── tests
│   └── ...
└── vars
    └── main.yml
```

## License
MIT

## Author Information
Created by Alain Pinero Igban for apigban.com