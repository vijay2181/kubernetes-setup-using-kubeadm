Setup of Single Node control Plane using KUBEADM:
-------------------------------------------------
- Take 3 ubuntu machines
- 1 will be master
- 2 will be worker nodes
  
![image](https://github.com/vijay2181/vijay-private/assets/66196388/4d043bda-5c58-43f2-8c64-6b16522df073)

```
 - allow 22 port from anywhere
 - allow all other port traffic inside of default vpc only
 - do this in all 3 machines
 - if not you can select ports to be allowed by using below document

 https://kubernetes.io/docs/reference/networking/ports-and-protocols/
```
  
![image](https://github.com/vijay2181/vijay-private/assets/66196388/1ffce110-052c-4528-8aa2-2c72211b6d39)

- or setup like below on master using master-sg

![image](https://github.com/vijay2181/vijay-private/assets/66196388/5be9cb07-1aeb-4c5a-9990-2b3c9e1f7159)


- on workers using worker-sg


![image](https://github.com/vijay2181/vijay-private/assets/66196388/f8c956a2-a875-42dc-877e-84734d1a7e1f)




![image](https://github.com/vijay2181/vijay-private/assets/66196388/86e540c1-9c5d-47dd-aa1e-75fe9e5fc6bc)




- after installation is setup, then use below document to configure kubeadm on machines

  ```
  https://www.linuxtechi.com/install-kubernetes-on-ubuntu-22-04/
  ```


commands:
---------
```
kubectl version  
kubectl cluster-info
kubeadm version
kubectl get nodes
kubectl get pods -n kube-system

curl -v telnet://k8smaster.example.net:6443
ssh -v -p 6443 k8smaster.example.net

>kubeadm token list
if no results it means token expired
Genrate new token like below
>kubeadm token create
if you want to join workers with existing token then
>kubeadm token create --print-join-command
you will get join command with token, then execute the command on worker nodes

>kubectl cluster-info dump
It dumps relevant information regarding cluster for debugging and diagnosis

NAMESPACE:
----------
kubectl get namespaces
kubectl get ns

kubectl get all                       -- get all resources(pods,services,daemonsets,deployments,replicaset) in the namespace
kubectl get all --namespace default   -- get all resources/objects in the deafult namespace

kubectl get all --namespace kube-system
kubectl get all --ns kube-system

 
kubectl api-resources    --- SHOWS ALL API CALLS INSIDE API-SERVER

kubectl create -f <fileName>.yaml
kubectl apply -f <fileName>.yaml
kubectl apply (does create or apply)
kubectl update -f <fileName>.yaml 
kubectl delete -f <fileName>.yaml

kubectl describe ns test-ns    -- describes about namespace
kubectl get ns test-ns -o yaml   
kubectl get all -n test-ns      -- get all objects in test-ns namespace
kubectl get all --all-namespaces     -- get all objects in all namespace
kubectl get all -A
kubectl get pods -A
kubectl get services -A
kubectl get deployments -A

kubectl get pods -ns test-ns

```
