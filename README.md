# ionos_vps_docker_prepare
Get IONOS VPS Linux (Ubuntu) ready to update all packages, create user "foo" with sudo, install some essential packages, install docker and portainer.

The VPS is called `vps-foo` with IP `127.0.0.1` in this README and the examples.

## List of ansible playbooks:

### master_playbook.yml
The one that does everything. This playbook just imports all the other playbooks in the correct order. 

### apb_ionos_00_upd.yml
Playbook that updates Ubuntu server with newest packages, removes unused packages etc. It's similar to the command:
> sudo apt update && sudo apt -y upgrade && sudo apt full-upgrade && sudo apt dist-upgrade && sudo apt autoremove

### apb_ionos_010__mandatory.yml
Add (my favored/)mandatory necessary packages.

### apb_ionos_020__create_user.yml
Playbook to create the non-root user, start it before adding users, so that user become user-id 1000, group-id 1000, what might be important for alle the following playbooks or even bash-scripts (there might be some in the future).

Either you have to place your vars `username`, `user_password_hash`, `user_ssh_key` and `delete_user_first` in the `inventory.yml` (recommended), the playbook directly or call the playbook like this:

> ansible-playbook apb_ionos_020__create_user.yml -i inventory.ini \
>  -e "username=foo" \
>  -e "user_password_hash='$6$83b6....'" \
>  -e "user_ssh_key='ssh-ed25519 AAA...'" \
>  -e "delete_user_first=true"

You can test with the following command:

> ansible -i inventory.ini all -m command -a "id foo" --become

Replace `foo` with your username.

### apb_ionos_030__aliases_global.yml
A list of aliases. The aliases go to /etc/profile.d/profile.local.sh. The playbook checks existence of entries to avoid duplicate entries.

### apb_ionos_050__dockersetup.yml
Installs docker to Ubuntu according to the [Docker Docs](https://docs.docker.com/engine/install/ubuntu/) (according to the time of writing this).

### apb_ionos_052__portainer_install.yml
Installs [Portainer Community Edition (CE)](https://docs.portainer.io/start/install-ce) (according to the time of writing this).

## Other files
### ansible.cfg
Config-file with `remote_user` and `private_key_file` definitions.

### inventory.yml.example
Example inventory file. Use this for your inventory.yml (inventory.yml and inventory.ini are in .gitignore). Do not use the example with your playbooks
