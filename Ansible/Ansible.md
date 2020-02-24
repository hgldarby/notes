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

### 3./4.

- Control machine - where we install ansible and do all config management 
- **Vagrant** - wrapper around virtualbox and vmware fusion
- Control machine - can't use windows as a control machine, must be Linux
- Ubuntu - Linux distribution, base operating system
- All commands run through control machine
- Control machine needs ssh (public key trusts) authentication.
- User made to have ansible access will have super user access.

### 5. Inventory Pt 1

- With ansible, potential targets need to be set up in advance using an inventory

- Can be done using:

  - A static file - Contains a list of hosts
  - A dynamic file - Normally implemented as a script which calls some other API/service to populate all the host information variable data

- Use a static file called "hosts" for now to populate a simple list of new hosts with some groups

  ```
  [loadbalancer]
  lb01
  
  [webserver]
  app01
  app02
  
  [database]
  db01
  
  [control]
  control
  ```

- Inventory - lists the hosts but can also list some additional information alongside those host names

- Extra details - mostly about how you connect to the host

- By putting the parameters in the inventory, you can assure that whenever you connect to the host, the right parameters are used

- You can also group in an inventory

### 6. Inventory Pt 2

- In the inventory, add the control server

- `ansible --list-hosts all` - lists the hosts in that directory

- `ansible -i <filename> --list-hosts all` - lists all hosts in the file given

- Ansible, by default, will attempt to ssh into every host that is in the inventory

- As we are executing ansible from the control host, it will try to ssh into itself which is unnecessary

- Ansible allows us to specify the connection type which we can set to local

  ```
  control ansible_connection_type=local
  ```

### 7. Host selection

- `*` is the equivalent of using `all`
- So `ansible --list-hosts "*"` is the same as `ansible --list-hosts all`
- `ansible --list-hosts <groupname>` lists all hosts within the group
-  using the same command with `"app0*"` returns the hosts with `app0` in the name
- `ansible --list-hosts <groupname>[0]` returns the first in the list
- ``ansible --list-hosts \!control` - every host that isn't in the control group

### 8. Tasks

- `ansible -m ping all` - `-m` selects the `ping` module - pings all hosts
- `ansible -m command -a "hostname" all` - `command` module is default so could just run `ansible -a "hostname" all`
- `command` accepts parameters in the form of text

### 9. Plays

- Playbooks are used to write tasks down so they can be executed in bulk to manage our systems 

- Playbook - file written in yaml syntax made up of plays
- Play - A set of target hosts and the task to execute against those hosts
- syntax of playbook is a list of plays
- adhoc commands - good for troubleshooting, getting information about the environment

### 10. Playbook Execution

- `ansible-playbook <playbookpath>` - runs the playbook in the path provided

### 11. Playbooks Introduction

- 4 pillars of a linux application:
  - The packages you require
  - The service tracker
  - The overall system config (files/directories need creating to support the application etc)
  - The config files for the app itself

### 12. Packages: apt

- NGINX - a web server which can be used as a reverse proxy, load balancer, mail proxy ad HTTP cache
- Used as a load balancer in this section
- using apt:
  - name - name of the package (nginx)
  - state - present (current latest version, doesn't update if there is a new one), latest (updates at every new version)
  - update_cache - 
- perform the same task for the databases using mysql-server
- mysql server - relational database management tool

### 13. Packages: become

- To invoke super user privileges write:

  ```yaml
  become: true
  ```

  as such:

  ```yaml
  ---
  - hosts: loadbalancer
    become: true
    tasks:
      - name: install nginx
        apt: 
        	name: nginx
          state: present
          update_cache: yes
  ```

- perform the same task for the databases

### 14. Packaged: with_items

- with_items - acts like a loop where in this case we want to install  several packages. The `name: {{items}}` is jinja and means we can inject variables into it so we use each of the items in the `with_items` to run the code with

  ```yaml
  ---
  - hosts: webserver
    become: true
    tasks:
      - name: install web components
        apt:
          name: "{{item}}"
          state: present
          update_cache: yes
        with_items:
          - apache2
          - libapache2-mod-wsgi
          - python-pip
          - python-virtualenv
  ```

- The output from running `ansible-playbook webserver.yml` allows us to see what has been installed as items

### 15. Services: service

- Adding in a service in the loadbalancer.yml:

  ```yaml
  - name: ensure nginx started
        service:
          name: nginx
          state: started
          enabled: yes
  ```

- where:

  - name - the name of the application
  - state - ensure that the application is started
  - enabled - yes means we want this to start when we start the vm

- Do the same for the webserver (apache2) and database (mysql)

### 16. Support Playbook 1 - Stack Restart

- This allows us to perform a hard reset and get back to a state that we know will work

  ```yaml
  ---
  # Bring stack down
  - hosts: loadbalancer
    become: true
    tasks:
      - service:
          name: nginx
          state: stopped
  
  - hosts: webserver
    become: true
    tasks:
      - service:
          name: apache2
          state: stopped
  
  # Restart mysql
  - hosts: database
    become: true
    tasks:
      - service:
          name: mysql
          state: restarted
  
  # Bring stack up
  - hosts: webserver
    become: true
    tasks:
      - service:
          name: apache2
          state: started
  
  - hosts: loadbalancer
    become: true
    tasks:
      - service:
          name: nginx
          state: started
  ```

### 17. Services: apache2_module, handlers, notify

- Ensure apache module mod-wsgi is running

- add a new task to ensure mod_wsgi is enabled as such:

  ```yaml
  - name: ensure mod_wsgi enabled
        apache2_module:
          state: present
          name: wsgi
  ```

  state in this case is present or absent, common in ansible.

- This enables the module in apache

- We need to restart apache for the module to take effect so we can add a handler as such:

  ```yaml
  handlers:
      - name: restart apache2
        service:
          name: apache2
          state: restarted
  ```

- Written the same way a service task is written

- We need to request the restart is triggered by adding `notify` as shown below

  ```yaml
  - name: ensure mod_wsgi enabled
        apache2_module:
          state: present
          name: wsgi
        notify: restart apache2
  ```

### 18.  Files: copy

- Next step - move application over to application hosts and configured in apache

- Flask application

- Add a task in webserver to copy demo app source from the source to the destination

  ```yaml
  - name: copy demo app source
        copy:
          src: demo/app/
          dest: /var/www/demo
          mode: 0755
        notify: restart apache2
  ```

  - parameters described in documentation
  - src - source relative to the control machine playbook directory
  - dest - destination on app server host. will create the directory for us
  - mode - the permissions for the destination file or directory

### 19. Application Modules: pip

- Create a new task in webserver to setup python virtualenv

  ```yaml
  - name: setup python virtualenv
        pip:
          requirenemts: /var/www/demo/requirements.txt
          virtualenv: /var/www/demo/.venv
        notify: restart apache2
  ```

  remember to restart apache to ensure the module is installed

### 20. Files: file

- Add two new tasks to the webserver.yml 

  ```yaml
  - name: de-activate default apache site
        file:
          path: /etc/apache2/sites-enabled/000-default.conf
          state: absent
        notify: restart apache2
  
  - name: activate demo apache site
  	  file:
          src: /etc/apache2/sites-available/demo.conf
          dest: /etc/apache2/sites-enabled/demo.conf
          state: link
         notify: restart apache2
  ```

- Using `curl http://192.168.56.110` (app01's ip) we should get a nice message back from the chap
- Same should work for app02
- Doing it for lb01 - nginx has no awareness of the server backend and is still in its default config

