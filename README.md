# k8s-spark-cluster

## Tested version
- helm v3.12.2
- kustomize v5.1.0
## Render manifest for blue deployment (with the current version of spark chart)

```
# dev environment
kustomize build --enable-helm blue/overlays/dev
```

```
# prod environment
kustomize build --enable-helm blue/overlays/prod
```

```
# blue/green deployment where the spark chart version is newer
kustomize build --enable-helm green/overlays/upgrade
```

## Render manifest and deploy to the current cluster

```
# dev environment
kustomize build --enable-helm blue/overlays/dev | kubectl apply -f-
```

```
# prod environment
kustomize build --enable-helm blue/overlays/prod | kubectl apply -f-
```

```
# blue/green deployment where the spark chart version is newer 
kustomize build --enable-helm green/overlays/upgrade | kubectl apply -f-
```

## Get spark cluster pods

```
kubectl get po -n spark
NAME                 READY   STATUS    RESTARTS      AGE
spark-master-0       1/1     Running   0             31m
spark-master-dev-0   1/1     Running   0             78m
spark-worker-0       1/1     Running   1 (29m ago)   31m
spark-worker-dev-0   1/1     Running   5 (33m ago)   78m

kubectl get po -n spark-upgrade
NAME             READY   STATUS    RESTARTS   AGE
spark-master-0   1/1     Running   0          33m
spark-worker-0   1/1     Running   0          33m
```

## Access to Master UI

