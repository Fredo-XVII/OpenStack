# OpenStack
Everything OpenStack

# Resources
  - SSH Keys - https://linuxize.com/post/how-to-set-up-ssh-keys-on-centos-7/
  - WinSCP - https://github.com/naturalis/openstack-docs/wiki/Howto:-Copying-files-to-your-OpenStack-instance-on-Windows
  
  - Create New Sudo User and Password:
    - https://linuxize.com/post/create-a-sudo-user-on-centos/
    - https://www.centos.org/docs/5/html/5.1/Deployment_Guide/s2-users-add.html

  - Set Password on Centos
    > **Set password:** sudo passwd cloud-user

    > **Modify config (Change to 'PasswordAuthentication yes'):** sudo nano /etc/ssh/sshd_config

    > **Restart ssh server:** sudo systemctl restart sshd
