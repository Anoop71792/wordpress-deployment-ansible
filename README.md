# Automated WordPress Deployment using Ansible

Ansible-based automation project for deploying and configuring a complete WordPress environment on an AWS EC2 instance.

The project automates the installation and configuration of the web server, database, PHP environment, WordPress, SFTP access, phpMyAdmin, and HTTPS.

## Project Overview

This project uses Ansible to automate WordPress deployment on an Amazon Linux 2023 EC2 instance. A WSL Ubuntu environment is used as the Ansible control node, while the EC2 instance acts as the managed node.

The deployment is performed through an Ansible playbook, reducing manual configuration and ensuring a consistent server setup.

## Technologies Used

- **Cloud Platform:** AWS EC2
- **Operating System:** Amazon Linux 2023
- **Configuration Management:** Ansible
- **Control Node:** Ubuntu on WSL
- **Web Server:** Nginx
- **Database:** MariaDB 10.6
- **Backend:** PHP 8.2 and PHP-FPM
- **CMS:** WordPress
- **Database Management:** phpMyAdmin
- **File Transfer:** SFTP
- **Security:** SSH, firewall configuration, self-signed SSL/TLS certificate

## Architecture

The deployment follows a control-node and managed-node architecture.

1. Ansible runs from the Ubuntu WSL control node.
2. Ansible connects to the AWS EC2 instance over SSH.
3. The playbook installs and configures Nginx, MariaDB, and PHP-FPM.
4. WordPress is downloaded and configured with the database.
5. SFTP access and phpMyAdmin are configured.
6. A self-signed SSL/TLS certificate is generated for HTTPS access.

## Features

- Automated WordPress deployment
- Nginx web server configuration
- MariaDB database installation and configuration
- PHP-FPM integration
- WordPress database setup
- SFTP user configuration
- phpMyAdmin installation
- Self-signed HTTPS configuration
- Ansible-based service management
- Reusable configuration through variable files

## Project Structure

```text
wordpress-ansible/
│
├── ansible.cfg
├── site.yml
├── .gitignore
├── README.md
│
├── inventory/
│   └── hosts.example.ini
│
└── group_vars/
    └── all.example.yml
```

## Prerequisites

Before deployment, ensure you have:

- An AWS account
- An Amazon Linux 2023 EC2 instance
- An SSH key pair for EC2 access
- Ubuntu on WSL or another Linux control node
- Ansible installed on the control node
- SSH connectivity to the EC2 instance

## Configuration

The repository contains example configuration files. Create your own local configuration files before deployment.

Copy the example files:

```bash
cp inventory/hosts.example.ini inventory/hosts.ini
cp group_vars/all.example.yml group_vars/all.yml
```

### 1. Configure Inventory

Edit `inventory/hosts.ini` and provide your EC2 public IP address, SSH username, and private key path.

### 2. Configure Variables

Edit `group_vars/all.yml` and update the required values:

- SFTP username and password
- Database name, username, and password
- phpMyAdmin authentication credentials
- WordPress administrator credentials
- WordPress site details
- Administrator email address

Replace all placeholder values before deployment.

## Deployment

### 1. Test SSH Connectivity

```bash
ansible webservers -m ping
```

### 2. Run the Ansible Playbook

```bash
ansible-playbook site.yml
```

Ansible will execute the tasks defined in `site.yml` and configure the managed EC2 instance.

## Verification

After successful deployment, verify the following:

- Nginx service is running.
- MariaDB service is running.
- PHP-FPM service is running.
- WordPress website is accessible.
- Database connection is successful.
- SFTP login works.
- phpMyAdmin is accessible.
- HTTPS access is configured.

## Security Considerations

- Never commit private SSH keys or passwords.
- Keep `group_vars/all.yml` and `inventory/hosts.ini` out of version control.
- Use strong passwords for all accounts.
- Restrict EC2 security group rules to trusted sources wherever possible.
- Use Ansible Vault to encrypt sensitive variables.
- The project uses a self-signed SSL/TLS certificate; browsers may display a security warning. Use a trusted certificate for production deployments.

## Important Notes

The example configuration files are templates. Replace placeholder values with your own environment details before running the playbook.

The deployment is designed as a learning and demonstration project. Additional hardening and production-grade security configuration may be required before exposing it to real users.

## Author

**Anoop H**

Cloud and DevOps Trainee

## License

This project is available for learning and educational purposes.
