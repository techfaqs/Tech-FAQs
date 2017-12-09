# Docker Installation

### Ubuntu 16.04

1. Add the GPG key for the official Docker repository to the system:

       curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    
2. Add the Docker repository to APT sources:

       sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
    
3. update the package database with the Docker packages from the newly added repo:

       sudo apt-get update
       
4. Make sure you are about to install from the Docker repo instead of the default Ubuntu 16.04 repo:

       apt-cache policy docker-ce
    You should see output similar to the following:
    
        Output of apt-cache policy docker-ce

        docker-ce:
          Installed: (none)
          Candidate: 17.03.1~ce-0~ubuntu-xenial
          Version table:
             17.03.1~ce-0~ubuntu-xenial 500
                500 https://download.docker.com/linux/ubuntu xenial/stable amd64 Packages
             17.03.0~ce-0~ubuntu-xenial 500
                500 https://download.docker.com/linux/ubuntu xenial/stable amd64 Packages


5. Finally, install Docker:

       sudo apt-get install -y docker-ce

6. Installation must have completed now, check that it's running:

       sudo systemctl status docker
       
   Use `q` to come back to terminal
   


