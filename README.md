# awx-install-on-k3s
Install AWX on k3s


Automated deployment of single node k3s cluster running AWX

Special thanks to @kurokobo for his help. This role is based on his repo:

https://github.com/kurokobo/awx-on-k3s

Requirements
------------

Ubuntu 20.04/22.04 **Recommended**

Cent0S 8 Stream

4 GB RAM

2 CPU

**kubernetes.core collection on the control host:**

```
ansible-galaxy collection install kubernetes.core

```

Role Variables
--------------


**k3s_version**: The k3s release to deploy, default is v1.25.2+k3s1

**operator_version:** The awx operator release, default 0.29.0

**awx_version**: AWX release, default 21.6.0

**awx_admin_password**: Set admin password for web interface "awxadminpasswd"

**postgres_password:** Set database password, default "mydbpasswd"

**awx_hostname**: Set web address, default "my.awx.home"

**namespace_k3s:** Set the namespace, default "awx"


Example Playbook
----------------

1. deploy.yml can be used to execute against an inventory

```
ansible-playbook -i YourInventoryFile deploy.yml

```
2. If using ansible-navigator with the config included in his repo,
   antuelle78/awx-ee:2.13.4 EE image is used and the container is launched on
   the host network.

```
ansible-navigator run deploy.yml -i YourInventoryFile

```

3. Add "-m stdout" to replicate ansible-playbook behaviour when using
   ansible-navigator

```
ansible-navigator run deploy.yml -i YourInventoryFile -m stdout

```

4. Add "--skip-tags=k3s_install" to bypass reinstalling k3s on subsequent runs.

```
ansible-navigator run deploy.yml -i YourInventoryFile --skip-tags=k3s_install

```

5. This repo can also be imported into an existing AWX/Tower instance as a project:

https://github.com/antuelle78/awx-install-on-k3s/blob/main/Configure%20AWX%20project.pdf

**Ansible Navigator Documentation:**

https://ansible-navigator.readthedocs.io/en/latest/


Access AWX Web Interface
----------------

Visit http://my.awx.home after successful deployment when using default values.



Backup AWX Instance
----------------

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


license
-------

GPLv3

Author Information
------------------

Name: Michael Nelson

LET'S GET IT AUTOMATED AND BE LAZY :<)
