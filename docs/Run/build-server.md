# Build Server

## Bill of Materials

Following are the softwares along with their versions running in Build environment

  Software             |     Version
  ---------------------|-------------------                    
  Gitlab-runner        |  16.2.0
  aws-cli              |  2.15.21
  docker               |  20.10.21
  docker-compose       |  1.29.2
  reposolite           |  3.4.10
  Makedocs             |  1.5.3
  SonarQube            |  9-community
  helm                 |  v3.14.2
  owasp-depscan        |  ghcr.io/owasp-dep-scan/dep-scan
  
# Setup

## Gitlab-Runner
    
### Install

Download
    
```               
sudo curl -L --output /usr/local/bin/gitlab-runner "https://s3.dualstack.us-east-1.amazonaws.com/gitlab-runner-downloads/latest/binaries/gitlab-runner-linux-amd64"
```  

Give it permissions to execute:
	  
```     
sudo chmod +x /usr/local/bin/gitlab-runner
``` 
  
Create a GitLab CI user:
	  
```     
sudo useradd --comment 'gitlab-runner' --create-home gitlab-runner --shell /bin/bash
```  

Install and run as service:

```	  
/usr/bin/gitlab-runner run --working-directory /home/gitlab-runner --config /etc/gitlab-runner/config.toml --service gitlab-runner --user gitlab-runner
		
sudo gitlab-runner start
```  
Advanced configuration:
	  
To change the behavior of GitLab Runner and individual registered runners, modify the config.toml file.

We can find the config.toml file in:
	  
- /etc/gitlab-runner/ on *nix systems when GitLab Runner is executed as root. This directory is also the path for service configuration.
- ~/.gitlab-runner/ on *nix systems when GitLab Runner is executed as non-root.
- ./ on other systems.
	  
GitLab Runner does not require a restart when you change most options. This includes parameters in the [[runners]] section and most parameters in the global section, except for listen_address. If a runner was already registered, you don’t need to register it again.

GitLab Runner checks for configuration modifications every 3 seconds and reloads if necessary. GitLab Runner also reloads the configuration in response to the SIGHUP signal.
	  
	  
### Register Runner
	  
Prerequisites:

Obtain a runner authentication token. You can either:

- Create a shared, group, or project runner.
- Locate the runner authentication token in the config.toml file. Runner authentication tokens have the prefix, glrt-.
		
After registering the runner, the configuration is saved to the config.toml.

To register the runner with a runner authentication token:

Run the register command:
```
sudo gitlab-runner register
```
Enter your GitLab URL

- For runners on GitLab self-managed, use the URL for your GitLab instance. For example, if your project is hosted on gitlab.example.com/yourname/yourproject, your GitLab instance URL is https://gitlab.example.com.
- For runners on GitLab.com, the gitlab-ci coordinator URL is https://gitlab.com. 

Our gitlab-ci coordinator URL is https://gitlabnew.techwave.net
		
Enter the runner authentication token.

Enter a name for the runner.

Enter the type of executor.
	  
To register multiple runners on the same host machine, each with a different configuration, repeat the register command.

	  
	  
	  
### Update the Gitlab-runner
  
1.Stop the service (we need elevated command prompt as before):
```	  
sudo gitlab-runner stop
```
2.Download the binary to replace the GitLab Runner executable. For example:
```	  
sudo curl -L --output /usr/local/bin/gitlab-runner "https://s3.dualstack.us-east-1.amazonaws.com/gitlab-runner-downloads/latest/binaries/gitlab-runner-linux-amd64"
```
3.Give it permissions to execute:
```	  
sudo chmod +x /usr/local/bin/gitlab-runner
```
4.Start the service:
```
sudo gitlab-runner start
```

## aws-cli

The latest AWS CLI version is 2. So download the AWS CLI.
```	  
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
```

Unzip the file using the following command.
```	  
unzip awscliv2.zip
```
	  
Install the AWS CLI using the following command.
```	  
sudo ./aws/install
```  
We can get the AWS CLI version using the below command.
```	  
aws --version
```  
	  
## Docker

