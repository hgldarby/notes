# Vagrant getting started

### Installing vagrant

- Download and install appropriate package from:
  https://www.vagrantup.com/downloads.html
- To verify install, open a command prompt and type `vagrant`

### Project setup

- Make a root directory for the project
- `mkdir vagrant_getting_started` - creates a directory
- `cd` into the new directory
- `vagrant init hashicorp/bionic64` - this initialises a directory and adds a `Vagrantfile` in the current directory

### Boxes

- Boxes - Instead of building a virtual machine from scratch, which would be a slow and tedious process, Vagrant uses a base image to quickly clone a virtual machine. These base images are boxes.

- `vagrant box add <nameofbox>` - This stores the box under a specific name so that multiple vagrant environments can re-use it.

- Now a box has been added to vagrant, we need to configure the project to use it as a base.

- Open the 'Vagrantfile' in the directory created

- Make the contents:

  ```yaml
  Vagrant.configure("2") do |config|
    config.vm.box = "hashicorp/bionic64"
  end
  ```

  the 'hashicorp/bionic64' must match the name used to add the box above

- A specific version of the box can be specified using `config.vm.box_version` as such:

  ```yaml
  Vagrant.configure("2") do |config|
    config.vm.box = "hashicorp/bionic64"
    config.vm.box_version = "1.1.0"
  end
  ```

- The URL of a box can be specified using `config.vm.box_url` as such:

  ```yaml
  Vagrant.configure("2") do |config|
    config.vm.box = "hashicorp/bionic64"
    config.vm.box_url = "https://vagrantcloud.com/hashicorp/bionic64"
  end
  ```

### Up and SSH

- `vagrant up <vmname>` - boots up the virtual machine running ubuntu with the given name if specified, otherwise all
- `vagrant ssh` - drops you into a full SSH session

- 'Ctrl' + 'd' - close the SSH session
- `vagrant destroy` - terminate the use of any resources by the virtual machine

### Synced Folders

- Using synced folders allows vagrant to automatically sync files to and from the guest machine (virtual machine)
- By default vagrant shares the project directory ( the one with the vagrantfile) to the `/vagrant` directory in the guest machine
- When `vagrant ssh` ing into the machine you're in `/home/vagrant`
- `/home/vagrant` is a different directory from the synced `/vagrant` directory
- Vagrant keeps the folders in sync between the host and the guest/vurtual machines.

### Provisioning

- Vagrant has built in support for automated provisioning

- Using this, vagrant will automatically install software when running `vagrant up` so that the guest machine can be repeatedly created and ready to use

- **Apache** - The Apache HTTP Server Project is an effort to develop and maintain an open-source HTTP server for modern operating systems

- Setting up apache requires setting up a shell script as below named 'bootstrap.sh':

  ```
  apt-get update
  apt-get install -y apache2
  if ! [ -L /var/www ]; then
    rm -rf /var/www
    ln -fs /vagrant /var/www
  fi
  ```

- We then need to configure vagrant to run the shell script when setting up the machine

- This is done by editing the Vagrantfile to look like:

  ```
  Vagrant.configure("2") do |config|
    config.vm.box = "hashicorp/bionic64"
    config.vm.provision :shell, path: "bootstrap.sh"
  end
  ```

- The provision line is new and tells Vagrant to use the `shell` provisioner to setup the machine with the 'bootstrap.sh' file.

- Once all is configured, run `vagrant up` 

- If guest machine is already running from a previous step, then run `vagrant reload --provision` - this restarts the vm, skipping the initial import step

- The `--provision` command tells vagrant to run the provisioners

### Networking

- Vagrants networking features give us additional options for accessing the machine from our host machine.

- One option is **port forwarding** - this allows us to specify ports (a communication endpoint) on the guest machine to share via a port on the host machine

- This allows access to a port on your own machine, but have all the network traffic forwarded to a specific port on the guest machine.

- Setting up a forwarded port, so that we can access Apache in the guest machine, requires editing of the Vagrantfile like so:

  ```
  Vagrant.configure("2") do |config|
    config.vm.box = "hashicorp/bionic64"
    config.vm.provision :shell, path: "bootstrap.sh"
    config.vm.network :forwarded_port, guest: 80, host: 4567
  end
  ```

- Just run `vagrant reload` if the machine is still running so that the changes take effect

### Share

- Vagrant makes it easy to shar and collaborate on the environments
- Vagrant share lets you share the vagrant environment to anyone around the world with an internet connection
- It will give a URL that will route to the vagrant environment from any device connected to the internet.
- The `vagrant-share` plugin is needed for this to work
- Then run `vagrant share`
- Ending the sharing session requires 'Ctrl' + 'c'

### Teardown

- `vagrant suspend` - saves the current state of the machine and stops it. Running `vagrant up` will run the machine from where it was suspended
- `vagrant halt` - gracefully shuts down the machine
- `vagrant destroy` - removes all traces of the guest machine from the system



