# Ansible

### 1.

- Fits into category of tools called **infrastructure automation**
- Purpose of automation:
  - reduce time and risk associated with making changes
  - more opportunity to find errors

### 2.

- Ansible - configuration management tool
- Config management:
  - Cross platform implementations
  - Templating
  - Variables
  - Framework for building modular code
  - Idempotence - Re-running code provides the same outcome - this builds confidence in the infrastructure
- Orchestration:
  - In charge of applying the database schemas before updating web servers etc

### 3.

- Control machine - where we install ansible and do all config management 
- **Vagrant** - wrapper around virtualbox and vmware fusion
- Control machine - can't use windows as a control machine, must be Linux
- Ubuntu - Linux distribution, base operating system
- All commands run through control machine
- Control machine needs ssh (public key trusts) authentication.
- User made to have ansible access will have super user access.