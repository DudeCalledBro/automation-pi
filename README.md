# Automation Pi

[![CI](https://github.com/DudeCalledBro/automation-pi/actions/workflows/ci.yml/badge.svg)](https://github.com/DudeCalledBro/automation-pi/actions/workflows/ci.yml)

A Raspberry Pi Configuration for Automation Tools in My Homelab.

This repository is a treasure trove for homelab enthusiasts, packed with a carefully curated collection of Ansible playbooks and configuration files. It's designed to supercharge your homelab setup, making the installation, configuration, and management of popular automation tools a breeze.

* [SemaphoreUI](https://github.com/semaphoreui/semaphore) is a modern UI for Ansible. It lets you easily run Ansible playbooks, get notifications about fails, control access to deployment system.

* **TODO**: [Gitea](https://github.com/go-gitea/gitea) is a community managed painless self-hosted Git service.

## Prerequisites

- Ensure you have Ansible installed (e.g. `pip3 install ansible`)
- Ensure Docker is installed on the Home Assistant server (you may want to checkout my [ansible-docker-role](https://github.com/DudeCalledBro/ansible-role-docker))

## Setup

Follow these steps to kickstart your automated homelab journey:

### Setting Up Your Inventory

1. Navigate to the inventories directory:

    ```bash
    cd inventories
    ```

2. Create a copy of the example hosts file:

    ```bash
    cp example.hosts.yml hosts.yml
    ```

3. Edit the `hosts.yml` file to match your homelab setup:

    ```bash
    vim hosts.yml
    ```

    Customize the file according to your network layout. For example:

    ```yaml
    all:
      hosts:
        server1:
          ansible_host: 192.168.1.10
    ```

### Configuring Variables

1. Create and edit a new variables file:

    ```bash
    vim group_vars/all/main.yml
    ```

2. Add your configurations to this file. For example:

    ```yaml
    # Semaphore configuration
    semaphore_docker_env:
      SEMAPHORE_DB_DIALECT: bolt
      SEMAPHORE_ADMIN: admin
      SEMAPHORE_ADMIN_PASSWORD: changeme
      SEMAPHORE_ADMIN_NAME: Admin
      SEMAPHORE_ADMIN_EMAIL: admin@localhost
    ```

    > For role-specific defaults, check the `roles/*/defaults/main.yml` files. You can override these in your `group_vars/all/main.yml` or create host-specific variables in `host_vars/`.

### Deploying Your Automation Stack

You have flexibility in how you deploy your automation stack:

1. To deploy the entire stack:

    ```bash
    ansible-playbook play-main.yml
    ```

2. To deploy a single role:

    ```bash
    ansible-playbook play-nginx.yml
    ```

3. For a dry run to see what would change:

    ```bash
    ansible-playbook play-main.yml --check
    ```

## Modular Deployment

Remember, you don't need to deploy the entire stack at once. Many components can function independently. For instance:

- Semaphore can operate without a reverse proxy or an external database.

Tailor your deployment to your specific needs and gradually build up your homelab infrastructure.

## License

Copyright © 2024 Niclas Spreng

Licensed under the [MIT license](LICENSE).