### 21. Files. Templates

- File module - template

- Instead of copying a file directly from the control machine onto the end host, Template subs out any variable values that we've supplied first and then render the final content into the end host

- Create a template file

  ```jinja2
  upstream demo {
  {% for server in groups.webserver %}
      server {{ hostvars[server]['ansible_host'] }};
  {% endfor %}
  }
  
  server {
      listen 80;
  
      location / {
          proxy_pass http://demo;
      }
  }
  ```

  - upstream - a list of backends that we can use to load-balancing

  - Use a for loop to loop through the servers that we have
  - Create a server line containing the server based off the server and ip

- Move task `ensure nginx started` to the end of the tasks in load-balancer

- Add creation of an error log file:

  ```yaml
  - name: Create nginx error log file
        file:
          path: /var/log/nginx/error.log
          state: touch
          owner: root
          group: root
        changed_when: false
  ```

### 22. Files: lineinfile

- **Lineinfile** is an ansible module 
- Allows us to preserve the file as is on the filesystem, but we can edit one or several lines to change a particular line to a specific value
- Issues needed to be resolved:
  - Add task create mysql error log file in database
  - Change owner and group from root to mysql
  - Add task to add "[mysqld]" at the start of the config file /etc/mysql/my.cnf

### 23. Application Modules: mysql_db mysql_user

- Adding two tasks to database
- Create a demo database
- Create a demo user

### 24. Support Playbook 2 - Stack Status: wait_for

- We used the service module to start or stop the service
- Service module doesn't have a status check

- Using the service module would affect the status of that particular service
- For example, it may try to start nginx for example if we configured it that way
- Therefore, we use the command module instead
- Use module **wait for** - This stops the playbook and starts attempting to connect and see if the particular port is listening, once it's listening, the playbook will continue

### 25. Support Playbook 2 - Stack Status: uri, register, fail, when

- **uri** - allows us to get an end to end test

### 26. Playbook Summary

