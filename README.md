###  Project: 
 
  * Automate Docker Compose deployments with Ansible and AWS dynamic inventory. 
### Technologiesused: 
  * Ansible, Terraform, AWS


### Project Description:
  *  Create three  EC2 Instance with Terraform and assign public DNS to to EC2 Instance.

#### Written Ansible Playbook that installs necessary technologies like Docker and Docker Compose, copies docker-compose file to the server and starts the Docker containers configured inside the docker- compose file

1. Install Pip3, Docker, and Docker-Compose

   * Target hosts: ```docker_server```.

   * This section installs Python 3 (pip3), Docker, and Docker-Compose on the  hosts.

   * Ensure Pip3 and Docker Installed

      * Uses the ```yum``` module to install the 'python3-pip' and 'docker' packages.
      * Updates the package cache and ensures that these packages are installed.
   * Install Docker-Compose

      * Downloads the Docker-Compose binary from the official GitHub releases based on the host's architecture.
      * Sets the binary to be executable and places it in '/usr/local/bin'.
   * Start Docker Daemon

      * Uses the ```systemd``` module to ensure the Docker service is started.
2. Install Docker Python Modules

   * Target hosts: ```docker_server```.

   * This section installs Docker-related Python modules using the ```ansible.builtin.pip``` module.

   * Install Docker Python Module

      * Installs the 'docker' and 'docker-compose' Python modules.
3. Add ec2-user to Docker Group

   * Target hosts: ```docker-server```.

   * This section adds the 'ec2-user' to the 'docker' group, granting them access to Docker.

   * ```Add ec2-user to Docker Group``` 

     * Uses the ```user``` module to add the 'ec2-user' to the 'docker' group, ensuring that the 'append' option is set to 'yes'.
     * Reconnects to the server session for the changes to take effect.
4. Start Docker Container

   * Target hosts: ```docker_server```.

   * Uses variables from a file named ```project-vars``` to set the dockerhub password as variable.

   * ```Copy Docker Compose File```

     * Copies a Docker Compose file from the source directory to the 'ec2-user' home directory.
   * ```Docker Login```

     * Uses the ```community.docker.docker_login``` module to log in to the Docker registry using the specified username and password.
   * ```Start Container from Compose```

     * Uses the ```docker_compose``` module to start a Docker container using the Docker Compose file.
     * The ```project_src``` parameter specifies the location of the Docker Compose file.
  
* Ansible AWS EC2 Plugin to dynamically sets inventory of EC2 servers that Ansible should manage, instead of hard-coding server addresses in Ansible inventory file

  ### plugin configuration for aws_ec2

  1. ```Plugin```: Specifies that the plugin to be used is the ```aws_ec2``` plugin. This plugin interacts with the AWS API to discover EC2 instances.
  2. Enable plugins in ansible.cfg for  aws_ec2 as ```Enable_plugins= aws_ec2``` 

2. ```Regions```: Lists the AWS regions where the dynamic inventory should look for EC2 instances.  it specifies "eu-central-1". 

3. ```Keyed Groups```: This section configures groups that are created based on specific attributes of EC2 instances. The purpose of these groups is to organize instances in the inventory.

   * ```Tags```: Instances are grouped based on their tags. A group is created for each unique tag key with the prefix "tag."

   * ```Instance Type```: Instances are grouped based on their instance type. A group is created for each unique instance type with the prefix "instance_type."



### Execute the ansible-playbook

<img src="https://github.com/Rajib-Mardi/ansible-projects/assets/96679708/1e027a04-bdb3-4d13-85dd-1fc77ae5bf2d" width="700">
<img src="https://github.com/Rajib-Mardi/ansible-projects/assets/96679708/f8f5cd03-22e3-4dd5-b4a3-991a0092dbc1" width="700">
<img src="https://github.com/Rajib-Mardi/ansible-projects/assets/96679708/35d8cb4a-d792-4779-a19b-6e23086827e6" width="700">


<img src="https://github.com/Rajib-Mardi/ansible-projects/assets/96679708/029d0f7d-c094-4117-8a34-6a542456920c" width="700">

<img src="https://github.com/Rajib-Mardi/ansible-projects/assets/96679708/9e6fe2ac-0a3f-4eb7-8063-46b70ca2fc26" width="800">

