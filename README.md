# ☸ Locust on Kubernetes

[Locust](https://locust.io/) is an open source load testing tool.

Locust version tested: `1.4.1`.

## Kubernetes

### Create a ConfigMap containing locust-tasks folder items

`locust-tasks` contains your script and dependencies for load testing.

Your script must have the name `locustfile.py`.

```bash
kubectl create configmap locust-configmap --from-file=locust-tasks/
```
### (Optional) Activate HPA

In `k8s` folder, open and modify: 
- `locust-master.yaml`: uncomment the TODO (line 26-30).
- `locust-hpa-autoscalling.yaml`: uncomment the content.

### Deploy

```bash
kubectl create -f k8s
```

### Get external IP to access to Locust portal 

```bash
kubectl get svc locust-master -o jsonpath="{.status.loadBalancer.ingress[0].ip}"
```

### Launch Locust portal
`http://[external_ip]:8089`

## Useful links

- [Locust repository](https://github.com/locustio/locust)
- [Locust environment variables](https://docs.locust.io/en/stable/configuration.html?#environment-variables)