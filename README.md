# Ansible Playbooks for AWS EC2

This repository is an Ansible demo for CS 312 System Administration course.

The course uses AWS Academy Learner Lab. The code described here can work with any AWS EC2 instances.

SSH connection needs to be allowed on the security group.

1. Get the public Public IPv4 DNS of your EC2 instance(s)
2. Add the these addresses to the `inventory/hosts` file
3. Update `ansible_ssh_private_key_file` with the path to the private key(s) for your instance(s)
4. Update `ansible_user` with the right username for your instance(s)
5. Run the playbook:

```shell
ansible-playbook playbooks/ping.yml -i inventory/hosts
```

The equivalent non-Playbook version of this is:

```shell
ansible -i inventory/hosts "*" -m ping
```

This repo contains three playbooks with each one task. In practice, a playbook can contain multiple plays, tasks, and modules.

The `hosts` file does not need to be in the `/inventory` directory, and the playbooks don't need to be in the `/playbooks` directory. I am using these directories to organize the code.

The `hosts` file containes one group `[servers]`. In the playbooks, I use both `hosts: servers` and `hosts: "*"` to select that group. The second option selects all groups in the inventory.

You can use Ansible playbooks on `localhost` as well.

## Prerequisites

For the purpose of this demo:

- You need a Unix-like system for the control node (i.e., the computer where you execute `ansible` commands or run playbook). If using Windows, you'll need (to use) WSL.
- Ansible needs to be installed. Please refer to their documentation to do so.
- I use the same private key `ansible.pem` to SSH into all instances.
- Instances are running Ubuntu Server, hence the default username is `ubuntu`.
- SSH and ICMP need to be open on your security groups. All instances are on the same security group.
- The Public IPv4 DNS of my EC2 instance(s) are from an AWS Academy Learner Lab. They change every time the learner lab restarts.
- The AWS CLI credentials also change every time the learner lab restarts.

### Pre and Post Demo Playbooks

For in-class demonstrations, I've created two playbooks to initialize the required EC2 resources.

Before the demo, run `ansible-playbook ./playbooks/pre-demo.yml`. This will create a key pair, create three EC2 instances running Ubuntu, update the security group, and create a `hosts` file.

After the demo, run `ansible-playbook ./playbooks/post-demo.yml`. This will delete the key pair, delete **all** EC2 intances, and delete the `hosts` file.

## References

Loosely based on [Automate EVERYTHING with Ansible! (Ansible for Beginners) (youtube.com)](https://www.youtube.com/watch?v=w9eCU4bGgjQ)

Because I am using AWS Academy, the instances' address changes every time I restart the learner lab. Ansible won't be happy with that, because it does host key checking every time, see discussion here [ansible ssh prompt known_hosts issue (stackoverflow.com)](https://stackoverflow.com/questions/30226113/ansible-ssh-prompt-known-hosts-issue).

There are several way to resolve that issue. The easiest is to run `export ANSIBLE_HOST_KEY_CHECKING=False` in your terminal before executing Ansible commands.
