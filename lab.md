# Lab

Let's explore the operation of a basic service. To begin create a set of three pods running the httpd web server:

`
kubectl create deployment website --replicas=3 --image=httpd
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
  name: website
spec:
  ports:
  - port: 80
    name: http
  selector:
    app: website
```

Run 
`kubectl apply -f service.yaml`
