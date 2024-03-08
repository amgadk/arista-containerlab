AVD Arista Validated Design for Arista Test Drive
Arista CloudVision Automation Arista EOS Automation

About
This repository is configured to run arista.cvp & arista.avd Ansible collections against the Arista Test Drive (ATD) single data center topology.

Arista CloudVision and Ansible

To access an ATD topology, please get in touch with your Arista representative.

Lab topology
The diagram below shows that the ATD lab topology has two data centers. We will only leverage DC1 in this example.

ATD Lab Topology

ATD topology device list
Device	 IP Address
s1-spine1	192.168.0.10
s1-spine2	192.168.0.11
s1-leaf1  	192.168.0.12
s1-leaf2  	192.168.0.13
s1-leaf3  	192.168.0.14
s1-leaf4  	192.168.0.15
s1-host1  	192.168.0.16
s1-host2  	192.168.0.17
Current repository is built with cEOS management interface (Management0). If you run a vEOS topology, please update mgmt_interface field to Management1 in the ATD_LAB group_vars.

Getting Started
Connect to your ATD lab environment
Don't hesitate to contact your local account team if you need an ATD Lab instance.
Once connected to the ATD lab instance, select the Programmability IDE.
This container is built with all the requirements and Python modules to run AVD playbooks.
Next (optional), set up a Git user and email for the ATD lab environment

Open a terminal window in VS Code View -> Terminal from the menu, and run the following commands:
# Setup your git global config (optional)
git config --global user.email "you@example.com"
git config --global user.name "Your Name"
Set credentials and install any required tools

cd /home/coder/project/labfiles
export LABPASSPHRASE=`cat /home/coder/.config/code-server/config.yaml| grep "password:" | awk '{print $2}'`
ansible-galaxy collection install arista.avd:==4.4.0
export ARISTA_AVD_DIR=$(ansible-galaxy collection list arista.avd --format yaml | head -1 | cut -d: -f1)
pip3 install -r ${ARISTA_AVD_DIR}/arista/avd/requirements.txt
git clone https://github.com/arista-netdevops-community/atd-avd.git
cd atd-avd
Run the playbook to prepare CloudVision for AVD

Execute the following command:

ansible-playbook playbooks/atd-prepare-lab.yml
Check that tasks in CloudVision have been automatically completed

Run playbook to deploy AVD setup

Run the following commands:

ansible-playbook playbooks/atd-fabric-build.yml
ansible-playbook playbooks/atd-fabric-provision.yml
Run pending tasks in CloudVision Portal manually.

Run validation and snapshot playbooks

Run the following commands:

# Run audit playbook to validate the fabric state
ansible-playbook playbooks/atd-validate-states.yml

# Run the atd-snapshot playbook to collect show commands
ansible-playbook playbooks/atd-snapshot.yml
Review generated output.

Step-by-step walkthrough
A complete step-by-step guide is available.

Resources
Arista Ansible AVD Collection
Arista CloudVision Collection
Arista AVD documentation
License
This Project is published under Apache License.










# arista-containerlab

# Install Docker

-Install using docker convenience script

 curl -fsSL https://get.docker.com -o get-docker.sh
 
 sudo sh get-docker.sh

sudo docker run hello-world

# Install cEOS container

Installing Arista cEOS-Lab image

Download the image from www.arista.com > Software Downloads > cEOS-Lab > EOS-4.3x.y > cEOS-lab-4.3x.y.tar.xz
Copy the cEOS-lab-4.3x.y.tar.xz to the host/server/VM.
Ensure Docker is already set up and running.

docker version

Next, use the tar file to import the cEOS-Lab image using the following command

docker import cEOS-lab.tar.xz ceosimage:TAG

Example

docker import cEOS-lab-4.30.4M.tar.xz ceosimage:4.30.4M

Now you should be able to see the Arista cEOS-Lab image.

docker images | egrep "REPO|ceos"

# Install alpine host

Installing the alpine-host image

Build the alpine-host image using the modified Dockerfile
Navigate to alpine_host directory in this repository

├── alpine_host
   ├── Dockerfile
   ├── README.md
   ├── build.sh
   └── entrypoint.sh

Run the build.sh script

./build.sh

NOTE: If permission is denied run 'chmod +x build.sh'

Verify the alpine-host image is created

docker images | egrep "TAG|alpine"



# Install Containerlab


bash -c "$(curl -sL https://get.containerlab.dev)"

# Add images for devices

-Ariista

1. Download the image from www.arista.com > Software Downloads > cEOS-Lab > EOS-4.2x.y > cEOS-lab-4.2x.y.tar.xz
2. upload the image to the EC2 instance (clab)

   scp -i lab-kp-australia.pem cEOS-lab-4.30.4M.tar ubuntu@3.26.54.54:~/



3. Ensure Docker is already set up and running.

   docker version

4. Use the tar file to import the cEOS-Lab image using the following command

    docker import cEOS-lab.tar.xz ceos:TAG

    Example

   sudo docker import cEOS-lab-4.30.4M.tar ceosimage:4.30.4M

5. Now you should be able to see the Arista cEOS-Lab image.

       docker images | egrep "REPO|ceos"

# Deploy Containerlab (based on topology)

-navigate to where the topology.yaml is

-the following command will deploy the lab

sudo containerlab deploy -t topology.yaml

-after deployed you can check the lab like this

sudo containerlab inspect -t topology.yaml

-to access ceos devices use ssh and the ip address (username and password are admin)

ssh admin@172.16.1.101

-to access linux hosts use the following command

sudo docker exec -it clab-avdirb-client1 /bin/sh

