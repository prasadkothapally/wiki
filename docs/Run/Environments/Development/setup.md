# Setup


## **Setup of Dev Server**

Following are the softwares along with their versions running in the DEV 

  Software             |     Version
  ---------------------|------------------- 
  Docker               |     24.0.4
  minikube             |     v1.30.1
  kubectl              |     v1.27.3
  haproxy              |     2.0.31-0ubuntu0.3
  caddy                |     v2.6.4
  kestra               |     kestra/kestra:latest-full
  openobserve          |     v0.7.0

### Docker

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

### Minikube

Minikube is an open source tool that allows you to set up a single-node Kubernetes cluster on our local machine. The cluster is run inside a virtual machine and includes Docker, allowing us to run containers inside the node.

This is an excellent way to test in a Kubernetes environment locally, without using up too much resources
	  
Prereuisites:
	  
- 2 CPUs or more
- 2GB of free memory
- 20GB of free disk space
- Internet connection
- Container or virtual machine manager, such as: Docker, QEMU, Hyperkit, Hyper-V, KVM, Parallels, Podman, VirtualBox, or VMware Fusion/Workstation
		
1.Installation
	  
To install the latest minikube stable release on x86-64 Linux using binary download:
```	  
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
```	  
Next, give the file executive permission using the chmod command:
```	  
sudo chmod 755 /usr/local/bin/minikube
```	  
2.Start minikube cluster
	  
From a terminal with administrator access (but not logged in as root), run:
```	  
minikube start
```
3.Manage minikube cluster
	  
Pause Kubernetes without impacting deployed applications:
```	  
minikube pause
```
Unpause a paused instance:
```	  
minikube unpause
```   
Halt the cluster:
```	  
minikube stop
``` 
Browse the catalog of easily installed Kubernetes services
```	  
minikube addons list
```
The below list of addons are enabled on our DEV minikube

- default-storageclass

- ingress

- ingress-dns

- metrics-server

- storage-provisioner

To login into the minikube:
```
minikube ssh
```
To get the IP of minikube:
```
minikube ip
```


### Kubectl

To deploy and manage clusters, we need to install kubectl, the official command line tool for Kubernetes.
	 
1.Download kubectl with the following command
```	 
$ curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl
```	 
2.Make the binary executable by typing
```	 
chmod +x ./kubectl
```	 
3.Then, move the binary into your path with the command:
```	 
sudo mv ./kubectl /usr/local/bin/kubectl
```	 
4.Verify the installation by checking the version of your kubectl instance:
```	 
kubectl version --short
```	 

### HAPROXY

HAProxy, which stands for High Availability Proxy, is a popular open source software TCP/HTTP Load Balancer and proxying solution which can be run on Linux, macOS, and FreeBSD.
	   
Its most common use is to improve the performance and reliability of a server environment by distributing the workload across multiple servers (e.g. web, application, database).

Installation
```
sudo apt install --no-install-recommends software-properties-common

sudo add-apt-repository ppa:vbernat/haproxy-2.4 -y
```
The first command installs the software-properties-common package which helps you manage any PPAs you install. It’s probably already installed, but running it again ensures that it’s available. 
	 
The second command puts the PPA into the list of software sources.
	 
We’re now ready to install the very latest HAProxy:
```	 
sudo apt install haproxy=2.3.\*
``` 
To check the haproxy version 
```	 
haproxy -v
``` 
acc-api, acc-bo, acc-analytics, mfusessionprovider modules are exposed publicly via HAProxy
	 
We can find the routes configuration at /etc/haproxy/haproxy.cfg
```
frontend apiproxy
  mode tcp
  bind :18080
  default_backend k8s_api
backend k8s_api
  mode tcp
  balance leastconn
  server s4 192.168.49.2:30007
frontend boproxy
  mode tcp
  bind :18081
  default_backend k8s_bo
backend k8s_bo
  mode tcp
  balance leastconn
  server s5 192.168.49.2:30008
```

	 
To check the status of haproxy, run 
```	 
systemctl status haproxy
```	 
After the routes configuration in /etc/haproxy/haproxy.cfg , run the below command so that new routes will be available to access.
```	 
systemctl reload haproxy 
```

### Caddy

Caddy is a powerful, extensible platform to serve your sites, services, and apps
	 
