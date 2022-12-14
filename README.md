# Kubernetes-Basic

Theory:

pods: kubernetes containers encapsulation. Can have one ore more containers. Each pod has an IP and container will have a port


commands:

kubectl get nodes >> get nodes

kubectl run nginx-pod --image=nginx:latest >> create nginx pod

kubectl get pods >> get pods

kubectl describe pod nginx-pod >> describe pod

kubectl edit pod nginx-pod > open txt to edit pod

----------------------------------------------------------------------------------------------
PODS
creating .yaml file
Exemple:

apiVersion: v1
kind: Pod
metadata:
  name: pod-2
  labels:
    app: second-pod
spec:
  containers:
    - name: container-pod-2
      image: nginx:latest
      ports:
        - containerPort: 80
----------------------------------------------------------------------------------------------

kubectl apply -f .\first-pod.yaml >> execute .yaml file

kubectl delete pod nginx-pod >> delete pod

kubectl exect -it [file] -- [command (bash)] >> same as docker exec
-------------------------------------------------------------------------------------------------
SVC
creating .yaml file
Exemple:

apiVersion: v1
kind: Service
metadata:
  name: svc-pod-2
spec:
  type: ClusterIP
  selector:
    app: second-pod         ##labels:app: from POD
  ports:
    - port: 9000            ##door svc hear
      targetPort: 80        ##door svc dispatch
---------------------------------------------------------------------------------

apply -f .\svc-pod-2.yaml

kubectl get svc

---------------------------------------------------------------------------------
NodePort

very similar with svc syntax

Exemple:

apiVersion: v1
kind: Service
metadata:
  name: svc-pod-1
spec:
  type: NodePort
  selector:
    app: first-pod
  ports:
    - port: 80
      targetPort: 80
      nodePort: 30000     ##door you can acess in your localhost
---------------------------------------------------------------------------------
apply -f .\svc-pod-1.yaml

kubectl get nodes -o wide

---------------------------------------------------------------------------------
LoadBalancer

ItapiVersion: v1
kind: Service
metadata:
  name: svc-pod-1-loadbalancer
spec:
  type: LoadBalancer
  selector:
    app: first-pod
  ports:
    - port: 80
      targetPort: 80
      nodePort: 30000
---------------------------------------------------------------------------------