- Completed basic config for all our services in all three tiers including our control machine
- Learnt about many of the core modules that will be used day to day
- Built two support playbooks - `stack_status` and `stack_restart`
- Make it work, make it right, make it fast
- So far we've made it work

### 27. Roles Overview

- Role - A folder to keep tasks, files, variables, handlers that are part of a specific function
- Servers can be composed as a combination of various roles
- Benefits:
  - Code reuse
  - Set a foundation for scaling up infrastructure
- Ansible Galaxy - used as a file generator in this case. A repo for Ansible roles that are available to drop directly into the playbooks to streamline automation projects.

### 28. Converting to Roles: tasks, handlers

- Move the tasks from the playbook into the tasks/main.yml file and call the roles from the playbook instead

- Same idea with the handlers

### 29. Converting to Roles: files, templates

- Follow the video to move content of the other playbooks, templates and demo into the new roles

### 30. Site.yml: include

- Make sure nothing has broken
- Run all the playbooks again
- `site.yml` can be used as a playbook to run the other playbooks

### 31. Variables: facts

- Adjust the `bind-address` so that it only listens to `ansible_enp0s8`

  ```yaml
  "bind-address = {{ansible_enp0s8['ivp4']['address']}}"
  ```

  This gives the IP address of the db01 machine.

- `bind-address` - Config within MySQL on which networks it can listen for connections on.

### 32. Variables: defaults

- Main objective: to set default values in the role/defaults/main.yml file 
- For this we've changed mysql/tasks/main.yml to remove the "demo" fields in create demo database and user and moved the defaults into the defaults/main.yml file

### 33. Variables: vars

- https://docs.ansible.com/ansible/latest/user_guide/playbooks_variables.html

- Keep the variables simple

### 34. Variable: with_dict

- Variation of `with_items`
- Just a key value mapping
- `with_dict: sites` doesn't work
- New syntax requires `with_dict: "{{ sites }}"`

### 35. Selective Removal: shell, register, with_items, when

- sshing into lb01 and looking at /etc/nginx/sites-enabled/ shows us a demo which we configured before and a myapp which has just been configured
- So we have two active sites - demo and myapp
- Ansible no longer knows about demo as it's not in the playbooks

### 36. Variables - continued

- Follow the lecture for info

### 37. Variables: vars_files, group_vars

- Follow lecture

### 38. Variables: vault

- Ansible vault - used to encrypt variables inside our setup
- vault encrypts the entire contents of the file
- We don't use vault
- Good if you need to store passwords on a public domain

### 39. External Roles and Galaxy

- Galaxy - external repo for roles

### 40. Advanced Execution Intro

- Make it fast
- `time ansible-playbook <playbook_name>`

### 41. Removing Unnecessary Steps: gather_facts

- Look for places where we gather facts
- If some are unnecessary, set `gather_facts: false`

### 42. Extracting Repetitive Tasks: cache_valid_time

- `update_cache` important on initial install
- After, this is not so necessary
- Use `cache_valid_time` to skip `update_cache`

### 43. Limiting Execution by Hosts: limit

- `ansible-playbook <playbook_name> --limit <host>`
- Limits the playbook to only run on that particular host

### 44. Limiting Execution by tasks: tags

- `ansible-playbook <playbook_name> --list-tags` - lists the tags available
- `ansible-playbook <playbook_name> --tags "<tag>"` - runs the playbook for that specific tag

- `ansible-playbook <playbook_name> --skip-tags "<tag>"` - runs the playbook but skipping the certain tags

### 45. Idempotence: changed_when, failed_when

- `changed_when: false`  - outcome can only be ok or failed when we run
- `failed_when` - similar idea to changed_when - can determine when ansible tells you when something has failed

### 46. Accelerated Mode and Pipelining

- Read the docs page
- Pipelining is best

### 47. Troubleshooting Ordering Problems

- Ordering - A common issue when trying to run playbooks
- `ignore_errors: true` - allows us to continue through a failure
- reorder the tasks in a playbook

### 48. Jumping to Specific Tasks: list_tasks, step, start-at-task

- `ansible-playbook <playbook_name> --step` - allows you to step through the tasks in the playbook
- `ansible-playbook <playbook_name> --start-at-task "<taskname>"` - allows you to run the playbook from a specific task

### 49. Retrying Failed Hosts

- Watch Lecture

### 50. Syntax-Check & Dry-Run: syntax-check, check

- `ansible-playbook --syntax-check <playbook_name>` - checks the syntax for a specific playbook
- dry run - will perform the run but not make the changes. Ansible will store what it thinks the run is going to do when it comes time to execute the change
- `ansible-playbook --check <playbook_name>` - performs the dry run

### 51. Debugging: debug

- Leave debug statements out of production

- https://docs.ansible.com/ansible/latest/modules/debug_module.html