Most people use Caddy as a web server or proxy, but at its core, Caddy is a server of servers. With the requisite modules, it can take on the role of any long-running process.
	 
Configuration is both dynamic and exportable with Caddy's API. Although no config files required, you can still use them; most people's favorite way of configuring Caddy is using the Caddyfile. The format of the config document takes many forms with config adapters, but Caddy's native config language is JSON.
	 
Caddy compiles for all major platforms and has no runtime dependencies.
	 
1.Installation
	  
Download Caddy from the following releases pages , choose the version and system compatible one.

[caddy](https://github.com/caddyserver/caddy/releases)
	 
2.The Caddyfile
	 
The Caddyfile is a convenient Caddy configuration format for humans. 

It is most people's favorite way to use Caddy because it is easy to write, easy to understand, and expressive enough for most use cases.
	 
We have Caddyfile available at below path in DEV environment
/home/laxma/software 
	 
3.Caddy has a standard unix-like command line interface. Basic usage is:
```	 
caddy start - Starts the Caddy process in the background
	 
caddy run - Starts the Caddy process in the foreground
	 
caddy stop - Stops the running Caddy process
	 
caddy upgrade - Upgrades Caddy to the latest release
	 
caddy file-server - A simple but production-ready file server
	 
caddy reload - Changes the config of the running Caddy process
```
	 
For more information, please check the below documentation
	 
[Caddy documentation](https://caddyserver.com/docs/command-line)
	 
### Kestra

The chart repository is available under helm.kestra.io.
	 
The source code of the charts can be found in the kestra-io/helm-charts repository.
	 
1.Install the Chart
```	 
helm repo add kestra https://helm.kestra.io/
```	 
By default, the chart will only deploy one Kestra standalone service with only one replica. This means that all Kestra server components will be deployed within a single pod.
	 
2.Modify the kestra configuration to use the local storage
```	 
	 configuration:
	   kestra:
	     storage:
           type: local
           local:
             base-path: /tmp/kestra/storage/
```		 
3.Disable the default postgres deployment available in helm chart, and add our own datasource.
```	
	configuration:
	  datasources:
        postgres:
          url: jdbc:postgresql://172.16.22.16:5432/accounting?currentSchema=kestra
          driverClassName: org.postgresql.Driver
          username: ****
          password: ****
		  
	#### Postgresql
    postgresql:
      enabled: false
      auth:
        database: kestra
        username: kestra
        password: kestra
      primary:
        persistence:
          enabled: false
          size: 8Gi
```
		  
4.Disable all other deployments and enable only standalone deployment.
```	
    deployments:
      webserver:
        enabled: false
		kind: Deployment
	  executor:
        enabled: false
        kind: Deployment
        command: "server executor"
      indexer:
        enabled: false
        kind: Deployment
        command: "server indexer"
      scheduler:
        enabled: false
        kind: Deployment
        command: "server scheduler"
      worker:
        enabled: false
        kind: Deployment
        command: "server worker --thread={{ .Values.deployments.worker.workerThreads }}"
        terminationGracePeriodSeconds: 60
        workerThreads: 128
      standalone:
        enabled: true
        kind: Deployment
        command: "server standalone --worker-thread={{ .Values.deployments.standalone.workerThreads }}"
        terminationGracePeriodSeconds: 60
        workerThreads: 128
```
5.Install the helm chart using the below command.
```	
helm install kestra . -n kestra -f values.yaml
```	
6.Check the deployment, service and configmap using the below command.
```	
kubectl get deployment -n kestra
kubectl get svc -n kestra
kubectl get cm -n kestra
```	
7.Create a temporary tunnel by port-forwarding the kestra-service.
```	
kubectl -n kestra port-forward --address 0.0.0.0 svc/kestra-service 8080:8080
```	
8.Access the kestra at the below address
	 
	http://172.16.22.22:8080/
	

### Openobserve

OpenObserve is a cloud native observability platform (Logs, Metrics, Traces) for real life log data, significantly lower operational cost and ease of use. 

It can scale to petabytes of data, is highly performant and allows you to sleep better at night 😀. 

Check the more information at [Openobserve documentation](https://openobserve.ai/docs/)
	
Binaries can be downloaded from releases page for appropriate platform. [Openobserve](https://github.com/openobserve/openobserve/releases)
	
Created a script to run the "openobserve" executable which is available at below path

    /home/laxma/openobserve/openobserve_start.sh
	
Now point your browser to http://172.16.22.22:5080 and login
	
#### Configure the fluent-bit for the logs aggregation

Fluentbit is a lightweight and open-source log forwarder for Kubernetes. It is designed to be fast and efficient.
	
It is also a part of the Fluentd ecosystem, which is a popular open-source log collector.
	
It works by tailing the files that contain the logs you want to forward. It then parses the logs and sends them to the destination you specify. 
	
It can also enrich your logs with additional metadata, such as the Kubernetes pod name, pod ID, and container name
	
1.Install Fluentbit
```	
helm repo add fluent https://fluent.github.io/helm-charts

helm repo update

helm upgrade --install fluent-bit fluent/fluent-bit --namespace fluent-bit --create-namespace
```
	
This will install FluentBit as a daemonset(A daemonset ensures that one and only one pod runs on every node of the cluster.) and create the necessary service accounts, roles, and configuration needed to run FluentBit on cluster. 

Default values in the chart will enrich the logs with additional metadata, such as the Kubernetes pod name, pod ID, and container name.
	
2.Configure FluentBit to Forward Logs to OpenObserve
	
Once FluentBit is installed and running on your Kubernetes cluster, the next step is to configure FluentBit to send logs to OpenObserve

OpenObserve supports an HTTP endpoint, and FluentBit has an HTTP output plugin which we can use for this purpose.
	
To do this, we'll need to modify the FluentBit ConfigMap, specifically the OUTPUT section, to include the HTTP output plugin and the OpenObserve endpoint details.

Head over to OpenObserve UI > Ingestion > Logs > Fluentbit and copy the configuration from there.
	
Get the default configmap for fluentbit that is part of the installation.
```
kubectl -n fluent-bit get configmap fluent-bit -o yaml > fluent-bit.yaml
```	
This will create a file called fluent-bit.yaml in current directory. Open this file in editor and we will find two sections, for OUTPUT. 

Paste the configuration that we got from OpenObserve UI in the fluent-bit.yaml file replacing 2 existing OUTPUT sections.
	
Check the manifest of fluentbit configmap at /home/laxma/openobserve/fluent-bit.yaml
	
3.Apply Changes and Start Forwarding Logs
	
Once ave updated the FluentBit ConfigMap, can apply the changes by running:
```	
kubectl apply -f fluent-bit.yaml
```
	
One last step is to restart the FluentBit pods so that they pick up the new configuration
```	
kubectl delete pods -n fluent-bit -l app.kubernetes.io/name=fluent-bit
```	
FluentBit should now begin to forward logs from cluster to the OpenObserve endpoint specified. We can then use OpenObserve UI to view and analyze the logs.
	
Reference doc:[fluent-bit](https://openobserve.ai/blog/how-to-send-kubernetes-logs-using-fluent-bit/)
	
	
### Shell Auto-Completion for Kubectl
   
kubectl provides autocompletion support for Bash, Zsh, Fish, and PowerShell, which can saves a lot of typing.
	
1.Install bash-completion
```	
apt-get install bash-completion
```	
The above commands create /usr/share/bash-completion/bash_completion, which is the main script of bash-completion.
	
Depending on our package manager, we have to manually source this file in our ~/.bashrc file.
```	
source /usr/share/bash-completion/bash_completion
```	
2.Enable kubectl autocompletion
	
Now we need to ensure that the kubectl completion script gets sourced in all our shell sessions.
```	
echo 'source <(kubectl completion bash)' >>~/.bashrc
```	
After reloading our shell, kubectl autocompletion should be working. To enable bash autocompletion in current session of shell, source the bashrc file:
```	
source ~/.bashrc
```


## **Setup of Dev Replication Server**

Following are the softwares along with their versions running in Build environment

  Software             |     Version
  ---------------------|-------------------
  Docker               |   24.0.7
  docker-compose       |   1.29.2
  
### Docker

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
	  
### docker-compose

Prerequisites:

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

We are running 3 docker containers along with data volumes in this machine. Check them using below command.
```   
docker ps
```  
We are running PostgresDB, MongoDB and RabbitMQ.

Respective docker-compose files for these DBs and message brokers are available at:
 
    /home/devreplica/Fintrust/Postgress
	  /home/devreplica/Fintrust/Mongo
	  /home/devreplica/Fintrust/RabbitMQ