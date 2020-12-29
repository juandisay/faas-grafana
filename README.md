# faas-grafana

OpenFaaS Grafana [Docker image](https://hub.docker.com/r/stefanprodan/faas-grafana/)

### Kubernetes

Run Grafan in OpenFaaS Kubernetes namespace:

```bash
kubectl -n openfaas run --generator=run-pod/v1 --image=stefanprodan/faas-grafana:4.6.3 \   
--port=3000 \
grafana
```

Expose Grafan with a NodePort:

```bash
kubectl -n openfaas expose pod grafana --type=NodePort --name=grafana
```

Find Grafana node port address:

```bash
$GRAFANA_PORT=$(kubectl -n openfaas get svc grafana -o jsonpath="{.spec.ports[0].nodePort}")
```

URL: `http://<KUBE_IP>:<GRAFANA_PORT>/dashboard/db/openfaas`
Credentials: `admin/admin`

### Swarm

Run Grafana in OpenFaaS Swarm network:

```bash
docker service create -d \
--name=func_grafana \
--publish=3000:3000 \
--network=func_functions \
stefanprodan/faas-grafana:4.6.3
```

URL: `http://<SWARM_IP>:3000/dashboard/db/openfaas`
