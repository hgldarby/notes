# Install ansible to virtual machine

- Follow the following process in the ubuntu virtual machine to build a **PPA **(personal package archives):

  ```
  $ sudo apt update
  $ sudo apt install software-properties-common
  $ sudo apt-add-repository --yes --update ppa:ansible/ansible
  $ sudo apt install ansible
  ```


- To check we have access to the ansible command line tool use:

  ```
  ansible --version
  ```

- Add the ansible playbook

  ```
  ansible playbook --version 
  ```

- Also need the ansible galaxy tool

  ```
  ansible galaxy --help
  ```

  

