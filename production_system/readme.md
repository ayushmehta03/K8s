# Kubernetes Distributions and KOPS

## Kubernetes Distributions

A Kubernetes distribution packages the core Kubernetes engine with extra tooling,
a user interface, and commercial support on top.

| Distribution | Maintained by |
|---|---|
| OpenShift | Red Hat |
| Rancher | SUSE |
| Tanzu | VMware |
| EKS | Amazon Web Services |

These distributions add a better user experience and dedicated customer support.
However, many organisations use plain (upstream) Kubernetes in staging, pre-production,
and production environments.

### Usage ranking

1. OpenShift
2. Rancher
3. Tanzu (VMware)
4. EKS (Amazon)

---

## Kubernetes vs EKS

EKS (Elastic Kubernetes Service) is built on top of Kubernetes — it is not a
replacement. The difference is support: when something breaks on EKS, Amazon
provides quick assistance. With plain Kubernetes you rely on the community.

---

## KOPS

KOPS (Kubernetes Operations) is an open-source command-line tool that manages
the full lifecycle of a Kubernetes cluster:

```
┌──────────┐     ┌──────────┐     ┌──────────┐     ┌──────────┐
│  Create  │ ──► │ Upgrade  │ ──► │  Manage  │ ──► │  Delete  │
└──────────┘     └──────────┘     └──────────┘     └──────────┘
```

---

## Steps to Set Up KOPS on AWS

### 1. Install dependencies

- Python 3
- AWS CLI
- `kubectl`
- KOPS binary

### 2. Grant IAM permissions

If using an IAM user, attach the following policies:

- EC2 full access
- S3 full access
- VPC full access
- IAM full access

### 3. Configure AWS CLI

```bash
aws configure
```

### 4. Create an S3 bucket

KOPS uses an S3 bucket to store all cluster configuration and state.

```bash
aws s3 mb s3://your-bucket-name --region your-region
export KOPS_STATE_STORE=s3://your-bucket-name
```

### 5. Create the cluster

```bash
kops create cluster \
  --name your-cluster.k8s.local \
  --state s3://your-bucket-name \
  --zones your-availability-zone \
  --node-count 2 \
  --node-size t3.medium \
  --master-size t3.medium
```

### 6. Apply the cluster

```bash
kops update cluster --name your-cluster.k8s.local --yes
```

---

## For Production

In a production setup, replace `.k8s.local` (local DNS) with a **real domain**.
Use **AWS Route 53** to manage DNS for the cluster.

### Steps

1. Register or delegate a domain in Route 53.
2. Create a hosted zone for your cluster subdomain (e.g. `k8s.yourdomain.com`).
3. Use that domain as the cluster name in the `kops create cluster` command:

```bash
kops create cluster \
  --name k8s.yourdomain.com \
  --state s3://your-bucket-name \
  --zones your-availability-zone \
  --dns-zone k8s.yourdomain.com
```

Route 53 will handle DNS resolution so nodes and the API server can find each other
by name across the cluster.

---

*KOPS docs: https://kops.sigs.k8s.io*