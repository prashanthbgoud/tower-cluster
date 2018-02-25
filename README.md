# Tower Cluster Builder

This playook and set of roles will deploy a functional Ansible Tower cluster. 

This has been tested on Tower 3.2.2.

## Requirements
  - RHEL or CentOS with a Valid Subscription
  - The VM acting as the tower db has a blank disk assigned for the postgres volume group
  - Inventory file contains correct information
  - Variables files contain correct information
  - The group_vars/vault file is encrypted with ansible vault to protect your license and admin password
  - You have sudo access to all nodes and the nodes can communicate via root over SSH (you can lock this down post-install)

## Certificates
  - If you are using self signed certificates update the following locations with your certificates
    ```
    ./roles/tower-cluster-config/files/tower.cert
    ./roles/tower-cluster-config/files/tower.key
    ./roles/tower-haproxy/files/tower.pem
    ```

## ./group_vars/tower

  - tower_nodes is a list of nodes which will be part of the "tower" node group. This can be a single node.
  - tower_db is the nominated database node which must have a second disk assigned for the tower DB volume group
  - The group_vars/vault file is encrypted with ansible vault to protect your license and admin password
  - If you want isolated nodes set tower_isolated_nodes to true
  - If tower_isolated_nodes is true, set out your node groups and the isolated nodes contained in these groups under tower_isolated_groups.
  - These names must match the inventory file
  - The variables for keepalived vip_addresses and vip_interface need to be set such that hapxory can be configured for failover.

## ./group_vars/vault

  - Fill out the file with the tower admin password you wish to use which is vault_tower_pass
  - Obtain a valid tower license and assign it to vault_tower_lic
  - Add eula_accepted" : "true" to the top of the license json as this may not be there initially
  - Encrypt this file with ansible-vault when finished (ansible-vault encrypt vault)
 
## ./roles/tower-db-filesystems/vars/main.yml

 - vg_name: this is the name of the volume group
 - pe_size: this is the patition size of your volume group
 - pv_name: this is device name of the blank disk

# Running the playbook
Run the playbook as per the below.
```sh
$ ansible-playbook -i inventory deploy_tower.yml --ask-vault-pass --ask-pass --ask-become-pass
```
