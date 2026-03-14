# traefik-ingress-controller

Kubernetes manifests to deploy **Traefik v1.7** as an Ingress Controller using a DaemonSet.

## Files

| File | Description |
|------|-------------|
| `traefik-ds.yaml` | DaemonSet, ServiceAccount, and Service for Traefik |
| `traefik-rbac.yaml` | ClusterRole and ClusterRoleBinding for Traefik RBAC |

## Architecture

Traefik runs as a **DaemonSet** in the `kube-system` namespace, binding directly to the host network on ports:

- `80` — HTTP traffic
- `8080` — Traefik Admin/Dashboard

## Deployment

### 1. Apply RBAC rules

```bash
kubectl apply -f traefik-rbac.yaml
```

### 2. Deploy Traefik DaemonSet

```bash
kubectl apply -f traefik-ds.yaml
```

### 3. Verify

```bash
kubectl get pods -n kube-system -l k8s-app=traefik-ingress-lb
kubectl get svc -n kube-system traefik-ingress-service
```

## Requirements

- Kubernetes 1.14+
- `kubectl` configured with cluster access

## Notes

- Traefik image used: `traefik:v1.7`
- For production, consider upgrading to Traefik v2+ and using the official Helm chart
