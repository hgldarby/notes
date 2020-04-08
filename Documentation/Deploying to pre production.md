# Deploying to pre production

- Use cmd, navigate to D:\infra\vagrant and run - `vagrant up control`
- Use Putty and connect to `infra_control`

- Make sure ssh key is in pageant
- Ensure in top bar, tools->deployment->configuration is set up as such with relevant information, i.e. my name
- ![image-20200408122418897](C:\Users\darbyh\AppData\Roaming\Typora\typora-user-images\image-20200408122418897.png)
- Ensure mapping looks like this
- ![image-20200408122337737](C:\Users\darbyh\AppData\Roaming\Typora\typora-user-images\image-20200408122337737.png)
- Copy entire ansible infra repo into the virtual machine - control
- right click on project folder navigate to deployment -> upload to control

### Backend

- Navigate to engine in pycharm
- find `tools\buildbot\deploy_to_testing.py`
- run the file



### Frontend

- bit more complex

