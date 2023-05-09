# Ansible Playbooks for AWS EC2

Manage EC2 instances using Ansible playbooks.

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
ansible -i inventory/hosts "*" -m ping --user ubuntu --private-key ~/.ssh/ansible.pem
```

## Prerequisites

For the purpose of this demo:

- I use the same private key `ansible.pem` to SSH into both instances.
- Instances are running Ubuntu Server, hence the default username is `ubuntu`.
- SSH needs to be open on your security groups. All instances are on the same security group.
- The Public IPv4 DNS of my EC2 instance(s) are from an AWS Academy Learner Lab. They change every time the learner lab restarts.

## References

Loosely based on [Automate EVERYTHING with Ansible! (Ansible for Beginners) (youtube.com)](https://www.youtube.com/watch?v=w9eCU4bGgjQ)

Because I am using AWS Academy, the instances' address changes every time I restart the learner lab. Ansible won't be happy with that, because it does host key checking every time, see discussion here [ansible ssh prompt known_hosts issue (stackoverflow.com)](https://stackoverflow.com/questions/30226113/ansible-ssh-prompt-known-hosts-issue).

There are several way to resolve that issue. The easiest is to run `export ANSIBLE_HOST_KEY_CHECKING=False` in your terminal before executing Ansible commands.
