# Knowledge
Useful links for tech and non tech

# JAVA
Exception in thread "main" java.lang.UnsupportedClassVersionError: org/springframework/boot/SpringApplication has been compiled by a more recent version of the Java Runtime (class file version 61.0), this version of the Java Runtime only recognizes class file versions up to 59.0

Resolution: 
https://stackoverflow.com/questions/12252123/build-path-entry-is-missing-error-when-trying-to-create-a-new-project-in-eclip
1) I have installed jdk 22 on my machine and then changed JAVA_HOME and Path %JAVA_HOME%/bin variable
2) Added new JRE in eclipse Window>>Preferences>>Java>>Installed JRES .. Remove old JRE
3) Now right click Project>>Java Build Path>>Libraries>> Edit the existing JRE to Installed JRE
4) mvn clean install
   


https://www.baeldung.com/java-lang-unsupportedclassversion
 major version numbers map to Java versions:

45 = Java 1.1
46 = Java 1.2
47 = Java 1.3
48 = Java 1.4
49 = Java 5
50 = Java 6
51 = Java 7
52 = Java 8
53 = Java 9
54 = Java 10
55 = Java 11
56 = Java 12
57 = Java 13
58 = Java 14
59 = Java 15
60 = Java 16
61 = Java 17
62 = Java 18
63 = Java 19
64 = Java 20
65 = Java 21
66 = Java 22

# AZURE

azure cloud shell

az version

az login

kubectl version

**Install NGINX on Azure Linux VM**

sudo su

apt-get -y update

apt-get -y install nginx

echo " Welcome to nginx $(whoami) $(hostnamme)" > /var/www/html/index.html

**Go to browser and hit http://<public ip of VM> . It will display above message**

**Custom data & cloud init**

you can automate above steps while creating Azure VM

While creating VM, go to **Advanced** and paste below script in Custom data box

#!/bin/sh

sudo su

apt-get -y update

apt-get -y install nginx

echo " Welcome to nginx $(whoami) $(hostnamme)" > /var/www/html/index.html


# AWS

EFS article :
https://aws.amazon.com/blogs/storage/persistent-storage-for-kubernetes/

EFS is the remote File system. EFS follows NFS protocol(NFSv4.1 & 4.0) for connection. EFS can be mounted on local directory in any machine for example EC2 machines. Once EFS is mounted, then the files created in the local directory will be synced to EFS volume.
IMP Terms : EFS is elastic(grow and shrink automatically) , serverless fully managed service(avoid complexity of deploying,patching & maintaining complex file system configurations) ,highly durable , scalable(can grow in size to petabytes) and highly available
IMP Settings:
Availability Zone : 
Regional :store data redundantly across AZ in same region. Recommended setting for prodcution like use cases
One 
: store data in single zone 

# Throuhput Mode :( speed bytes /sec for transfer)
Elastic : AWS will manage throughput as per workload need.
Others are Provisioned and Bursting

# Performace Mode :
General Purpose: recommended as has lowest latencty per read/write operation
others are MAX I/O Modes

# SHARING EFS to MULTIPLE Applcations via ACCESS Points
1) Each application will create its own access point giving different "Root directory path". Root directory path is mandatory to give . Rest params like USER ID, GROUP ID ,Owner USER ID, OWNER Group ID,Acess point permissions(0755), you can give like 1000, 1000 for all feilds . If you dont give USER ID, GROUP ID ,Owner USER ID, OWNER Group ID, then you will get "Access denied by Server while mounting 127.0.0.1 error" while mounting access point on second machine. Seconday group IDs can be optional
   
   For example, app 1 will have accesspint app1accpoint with root dir path as /data/app1
   
   For example, app 2 will have accesspint app2accpoint with root dir path as /data/app2

    So remote server hosting EFS will have two dirs app1 and app2 for two applications

# Load balancer 
 1) Route 53 >> A record pointing to Application LB in public subnets with internet facing scheme >> EC2 machines in private subnets >> Works perfectly fine
 2) Route 53 >> A record pointing Application LB with internal scheme >>> It wont work as internal LB wont have publically resolvable ip
   
   

# HELM 

where helm charts files are stored locally after helm repo add   : https://stackoverflow.com/questions/62924278/where-are-helm-charts-stored-locally : https://helm.sh/docs/helm/helm/

do helm env .. it will show all directories

HELM_BIN="helm"
HELM_CACHE_HOME="/Users/username/Library/Caches/helm"
HELM_CONFIG_HOME="/Users/username/Library/Preferences/helm"
HELM_DATA_HOME="/Users/username/Library/helm"
HELM_DEBUG="false"
HELM_KUBEAPISERVER=""
HELM_KUBEASGROUPS=""
HELM_KUBEASUSER=""
HELM_KUBECAFILE=""
HELM_KUBECONTEXT=""
HELM_KUBETOKEN=""
HELM_MAX_HISTORY="10"
HELM_NAMESPACE="default"
HELM_PLUGINS="/Users/username/Library/helm/plugins"
HELM_REGISTRY_CONFIG="/Users/username/Library/Preferences/helm/registry.json"
HELM_REPOSITORY_CACHE="/Users/username/Library/Caches/helm/repository"
HELM_REPOSITORY_CONFIG="/Users/username/Library/Preferences/helm/repositories.yaml"

