# Ansible Playbooks for AWS EC2

Manage EC2 instances using Ansible playbooks.

1. Get the public Public IPv4 DNS of your EC2 instance(s)
2. Add the these addresses to the `inventory/hosts` file
3. Update `ansible_ssh_private_key_file` with the path to the private key(s) for your instance(s)
4. Update `ansible_user` with the right username for your instance(s)
5. Run the playbook:

```shell
ansible-playbook playbooks/apt.yml -i inventory/hosts
```

## Prerequisites

For the purpose of this demo:

- I use the same private key `ansible.pem` to SSH into both instances.
- Instances are running Ubuntu Server, hence the default username is `ubuntu`.
- SSH needs to be open on your security groups. All instances are on the same security group.
