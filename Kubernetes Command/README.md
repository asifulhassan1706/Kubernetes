# ☸️ Kubernetes Commands Cheatsheet

A complete reference for essential **Kubernetes (kubectl)** commands used in production environments.  

## 🔍 Cluster Information
| Command                           | Description                     |
|-----------------------------------|---------------------------------|
| `kubectl cluster-info`            | Show cluster info              |
| `kubectl get nodes`               | List all nodes                 |
| `kubectl describe node <node>`    | Node details                   |
| `kubectl top nodes`               | Show resource usage of nodes   |

## 📦 Namespaces
| Command                           | Description                     |
|-----------------------------------|---------------------------------|
| `kubectl get ns`                  | List namespaces                |
| `kubectl create ns my-namespace`  | Create namespace               |
| `kubectl delete ns my-namespace`  | Delete namespace               |
| `kubectl config set-context --current --namespace=ns` | Set default namespace |

## 🛠️ Pods
| Command                           | Description                     |
|-----------------------------------|---------------------------------|
| `kubectl get pods`                | List pods                      |
| `kubectl get pods -o wide`        | List pods with details         |
| `kubectl describe pod <pod>`      | Pod details                    |
| `kubectl logs <pod>`              | Show pod logs                  |
| `kubectl logs -f <pod>`           | Stream pod logs                |
| `kubectl exec -it <pod> -- bash`  | Access pod shell               |
| `kubectl delete pod <pod>`        | Delete pod                     |


## 🚀 Deployments
| Command                                         | Description                  |
|-------------------------------------------------|------------------------------|
| `kubectl get deploy`                            | List deployments            |
| `kubectl describe deploy <deploy>`              | Deployment details           |
| `kubectl rollout status deploy <deploy>`        | Show rollout status          |
| `kubectl rollout history deploy <deploy>`       | Show rollout history         |
| `kubectl rollout undo deploy <deploy>`          | Rollback deployment          |
| `kubectl scale deploy <deploy> --replicas=3`    | Scale deployment             |
| `kubectl rollout restart deploy <deploy>`       | Restart deployment           |


## 📜 Services
| Command                           | Description                     |
|-----------------------------------|---------------------------------|
| `kubectl get svc`                 | List services                  |
| `kubectl describe svc <svc>`      | Service details                |
| `kubectl expose pod <pod> --port=80 --type=NodePort` | Expose pod |


## 🌐 Ingress
| Command                           | Description                     |
|-----------------------------------|---------------------------------|
| `kubectl get ingress`             | List ingress rules             |
| `kubectl describe ingress <ing>`  | Ingress details                |
| `kubectl delete ingress <ing>`    | Delete ingress                 |


## 📂 ConfigMaps & Secrets
| Command                           | Description                     |
|-----------------------------------|---------------------------------|
| `kubectl get configmap`           | List ConfigMaps                |
| `kubectl describe configmap <cm>` | ConfigMap details              |
| `kubectl create configmap my-cm --from-literal=key=value` | Create ConfigMap |
| `kubectl get secret`              | List secrets                   |
| `kubectl describe secret <secret>`| Secret details                 |
| `kubectl create secret generic my-secret --from-literal=pwd=123` | Create secret |


## 📊 Monitoring & Debugging
| Command                           | Description                     |
|-----------------------------------|---------------------------------|
| `kubectl top pods`                | Show pod resource usage        |
| `kubectl get events`              | Show events                    |
| `kubectl describe <resource>`     | Resource details               |
| `kubectl get all`                 | List all resources in namespace|


## ⚙️ Apply & Delete
| Command                           | Description                     |
|-----------------------------------|---------------------------------|
| `kubectl apply -f file.yaml`      | Apply config                   |
| `kubectl delete -f file.yaml`     | Delete resource                |
| `kubectl delete pod <pod>`        | Delete pod                     |
| `kubectl delete deploy <deploy>`  | Delete deployment              |


## 🧰 Advanced
| Command                           | Description                     |
|-----------------------------------|---------------------------------|
| `kubectl config view`             | Show kubeconfig details        |
| `kubectl config get-contexts`     | List contexts                  |
| `kubectl config use-context <ctx>`| Switch context                 |
| `kubectl drain <node>`            | Safely drain node              |
| `kubectl cordon <node>`           | Mark node unschedulable        |
| `kubectl uncordon <node>`         | Mark node schedulable again    |