# You can debug by using helm template to see the fully rendered template:
helm template . --debug
helm list -A
helm install <my-release> . -n <ns>
helm uninstall <my-release> . -n <ns>



# LINUX
 sudo su >> sudo will give superprevilages to current user and su will switch user to root
 
 su ssm-user >> switch user to ssm-user
 
 / is the root dir
 
 cat /etc/passwd will display all linux users
 
 777  >> how 7   r w x  >> 1 1 1 = 4+2+1 =7
 
 first 7 is for user which has rwx. second 7 is for group which has rwx  and last 7 is for world which has rwx
 
 750 >> Uer has rwx . Group has rx and world has nothing

 root@7174e15d8f54:/# **whoami**
 
root

root@7174e15d8f54:/# **id**

uid=0(root) gid=0(root) groups=0(root)

root@7174e15d8f54:/usr/sbin# **find** / -type f -name "*.html"

/usr/share/nginx/html/50x.html

/usr/share/nginx/html/index.html


# POSTGRESQL
\c "employees"     to switch to employees DB

\l    to show all databases in server

\dt to show all tables/relation for a connected database

\d "employees"    to show view/schema for a table employees

\i    to import back up into connected DB
\dn to show schemas

**BY default, indexes are created for primary key and unique values**
employees=#  Select * from pg_indexes where tablename = 'employees';

 schemaname | tablename |          indexname           | tablespace |                                           indexdef

------------+-----------+------------------------------+------------+----------------------------------------------------------------------------------------------
 public     | employees | employees_pkey               |            | CREATE UNIQUE INDEX employees_pkey ON public.employees USING btree (empid)
 public     | employees | uk_j9xgmd0ya5jmus09o0b8pqrpb |            | CREATE UNIQUE INDEX uk_j9xgmd0ya5jmus09o0b8pqrpb ON public.employees USING btree (email)
 public     | employees | uk_968bmvh68d9mn4n1tomcml6d8 |            | CREATE UNIQUE INDEX uk_968bmvh68d9mn4n1tomcml6d8 ON public.employees USING btree (mobile_no)
(3 rows)

CREATE UNIQUE INDEX idx_first_name ON public.employees USING btree (first_name);

DROP INDEX idx_first_name;

To know indepth about index, refer https://github.com/ashiqsayyad/employeesystem/blob/main/README.md


# Kubernetes K8s 
# Minikube
https://minikube.sigs.k8s.io/docs/tutorials/multi_node/

minikube start --nodes 3 -p multinode-demo --cni calico

PS C:\Users\Lenovo> minikube status -p multinode-demo

multinode-demo
type: Control Plane
host: Running
kubelet: Running
apiserver: Running
kubeconfig: Configured

multinode-demo-m02
type: Worker
host: Running
kubelet: Running

multinode-demo-m03
type: Worker
host: Running
kubelet: Running

kubectl port-forward svc/url-shortner-ask-url-shortner <local-machine-port where you want port to be forwarded>:<service-port where svc is running> -n ask-url-shortner

kubectl port-forward svc/url-shortner-ask-url-shortner 8089:8080 -n ask-url-shortner  

8080 is the port where my kubernetes svc is running and 8089 is the port where local port forwarding will happen http://localhost:8089/hello


==========================================================================================
PS C:\Users\Lenovo> minikube start --nodes 3 -p multinode-demo --cni calico
W0504 00:04:40.579822   16316 main.go:291] Unable to resolve the current Docker CLI context "default": context "default": context not found: open C:\Users\Lenovo\.docker\contexts\meta\37a8eec1ce19687d132fe29051dca629d164e2c4958ba141d5f4133a33f0688f\meta.json: The system cannot find the path specified.
* minikube v1.33.0 on Microsoft Windows 11 Home Single Language 10.0.22631.3447 Build 22631.3447
* Kubernetes 1.30.0 is now available. If you would like to upgrade, specify: --kubernetes-version=v1.30.0
* Using the docker driver based on existing profile
! You cannot change the number of nodes for an existing minikube cluster. Please use 'minikube node add' to add nodes to an existing cluster.
* Starting "minikube" primary control-plane node in "minikube" cluster
* Pulling base image v0.0.43 ...
* Restarting existing docker container for "minikube" ...
* Preparing Kubernetes v1.25.2 on Docker 20.10.18 ...
! kubeadm certificates have expired. Generating new ones...
Bad local forwarding specification '0:localhost:8443'
* Configuring Calico (Container Networking Interface) ...
* Verifying Kubernetes components...
  - Using image gcr.io/k8s-minikube/storage-provisioner:v5
* Enabled addons: storage-provisioner, default-storageclass

! C:\Program Files\Docker\Docker\resources\bin\kubectl.exe is version 1.29.1, which may have incompatibilities with Kubernetes 1.25.2.
  - Want kubectl v1.25.2? Try 'minikube kubectl -- get pods -A'
* Done! kubectl is now configured to use "minikube" cluster and "default" namespace by default
* =========================================================================================================================================
# For Resolution of ISSUE
>> Unable to resolve the current Docker CLI context "default": context "default": context not found: open C:\Users\Lenovo\.docker\contexts\meta\37a8eec1ce19687d132fe29051dca629d164e2c4958ba141d5f4133a33f0688f\meta.json: The system cannot find the path specified.

PS C:\Users\Lenovo> docker context show
default
PS C:\Users\Lenovo> docker context use default
default
Current context is now "default"
======================================================================================================================================================

