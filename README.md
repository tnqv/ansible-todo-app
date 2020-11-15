# ansible-todo-app

## Prerequisites
- Install Vagrant
- Install Ansible

### Step 1: Vagrant Up based on Vagrantfile

`vagrant up`

### Step 2: Install required Roles by running 
`ansible-galaxy install -r requirements.yml`

### Step 3: Create inventories/vagrant folder for inventory

My example **inventory**:

```
[service]
IP service machine

[db]
IP db machine

[all:vars]
ansible_connection=ssh
ansible_user=vagrant
ansible_ssh_private_key_file="/foo/bar/.vagrant.d/insecure_private_key"
```

### Step 3: Apply ansible playbook of database and service by running
`ansible-playbook playbooks/service/main.yaml -i inventories/vagrant -v`

`ansible-playbook playbooks/db/main.yaml -i inventories/vagrant -v`

### Check out results

- Now If you are using Mac/Ubuntu: Add your `/etc/hosts` with (IP of machine) `192.168.2.2 service.test`
- Then go to browser with `service.test`