The Docker installation package available in the official Ubuntu repository may not be the latest version. To ensure we get the latest version, we’ll install Docker from the official Docker repository. To do that, we’ll add a new package source, add the GPG key from Docker to ensure the downloads are valid, and then install the package.

First, update your existing list of packages:
```	  
sudo apt update
```  
Next, install a few prerequisite packages which let apt use packages over HTTPS:
```	  
sudo apt install apt-transport-https ca-certificates curl software-properties-common
```	  
Then add the GPG key for the official Docker repository to your system:
```	  
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```	  
Add the Docker repository to APT sources:
```	  
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
```	  
This will also update our package database with the Docker packages from the newly added repo.

Make sure to install from the Docker repo instead of the default Ubuntu repo:
```	  
apt-cache policy docker-ce
```  
Finally, install Docker:
```	  
sudo apt install docker-ce
```	  
Docker should now be installed, the daemon started, and the process enabled to start on boot. Check that it’s running:
```	  
sudo systemctl status docker
```

## docker-compose

Prerequisites

- Make sure Docker installed on server
	   
Download the executable
```	   
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```	   
Next, set the correct permissions so that the docker-compose command is executable:
```
sudo chmod +x /usr/local/bin/docker-compose
```	   
To verify that the installation was successful, run:
```	   
docker-compose --version
```

## helm

Use wget to download the latest version of Helm. The download links for all supported architectures are available on the official website.
```
wget https://get.helm.sh/helm-v3.9.3-linux-amd64.tar.gz
```
Next, unpack the Helm file using the Linux tar command:
```
tar xvf helm-v3.9.3-linux-amd64.tar.gz
```
Move the linux-amd64/helm file to the /usr/local/bin directory
```
sudo mv linux-amd64/helm /usr/local/bin
```
Remove the downloaded file using the following command:
```
rm helm-v3.4.1-linux-amd64.tar.gz	
```
Remove the linux-amd64 directory to clean up space by running:
```
rm -rf linux-amd64
```
Finally, verify you have successfully installed Helm by checking the version of the software:
```
helm version
```	

## SonarQube

In order to quickly configure and manage the SonarQube server we will be using the docker-compose file which will set up a sonar instance along with the postgres database.
	  
The docker-compose.yml file is located at the below directory.
	  
/home/build/Fintrust/sonarqube-docker
	  
To set up the sonar server along with postgres just run the below command which will pull in all the specified images for sonar and Postgres and will start up the containers using which we can access our server.
```	  
docker-compose up -d 
```  
Post running the above command, verify if images are downloaded and containers are up and running using the below commands.
```	  
docker images
```	  
```
docker ps
```	  
Connect to our Sonar server using the instance public-ip address along with the port which we had specified: 9000
	  
In our case it is http://172.16.8.234:9090
	  
In order to tear down the complete infra, we can run the below command which will remove all the containers and our server will no longer be accessible.
```	  
docker-compose down
```

## Reposilite

Reposilite (formerly NanoMaven) is lightweight repository manager for Maven artifacts. It is a simple solution to replace managers like Nexus, Archiva or Artifactory.

Prerequisites"
 
- Java 8+
	  
- RAM 12MB+
  
Download the Reposilite from GitHub release page
	  
