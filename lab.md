# Lab

Let's explore the operation of a basic service. To begin create a set of three pods running the httpd web server:

`
kubectl create deployment websanog --replicas=4 --image=httpd
`

Display the Deployment and the pods it created:

`kubectl get deploy`

Let's create a simple service to provide a stable interface to our set of pods. Create a Service manifest in yaml and apply it to your cluster:

`vim service.yaml`

Here is file 
`cat service.yaml`

```yaml
apiVersion: v1
kind: Service
metadata:
  name: websanog
spec:
  ports:
  - port: 80
    name: http
  selector:
    app: websanog
```

Run 
`kubectl apply -f service.yaml`

List your service:
`kubectl get service`
and 
`kubectl get endpoints`

Use curl to any IP
`curl 10.114.14.14`

Scale, Scale 

`kubectl scale deployment websanog --replicas=4`


### Using DNS

Most Kubernetes distributions use CoreDNS as the "built-in" DNS service for Kubernetes. The Kubernetes DNS can be used to automatically resolve a service name to it's ClusterIP. Let's try it with our website service!

Create a website Deployment and service:

`kubectl create deployment sanogweb --replicas=3 --image=httpd

and exposing now 

`kubectl expose deployment sanogweb --port=80`

Run a client Pod interactively:

`kubectl run -it client --image busybox`

Now try hitting the website service by name: *sanogweb*

`wget -qO - website`





