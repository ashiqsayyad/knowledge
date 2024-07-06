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

Throuhput Mode :( spped bytes /sec for transafer)
Elastic : AWS will manage throughput as per workload need 
Others are Provisioned and Bursting

Performace Mode :
General Purpose recommended as has lowest latencty per read/write operation
others are MAX I/O Mode

# LINUX
 sudo su >> sudo will give superprevilages to current user and su will switch user to root
 
 su ssm-user >> switch user to ssm-user
 
 / is the root dir
 
 cat /etc/passwd will display all linux users
 
 777  >> how 7   r w x  >> 1 1 1 = 4+2+1 =7
 
 first 7 is for user which has rwx. second 7 is for group which has rwx  and last 7 is for world which has rwx
 
 750 >> Uer has rwx . Group has rx and world has nothing
 


# POSTGRESQL
\c "employees"     to switch to employees DB

\l    to show all databases in server

\dt to show all tables/relation for a connected database

\d "employees"    to show view/schema for a table employees

\i    to import back up into connected DB
\dn to show schemas

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

