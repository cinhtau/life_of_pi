
## General

Use ansible to upgrade all nodes.

Use [playbook](ansible/playbook.yml).

## Check Ansible

```bash
tan@omega:~/Sources/docs$ ansible --version
ansible 2.4.3.0
  config file = /etc/ansible/ansible.cfg
  configured module search path = [u'/home/tan/.ansible/plugins/modules', u'/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/lib/python2.7/dist-packages/ansible
  executable location = /usr/bin/ansible
  python version = 2.7.12 (default, Dec  4 2017, 14:50:18) [GCC 5.4.0 20160609]
```

## Check Cluster

Check if all nodes are up

```bash
tan@omega:~$ ansible all -m ping -u root
delta | SUCCESS => {
    "changed": false, 
    "ping": "pong"
}
beta | SUCCESS => {
    "changed": false, 
    "ping": "pong"
}
alpha | SUCCESS => {
    "changed": false, 
    "ping": "pong"
}
gamma | SUCCESS => {
    "changed": false, 
    "ping": "pong"
}
```

## Update

The playbook does

* update
* upgrade
* dist-upgrade
* clean
* auto-remove

```bash
tan@omega:~$ ansible-playbook playbook.yml -u root

PLAY [all] *************************************************************************************************************************************************************************************************

TASK [Gathering Facts] *************************************************************************************************************************************************************************************
ok: [delta]
ok: [alpha]
ok: [gamma]
ok: [beta]

TASK [ping] ************************************************************************************************************************************************************************************************
ok: [delta]
ok: [beta]
ok: [alpha]
ok: [gamma]

TASK [Update repositories cache] ***************************************************************************************************************************************************************************
changed: [gamma]
changed: [beta]
changed: [alpha]
changed: [delta]

TASK [Upgrade all packages to the latest version] **********************************************************************************************************************************************************
changed: [beta]
changed: [gamma]
changed: [delta]
changed: [alpha]

TASK [Update all packages to the latest version] ***********************************************************************************************************************************************************
ok: [alpha]
ok: [delta]
ok: [beta]
ok: [gamma]

TASK [Remove useless packages from the cache] **************************************************************************************************************************************************************
ok: [beta]
ok: [gamma]
ok: [delta]
ok: [alpha]

TASK [Remove dependencies that are no longer required] *****************************************************************************************************************************************************
ok: [beta]
ok: [gamma]
ok: [alpha]
ok: [delta]

PLAY RECAP *************************************************************************************************************************************************************************************************
alpha                      : ok=7    changed=2    unreachable=0    failed=0   
beta                       : ok=7    changed=2    unreachable=0    failed=0   
delta                      : ok=7    changed=2    unreachable=0    failed=0   
gamma                      : ok=7    changed=2    unreachable=0    failed=0   
```