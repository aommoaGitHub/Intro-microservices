# Introduction to Microservices, Docker, and Kubernetes
Reference: https://www.youtube.com/watch?v=1xo-0gCVhTU

## 1) Docker
    $ docker run -p 3000:80 tutum/hello-world
or

    $ docker run -d -p 3000:80 tutum/hello-world
and then go to localhost:3000, you will see a web page hello world

## 2) Kubernetes
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
hello-world-858c579f6b-54lkv |  1/1 |    Running |  0  |        4m27s<br>
hello-world-858c579f6b-5lnwz  | 1/1  | Running  | 0  |        4m27s<br>
hello-world-858c579f6b-5tv7c |  1/1  | Running |  0   |       4m27s<br>
hello-world-858c579f6b-9tjq5 |  1/1  | Running | 0  |      4m27s<br>
hello-world-858c579f6b-b66qq |  1/1 |  Running  | 0     |     4m27s<br>



    $ kubectl get deployments

NAME | READY  | UP-TO-DATE  | AVAILABLE  | AGE
---- | ---- | ---- | --- | ---
hello-world |  5/5  |   5   |         5      |     9m54s

    $ minikube ip
get ip address of kubernetes cluster such as 192.168.99.100 and go to http://192.168.99.100:30002/ (number of port are set in `deploymet.yml`)

For change the number of replicas `Dashboard -> Deployments -> click : on the most right -> Scale` If it's increasing replicas, pods will be created. If it's decreasing, available pods will be terminated.

Load-Blancing = balance number of clients of each pods (users access the same deployments)


# Containerize a Node App
Reference: https://nodejs.org/en/docs/guides/nodejs-docker-webapp/

1 ) install dependencies

    $ npm i express --save

2 ) create deployment-node-app.yml, index.js, Dockerfile, and .dockerignore following the reference

3 ) build and run container

    $ docker build -t vittunyuta/k8snodeapp:v1.0.0 .
    $ docker run -p 8081:8080 -d vittunyuta/k8snodeapp:v1.0.0

4 ) push to docker hub (login docker first). In this case username is vittunyuta, repository name is k8snodeapp, and tagname is v1.0.0

    $ docker push <username>/<repo_name>:<tagname>

5 ) create a deployment and pods on kubernetes

    $ kubectl create -f deployment-node-app.yml

6 ) get ip address such as 192.168.99.100

    $ minikube ip

7 ) go `192.168.99.100:30005`
