# OpenStack
Everything OpenStack

# Resources
  - SSH Keys - https://linuxize.com/post/how-to-set-up-ssh-keys-on-centos-7/
  - WinSCP - https://github.com/naturalis/openstack-docs/wiki/Howto:-Copying-files-to-your-OpenStack-instance-on-Windows
  
  - Create New Sudo User and Password:
    - https://linuxize.com/post/create-a-sudo-user-on-centos/
    - https://www.centos.org/docs/5/html/5.1/Deployment_Guide/s2-users-add.html
    - Adding password: 
        - Set password: Sudo passwd cloud-user
        - Modify config (Change to 'PasswordAuthentication yes'): Sudo nano /etc/ssh/sshd_config 
        - Restart ssh server: Sudo systemctl restart sshd

  - Set Password on Centos
    > **Set password:** sudo passwd cloud-user

    > **Modify config (Change to 'PasswordAuthentication yes'):** sudo nano /etc/ssh/sshd_config

    > **Restart ssh server:** sudo systemctl restart sshd

# Install Docker on Centos/Fedora      
  - https://docs.docker.com/install/linux/docker-ce/centos/#set-up-the-repository
  - skip docker install step #2.

# STEP #3 - Set up the instance:
- Set up key pair SSH:  find public resource
- Set up key pair SSH for yourself: find public resource

# STEP #4 - Accessing the OpenStack Instance:
  - In GIT BACH: **"ssh -A cloud-user@ip"**
  - ssh -i <your pem file> cloud-user@ip
  - ssh -A -i C:\\Users\\XXXXX\\.ssh\\file.pem cloud-user@ip
  
    ### with WinSCP
  - https://github.com/naturalis/openstack-docs/wiki/Howto:-Copying-files-to-your-OpenStack-instance-on-Windows
  ### SCP with ssh on GitBASH
  - scp location_to_file_on_local cloud-user@ip:/srv/Docker/foldername
  
