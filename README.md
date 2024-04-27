# espocrm-k8s

EspoCrm as k8s deployment

## Install

In the folder were you have all .yaml files run the following command:

```
kubectl apply -k .
```

If it does not work for minikube then try:

```
minikube kubectl apply -k .
```

If it does not work for microk8s then try:

```
microk8s kubectl apply -k .
```

You should see in the `default` namespace defined for kubernetes all the new objects.
The corresponding service is called `espocrm`.

If you want to use it in a different namespace then just add "-n &lt;namespace&gt;" as argument to kubectl call.

You need to use a proxy in front of it (like nginx) to redirect to the exposed port on k8s node.
To find the mapped ports for port 80 just check the "Internal Endpoints" of the service "espocrm"
or run `kubectl get svc` from the shell of the server running the cluster.

## Customization

You must customize some values in `espocrm-env-configmap.yaml`:

- ESPOCRM_ADMIN_USERNAME: the account for espocrm administration
- ESPOCRM_ADMIN_PASSWORD: the passowrd for espocrm administration account

All other values should not be changed.

## Notice

The .yaml files are generated from the docker-compose.yml of the specified release.

The pod for `espocrm` runs two containers inside.
