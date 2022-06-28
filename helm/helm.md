# Helm

### Links:

- Helm [docs](https://helm.sh/docs/)
- [Artifact Hub](https://artifacthub.io/)
- [getbetterdevops](https://getbetterdevops.io/helm-quickstart-tutorial/)

## Tutorials

- [learning scenarion O'Reilly](https://learning.oreilly.com/scenarios/kubernetes-pipelines-helm/9781492078968/)

### Install

https://helm.sh/docs/intro/install/#from-script

```bash
$ curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
$ chmod 700 get_helm.sh
$ ./get_helm.sh
```

### Commands

```bash
# Start
$ helm version --short
$ helm completion bash > /etc/bash_completion.d/helm
$ helm env

# Help
$ helm help
$ helm help list
$ helm list --help

# Repos
$ helm repo ls
$ helm repo add bitnami https://charts.bitnami.com/bitnami
$ helm repo add bitnamix https://charts.bitnami.com/bitnami
$ helm repo ls
$ helm repo remove bitnamix
$ helm repo update bitnami

# Charts
$ helm ls --all-namespaces
$ helm search hub redis | grep bitnami
$ helm search repo bitnami

# Charts - show
$ helm show <all|chart|crds|readme|values>
$ helm show chart bitnami/redis
$ helm show readme bitnami/redis
$ helm show values bitnami/redis

# Chart - install

$ kubectl apply -f pv.yaml
$ helm install red bitnami/redis --version 16.12.0 --namespace redis --create-namespace --values redis-values.yaml

# Chart - upgrade 
$ helm ls --namespace redis
$ helm history red -n redis
$ helm upgrade red bitnami/redis --version 16.13.0 --namespace redis --values redis-values.yaml

# Test REDIS
$ export REDIS_PASSWORD=$(kubectl get secret --namespace redis red-redis -o jsonpath="{.data.redis-password}" | base64 --decode)
$ kubectl port-forward --namespace redis service/red-redis-master 6379:6379 > /dev/null &
$ redis-cli -h 127.0.0.1 -p 6379 -a $REDIS_PASSWORD ping | grep PONG
Warning: Using a password with '-a' or '-u' option on the command line interface may not be safe.
PONG
```

**redis-values.yaml**

```yaml
replica:
   replicaCount: 2
volumePermissions:
  enabled: true
securityContext:
  enabled: true
  fsGroup: 1001
  runAsUser: 1001
```

**pv.yaml**

```yaml
$ cat pv.yaml 
kind: PersistentVolume
apiVersion: v1
metadata:
  name: pv-volume1
  labels:
    type: local
spec:
  capacity:
    storage: 10Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: "/mnt/data1"
---
kind: PersistentVolume
apiVersion: v1
metadata:
  name: pv-volume2
  labels:
    type: local
spec:
  capacity:
    storage: 10Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: "/mnt/data2"
---
kind: PersistentVolume
apiVersion: v1
metadata:
  name: pv-volume3
  labels:
    type: local
spec:
  capacity:
    storage: 10Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: "/mnt/data3"$
```

### Create

```
$ helm create devops/kubernetes/helm/app-chart --namespace eart-systemteam-ns
$ helm install lucky-app devops/kubernetes/helm/app-chart / --values devops/kubernetes/helm/app-chart/values.yaml --namespace eart-systemteam-ns

helm install lucky-app devops/kubernetes/helm/app-chart/ --values devops/kubernetes/helm/app-chart/values.yaml --namespace eart-systemteam-ns
```# Helm


### Links:

- Helm [docs](https://helm.sh/docs/)
- [Artifact Hub](https://artifacthub.io/)

## Tutorials

- [learning scenarion O'Reilly](https://learning.oreilly.com/scenarios/kubernetes-pipelines-helm/9781492078968/)

### Install

https://helm.sh/docs/intro/install/#from-script

```bash
$ curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
$ chmod 700 get_helm.sh
$ ./get_helm.sh
```

### Commands

```bash
# Start
$ helm version --short
$ helm completion bash > /etc/bash_completion.d/helm
$ helm env

# Help
$ helm help
$ helm help list
$ helm list --help

# Repos
$ helm repo ls
$ helm repo add bitnami https://charts.bitnami.com/bitnami
$ helm repo add bitnamix https://charts.bitnami.com/bitnami
$ helm repo ls
$ helm repo remove bitnamix
$ helm repo update bitnami

# Charts
$ helm ls --all-namespaces
$ helm search hub redis | grep bitnami
$ helm search repo bitnami

# Charts - show
$ helm show <all|chart|crds|readme|values>
$ helm show chart bitnami/redis
$ helm show readme bitnami/redis
$ helm show values bitnami/redis

# Chart - install

$ kubectl apply -f pv.yaml
$ helm install red bitnami/redis --version 16.12.0 --namespace redis --create-namespace --values redis-values.yaml

# Chart - upgrade 
$ helm ls --namespace redis
$ helm history red -n redis
$ helm upgrade red bitnami/redis --version 16.13.0 --namespace redis --values redis-values.yaml

# Test REDIS
$ export REDIS_PASSWORD=$(kubectl get secret --namespace redis red-redis -o jsonpath="{.data.redis-password}" | base64 --decode)
$ kubectl port-forward --namespace redis service/red-redis-master 6379:6379 > /dev/null &
$ redis-cli -h 127.0.0.1 -p 6379 -a $REDIS_PASSWORD ping | grep PONG
Warning: Using a password with '-a' or '-u' option on the command line interface may not be safe.
PONG
```

**redis-values.yaml**

```yaml
replica:
   replicaCount: 2
volumePermissions:
  enabled: true
securityContext:
  enabled: true
  fsGroup: 1001
  runAsUser: 1001
```

**pv.yaml**

```yaml
$ cat pv.yaml 
kind: PersistentVolume
apiVersion: v1
metadata:
  name: pv-volume1
  labels:
    type: local
spec:
  capacity:
    storage: 10Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: "/mnt/data1"
---
kind: PersistentVolume
apiVersion: v1
metadata:
  name: pv-volume2
  labels:
    type: local
spec:
  capacity:
    storage: 10Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: "/mnt/data2"
---
kind: PersistentVolume
apiVersion: v1
metadata:
  name: pv-volume3
  labels:
    type: local
spec:
  capacity:
    storage: 10Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: "/mnt/data3"$
```

### Create

```
$ helm create devops/kubernetes/helm/app-chart --namespace eart-systemteam-ns
$ helm install lucky-app devops/kubernetes/helm/app-chart / --values devops/kubernetes/helm/app-chart/values.yaml --namespace eart-systemteam-ns

helm install lucky-app devops/kubernetes/helm/app-chart/ --values devops/kubernetes/helm/app-chart/values.yaml --namespace eart-systemteam-ns
```