[reposilite](https://github.com/dzikoysk/reposilite/releases)
	  
Reposilite stores data in current working directory, by default it is a place where we've launched it , below is the path.
	  
/home/build/Fintrust/reposilite
	  
We have a script to start the reposilte which is located at the below path
	  
/home/build/Fintrust/reposilite/start-reposilite.sh
	  
Access it using the below address
	  
http://172.16.8.234:80
	  
	  
	  
### Add reposilite to the init service and let it run under non-root context using Supervisor

Begin by updating package sources and installing Supervisor:
```	  
sudo apt update && sudo apt install supervisor
```  
The supervisor service runs automatically after installation. You can check its status:
```	  
sudo systemctl status supervisor
```	  
A best practice for working with Supervisor is to write a configuration file for every program it will handle.
	  
The per-program configuration files for Supervisor programs are located in the /etc/supervisor/conf.d directory, typically running one program per file and ending in .conf. We’ll create a configuration file for this script, as /etc/supervisor/conf.d/repo.conf:
	  
Make the script executable
```	  
chmod +x /etc/supervisor/conf.d/repo.conf
```	  
Once our configuration file is created and saved, we can inform Supervisor of our new program through the supervisorctl command. First we tell Supervisor to look for any new or changed program configurations in the /etc/supervisor/conf.d directory with:
```	  
sudo supervisorctl reread
```	  
Followed by telling it to enact any changes with:
```	  
sudo supervisorctl update
```	  
Any time we make a change to any program configuration file, running the two previous commands will bring the changes into effect.
	  

## Mkdocs

Makesure pip is installed in system
	 
We have wiki repository available which contains the Dockerfile and makedocs.yml to install and configure the Makedocs.
	 
    Repository URL : https://gitlabnew.techwave.net/fintrust/wiki
	 
Check the below documentation for more information
	 
    https://www.mkdocs.org/getting-started/#getting-started-with-mkdocs
	 
	 
## Depscan
    
OWASP dep-scan is a next-generation security and risk audit tool based on known vulnerabilities, advisories, and license limitations for project dependencies. 
Both local repositories and container images are supported as the input, and the tool is ideal for integration with ASPM/VM platforms and in CI environments.

### Features
     
- Scan most application code - local repos, Linux container images, Kubernetes manifests, and OS - to identify known CVEs with prioritization
- Perform advanced reachability analysis for multiple languages
- Package vulnerability scanning is performed locally and is quite fast. No server is used!
- Generate Software Bill-of-Materials (SBOM) with Vulnerability Disclosure Report (VDR) information
- Generate a Common Security Advisory Framework (CSAF) 2.0 VEX document 
- Perform deep packages risk audit for dependency confusion attacks and maintenance risks 
 
### Vulnerability DataSources

- OSV
- NVD
- GitHub
- NPM
- Linux vuln-list
  
Application vulnerabilities would be reported for all Linux distros and Windows. 

To download the full vulnerability database suitable for scanning OS, invoke dep-scan with `` for the first time. 

 dep-scan would also download the appropriate database based on project type automatically.

### *Usage

 dep-scan is ideal for use during continuous integration (CI) and as a local development tool.

### Scanning projects locally (Python version)
``` 
sudo npm install -g @cyclonedx/cdxgen
pip install owasp-depscan
```

This would install two commands called cdxgen and depscan.

We can invoke the scan command directly with the various options.
```
cd <project to scan>
depscan --src $PWD --reports-dir $PWD/reports
```

### Scanning projects locally (Docker container)

- ghcr.io/owasp-dep-scan/dep-scan container image can be used to perform the scan. 
 
To scan with default settings
```
docker run --rm -v $PWD:/app ghcr.io/owasp-dep-scan/dep-scan --src /app --reports-dir /app/reports
```


### Integration in Fintrust GitLab CI/CD

We integrated the docker setup of depscan in code scan stage of CI/CD using the below command
```
docker run --rm -v $PWD:/app ghcr.io/owasp-dep-scan/dep-scan --src /app --reports-dir /app/reports
```
But with the above setup, the depscan reports are generated with 'root' user, which are unable to clear by the gitlab-runner user for the subsequent build

Able to fix the issue using by passing the user and group while running the docker command
```
docker run --rm -v $PWD:/app --user $(id -u):$(id -g) ghcr.io/owasp-dep-scan/dep-scan --src /app --reports-dir /app/reports 
```
But the above command throws an error, because process inside the container is trying to create a  file at the root level (/.local), but it doesn't have the necessary permissions.

Able to fix the issue by setting up an HOME directory, so that the file will be created in /tmp directory.
```
docker run --rm -v $PWD:/app --user $(id -u):$(id -g) -e HOME=/tmp ghcr.io/owasp-dep-scan/dep-scan --src /app --reports-dir /app/reports 
``` 
To download the depscan reports as an artifacts, written the stage as below.

     artifacts:
        when: always
        name: depscan-reports
        paths:
        - reports 

 
For reference, please visit [depscan](https://github.com/owasp-dep-scan/dep-scan?tab=readme-ov-file#scanning-projects-locally-docker-container)