# File server

Simple file server install tested in Ubuntu 22.04. NFS won't work on older
releases due to the changes made to config files (more details here 
[here](https://ubuntu.com/server/docs/service-nfs)). Samba will most likely 
work on Ubuntu Focal but may not work on older releases (and most likely not
on any orther distros)

You can either select to install NFS or Samba.

## Instructions

Make sure you configure the `group_vars/all.yaml` files to match your needs
(e.g., update `internal_subnet` to a proper value, add/delete users and
user details as needed)

Execute:

```
# assuming that user1 and user2 were defined in group_vars/all.yaml
sudo adduser --system --no-create-home --group --disabled-login user1
sudo adduser --system --no-create-home --group --disabled-login user2

# get the repo and install
sudo apt-get update && sudo apt-get install  -y ansible
git clone https://github.com/lnx1288/home-file-server.git
cd home-file-server
ansible-playbook -i hosts main.yaml
```

## TO-DO

  * Add hardening
  * Make deployment a bit more idempotent (add various distros)

## Acknowledgements

Based on the work by Bert Van Vreckem et all: https://github.com/bertvv/ansible-role-samba