# Virtual box Configuration

### GUI vs Headless

- By default, VirtualBox machines start in headless mode

- **Headless mode** - there is no UI for the machines visible on the host machine

- Sometimes you want a UI, maybe to see a browser running in the machine or debugging a strange boot issue

- To boot the vm with a GUI alter the vagrantfile with:

  ```yaml
  config.vm.provider "virtualbox" do |v|
    v.gui = true
  end
  ```

### Virtual Machine Name

- You can customise the name that appears in the VirtualBox GUI by setting the `name` property

- By default, Vagrant sets the name to the containing folder of the Vagrantfile plus a timestamp of when the machine was created

- To customise the vm's name use:

  ```yaml
  config.vm.provider "virtualbox" do |v|
    v.name = "my_vm"
  end
  ```

### Default NIC Type

- **NIC** - Network Interface Controller

- By default Vagrant will not set the NIC type for network interfaces

- This allows VirtualBox to apply the default NIC type for the guest

- To use a specific NIC type by default for guests, set the `default_nic_type` option like so:

  ```yaml
  config.vm.provider "virtualbox" do |v|
    v.default_nic_type = "82543GC"
  end
  ```

### VBoxManage Customisations

- VBoxManage - A utility that can be used to make modifications to VirtualBox vm's from the command line

- Vagrant exposes a way to call any command against VBoxManage just prior to booting the machine:

  ```yaml
  config.vm.provider "virtualbox" do |v|
    v.customize ["modifyvm", :id, "--cpuexecutioncap", "50"]
  end
  ```

  In the example above, the VM is modified to have a host CPU execution cap of 50%, meaning that no matter how much CPU is used in the VM, no more than 50% would be used on your own host machine

- The `:id` special parameter is replaced with the ID of the virtual machine being created, so when a VBoxManage command requires an ID, you can pass this special parameter.

- Multiple `customize` directives can be used. They will be executed in the order given.

- There are some convenience shortcuts for memory and CPU settings:

  ```yaml
  config.vm.provider "virtualbox" do |v|
    v.memory = 1024
    v.cpus = 2
  end
  ```