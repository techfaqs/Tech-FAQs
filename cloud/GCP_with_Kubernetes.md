Google Cloud Platform with Kubernetes

**gcloud** is the command-line tool for Google Cloud Platform.

List the active account name with this command:

    gcloud auth list

List the project ID with this command:

    gcloud config list project

## Google Kubernetes Engine

In the cloud shell environment, to set the zone:

    gcloud config set compute/zone us-central1-b

Now start up a cluster for use:

    gcloud container clusters create io


Following as per GCP Kubernates tutorial:

    git clone https://github.com/googlecodelabs/orchestrate-with-kubernetes.git
    cd orchestrate-with-kubernetes/kubernetes

#### The easiest way to get started with Kubernetes is to use the `kubectl create` command.

In Kubernetes, all containers run in a pod. Use the `kubectl` get pods command to view the running container

Expose running container using the `kubectl expose`.
You may list services using the `kubectl get services` command

Kubernetes supports an easy to use workflow out of the box using the `kubectl` run and expose commands.

-------

### Kubernates Components -

**Pods** represent and hold a collection of one or more containers.
Generally, if you have multiple containers with a hard dependency on each other, you package the containers inside a single pod.

Pods also have Volumes. Volumes are data disks that live as long as the pods live, and can be used by the containers in that pod.
Pods provide a shared namespace for their contents. Pods also share a network namespace. This means that there is one IP Address per pod.

#### Creating Pods
Pods can be created using pod configuration files. 

Sample config file:

```
  name: monolith
  labels:
    app: monolith
spec:
  containers:
    - name: monolith
      image: kelseyhightower/monolith:1.0.0
      args:
        - "-http=0.0.0.0:80"
        - "-health=0.0.0.0:81"
        - "-secret=secret"
      ports:
        - name: http
          containerPort: 80
        - name: health
          containerPort: 81
      resources:
        limits:
          cpu: 0.2
          memory: "10Mi"
```

Create the monolith pod using kubectl (above sample file is named `monolith.yaml` in pods diretory):

    kubectl create -f pods/monolith.yaml

Use the `kubectl get pods` command to list all pods running in the default namespace.
Use `kubectl describe pods [<pod_name>]` command to get more information.

#### Interacting with Pods

By default, pods are allocated a private IP address and cannot be reached outside of the cluster.
Use the `kubectl port-forward command` to map a local port to a port inside the monolith pod(created above).
To test this, ona cli use: `kubectl port-forward monolith 10080:80`
On another cli use: `curl http://127.0.0.1:10080`

Use the `kubectl logs` command to view the logs for the monolith Pod.

    kubectl logs monolith

To get a stream of the logs happening in real-time:

    kubectl logs -f monolith

### Services
Pods aren't meant to be persistent. They can be stopped or started for many reasons - like failed liveness or readiness checks.
Services use labels to determine what Pods they operate on. 

The level of access a service provides to a set of pods depends on the Service's type. Currently there are three types:

**ClusterIP (internal)** -- the default type means that this Service is only visible inside of the cluster,
**NodePort** gives each node in the cluster an externally accessible IP and
**LoadBalancer** adds a load balancer from the cloud provider which forwards traffic from the service to Nodes within it.

Creating a Service

Create the secure-monolith pods and their configuration data:

    kubectl create secret generic tls-certs --from-file tls/
    kubectl create configmap nginx-proxy-conf --from-file nginx/proxy.conf
    kubectl create -f pods/secure-monolith.yaml

Things to note:

1. There's a selector which is used to automatically find and expose any pods with the labels "app=monolith" and "secure=enabled"
2. Now you have to expose the nodeport here because this is how we'll forward external traffic from port 31000 to nginx (on port 443).
Use the kubectl create command to create the monolith service from the monolith service configuration file (same as earlier):

    kubectl create -f services/monolith.yaml

You're using a port to expose the service. This means that it's possible to have port collisions if another app tries to bind to port 31000 on one of your servers.

Normally, Kubernetes would handle this port assignment.

Use the gcloud compute firewall-rules command to allow traffic to the monolith service on the exposed nodeport:

    gcloud compute firewall-rules create allow-monolith-nodeport --allow=tcp:31000


List all compute instances:

    gcloud compute instances list

#### Adding Labels to Pods

Currently the monolith service does not have endpoints. Use the kubectl get pods command with a label query:

    kubectl get pods -l "app=monolith"

Check if labels have been updated:

    kubectl label pods secure-monolith 'secure=enabled'
    kubectl get pods secure-monolith --show-labels

To view the list of endpoints on the monolith service:

    kubectl describe services monolith | grep Endpoints

#### Deploying Applications with Kubernetes

Deployments are a declarative way to ensure that the number of Pods running is equal to the desired number of Pods, specified by the user.
The main benefit of Deployments is in abstracting away the low level details of managing Pods. Behind the scenes Deployments use Replica Sets to manage starting and stopping the Pods.
If Pods need to be updated or scaled, the Deployment will handle that. Deployment also handles restarting Pods if they happen to go down for some reason.

**Creating Deployments**

We're going to break the monolith app into three separate pieces:

`auth` - Generates JWT tokens for authenticated users.
`hello` - Greet authenticated users.
`frontend` - Routes traffic to the auth and hello services.

Examine the auth deployment configuration file:

    cat deployments/auth.yaml

Create your deployment object:

    kubectl create -f deployments/auth.yaml
    
    
create the auth service:

    kubectl create -f services/auth.yaml

Create and expose the hello deployment:

    kubectl create -f deployments/hello.yaml
    kubectl create -f services/hello.yaml

Create and expose the frontend Deployment:

    kubectl create configmap nginx-frontend-conf --from-file=nginx/frontend.conf
    kubectl create -f deployments/frontend.yaml
    kubectl create -f services/frontend.yaml

Interact with the frontend by grabbing it's External IP and then curling to it:

    kubectl get services frontend
    curl -k https://<EXTERNAL-IP>

