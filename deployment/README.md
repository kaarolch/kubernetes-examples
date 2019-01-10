# Pods examples
Below there are short description about objects definition inside yaml files.

## Deployment

```
kubectl create -f nginx-start.yml
kubectl get deployment
kubectl get pods --show-labels
kubectl create -f nginx-update.yml
kubectl edit deployment.v1.apps/nginx-deployment
```
Check update status and rollback to revision 2 :  
```
kubectl rollout status deployment nginx-deployment
kubectl rollout history deployment nginx-deployment --revision=2
```
Check rollout status :  
```
kubectl rollout status deployment nginx-deployment
```
Scale current deployment to 4 replicas :  
```
kubectl scale deployment nginx-deployment --replicas=4
```
Change update strategy to Recreate:

```
kubectl edit deployment nginx-deployment
```
content:
```
# FROM
strategy:
  type: RollingUpdate
# TO  
  strategy:
    type: Recreate
```

Pause and resume deployment:

```
kubectl rollout pause deployment nginx-deployment
```
Now you can edit deployment multiple times.
```
kubectl rollout resume deployment nginx-deployment
```
