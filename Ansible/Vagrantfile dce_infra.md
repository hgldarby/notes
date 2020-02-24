# Vagrantfile dce_infra

- Vagrantfile - where all the virtual machines are setup. The machines are described it also holds information on how to configure and provision the machines.
- `config.ssh.forward_agent = true` - forwards the ssh key to each new VM that you create automatically so you don't have to do it manually each time

For each VM:

- 