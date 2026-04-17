# Kubernetes Production Manifests

Battle-tested Kubernetes manifests for production workloads. Includes RBAC, NetworkPolicy, HPA, PodDisruptionBudget, Ingress, and resource limits — everything a real cluster needs.

## Contents

```
.
├── namespaces/        # Namespace definitions
├── deployments/       # App deployments (nginx, api, worker)
├── services/          # ClusterIP, NodePort, LoadBalancer
├── ingress/           # Nginx Ingress with TLS
├── hpa/               # Horizontal Pod Autoscalers
├── rbac/              # ServiceAccounts, Roles, RoleBindings
├── networkpolicies/   # Network isolation rules
├── configmaps/        # App config
└── secrets/           # Sealed Secrets examples
```

## Quick Start

```bash
# Apply namespace first
kubectl apply -f namespaces/

# Apply RBAC
kubectl apply -f rbac/

# Deploy everything
kubectl apply -f configmaps/ -f secrets/ -f deployments/ -f services/ -f ingress/ -f hpa/

# Watch rollout
kubectl rollout status deployment/webapp -n production
```

## Requirements

- Kubernetes >= 1.28
- Nginx Ingress Controller
- cert-manager (for TLS)
- Metrics Server (for HPA)

## Best Practices Applied

- Non-root containers with `securityContext`
- Resource `requests` and `limits` on every container
- `readinessProbe` and `livenessProbe` on every Deployment
- `PodDisruptionBudget` for zero-downtime maintenance
- `NetworkPolicy` to enforce least-privilege networking
- `HorizontalPodAutoscaler` for CPU/memory-based scaling
