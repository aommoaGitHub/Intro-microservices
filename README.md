# Introduction to Microservices, Docker, and Kubernetes
Reference: https://www.youtube.com/watch?v=1xo-0gCVhTU

## 1 Docker
    $ docker run -p 3000:80 tutum/hello-world
or
    $ docker run -d -p 3000:80 tutum/hello-world
and then go to localhost:3000, you will see a web page hello world

## 2 Kubernetes
    $ minikube start 
    $ kubectl get pods //No resources found.
    $ kubectl get deployments //No resources found.
    $ minikube dashboard
start **minikube** and show the k8s dashboard GUI

    $ kubectl create -f deployment.yml
create **exampleservice** service and **myappdeployment** deployment

    $ kubectl get pods
There are 5 replicas of **myappdeployment** (as set in `deploymet.yml`)
NAME     |      READY |  STATUS   |          RESTARTS |  AGE<br>
--- | --- | --- | --- | ---
myappdeployment-65665fbfcd-9zkfl |  1/1 |    ImagePullBackOff |  0  |        4m27s<br>
myappdeployment-65665fbfcd-fpzzq  | 1/1  |   ImagePullBackOff  | 0  |        4m27s<br>
myappdeployment-65665fbfcd-kg976 |  1/1  |   ImagePullBackOff |  0   |       4m27s<br>
myappdeployment-65665fbfcd-m6zj8 |  1/1  |   ImagePullBackOff  | 0  |      4m27s<br>
myappdeployment-65665fbfcd-s6krp |  1/1 |    ImagePullBackOff  | 0     |     4m27s<br>



    $ kubectl get deployments

NAME | READY  | UP-TO-DATE  | AVAILABLE  | AGE
---- | ---- | ---- | --- | ---
myappdeployment |  5/5  |   5   |         5      |     9m54s

    $ minikube ip
get ip address of k8s cluster such as 192.168.99.100 and go to http://192.168.99.100:30002/ (number of port are set in `deploymet.yml`)

For change the number of replicas `Dashboard -> Deployments -> click : on the most right -> Scale` If it's increasing replicas, pods will be created. If it's decreasing, available pods will be terminated.

Load-Blancing = balance number of clients of each pods (users access the same deployments)


## 3 Containerize a Node App
Reference: https://nodejs.org/en/docs/guides/nodejs-docker-webapp/
