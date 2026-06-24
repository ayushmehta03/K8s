
## Deployment Wrapper in Kubernetes

A Deployment is a higher-level Kubernetes object that manages Pods through ReplicaSets. It provides production-grade features such as auto-healing, scaling, and rolling updates.

---

# Difference Between Container, Pod, and Deployment

| Container | Pod | Deployment |
|------------|-----|------------|
| Runs an application process | Runs one or more containers | Manages Pods |
| Created using commands | Defined using YAML | Defined using YAML |
| Single-host nature | Contains networking and volume configuration | Supports production workloads |
| Ephemeral in nature | Smallest deployable unit in Kubernetes | Supports auto-healing and scaling |

---

## Container

A container:

- Runs on commands.
- Has a single-host nature.
- Is ephemeral in nature.

---

## Pod

A pod:

- Can run a single container or multiple containers.
- Contains the running specification of containers.
- Uses YAML configuration instead of CLI commands.
- Stores information about:
  - Network
  - Volumes
  - Container configuration

---

## Deployment

A deployment:

- Works on top of Pods.
- Used in production environments.
- Supports:
  - Auto-healing
  - Auto-scaling
  - Rolling updates

---

# Kubernetes Architecture

```text
┌─────────────────┐
│   Deployment    │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│   ReplicaSet    │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│      Pods       │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│   Containers    │
└─────────────────┘
```

---

## How Deployment Works

A Deployment is specified using a YAML file.

### Workflow

1. Deployment creates ReplicaSets.
2. ReplicaSets are controllers written in Golang.
3. ReplicaSets ensure that the desired state and actual state remain the same.
4. ReplicaSets create and manage Pods.

```text
Deployment
    │
    ▼
ReplicaSet
    │
    ▼
Pods
    │
    ▼
Containers
```

---

# Auto-Healing

If a Pod is deleted or crashes:

1. ReplicaSet detects the mismatch.
2. The failed Pod enters the termination state.
3. A new Pod is automatically created.

This functionality is not available when using standalone Pods directly.

```text
Pod Deleted
     │
     ▼
ReplicaSet Detects Change
     │
     ▼
Creates New Pod
```

---

# Auto-Scaling

To scale applications:

- Increase or decrease the replica count in `deployment.yaml`.

Example:

```yaml
spec:
  replicas: 3
```

Kubernetes will automatically create or remove Pods to match the desired count.

---

# Useful Commands

## List all resources in the current namespace

```bash
kubectl get all
```

## List all resources from all namespaces

```bash
kubectl get all -A
```

## List Deployments

```bash
kubectl get deployment
```

## Apply a Deployment file

```bash
kubectl apply -f deployment.yml
```

## Watch Pod behavior in real time

```bash
kubectl get pods -w
```

## Scale a Deployment

```bash
kubectl scale deployment <deployment-name> --replicas=5
```

## Remove all Pods managed by a Deployment

```bash
kubectl scale deployment <deployment-name> --replicas=0
```

---

# Quick Summary

```text
Container
   ↓
Pod
   ↓
ReplicaSet
   ↓
Deployment
```

- Container → Runs application.
- Pod → Runs one or more containers.
- ReplicaSet → Maintains desired Pod count.
- Deployment → Manages ReplicaSets and provides production features.