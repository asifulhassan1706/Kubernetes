# ☸️ Kubernetes Cluster Setup – Master + Worker Nodes

This guide provides a **complete workflow to create a Kubernetes cluster** with master and worker nodes using kubeadm, suitable for production-like setups.

## 1️⃣ Prerequisites
- Linux servers (Ubuntu/Debian recommended)  
  - Master node: ≥2GB RAM  
  - Worker node(s): ≥1GB RAM  
- Docker installed  
- Swap disabled (`swapoff -a`)  
- Network connectivity between nodes  
- Unique hostname for each node  

## 2️⃣ Install Kubernetes Components (Master & Worker)
### Update packages
```bash
sudo apt update && sudo apt upgrade -y
````

### Install dependencies

```bash
sudo apt install -y apt-transport-https ca-certificates curl
```

### Add Kubernetes repo

```bash
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
sudo bash -c 'cat <<EOF >/etc/apt/sources.list.d/kubernetes.list
deb https://apt.kubernetes.io/ kubernetes-xenial main
EOF'
```

### Install kubeadm, kubelet, kubectl

```bash
sudo apt update
sudo apt install -y kubelet kubeadm kubectl
sudo apt-mark hold kubelet kubeadm kubectl
```

### Disable Swap

```bash
sudo swapoff -a
sudo sed -i '/ swap / s/^/#/' /etc/fstab
```

## 3️⃣ Initialize Master Node

### Initializes the master node and sets up control-plane

```bash
sudo kubeadm init --pod-network-cidr=10.244.0.0/16
```

* `--pod-network-cidr` depends on CNI plugin (Flannel: `10.244.0.0/16`)

## 4️⃣ Configure kubectl on Master

```bash
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

Check master node status:

```bash
kubectl get nodes
```
Expected output: **master node Ready**


## 5️⃣ Install Pod Network (CNI)

Example: Flannel

```bash
kubectl apply -f https://raw.githubusercontent.com/flannel-io/flannel/master/Documentation/kube-flannel.yml
```

Check pods:

```bash
kubectl get pods -n kube-system
```

## 6️⃣ Allow Scheduling Pods on Master (Optional)

> By default, master node is tainted and cannot schedule pods.

```bash
kubectl taint nodes --all node-role.kubernetes.io/master-
```

## 7️⃣ Add Worker Nodes

### a) On Master Node: Get join command

After `kubeadm init`, you’ll see output like:

```bash
kubeadm join <MASTER-IP>:6443 --token <TOKEN> --discovery-token-ca-cert-hash sha256:<HASH>
```

### b) On Worker Node(s): Run join command

```bash
sudo kubeadm join <MASTER-IP>:6443 --token <TOKEN> --discovery-token-ca-cert-hash sha256:<HASH>
```

### c) Verify nodes on Master

```bash
kubectl get nodes
```
* Worker nodes should appear as **Ready**


## 8️⃣ Common kubectl Commands (Post Cluster Setup)

| Command                                      | Description                     |
| -------------------------------------------- | ------------------------------- |
| `kubectl get nodes`                          | List all nodes                  |
| `kubectl get pods -A`                        | List all pods in all namespaces |
| `kubectl describe node <node>`               | Show node details               |
| `kubectl logs <pod>`                         | Show pod logs                   |
| `kubectl exec -it <pod> -- bash`             | Open shell inside pod           |
| `kubectl get deploy`                         | List deployments                |
| `kubectl rollout restart deploy <deploy>`    | Restart deployment              |
| `kubectl scale deploy <deploy> --replicas=3` | Scale deployment                |
| `kubectl apply -f file.yaml`                 | Apply resource from YAML        |
| `kubectl delete -f file.yaml`                | Delete resource from YAML       |

## ✅ Cluster Setup Complete

* Master node ready
* Worker nodes joined
* Pod network applied
* Cluster ready for deploying applications and services
