# k8s-spark-cluster

## Tested version

- helm v3.12.2
- kustomize v5.1.0

## Modify `etc/hosts` for local deloyment

```
cat /etc/hosts
##
# Host Database
#
# localhost is used to configure the loopback interface
# when the system is booting.  Do not change this entry.
##
127.0.0.1       localhost spark.test spark-dev.test spark-upgraded.test
255.255.255.255 broadcasthost
::1             localhost
```

## Render manifests for different environments

```
# dev environment
kustomize build --enable-helm sprak/overlays/dev
```

```
# prod environment
kustomize build --enable-helm spark/overlays/prod
```

```
# upgraded environment
kustomize build --enable-helm spark/overlays/upgraded
```

## Render manifest and deploy to the current cluster

```
# dev environment
kustomize build --enable-helm spark/overlays/dev | kubectl apply -f-
```

```
# prod environment
kustomize build --enable-helm spark/overlays/prod | kubectl apply -f-
```

```
# upgraded environment
kustomize build --enable-helm spark/overlays/upgraded | kubectl apply -f-
```

## Get spark cluster pods

```
kubectl get po -n spark
NAME                  READY   STATUS    RESTARTS        AGE
dev-spark-master-0    1/1     Running   0               10m
dev-spark-worker-0    1/1     Running   1 (3m57s ago)   10m
prod-spark-master-0   1/1     Running   0               10m
prod-spark-worker-0   1/1     Running   0               10m

kubectl get po -n spark-upgraded
NAME                      READY   STATUS    RESTARTS   AGE
upgraded-spark-master-0   1/1     Running   0          3m18s
upgraded-spark-worker-0   1/1     Running   0          3m18s
```

## Access to Master UI

### Dev cluster

![dev-spark](https://github.com/hungtran84/k8s-spark-cluster/assets/30172743/95e6d8df-df2c-48d1-afd8-aaceeb68b60c)


### Prod cluster

![prod-spark](https://github.com/hungtran84/k8s-spark-cluster/assets/30172743/6adbc3fb-0551-4d2f-8633-2d825000abce)


### Upgraded cluster

![upgraded-spark](https://github.com/hungtran84/k8s-spark-cluster/assets/30172743/3510306c-97c0-45a0-895a-70ae4f8563f3)


