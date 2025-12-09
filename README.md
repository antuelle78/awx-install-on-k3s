# 🚀 AWXai on k3s: AI-Maintained Ansible Automation Hub

[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)
[![YouTube Demo](https://img.shields.io/badge/YouTube-Demo-red)](https://youtu.be/pNHh6Ic-64E)

Deploy a full-featured **AWXai** instance on a lightweight k3s Kubernetes cluster with this automated Ansible playbook. AWXai is an AI-maintained fork of AWX with enhanced features for modern automation workflows.

This role is based on the great work of [@kurokobo](https://github.com/kurokobo) and his [awx-on-k3s](https://github.com/kurokobo/awx-on-k3s) repository, modified to deploy AWXai instead of standard AWX.

> **Note:** This role is optimized for **AWXai 25.1.1** and **awx-operator 2.19.1**.

---

## ✨ Features

*   **Automated Deployment:** Sets up a single-node k3s cluster and deploys AWXai with a single command.
*   **AI-Maintained AWX:** Deploys the enhanced AWXai fork with additional features and improvements.
*   **Lightweight & Efficient:** Uses k3s for a minimal Kubernetes footprint.
*   **SSL Ready:** Includes a playbook for deploying with a valid Let's Encrypt certificate using cert-manager and Cloudflare.
*   **Backup & Restore:** Comes with playbooks to easily back up and restore your AWXai instance.
*   **Flexible Configuration:** Easily customize your deployment with a comprehensive set of Ansible variables.
*   **Ansible Navigator Support:** Includes a configuration for a seamless experience with `ansible-navigator`.

---

## ✅ Prerequisites

Before you begin, ensure your control node and target host meet the following requirements:

*   **Operating System:**
    *   Ubuntu 20.04 - 24.04 (Recommended)
    *   CentOS 8 Stream
*   **Hardware:**
    *   4 GB RAM (minimum)
    *   2 CPU cores (minimum)
*   **On your Ansible Control Node:**
    *   The `kubernetes.core` Ansible collection must be installed:
        ```bash
        ansible-galaxy collection install kubernetes.core
        ```

---

## 🚀 Quick Start

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/antuelle78/awx-install-on-k3s.git
    cd awx-install-on-k3s
    ```

2.  **Create your inventory file** (e.g., `inventory.yml`):
    ```yaml
    all:
      hosts:
        awxai-node:
          ansible_host: 192.168.122.46
          ansible_user: your_user
    ```

3.  **Run the deployment playbook:**
    ```bash
    ansible-playbook -i inventory.yml deploy.yml
    ```
    You will be prompted to enter values for the deployment. To accept the defaults, simply press Enter.

4.  **Access AWXai:**
    Once the playbook is complete, open your browser and navigate to the hostname you configured (default: `http://awxai.antuelle78.com`).

---

## 🛠️ Configuration

You can customize the deployment by modifying the role variables. The most common variables are prompted during the execution of `deploy.yml`.

| Variable                | Description                                                                                             | Default Value      |
| ----------------------- | ------------------------------------------------------------------------------------------------------- | ------------------ |
| `k3s_version`           | The k3s release to deploy.                                                                              | `v1.34.2+k3s1`     |
| `operator_version`      | The awx-operator release to use.                                                                        | `2.19.1`           |
| `awx_version`           | The AWXai version to deploy.                                                                            | `25.1.1`           |
| `awx_admin_password`    | The password for the AWXai web interface `admin` user.                                                  | `LhTAKSFgTgLynAljakvkdLueVgNUXsQG` |
| `postgres_password`     | The password for the PostgreSQL database.                                                               | `mydbpasswd`       |
| `awx_hostname`          | The hostname or FQDN for the AWXai web interface.                                                       | `awxai.antuelle78.com` |
| `namespace_k3s`         | The Kubernetes namespace for the deployment.                                                            | `awxai`            |
| `cloudflare_api_key`    | Your Cloudflare API key (for SSL deployment). Define in `roles/awx_k3s_with_valid_ssl/defaults/main.yml`. | `""`               |
| `email_for_letsencrypt` | A valid email for Let's Encrypt registration. Define in `roles/awx_k3s_with_valid_ssl/defaults/main.yml`. | `""`               |

---

## 🔬 Advanced Usage

### Using Ansible Navigator

This repository is pre-configured for use with `ansible-navigator`. The included `ansible-navigator.yml` uses the `antuelle78/awx-ee:latest` execution environment.

```bash
ansible-navigator run deploy.yml -i inventory.yml -m stdout
```

### Skipping the k3s Installation

To speed up subsequent playbook runs, you can skip the k3s installation:

```bash
ansible-playbook -i inventory.yml deploy.yml --skip-tags=k3s_install
```

### Deploying with a Valid SSL Certificate (Cloudflare)

1.  **Edit the defaults file:**
    Open `roles/awx_k3s_with_valid_ssl/defaults/main.yml` and set your `cloudflare_api_key` and `email_for_letsencrypt`.

2.  **Run the SSL deployment playbook:**
    ```bash
    ansible-playbook -i inventory.yml deploy_nintr_cloudflare.yml
    ```

---

## 📦 Backup and Restore

This repository includes playbooks to back up your AWX instance.

### Interactive Backup

This playbook will prompt you for the backup name and retention period.

```bash
ansible-playbook -i inventory.yml backup_awx_intr.yml
```

### Automated Backup

This playbook uses default values (30-day retention) and will automatically delete backups older than the retention period.

```bash
ansible-playbook -i inventory.yml backup_awx.yml
```

---

## 🤝 Contributing

Contributions are welcome! Please feel free to open an issue or submit a pull request.

## 📄 License

This project is licensed under the **GPLv3**. See the [LICENSE](LICENSE) file for details.

---

### **LET'S GET IT AUTOMATED AND BE LAZY :<)**
*Michael Nelson*