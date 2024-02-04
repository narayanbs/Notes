#### Installation

**kubectl**
```bash
Download kubectl and verify the installer

$ curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
$ curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256"

$ echo "$(cat kubectl.sha256)  kubectl" | sha256sum --check

$ chmod +x kubectl 
$ mv kubectl ~/.local/bin/

$ kubectl version --client

```
**minicube**
```bash
$ curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube_latest_amd64.deb
$ sudo dpkg -i minikube_latest_amd64.deb 

$ minikube start
$ kubectl get po -A

# if you want to stop
$ minikube stop
```
**k9s**
```bash
$ curl -SLO https://github.com/derailed/k9s/releases/download/v0.31.7/k9s_linux_amd64.deb
$ sudo dpkg -i k9s_linux_amd64.deb

$ k9s

```

#### Commands

**Kubectl**
```bash
# Applying configuration to kubenetes cluster**
$ kubectl apply -f ./

$ kubectl get pod
$ kubectl get svc 
$ kubectl get all
$ kubectl describe <svc>
$ kubectl logs <pod>

$ kubectl scale deployment --replicas=1 <name>, <name>....

# Expose clusterip externally by forwarding port
$ kubectl get pods
$ kubectl port-forward rabbitmq-0 80 15672
```

**minikube**
```bash
minikube start
minikube stop
minikube dashboard
minikube tunnel
```

