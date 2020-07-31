# Kubernetes

# Connecting two pods from different namespace 
lets consider the two tier apllication where wordpress works as front and mysql as backend
```
$ git glone https://github.com/ajinkyaingole30/kube-pod-connect-of-diff-namespace.git
```
Create a basic Kubernetes Service for a HTTP server
```
$ kubectl create -f kube-dns.yml
```
To check service 
```
$ kubectl get svc 
```
create namespaces
```
$ kubectl create ns mysql-example

$ kubectl create ns wordpress-example
```
create our Mysql deployment resource
```
$ kubectl create -f mysql-deployment.yml
```
To allow any other container to speak to our database pod we need to expose it to a service resource
```
$ kubectl create -f mysql-service.yml
```
create our Wordpress container and configure it to talk to our Mysql pod
```
$ kubectl create -f wordpress-deployment.yml
```
check if pods are runing or not
```
$ kubectl get pod -n mysql-example

$ kubectl get pod -n wordpress-example
```
expose wordpress service
```
$ kubectl create -f wordpress-nodeport.yml

$ kubectl get svc  -n wordpress-example
```

Now you can finish the installation of your Wordpress application using the following details :
```
Database name : wordpress as defined in the mysqls yml file

User name : root

Password : redhat as defined in yml too

Database host : mysql.mysql-example.svc.cluster.local
```
