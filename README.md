# awx-install-on-k3s

Install AWX on k3s

**NEW:** Example (4), deploy with Letsencrypte certificate and CLOUDFLARE FQDN

Automated deployment of single node k3s cluster running AWX

Special thanks to @kurokobo for his help. This role is based on his repo:

https://github.com/kurokobo/awx-on-k3s

A short video is available here: https://youtu.be/pNHh6Ic-64E

## IMPORTANT NOTES: THIS ROLE WILL ONLY WORK UP TO VERSION 23.9.1
## OF AWX AND 2.12.1 OF THE AWX-OPERATOR.

## Requirements

Ubuntu 20.04/22.04 **Recommended**

Cent0S 8 Stream

4 GB RAM

2 CPU

**kubernetes.core collection on the control host:**

```
ansible-galaxy collection install kubernetes.core

```

## Role Variables

**k3s_version**: The k3s release to deploy, default is v1.33.4+k3s1

**operator_version:** The awx operator release, default 2.12.1

**awx_version**: AWX release, default 23.9.1

**awx_admin_password**: Set admin password for web interface "awxadminpasswd"

**postgres_password:** Set database password, default "mydbpasswd"

**awx_hostname**: Set web address, default "my.awx.home"

**namespace_k3s:** Set the namespace, default "awx"

**cloudflare_api_key:** Must be define in roles/awx_k3s_with_valid_ssl/defaults/main.yml
if you wish to deploy with a letsencrypt certificate managed by certmanager.

**email_for_letsencrypt:** Valid email to used for DNS when using awx_k3s_with_valid_ssl.
It can be added here: roles/awx_k3s_with_valid_ssl/defaults/main.yml

## Examples

1. deploy.yml can be used to execute against an inventory

```
ansible-playbook -i YourInventoryFile deploy.yml

```

2. If using ansible-navigator with the config included in his repo,
   antuelle78/awx-ee:latest EE image is used and the container is launched on
   the host network.

```
ansible-navigator run deploy.yml -i YourInventoryFile -m stdout

```

3. Add "--skip-tags=k3s_install" to bypass reinstalling k3s on subsequent runs.

```
ansible-navigator run deploy.yml -i YourInventoryFile --skip-tags=k3s_install

```

4. If you followed the instructions above and defined an api key for cloudflare as well as
   a valid email address, then you can run:
   This has only been tested with cloudflare, but might work with other providers.

```
ansible-playbook -i YourInventoryFile deploy_nintr_cloudflare.yml

```

5. This repo can also be imported into an existing AWX/Tower instance as a project:

https://github.com/antuelle78/awx-install-on-k3s/blob/main/Configure%20AWX%20project.pdf

**Ansible Navigator Documentation:**

https://ansible-navigator.readthedocs.io/en/latest/

## Access AWX Web Interface

Visit http://my.awx.home after successful deployment when using default values.

## Backup AWX Instance

The "backup_awx.yml" play can be used to create a backup of AWX

```
ansible-playbook -i YourInventoryFile backup_awx.yml

```

A backup will be created with the name awx-backup-"CurrentDate" with
a retention of 30 days

If you want to define these values run:

```
ansible-playbook -i YourInventoryFile backup_awx_intr.yml

```

and respond to the prompts.

Backups older than the retention period will be deleted on each run.

## license

GPLv3

## Author Information

Name: Michael Nelson

LET'S GET IT AUTOMATED AND BE LAZY :<)
