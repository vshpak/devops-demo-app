# Ansible Nginx deployment example

## Ansible installation

To install Ansible please refer to [the official documentation](https://docs.ansible.com/ansible/latest/installation_guide/installation_distros.html).

## Ansible setup

Ansible suppose that passwordless connection have been setup between Ansible host and target system(s).

To declare target hosts need to update `/etc/ansible/hosts` file.
For example:
```
[apps]
158.140.12.161
```

Where:

`[apps]` - group name of target system(s);

`158.140.12.161` - IP address of target system(s).

Also need to keep in mind that Ansible will use OS setting to establish connection to a terget system. So, if you have some custom/specific setting - you should aware about that and use additional Ansible parameters to set up that accordingly.

For example, if username for executing Ansible commands/playbooks (and corresponding SSH-keys) isn't the same as on the target system(s), then need to spesify username which will be used to execute commands on a target:
```
[apps]
158.160.16.176 ansible_user=ubuntu
```
In the above example specified username on the target system(s).

That's the same as use the following SSH-command for connection:
```
ssh ubuntu@158.160.16.176
```

After setting up Ansible you will be able to execute Ansible commands and playbooks.

## Ansible commands

The most simple way to execute required on a target system(s) - use Ansible CLI. It's like you are telling to Ansible: "execute me the following on the specified target":

For, example if you need to install Nginx server on all target systems in the `/etc/ansible/hosts` file you can use the below commad:
```
ansible all -m shell -a 'sudo apt install -y nginx'
```

Where:

`all` - directive which points to execute requested actions for all systems;

`-m shell` - directive which points to use `shell` module of Ansible (all actions on target(s) will be executed in shell)

`-a ` - directive which provides additional argument for modue, i.e. required shell command(s);

`sudo apt install -y nginx` - actual commad(s) which will be executed on target(s).
