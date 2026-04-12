# ionos_vps_docker_prepare
Get IONOS VPS Linux (Ubuntu) ready to update all packages, create user "foo" with sudo, install some essential packages, install docker and portainer.

## List of anisble playbooks:

### master_playbook.yml
The one that does everything. This playbook just imports all the other playbooks in the correct order. 

### apb_ionos_00_upd.yml
Playbook that updates Ubuntu server with newest packages, removes unused packages etc. It's similiar to the command:
> sudo apt update && sudo apt -y upgrade && sudo apt full-upgrade && sudo apt dist-upgrade && sudo apt autoremove

### apb_ionos_010__mandatory.yml
Add (my favored/)mandatory necessary packages.

### apb_ionos_020__create_user.yml
Playbook to create the non-root user, start it first, so that user become user-id 1000, group-id 1000, what might be important for alle the following playbooks or even bash-scripts (there might be some in the future)

### apb_ionos_030__aliases_global.yml
A list of aliases. The aliases go to /etc/profile.d/profile.local.sh. The playbook checks existence of entries to avoid dublicate entries.

### apb_ionos_050__dockersetup.yml
Installs docker to Ubuntu according to the Docker Docs on https://docs.docker.com/engine/install/ubuntu/ (according to the time of writing this).

### apb_ionos_052__portainer_install.yml
Installs Portianer COmmunity Edition (CE) according to https://docs.portainer.io/start/install-ce (according to the time of writing this).

## Other files
### ansible.cfg
Config-file with remote_user and private_key_file definitions.

### inventory.yml
Example inventory file. To avoid conflicts, it is recommended to create a copy, such as `ionos_inventory`, and use this copy with an ansible playbook. This will prevent conflicts with the version on GitHub.
