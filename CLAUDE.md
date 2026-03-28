# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 언어 설정

모든 답변은 **한국어**로 작성한다.

## Overview

This is a Kubernetes learning lab using KinD (Kubernetes in Docker) for local cluster experimentation. All files are raw Kubernetes manifests applied manually with `kubectl`.

## Common Commands

### Cluster Management
```bash
# Create the KinD cluster
kind create cluster --config 3-node-cluster.yml

# Delete the cluster
kind delete cluster --name cwave-cluster

# View cluster nodes
kubectl get nodes
```

### Applying Manifests
```bash
# Apply a manifest
kubectl apply -f <manifest>.yml

# Delete resources defined in a manifest
kubectl delete -f <manifest>.yml

# View running pods
kubectl get pods

# Describe a resource for debugging
kubectl describe pod <pod-name>
kubectl describe deployment <deployment-name>
```

## Cluster Configuration

The KinD cluster (`cwave-cluster`) uses:
- **1 control-plane + 2 worker nodes** (Kubernetes v1.32.2)
- **Pod subnet**: 10.110.0.0/16
- **Service subnet**: 10.120.0.0/16
- **Port mappings**: Host 80 → container 80, Host 443 → container 443 (for ingress)

## Manifest Overview

| File | Resource Type | Purpose |
|------|--------------|---------|
| `3-node-cluster.yml` | KinD ClusterConfig | Local multi-node cluster setup |
| `my-first-pod.yml` | Pod | Basic nginx Pod |
| `myapp-pod.yml` | Pod | Busybox Pod with shell command |
| `nginx-rc.yml` | ReplicationController | Deprecated controller (3 replicas) |
| `nginx-rs.yml` | ReplicaSet | Low-level controller (3 replicas) |
| `nginx-deployment.yml` | Deployment | Rolling-update deployment (3 replicas) |

The manifests follow a learning progression: basic Pods → ReplicationController (deprecated) → ReplicaSet → Deployment (preferred for production).
