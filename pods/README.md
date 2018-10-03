# Pods examples
Below there are short description about objects definition inside yaml files.

## Multiple containers in one pods

```
kubectl create -f multiple-containers.yml
```
This example run 3 containers inside a one pod called`nginx`:
*   `nginx` - run nginx that listen on port 80
*   `check-host-80` - check if nginx is accessible via `localhost:80`. Also it redirects
netstat result to local `/etc/hello` and `/data/hello`. The `/data/hello` is put
on persistent volumes claim `examplepvc`.
*   `check-files` - this container use watch with 15 seconds interval to check if
`/etc/hello` and `/data/hello` appear inside this container.

Useful command:

*   Get pods list (minikube default namespace is called `default`): `kubectl get pods`
*   Exec to `check-files` container inside `nginx` pod: `kubectl exec -it nginx -c check-files sh`
*   Get container logs with follow (`-f`): `kubectl logs nginx -c check-files`
*   Cleaning: `kubectl delete pod nginx && kubectl delete pvc examplepvc`

## Different container types
```
kubectl create -f different-container-type.yml
```

## Pod limits

```
kubectl create -f pods-limits.yaml
```
Useful command:
*   Check `limit` namespace settings: `kubectl describe namespace limit`
*   Get quota for the `limit` namespace: `kubectl get quota -n limit`
*   Get limits for the `limit` namespace: `kubectl get limits -n limit`
*   Get pods details: `kubectl describe pod nginx-overloaded -n limit`
*   Cleaning: `kubectl delete ns limit`
