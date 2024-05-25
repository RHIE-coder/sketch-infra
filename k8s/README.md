# Prerequsite
 - docker
 - kubectl
 - minikue (kubeadm, kops, KRIB, kubespray)

```sh
docker version
kubectl version
minikube version
```

# Flow 1: Pod - Service

```sh
minikube start
kubectl get pod -n kube-system
kubectl run mynginx --image=nginx
kubectl get pods -o wide
kubectl get services mynginx
kubectl expose pod mynginx --type=NodePort --port=80
minikube service mynginx --url

kubectl delete pod mynginx
kubectl delete service mynginx
```

# Flow 1-1: Pod - Service [YAML]

```sh
kubectl apply -f ./k8s/1-pod.yaml
minikube service nginx-service
```

# Flow 2: ReplicaSet

```sh
kubectl apply -f ./k8s/2-RS.yaml
minikube service mynetwork
kubectl describe rs/mynetwork
```

# Flow 3: Deployment

```sh
kubectl apply -f ./k8s/3-dpy.yaml
kubectl describe deployment/nginx-deployment
kubectl rollout status deployment nginx-deployment
kubectl rollout history deployment/nginx-deployment
kubectl rollout undo deployment nginx-deployment
```

# Flow 4: Guestbook

```sh
kubectl apply -f ./k8s/G1-leader.yaml
kubectl apply -f ./k8s/G2-follower.yaml
kubectl apply -f ./k8s/G3-front.yaml
kubectl get pods -l app=guestbook -l tier=frontend
```