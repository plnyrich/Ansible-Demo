# CNSM24 - PhD Workshop - Ansible
Sources used in the Ansible demo during the CNSM24 PhD Workshop.

The target of the demo is to create an Ansible for quick provisioning of a simple web server serving a static website.

| Ansible Folder      | Description                                                                                   |
|---------------------|-----------------------------------------------------------------------------------------------|
| `ansibleFromSlides` | Ansible code from slides, some of it may not work as it is for screenshots and demonstrations |
| `ansibleDemoPrep`   | Prepared Ansible project for the demo                                                         |
| `ansibleDemoDone`   | The resulting Ansible project (after the demo)                                                |

### Demo with Vagrant
Vagrantfile is prepared the demo - a VM with OracleLinux9.
The following points must be fullfilled in order to use it correctly:
1. `ansible.cfg` must be present in the root folder of the Ansible project with the following content:
```
[defaults]
host_key_checking = false
```
2. We must alter the SSH connection settings in the Ansible inventory to the following:
```
localhost ansible_ssh_user=vagrant ansible_ssh_pass=vagrant ansible_ssh_port=2222 ansible_become=yes
```
3. `selinux` on the target machine must be deactivated, otherwise httpd will not start:
```
setenforcing 0
```
Points 1. and 3. are already prepared in the `ansibleDemoPrep` and `ansibleDemoDone` folders. The user must manually select the correct SSH connection settings in `<ansibleProject>/inventory/inventory` file (point 2).

Firstly, we will bring VM online by calling in the root folder of this repository:
```
vagrant up --provider=virtualbox
```
Then, we can call `cd` and run the Ansible:
```
cd ansibleDemoDone
ansible-playbook -i inventory/inventory pb_deploy.yml --skip-tags 'cleanup'
```

Also note that the port forwarding is defined for port 12500 (default value specified in our Ansible's group_vars file, where httpd will listen to connections). If you decide to change the port in the group_vars, you must also define it in the Vagrantfile, otherwise the connection will not be established.

If the demo finished running successfully, you can call:
```
curl http://localhost:12500/home.html
```

### Contact
Contact: [plnyrich@fit.cvut.cz](mailto:plnyrich@fit.cvut.cz)
