# Kubernetes — Overview and Architecture

## What is Kubernetes?

Kubernetes (K8s) is an open-source **container orchestration platform** that automates deployment, scaling, and management of containerized applications. It was originally designed by Google and is now maintained by the Cloud Native Computing Foundation (CNCF).

---

## Why Kubernetes?

Docker alone is a simple container runtime — great for running containers but not built for production-grade workloads. Here's what Docker struggles with and how Kubernetes solves each problem:

| Problem | Docker Limitation | Kubernetes Solution |
|---|---|---|
| Ephemeral containers | Containers die and stay dead | **Auto-healing** — restarts containers automatically |
| Single host | Runs on one machine only | **Cluster support** — runs across many nodes |
| No auto-scaling | Can't scale up under load | **Horizontal Pod Autoscaler** |
| No self-healing | Failures need manual recovery | **Kubelet + ReplicaSet** ensure desired state |

> Kubernetes is designed for **enterprise-level** container orchestration at scale.

---

## Architecture Overview

Kubernetes follows a **master–worker** (control plane / data plane) architecture. Every Kubernetes cluster has two kinds of machines:

- **Control Plane** (master node) — manages the cluster, makes decisions
- **Data Plane** (worker nodes) — actually runs your application containers

```
┌─────────────────────────────────────────────────────┐
│                   KUBERNETES CLUSTER                 │
│                                                     │
│  ┌──────────────────┐    ┌────────────────────────┐ │
│  │  CONTROL PLANE   │    │     DATA PLANE          │ │
│  │  (Master Node)   │◄──►│   (Worker Nodes)        │ │
│  │                  │    │                         │ │
│  │  • API Server    │    │  • Container Runtime    │ │
│  │  • Scheduler     │    │  • Kubelet              │ │
│  │  • etcd          │    │  • Kube Proxy           │ │
│  │  • Controller Mgr│    │                         │ │
│  │  • Cloud Ctrl Mgr│    │  [ Pod ][ Pod ][ Pod ]  │ │
│  └──────────────────┘    └────────────────────────┘ │
└─────────────────────────────────────────────────────┘
```

---

## Control Plane Components

The control plane runs on the master node and is responsible for managing the entire cluster.

### 1. API Server
- The **heart of Kubernetes** — every interaction goes through it
- Exposes the Kubernetes API to users, tools (like `kubectl`), and internal components
- Validates and processes all REST requests
- Think of it as the **front door** to the cluster

### 2. Scheduler
- Watches for newly created Pods with no assigned node
- Selects the best worker node to run each Pod based on resource availability, constraints, and policies
- Acts on decisions made through the API server

### 3. etcd
- A distributed **key-value store** — the cluster's memory
- Stores all cluster state: nodes, pods, configs, secrets, and more
- Considered the **brain** of Kubernetes — if etcd is healthy, the cluster can recover from almost anything

### 4. Controller Manager
- Runs a set of **controllers** in a single process
- Each controller watches the cluster state and works to move it toward the desired state
- Example: the **ReplicaSet controller** ensures the right number of pod replicas are always running

### 5. Cloud Controller Manager
- An **optional, open-source** component
- Connects your cluster to a cloud provider's API (AWS, GCP, Azure, etc.)
- Manages cloud-specific resources like load balancers, storage volumes, and node lifecycles
- Keeps cloud-provider logic **separate from core Kubernetes** — making the platform portable

---

## Data Plane Components

The data plane runs on every **worker node** and is responsible for actually running workloads.

### 1. Container Runtime
- The software that **runs containers** on a node
- Just as the JVM runs Java programs, the container runtime runs container images
- Examples: `containerd`, `CRI-O`, Docker Engine
- Kubernetes supports any runtime that implements the **CRI (Container Runtime Interface)**

### 2. Kubelet
- An agent that runs on every worker node
- Ensures that the containers described in a Pod spec are **running and healthy**
- If a container crashes, Kubelet detects it and **reports to the API server**
- Central to Kubernetes' **auto-healing** capability

### 3. Kube Proxy
- Handles **networking** on each node
- Assigns IP addresses and manages network rules via **iptables**
- Provides basic **load balancing** across service endpoints
- Enables Pods to communicate with each other and with the outside world

---

## Key Kubernetes Concepts

### Pods
The smallest deployable unit in Kubernetes. A Pod wraps one or more containers that share networking and storage.

### ReplicaSet
Ensures a specified number of identical Pods are running at all times. If a Pod dies, ReplicaSet creates a new one — this is **auto-healing**.

### Deployment
A higher-level abstraction over ReplicaSet that adds rolling updates and rollback capabilities.

### Service
Exposes a set of Pods as a network endpoint — provides a stable IP and DNS name even as Pods come and go.

---

## How the Four Problems Are Solved

```
1. Ephemeral nature  →  Kubelet + ReplicaSet watch and restart failed containers
2. Single host       →  Cluster of nodes (master + workers) spans multiple machines
3. No auto-scaling   →  Horizontal Pod Autoscaler adjusts replica count based on metrics
4. No auto-healing   →  Kubelet detects failures; new Pod starts before the old one is removed
```

---

## Quick Reference

```
kubectl get nodes          # List all nodes in the cluster
kubectl get pods           # List all running pods
kubectl get deployments    # List deployments
kubectl describe pod <name> # Inspect a specific pod
kubectl apply -f file.yaml  # Apply a configuration
```

---

*Kubernetes docs: https://kubernetes.io/docs*