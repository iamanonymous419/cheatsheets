# Kubernetes, Minikube and EKS Cheatsheet

This cheatsheet provides a comprehensive reference for Kubernetes (kubectl), Minikube, and Amazon EKS commands and concepts. It covers everything from basic commands to advanced architecture and best practices for production environments.

## Table of Contents

- [Minikube Commands](#minikube-commands)
- [Kubectl Commands](#kubectl-commands)
- [Amazon EKS Commands](#amazon-eks-commands)
- [Kubernetes Core Concepts](#kubernetes-core-concepts)
- [Kubernetes Resource Types](#kubernetes-resource-types)
- [Kubernetes YAML Definitions](#kubernetes-yaml-definitions)
- [Kubernetes Networking](#kubernetes-networking)
- [Kubernetes Storage](#kubernetes-storage)
- [Kubernetes Security](#kubernetes-security)
- [Kubernetes Monitoring](#kubernetes-monitoring)
- [Kubernetes Package Management](#kubernetes-package-management)
- [Advanced Pod Management](#advanced-pod-management)  
- [Kubernetes Production Best Practices](#kubernetes-production-best-practices)
- [Troubleshooting Kubernetes](#troubleshooting-kubernetes)
- [Kubernetes Extensions and Ecosystem](#kubernetes-extensions-and-ecosystem)
- [Multi-Cluster and Hybrid Cloud Strategies](#multi-cluster-and-hybrid-cloud-strategies)
- [Kubernetes Patterns and Anti-Patterns](#kubernetes-patterns-and-anti-patterns)
- [Kubernetes Dashboard and UI Tools](#kubernetes-dashboard-and-ui-tools)
- [Performance Optimization](#performance-optimization)
- [Kubernetes Certifications and Learning Path](#kubernetes-certifications-and-learning-path)

---

## Minikube Commands

### Basic Minikube Management

| Command | Description |
|---------|-------------|
| `minikube start` | Start minikube cluster |
| `minikube start --driver=docker` | Start with docker driver |
| `minikube start --driver=virtualbox` | Start with VirtualBox driver |
| `minikube start --driver=hyperv` | Start with Hyper-V driver |
| `minikube start --driver=kvm2` | Start with KVM2 driver (Linux) |
| `minikube start --driver=podman` | Start with Podman driver |
| `minikube start --nodes=2 -p multinode-demo` | Start multi-node cluster |
| `minikube start --kubernetes-version=v1.26.1` | Start with specific K8s version |
| `minikube start --memory=4096 --cpus=4` | Start with resource limits |
| `minikube stop` | Stop minikube cluster |
| `minikube delete` | Delete minikube cluster |
| `minikube delete --all` | Delete all clusters |
| `minikube pause` | Pause minikube without deleting resources |
| `minikube unpause` | Unpause minikube cluster |
| `minikube status` | Check minikube status |
| `minikube update-check` | Check for minikube updates |
| `minikube version` | Show minikube version |

### Cluster Access and Services

| Command | Description |
|---------|-------------|
| `minikube logs` | View minikube logs |
| `minikube logs -f` | Stream minikube logs |
| `minikube logs --node=minikube-m02` | View logs for specific node |
| `minikube ip` | Get minikube IP address |
| `minikube ssh` | SSH into minikube VM |
| `minikube ssh 'sudo crictl images'` | Run command in minikube via SSH |
| `minikube ssh --node=minikube-m02` | SSH into specific node |
| `minikube dashboard` | Access Kubernetes dashboard |
| `minikube dashboard --url` | Get dashboard URL |
| `minikube service <service-name>` | Access a service |
| `minikube service <service-name> --url` | Get service URL |
| `minikube service list` | List all service URLs |
| `minikube tunnel` | Create route to services with LoadBalancer type |

### Addons and Configurations

| Command | Description |
|---------|-------------|
| `minikube addons list` | List available addons |
| `minikube addons enable <addon-name>` | Enable addon (e.g., metrics-server, ingress) |
| `minikube addons disable <addon-name>` | Disable addon |
| `minikube addons configure <addon-name>` | Configure addon |
| `minikube addons enable ingress` | Enable ingress controller |
| `minikube addons enable metrics-server` | Enable metrics-server |
| `minikube addons enable registry` | Enable Docker registry |
| `minikube addons enable dashboard` | Enable K8s dashboard |
| `minikube addons enable istio` | Enable Istio service mesh |
| `minikube addons enable ambassador` | Enable Ambassador API Gateway |
| `minikube config view` | Show minikube config |
| `minikube config set memory 4096` | Set memory allocation |
| `minikube config set cpus 4` | Set CPU allocation |
| `minikube config set driver docker` | Set default driver |
| `minikube config set kubernetes-version latest` | Set K8s version |
| `minikube config unset <key>` | Unset configuration |

### Image Management

| Command | Description |
|---------|-------------|
| `minikube image list` | List available images |
| `minikube image build -t image:tag /path/to/Dockerfile` | Build image |
| `minikube image pull <image-name>` | Pull an image |
| `minikube image load <local-image>` | Load local image into minikube |
| `minikube image rm <image-name>` | Remove an image |
| `minikube image tag <source> <target>` | Tag an image |
| `minikube image ls --format table` | List images in table format |
| `minikube cache list` | List cached images |
| `minikube cache add <image>` | Add image to cache |
| `minikube cache reload` | Reload cache images |

### Storage and Mounts

| Command | Description |
|---------|-------------|
| `minikube mount <source>:<target>` | Mount local directory into cluster |
| `minikube mount --uid=1000 --gid=1000 <source>:<target>` | Mount with specific user/group |
| `minikube mount --mode=775 <source>:<target>` | Mount with specific permissions |
| `minikube node add` | Add node to cluster |
| `minikube node delete` | Delete node from cluster |
| `minikube node list` | List nodes in cluster |
| `minikube node start <node-name>` | Start existing node |
| `minikube node stop <node-name>` | Stop specific node |

### Profiles and Context

| Command | Description |
|---------|-------------|
| `minikube update-context` | Update kubeconfig |
| `minikube profile list` | List all profiles |
| `minikube profile <name>` | Set current profile |
| `minikube profile <name> --no-kubernetes` | Create profile without K8s |
| `minikube -p <profile> start` | Start specific profile |
| `minikube -p <profile> stop` | Stop specific profile |
| `minikube -p <profile> delete` | Delete specific profile |

### Troubleshooting

| Command | Description |
|---------|-------------|
| `minikube update-check` | Check for minikube updates |
| `minikube start --alsologtostderr -v=3` | Start with verbose logging |
| `minikube ssh 'sudo systemctl restart kubelet'` | Restart kubelet service |
| `minikube ip --node=minikube-m02` | Get specific node IP |
| `minikube kubectl -- get pods` | Use bundled kubectl |
| `minikube logs --problems=true` | Show only problem logs |
| `minikube status -f {{.Host}}` | Format status output |

---

## Kubectl Commands

### Cluster Management

| Command | Description |
|---------|-------------|
| `kubectl version` | Show kubectl version |
| `kubectl cluster-info` | Display cluster info |
| `kubectl cluster-info dump` | Dump detailed cluster info |
| `kubectl config view` | Show kubeconfig settings |
| `kubectl config current-context` | Show current context |
| `kubectl config use-context <context>` | Switch to specific context |
| `kubectl config set-context <context>` | Set a context |
| `kubectl config get-contexts` | List available contexts |
| `kubectl api-resources` | List all resources/APIs |
| `kubectl api-versions` | List API versions |

### Node Operations

| Command | Description |
|---------|-------------|
| `kubectl get nodes` | List all nodes |
| `kubectl get nodes -o wide` | List nodes with more info |
| `kubectl describe node <node-name>` | Show details of a node |
| `kubectl drain <node-name>` | Drain node for maintenance |
| `kubectl cordon <node-name>` | Mark node as unschedulable |
| `kubectl uncordon <node-name>` | Mark node as schedulable |
| `kubectl top node` | Show node resource usage |
| `kubectl taint node <node-name> <key>=<value>:<effect>` | Add taint to node |
| `kubectl taint node <node-name> <key>:<effect>-` | Remove taint from node |

### Namespace Operations

| Command | Description |
|---------|-------------|
| `kubectl get namespaces` or `kubectl get ns` | List all namespaces |
| `kubectl create namespace <name>` or `kubectl create ns <name>` | Create namespace |
| `kubectl delete namespace <name>` | Delete namespace |
| `kubectl config set-context --current --namespace=<namespace>` | Switch namespace |

### Pod Operations

| Command | Description |
|---------|-------------|
| `kubectl get pods` | List all pods in current namespace |
| `kubectl get pods -A` or `--all-namespaces` | List pods in all namespaces |
| `kubectl get pods -n <namespace>` | List pods in specific namespace |
| `kubectl get pods -o wide` | List pods with more details |
| `kubectl get pods --show-labels` | Show pod labels |
| `kubectl get pods -l key=value` | Filter pods by label |
| `kubectl run <name> --image=<image>` | Create and run a pod |
| `kubectl describe pod <pod-name>` | Show pod details |
| `kubectl logs <pod-name>` | View pod logs |
| `kubectl logs -f <pod-name>` | Stream pod logs |
| `kubectl logs <pod-name> -c <container-name>` | View specific container logs |
| `kubectl exec -it <pod-name> -- <command>` | Execute command in pod |
| `kubectl exec -it <pod-name> -c <container> -- <command>` | Execute command in specific container |
| `kubectl port-forward pod/<pod-name> <local-port>:<pod-port>` | Forward local port to pod |
| `kubectl delete pod <pod-name>` | Delete pod |
| `kubectl delete pod <pod-name> --force --grace-period=0` | Force delete pod |
| `kubectl top pod` | Show pod resource usage |

### Deployment Operations

| Command | Description |
|---------|-------------|
| `kubectl get deployments` | List deployments |
| `kubectl get deployments -n <namespace>` | List deployments in namespace |
| `kubectl describe deployment <name>` | Show deployment details |
| `kubectl create deployment <name> --image=<image>` | Create deployment |
| `kubectl scale deployment/<name> --replicas=<count>` | Scale deployment |
| `kubectl set image deployment/<name> <container>=<image>` | Update container image |
| `kubectl rollout status deployment/<name>` | Check rollout status |
| `kubectl rollout history deployment/<name>` | View rollout history |
| `kubectl rollout undo deployment/<name>` | Rollback to previous version |
| `kubectl rollout undo deployment/<name> --to-revision=<number>` | Rollback to specific revision |
| `kubectl rollout restart deployment/<name>` | Restart all pods in deployment |
| `kubectl delete deployment <name>` | Delete deployment |

### Service Operations

| Command | Description |
|---------|-------------|
| `kubectl get services` or `kubectl get svc` | List all services |
| `kubectl get services -n <namespace>` | List services in namespace |
| `kubectl describe service <name>` | Show service details |
| `kubectl expose deployment <name> --port=<port> --target-port=<target>` | Create service for deployment |
| `kubectl delete service <name>` | Delete service |
| `kubectl port-forward service/<name> <local-port>:<service-port>` | Forward local port to service |
| `kubectl port-forward service/<name> <port>:<port> --address=0.0.0.0` | Forward port accessible from outside |

### ConfigMap and Secret Operations

| Command | Description |
|---------|-------------|
| `kubectl get configmaps` or `kubectl get cm` | List configmaps |
| `kubectl create configmap <name> --from-file=<path>` | Create configmap from file |
| `kubectl create configmap <name> --from-literal=key=value` | Create configmap from literal |
| `kubectl get secrets` | List secrets |
| `kubectl create secret generic <name> --from-literal=key=value` | Create secret from literal |
| `kubectl create secret tls <name> --cert=<path> --key=<path>` | Create TLS secret |

### ReplicaSet Operations

| Command | Description |
|---------|-------------|
| `kubectl get replicasets` or `kubectl get rs` | List replicasets |
| `kubectl scale replicaset/<name> --replicas=<count>` | Scale replicaset |
| `kubectl delete replicaset <name>` | Delete replicaset |

### StatefulSet Operations

| Command | Description |
|---------|-------------|
| `kubectl get statefulsets` or `kubectl get sts` | List statefulsets |
| `kubectl scale statefulset/<name> --replicas=<count>` | Scale statefulset |
| `kubectl delete statefulset <name>` | Delete statefulset |

### DaemonSet Operations

| Command | Description |
|---------|-------------|
| `kubectl get daemonsets` or `kubectl get ds` | List daemonsets |
| `kubectl describe daemonset <name>` | Show daemonset details |
| `kubectl delete daemonset <name>` | Delete daemonset |

### Job & CronJob Operations

| Command | Description |
|---------|-------------|
| `kubectl get jobs` | List jobs |
| `kubectl get cronjobs` | List cronjobs |
| `kubectl create job <name> --image=<image>` | Create job |
| `kubectl delete job <name>` | Delete job |
| `kubectl delete cronjob <name>` | Delete cronjob |

### Storage Operations

| Command | Description |
|---------|-------------|
| `kubectl get persistentvolumes` or `kubectl get pv` | List persistent volumes |
| `kubectl get persistentvolumeclaims` or `kubectl get pvc` | List persistent volume claims |
| `kubectl get storageclass` or `kubectl get sc` | List storage classes |
| `kubectl describe pv <name>` | Show PV details |
| `kubectl describe pvc <name>` | Show PVC details |

### Ingress Operations

| Command | Description |
|---------|-------------|
| `kubectl get ingress` or `kubectl get ing` | List ingress resources |
| `kubectl describe ingress <name>` | Show ingress details |
| `kubectl delete ingress <name>` | Delete ingress |

### RBAC Operations

| Command | Description |
|---------|-------------|
| `kubectl get roles` | List roles |
| `kubectl get rolebindings` | List role bindings |
| `kubectl get clusterroles` | List cluster roles |
| `kubectl get clusterrolebindings` | List cluster role bindings |
| `kubectl create role <name> --verb=<verbs> --resource=<resources>` | Create role |
| `kubectl create rolebinding <name> --role=<role> --user=<user>` | Create role binding |
| `kubectl auth can-i <verb> <resource>` | Check permissions |
| `kubectl auth can-i <verb> <resource> --as=<user>` | Check permissions for user |
| `kubectl auth whoami` | Show current user |

### Utility Commands

| Command | Description |
|---------|-------------|
| `kubectl apply -f <file.yaml>` | Apply resource from file |
| `kubectl apply -f <directory>` | Apply resources from directory |
| `kubectl apply -f <url>` | Apply resources from URL |
| `kubectl create -f <file.yaml>` | Create resource from file |
| `kubectl delete -f <file.yaml>` | Delete resource from file |
| `kubectl diff -f <file.yaml>` | Show differences before applying |
| `kubectl explain <resource>` | Get documentation for resource |
| `kubectl kustomize <kustomization_directory>` | Build kustomization |
| `kubectl get all` | Get all resources |
| `kubectl get all -n <namespace>` | Get all resources in namespace |
| `kubectl get all --all-namespaces` or `-A` | Get all resources in all namespaces |
| `kubectl label <resource> <name> key=value` | Add label to resource |
| `kubectl annotate <resource> <name> key=value` | Add annotation |
| `kubectl wait --for=condition=<condition> <resource>/<name>` | Wait for condition |
| `kubectl cp <pod-name>:/path /local/path` | Copy files from pod |
| `kubectl cp /local/path <pod-name>:/path` | Copy files to pod |

---

## Amazon EKS Commands

### EKS CLI Setup

| Command | Description |
|---------|-------------|
| `aws configure` | Configure AWS CLI credentials |
| `curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" \| tar xz -C /tmp` | Download eksctl |
| `sudo mv /tmp/eksctl /usr/local/bin` | Install eksctl |
| `eksctl version` | Check eksctl version |

### EKS Cluster Operations

| Command | Description |
|---------|-------------|
| `eksctl create cluster --name=<name> --region=<region> --nodes=<count>` | Create EKS cluster |
| `eksctl create cluster -f cluster.yaml` | Create cluster from config file |
| `eksctl get cluster [--name=<name>] [--region=<region>]` | List EKS clusters |
| `eksctl delete cluster --name=<name> --region=<region>` | Delete EKS cluster |
| `eksctl scale nodegroup --cluster=<name> --nodes=<count> --name=<nodegroup>` | Scale nodegroup |
| `eksctl update cluster --name=<name> --region=<region>` | Update cluster |
| `eksctl utils update-kube-proxy --cluster=<name> --region=<region>` | Update kube-proxy |
| `eksctl utils update-aws-node --cluster=<name> --region=<region>` | Update aws-node DaemonSet |
| `eksctl utils update-coredns --cluster=<name> --region=<region>` | Update CoreDNS |

### EKS NodeGroup Operations

| Command | Description |
|---------|-------------|
| `eksctl create nodegroup --cluster=<name> --region=<region> --name=<nodegroup>` | Create nodegroup |
| `eksctl get nodegroup --cluster=<name> --region=<region>` | List nodegroups |
| `eksctl delete nodegroup --cluster=<name> --region=<region> --name=<nodegroup>` | Delete nodegroup |
| `eksctl drain nodegroup --cluster=<name> --region=<region> --name=<nodegroup>` | Drain nodegroup |

### EKS IAM Operations

| Command | Description |
|---------|-------------|
| `eksctl create iamidentitymapping --cluster=<name> --region=<region> --arn=<arn> --group=<group>` | Create IAM identity mapping |
| `eksctl get iamidentitymapping --cluster=<name> --region=<region>` | Get IAM identity mappings |
| `eksctl delete iamidentitymapping --cluster=<name> --region=<region> --arn=<arn>` | Delete IAM identity mapping |
| `eksctl create iamserviceaccount --cluster=<name> --region=<region> --name=<sa-name> --namespace=<ns> --attach-policy-arn=<policy>` | Create IAM service account |

### EKS Fargate Operations

| Command | Description |
|---------|-------------|
| `eksctl create fargateprofile --cluster=<name> --region=<region> --name=<profile> --namespace=<ns>` | Create Fargate profile |
| `eksctl get fargateprofile --cluster=<name> --region=<region>` | List Fargate profiles |
| `eksctl delete fargateprofile --cluster=<name> --region=<region> --name=<profile>` | Delete Fargate profile |

### AWS EKS Console Commands

| Command | Description |
|---------|-------------|
| `aws eks update-kubeconfig --name <cluster-name> --region <region>` | Update kubeconfig for EKS cluster |
| `aws eks list-clusters --region <region>` | List all EKS clusters |
| `aws eks describe-cluster --name <cluster-name> --region <region>` | Describe EKS cluster |
| `aws eks list-nodegroups --cluster-name <cluster-name> --region <region>` | List nodegroups |
| `aws eks describe-nodegroup --cluster-name <cluster-name> --nodegroup-name <nodegroup> --region <region>` | Describe nodegroup |
| `aws eks list-addons --cluster-name <cluster-name> --region <region>` | List cluster addons |
| `aws eks describe-addon --cluster-name <cluster-name> --addon-name <addon> --region <region>` | Describe addon |
| `aws eks create-addon --cluster-name <cluster-name> --addon-name <addon> --region <region>` | Create addon |
| `aws eks delete-addon --cluster-name <cluster-name> --addon-name <addon> --region <region>` | Delete addon |

---

## Kubernetes Core Concepts

### Architecture
- **Master Node Components**
  - kube-apiserver: API server that exposes the Kubernetes API
  - etcd: Key-value store for all cluster data
  - kube-scheduler: Assigns pods to nodes
  - kube-controller-manager: Runs controller processes
  - cloud-controller-manager: Interacts with cloud providers

- **Worker Node Components**
  - kubelet: Agent that ensures containers are running in a pod
  - kube-proxy: Network proxy that maintains network rules
  - Container Runtime: Software responsible for running containers (Docker, containerd, CRI-O)

### Kubernetes Evolution
- Originally developed by Google (based on internal system called Borg)
- Released as open-source in 2014
- Now maintained by Cloud Native Computing Foundation (CNCF)

### Workload Types
- **Monolithic vs Microservices**
  - Monolithic: Single, unified application
  - Microservices: Multiple independent services working together

### Scheduling
- **Pod Scheduling**
  - Based on resource requests and limits
  - Node selector and affinity/anti-affinity
  - Taints and tolerations
  - Node conditions and pod conditions

---

## Kubernetes Resource Types

### Pods
- Smallest deployable unit in Kubernetes
- Can contain one or more containers
- Share network namespace, IPC, and hostname
- Ephemeral (not designed to survive failures)

### ReplicaSets
- Ensures a specified number of pod replicas are running
- Provides high availability
- Supports rolling updates

### Deployments
- Manages ReplicaSets
- Provides declarative updates for pods and ReplicaSets
- Supports rollout and rollback
- Maintains deployment history

### StatefulSets
- Manages stateful applications
- Maintains a sticky identity for each pod
- Provides ordered deployment and scaling
- Used for applications that need stable, unique network identifiers, stable persistent storage, and ordered deployment/scaling

### DaemonSets
- Ensures all nodes run a copy of a specific pod
- Used for node-level monitoring, logging, and cluster storage
- Examples: node exporter, fluentd, storage daemons

### Jobs and CronJobs
- **Jobs**: Run-to-completion tasks
- **CronJobs**: Jobs that run on a time-based schedule

### ConfigMaps and Secrets
- **ConfigMaps**: Store non-confidential configuration data
- **Secrets**: Store sensitive information (encoded in base64)

### Services
- Provide stable network endpoint for pods
- Types:
  - ClusterIP: Internal access only
  - NodePort: External access via node IP and port
  - LoadBalancer: External access via cloud provider load balancer
  - ExternalName: Maps to external DNS name

### Ingress
- Manages external access to services
- HTTP/HTTPS routing
- SSL termination
- Name-based virtual hosting

### Volumes and Persistent Volumes
- **Volumes**: Directory accessible to containers in a pod
- **PersistentVolumes (PV)**: Storage resource in the cluster
- **PersistentVolumeClaims (PVC)**: Request for storage by a user

### Custom Resource Definitions (CRDs)
- Extend Kubernetes API with custom resources
- Define new resource types
- Used by operators and controllers

---

## Kubernetes YAML Definitions

### Pod YAML Example
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
  labels:
    app: nginx
spec:
  containers:
  - name: nginx
    image: nginx:latest
    ports:
    - containerPort: 80
    resources:
      limits:
        cpu: "0.5"
        memory: "256Mi"
      requests:
        cpu: "0.1"
        memory: "128Mi"
```

### Deployment YAML Example
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:latest
        ports:
        - containerPort: 80
```

### Service YAML Example
```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  type: ClusterIP
  selector:
    app: nginx
  ports:
  - port: 80
    targetPort: 80
```

### ConfigMap YAML Example
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
data:
  app.properties: |
    key1=value1
    key2=value2
  config.json: |
    {
      "key": "value"
    }
```

### Secret YAML Example
```yaml
apiVersion: v1
kind: Secret
metadata:
  name: app-secret
type: Opaque
data:
  username: YWRtaW4=  # base64 encoded "admin"
  password: cGFzc3dvcmQ=  # base64 encoded "password"
```

### PersistentVolumeClaim YAML Example
```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: app-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
  storageClassName: standard
```

### Ingress YAML Example
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: app-ingress
spec:
  rules:
  - host: app.example.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: app-service
            port:
              number: 80
```

---

## Kubernetes Networking

### Pod Networking
- Each pod has its own IP address
- Containers within pod share network namespace
- Containers can communicate using localhost

### Service Discovery
- DNS-based service discovery
- Environment variables
- Kubernetes DNS service resolves service names to IPs

### Network Policies
- Control traffic flow to and from pods
- Similar to firewall rules
- Can restrict traffic based on namespaces, labels

### Service Mesh
- Advanced networking capabilities
- Examples: Istio, Linkerd, Consul
- Features: traffic management, security, observability

---

## Kubernetes Storage

### Storage Classes
- Define different classes of storage
- Provisioner determines how volumes are created
- Parameters define storage-specific configurations

### Volume Types
- **emptyDir**: Temporary directory that shares pod lifetime
- **hostPath**: Mounts file or directory from host node's filesystem
- **awsElasticBlockStore**: AWS EBS volume
- **azureDisk**: Azure Disk volume
- **gcePersistentDisk**: GCE Persistent Disk
- **nfs**: NFS share
- **persistentVolumeClaim**: Claims a PersistentVolume
- Many others depending on environment

### Storage Operators
- Manage storage resources
- Examples: Rook, OpenEBS, Portworx
- Provide storage services on top of Kubernetes

---

## Kubernetes Security

### RBAC (Role-Based Access Control)
- **Roles**: Permissions within a namespace
- **ClusterRoles**: Cluster-wide permissions
- **RoleBindings**: Bind roles to users in a namespace
- **ClusterRoleBindings**: Bind cluster roles to users

### Service Accounts
- Identity for processes running in pods
- Automatically mounted into pods
- Used for pod-level permissions

### Pod Security
- **SecurityContext**: Container-level security settings
- **PodSecurityPolicies** (deprecated)/Pod Security Standards: Cluster-level pod security settings
- **NetworkPolicies**: Control traffic to/from pods

### Secrets Management
- Kubernetes Secrets
- External secrets managers (HashiCorp Vault, AWS Secrets Manager)
- Key management services

---

## Kubernetes Monitoring

### Resource Metrics
- **Metrics Server**: Basic CPU and memory metrics
- **Prometheus**: Advanced metrics collection and storage
- **Grafana**: Metrics visualization

### Probes
- **Liveness Probe**: Determines if container is running
- **Readiness Probe**: Determines if container is ready to receive traffic
- **Startup Probe**: Determines if container has started

### Logging
- Container logs
- Node-level logging
- Cluster-level logging solutions (EFK stack, Loki)

### Tracing
- Distributed tracing
- Examples: Jaeger, Zipkin

### Autoscaling
- **Horizontal Pod Autoscaler (HPA)**: Scale number of pods
- **Vertical Pod Autoscaler (VPA)**: Scale pod resources
- **Cluster Autoscaler**: Scale number of nodes
- **KEDA**: Event-driven autoscaling

---

## Kubernetes Package Management

### Helm
- Package manager for Kubernetes
- **Charts**: Packages of pre-configured Kubernetes resources
- **Releases**: Instances of charts running in a cluster
- **Repositories**: Collections of charts

#### Helm Commands

| Command | Description |
|---------|-------------|
| `helm version` | Show Helm version |
| `helm create <chart-name>` | Create a new chart |
| `helm package <chart-path>` | Package a chart directory into chart archive |
| `helm install <release-name> <chart>` | Install a chart |
| `helm install <release-name> <chart> -n <namespace>` | Install chart in namespace |
| `helm install <release-name> <chart> --create-namespace -n <namespace>` | Install chart and create namespace |
| `helm list` or `helm ls` | List releases |
| `helm list -n <namespace>` | List releases in namespace |
| `helm upgrade <release-name> <chart>` | Upgrade a release |
| `helm rollback <release-name> <revision>` | Rollback a release to specific revision |
| `helm uninstall <release-name>` | Uninstall a release |
| `helm repo list` | List chart repositories |
| `helm repo add <repo-name> <url>` | Add chart repository |
| `helm repo update` | Update information of available charts |
| `helm search repo <keyword>` | Search repositories for charts |
| `helm pull <chart>` | Download a chart |
| `helm show values <chart>` | Show chart values |
| `helm get values <release-name>` | Show release values |
| `helm template <chart>` | Locally render templates |
| `helm history <release-name>` | Show release history |

### Kustomize
- Configuration customization for Kubernetes
- Overlay-based approach to configuration
- Built into `kubectl` (`kubectl apply -k`)

---

## Advanced Pod Management

### Init Containers

Init containers run and complete before application containers start. They are used for setup tasks like database schema creation, permissions settings, or dependency checks.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: init-pod
spec:
  initContainers:
  - name: init-service
    image: busybox:1.34.1
    command: ['sh', '-c', 'until nslookup myservice; do echo waiting for myservice; sleep 2; done;']
  - name: init-database
    image: busybox:1.34.1
    command: ['sh', '-c', 'until nslookup mydb; do echo waiting for mydb; sleep 2; done;']
  containers:
  - name: app
    image: myapp:latest
```

| Command | Description |
|---------|-------------|
| `kubectl get pod init-pod -c init-service` | Reference specific init container |
| `kubectl logs pod/init-pod -c init-service` | View logs from init container |
| `kubectl describe pod/init-pod` | Check init container status |

### Sidecar Containers

Sidecar containers extend and enhance the main container, such as for logging, monitoring, or security.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: sidecar-pod
spec:
  containers:
  - name: main-app
    image:

---

## Useful Resources

- [Kubernetes Documentation](https://kubernetes.io/docs/)
- [Minikube Documentation](https://minikube.sigs.k8s.io/docs/)
- [Amazon EKS Documentation](https://docs.aws.amazon.com/eks/)
- [eksctl Documentation](https://eksctl.io/)
- [Helm Documentation](https://helm.sh/docs/)
- [CNCF Landscape](https://landscape.cncf.io/)
- [kubectl Cheat Sheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)