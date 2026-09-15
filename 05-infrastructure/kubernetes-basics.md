# Kubernetes Basics

Kubernetes orchestrates containers across a cluster.

## Pod

The smallest deployable unit.

Usually one application container per pod, though sidecars are possible.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: api
spec:
  containers:
    - name: api
      image: example/api:1.0.0
      ports:
        - containerPort: 8000
```

In production, you normally use a Deployment rather than creating Pods directly.

## Deployment

Manages replicated pods and rolling updates.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: api
spec:
  replicas: 3
  selector:
    matchLabels:
      app: api
  template:
    metadata:
      labels:
        app: api
    spec:
      containers:
        - name: api
          image: example/api:1.0.0
          ports:
            - containerPort: 8000
```

## Service

Provides stable networking to pods.

```yaml
apiVersion: v1
kind: Service
metadata:
  name: api
spec:
  selector:
    app: api
  ports:
    - port: 80
      targetPort: 8000
```

## Important concepts to learn next

- Deployment
- Service
- Ingress
- ConfigMap
- Secret
- readiness probe
- liveness probe
- resource requests/limits
- HPA
- namespaces
- RBAC
- Jobs/CronJobs
- StatefulSets

## AI-specific Kubernetes

Learn:

- GPU scheduling
- node selectors/affinity
- taints/tolerations
- device plugins
- queue-based autoscaling
- separate CPU/GPU worker pools

The goal is not memorizing YAML. Understand the control plane, desired state, scheduling, service discovery, and failure recovery.
