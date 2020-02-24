# DCE_Infra Roles

### Ansible

- Tasks:
  - Lots of docstrings

### Autossh

##### Handlers

- Handler to restart autossh:

  - AutoSSH - a command that detects when [SSH](https://wiki.gentoo.org/wiki/SSH) connections drop and automatically reconnects them - https://wiki.gentoo.org/wiki/Autossh

    ```yaml
    - name: restart autossh
      systemd:
        name: "{{ autossh_service_name }}"
        state: restarted
      listen: restart postgresql
      tags:
        - postgres_config
    ```

  - systemd module - https://docs.ansible.com/ansible/latest/modules/systemd_module.html

  - listen - gets notifications from another handler - https://medium.com/@george.shuklin/listen-feature-for-handlers-in-ansible-29183524c7e1

  - tag - "postgres_config" 



##### Tasks

- Ensure packages are installed:
  - Install autossh
  - Call the handler to restart autossh
- Create a 2048-bit SSH key for user root
  - Alter the root user account - https://docs.ansible.com/ansible/latest/modules/user_module.html
  - generate an ssh key for the user
  - make it 2048 bits long
  - register the key as a host-level variable - https://docs.ansible.com/ansible/latest/user_guide/playbooks_variables.html
- Save public key on dbs server
  - `delegate_to` - 