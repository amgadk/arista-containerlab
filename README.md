# Arista Containerlab Labs



## About

This repository is configured to run [`Arista cEOS`](https://containerlab.dev/manual/kinds/ceos/) virtual labs using [`Containerlab`](https://containerlab.dev/) . Example labs can be found in the 'Labs' directory with accompanying details.

<p align="center">
  <img src='docs/imgs/image1.png' alt='Arista cEOS and Containerlab'/>
</p>

To access an ATD topology, please get in touch with your Arista representative.

## Lab topology

Each lab example will include a readme detailing the topology used.

## Getting Started

The following steps need to be followed to successfully run the cEOS labs with Containerlab

### Install Docker


1. Follow the appropriate steps to install docker on your enviornment: https://docs.docker.com/engine/install/

     Example: Install docker using the convenience script on linux

    ```shell
    curl -fsSL https://get.docker.com -o get-docker.sh
    sudo sh get-docker.sh
    sudo sh get-docker.sh
    ```
 
     To confirm that docker is succesfully installed run the following test.

    ```shell
    sudo docker run hello-world
    ```
### Install Containerlab


1. Follow the appropriate steps to install docker on your enviornment: https://containerlab.dev/install/

   Example: Install dContainerlabusing the convenience script on linux

      bash -c "$(curl -sL https://get.containerlab.dev)"

    ```shell
    bash -c "$(curl -sL https://get.containerlab.dev)"
    ```


### Installing Arista cEOS-Lab image

1. Download the cEOS image from www.arista.com

      -Software Downloads
         -cEOS-Lab
            -EOS-4.2x.y
               cEOS-lab-4.2x.y.tar.xz

2. Copy the cEOS-lab-4.2x.y.tar.xz to the host/server/VM.

3. Ensure Docker is already set up and running.

    ```shell
    docker version
    ```

4. Use the tar file to import the cEOS image to create a docker image ready for use

   ```shell
   docker import cEOS-lab-4.30.4M.tar.xz ceos:4.30.4M
   ```

    NOTE 1: make sure the docker import command is referncing the exact version you downloaded 

    NOTE 2: The tag is important, make sure to add "ceos" and the version 

5. Confirm that the cEOS image is ready using the following command

    ```shell
    docker images | egrep "REPO|ceos"
    ```

### Deploy topology using Containerlab

1. Navigate to where the topology.yaml is

2. The following command will deploy the lab

    ```shell
sudo containerlab deploy -t topology.yaml
    ```
-after deployed you can check the lab like this

sudo containerlab inspect -t topology.yaml

-to access ceos devices use ssh and the ip address (username and password are admin)

ssh admin@172.16.1.101

-to access linux hosts use the following command

sudo docker exec -it clab-avdirb-client1 /bin/sh


## Resources

- [Arista Ansible AVD Collection](https://github.com/aristanetworks/ansible-avd)
- [Arista CloudVision Collection](https://github.com/aristanetworks/ansible-cvp)
- [Arista AVD documentation](https://avd.arista.com)

## License

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

