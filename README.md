# k8s-lab

KinD(Kubernetes in Docker)를 사용한 로컬 Kubernetes 실습 환경입니다.
모든 리소스는 `kubectl`로 직접 적용하는 raw 매니페스트로 구성되어 있습니다.

## 사전 요구사항

- [Docker](https://www.docker.com/)
- [KinD](https://kind.sigs.k8s.io/)
- [kubectl](https://kubernetes.io/docs/tasks/tools/)

## 클러스터 구성

| 항목 | 값 |
|------|-----|
| 클러스터명 | `cwave-cluster` |
| 구성 | control-plane 1 + worker 2 |
| Kubernetes 버전 | v1.32.2 |
| Pod 서브넷 | 10.110.0.0/16 |
| Service 서브넷 | 10.120.0.0/16 |
| 포트 매핑 | Host 80 → 컨테이너 80, Host 443 → 컨테이너 443 |

## 빠른 시작

```bash
# 클러스터 생성
kind create cluster --config 3-node-cluster.yml

# 노드 확인
kubectl get nodes

# 매니페스트 적용
kubectl apply -f <manifest>.yml

# 클러스터 삭제
kind delete cluster --name cwave-cluster
```

## 매니페스트 목록

| 파일 | 리소스 | 설명 |
|------|--------|------|
| `3-node-cluster.yml` | KinD ClusterConfig | 로컬 멀티노드 클러스터 설정 |
| `my-first-pod.yml` | Pod | 기본 nginx Pod |
| `myapp-pod.yml` | Pod | 쉘 커맨드를 실행하는 Busybox Pod |
| `nginx-rc.yml` | ReplicationController | 레거시 컨트롤러 (3 replicas) |
| `nginx-rs.yml` | ReplicaSet | 저수준 컨트롤러 (3 replicas) |
| `nginx-deployment.yml` | Deployment | 롤링 업데이트 Deployment (3 replicas) |
| `nginx-clusterip-deploy.yml` | Deployment | ClusterIP 실습용 Deployment |
| `nginx-clusterip-svc.yml` | Service (ClusterIP) | 클러스터 내부 통신 |
| `nginx-nodeport-svc.yml` | Service (NodePort) | 노드 포트로 외부 노출 |
| `nginx-loadbalancer-svc.yml` | Service (LoadBalancer) | 로드밸런서로 외부 노출 |

매니페스트는 학습 순서에 따라 구성되어 있습니다:
**Pod → ReplicationController(deprecated) → ReplicaSet → Deployment → Service**

## 기여

[CONTRIBUTING.md](./CONTRIBUTING.md)를 참고하세요.
