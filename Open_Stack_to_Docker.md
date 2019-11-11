Open Stack Instance: (assumes that you have open stack server set up)
Prep Build:
Compute  → Overview → Determine specs for new instance.  For example, for the Stores Learning server will use 16GB RAM, 1 floating IP, 4VCPU.
Compute → Keypair → Generate key pair for instance and move downloaded key to ~/.ssh/ on Linux, on windows to C:\Users\PCID\.ssh
Network → Security Group →
Create Security Group → give group a name.
Will continue with this set up in the "Post Build Steps" instructions below.
Create Network: ( this step is only needed if you haven't created a subnet for your Open Stack server, skip if not needed )
Network → Networks → Provide Name for Network, click next.
Provide Name for Subnet. Select "Allocate address from pool", "Address Pool", "Network Mask".  I used the first option or defaults. Click next.
Subnet Details: No input, just click "Create"
Done, network created!!!

Build Instance: Compute  → Instances → Launch Instance
Quick Check: at this point you should have at least a security group and a key pair for your instance.  A network is optional if one already exists. if none exist, go to step #1 and build a network.
Details → Name the instance.  Click next.
Source → select CentOs flavor.  I usually go with "centos-7-latest". Click Next
Flavor → Flavors manage the sizing for the compute, memory and storage capacity of the instance. Use the information from Overview above. Click Next.
Network → Select network. click next
Network ports → select if available. None to select for this build.
Security Groups → select the security group from step #1.  In this case Stores Learning.  I leave the default security group alone.
Key Pair → select key pair generated in step #1.  In this case Stores Learning
Configuration → skip, click next.
Server Groups → skip, click next.
Scheduler Hints → skip, click next.
Metadata → skip, click next.
Launch Instance!!!! Yeah you made it!

Post Build Steps:  ( This may not be needed for the site to work properly )
Network → Network Topology → You will see your new instance built, if it is not connected to the "ext-core", hover over the "[X]" looking icon and click "Add Interface".  Select the subnet for the new instance, click submit. ***Skip is instance is connected to "ext-core".
Compute → Instances → Add Floating IP Address: Find "Create Snapshot" on the right hand side of the instance information, click on down arrow → Click "Associate Floating IP"
Select IP Address if available.  If no IP available, you will need to reach out to the OpenStack team to have them add some to your Open Stack account.
Click "Associate"
Network → Security Group →
Manage Rules → Add Rules →
Change the "Port" to 22.  This will allow you to ssh into the instance.
Leave all options alone, click "ADD".
Because this is going to be used for an RStudio Server container, I will add port 8787 now, otherwise, I will need to add it later.
Once you are done adding ports, go to the next step.

Log into Open Stack Instance →
On Windows w/ GIT BASH:  ssh -A -i C:\Users\PCID\.ssh\KEYPAIR_FROM_ABOVE.pem user@10.XX.XXX.XXX
Yeah!!! You are in your instance and now you can look around, type "ls -la", or you can download software ( more on that in the sections below ).


THIS NEXT STEP IS NOT NECESSARY, BUT IF THE PEM FILE IS CORRUPTED ON THE OPENSTACK INSTANCE, YOU WON'T BE ABLE TO SSH IN WITH THE COMMAND ABOVE AND YOU WILL BE LOCKED OUT OF YOUR SERVER WITH NO WAY IN.
SKIP THIS STEP AT YOUR OWN PERIL.  THIS PASSWORD CREATES A BACKDOOR TO GET INTO THE SERVER. I RECOMMEND TO USE A PASSWORD MANAGER TO STORE YOUR PASSWORDS. I USE KEEPASS BECAUSE IT HAS NO CLOUD ACCOUNT. 



Create Password for User → this assumes that you are logged in your openstack instance.
Modify config:
 Change to Root User: type "sudo -i"
Install Nano: nano is a text editor.  type "sudo yum install nano"
Resource for installing and using Nano: https://www.hostinger.com/tutorials/how-to-install-and-use-nano-text-editor#gref
 type "sudo nano /etc/ssh/sshd_config" 

Change "PasswordAuthentication no"to 'PasswordAuthentication yes'

Set password: type "sudo passwd user" → hit enter
Restart ssh server: type "sudo systemctl restart sshd"

Installing Docker on OpenStack:
The following instructions should be followed in order:

Got to this link and follow the prep instructions for docker: https://docs.docker.com/install/linux/docker-ce/centos/#set-up-the-repository
Type "yes" for the installation of the software.
skip "Install Docker CE" #2, go straight to #3
Once you have done step #4, run the hello-world container you are done.
Yeah....Docker is now installed and running.
Adjust the Docker settings so that you don't have to type sudo every time...a must to run datastream jobs: https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-centos-7
if logged in as user: type, or copy paste, "sudo usermod -aG docker $(whoami)"
log out and log back in to set the changes.
