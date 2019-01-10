# Pods examples
Below there are short description about objects definition inside yaml files.

## Deployment

```
kubectl create -f nginx-start.yml
kubectl get sts
kubectl get pods --show-labels
kubectl edit sts nginx-deployment
```
Check dns records:

```
kubectl run -i --tty --image busybox cli --restart=Never --rm /bin/sh
nslookup nginx-sts-1.show-sts.default.svc.cluster.local.

```

Ordering:

```
kubectl delete pod -l app=nginx-sts
kubectl get pod -w -l app=nginx-sts
kubectl scale sts nginx-sts --replicas=1
kubectl get pod -w -l app=nginx-sts
kubectl scale sts nginx-sts --replicas=5
```

Partial update:

```
kubectl patch sts nginx-sts -p '{"spec":{"updateStrategy":{"type":"RollingUpdate","rollingUpdate":{"partition":2}}}}'
kubectl get pod -w -l app=nginx-sts
kubectl patch sts nginx-sts --type='json' -p='[{"op": "replace", "path": "/spec/template/spec/containers/0/image", "value":"nginx:1.7.9"}]'
kubectl patch sts nginx-sts -p '{"spec":{"updateStrategy":{"type":"RollingUpdate","rollingUpdate":{"partition":0}}}}'
kubectl get pod -w -l app=nginx-sts
```
