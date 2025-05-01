# Kubernetes, Minikube, and EKS Cheatsheet

## Minikube Commands

### Cluster Management
- `minikube start` - Start a local Kubernetes cluster
- `minikube stop` - Stop the cluster
- `minikube delete` - Delete the cluster
- `minikube dashboard` - Launch the Kubernetes dashboard
- `minikube addons list` - List all available addons
- `minikube addons enable <addon-name>` - Enable an addon
- `minikube addons disable <addon-name>` - Disable an addon
- `minikube ip` - Get IP address of the Minikube cluster

### Image Management
- `minikube image load <image-name>` - Load a local Docker image into Minikube
- `minikube image build -t <image-name> .` - Build Docker image inside Minikube environment

### Accessing Services
- `minikube service <service-name>` - Open the exposed service in the browser
- `minikube tunnel` - Create a network tunnel to access LoadBalancer service type

---

## Kubectl Commands

### Basic Cluster Info
- `kubectl cluster-info` - Display cluster info
- `kubectl config view` - View kubeconfig file
- `kubectl get nodes` - List nodes
- `kubectl get namespaces` - List all namespaces

### Namespace Management
- `kubectl create namespace <name>`
- `kubectl delete namespace <name>`
- `kubectl config set-context --current --namespace=<name>`

### Pod & Deployment Management
- `kubectl get pods` - List pods
- `kubectl get deployments` - List deployments
- `kubectl get services` - List services
- `kubectl describe pod <pod-name>` - Pod details
- `kubectl logs <pod-name>` - View logs
- `kubectl exec -it <pod-name> -- /bin/bash` - Access pod shell
- `kubectl apply -f <file.yaml>` - Apply config
- `kubectl delete -f <file.yaml>` - Delete resources defined in file
- `kubectl scale deployment <deployment-name> --replicas=<n>` - Scale a deployment
- `kubectl rollout restart deployment <deployment-name>` - Restart pods in a deployment

### Port Forwarding
- `kubectl port-forward <pod-name> <local-port>:<pod-port>`

### Service Account and Role Binding
- `kubectl create sa <name>` - Create service account
- `kubectl create clusterrolebinding <name> --clusterrole=cluster-admin --serviceaccount=<namespace>:<sa-name>`

---

## Helm Commands

### Installation & Setup
- `helm repo add <repo-name> <repo-url>` - Add repo
- `helm repo update` - Update repos
- `helm install <release-name> <chart>` - Install a chart
- `helm uninstall <release-name>` - Uninstall release
- `helm list` - List releases
- `helm upgrade <release-name> <chart>` - Upgrade release
- `helm rollback <release-name> <revision>` - Rollback to previous revision
- `helm create <chart-name>` - Create new chart scaffold

---

## EKS CLI (eksctl) Commands

- `eksctl get cluster` - List clusters
- `aws eks update-kubeconfig --region <region> --name <cluster-name>` - Update kubeconfig to access EKS
- `aws eks get-token --cluster-name <cluster-name>` - Get authentication token for the cluster

---

## Kubernetes Core Concepts

### Containers
- **Init Containers**: Run before app containers in a pod; used for setup logic.
- **Sidecar Containers**: Run alongside main app containers to support functionality like logging, syncing, proxying, etc.

### Probes
- **Liveness Probe**: Checks if app is running. If fails, container is restarted.
- **Readiness Probe**: Checks if app is ready to accept traffic.
- **Startup Probe**: Used for apps that take long to start; disables other probes until it succeeds.

### Autoscaling
- **Horizontal Pod Autoscaler (HPA)**: Scales pods based on CPU/memory/custom metrics.
  - `kubectl autoscale deployment <deployment> --cpu-percent=<threshold> --min=<min> --max=<max>`
- **Cluster Autoscaler**: Adds/removes nodes based on resource requests.

### RBAC (Role-Based Access Control)
- **Roles & ClusterRoles**: Define permissions within a namespace or cluster-wide.
- **RoleBinding & ClusterRoleBinding**: Bind roles to users/service accounts/groups.

### Volumes
- **EmptyDir**: Temporary space for a pod
- **hostPath**: Mount host filesystem
- **ConfigMap**: Inject configuration data
- **Secret**: Inject sensitive data
- **PersistentVolume (PV)** & **PersistentVolumeClaim (PVC)**: Manage durable storage

### Resource Definitions
- **Deployment**: Manages pod replicas and updates
- **StatefulSet**: Like Deployment but preserves state and identity
- **DaemonSet**: Ensures one pod per node
- **Job/CronJob**: For batch and scheduled jobs

### Network Policies
- Define rules for pod-to-pod communication

### Ingress
- Route external traffic to services based on path/host rules

---

## Debugging & Troubleshooting
- `kubectl get events` - View events for debugging
- `kubectl describe <resource> <name>` - Detailed view
- `kubectl top pod` - Show resource usage
- `kubectl get all` - View all resources in namespace
- `kubectl get pod -o wide` - View pod node info and IPs



