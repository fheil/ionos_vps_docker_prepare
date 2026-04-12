# ionos_vps_docker_prepare
Get IONOS VPS Linux (Ubuntu) ready to update all packages, create user "foo" with sudo, install some essential packages, install docker and portainer.

List of anisble playbooks:

#master_playbook.yml
The one that does everything. This playbook just imports all the other playbooks in the correct order. 

#apb_ionos_00_upd.yml
Playbook that updates Ubuntu server with newest packages, removes unused packages etc. It's similiar to the command:
  sudo apt update && sudo apt -y upgrade && sudo apt full-upgrade && sudo apt dist-upgrade && sudo apt autoremove

#apb_ionos_020__create_user_foo.yml
Playbook to create the non-root user, start it first, so that user become user-id 1000, group-id 1000, what might be important for alle the following playbooks or even bash-scripts (there might be some in the future)
