Here's the formatted content for your Kubernetes and Minikube commands in a README file:

---

# Kubernetes & Minikube Commands Cheatsheet

This document includes essential commands for working with Minikube, Kubernetes (kubectl), Helm, and various Kubernetes services and concepts.

## Minikube Commands

- `minikube start`: Start the Minikube cluster.
- `minikube delete`: Delete the Minikube cluster.
- `minikube stop`: Stop the Minikube cluster without deleting the data.
- `minikube logs`: View the Minikube logs.
- `minikube service <service-name>`: Access a service running in Minikube.
- `minikube addons enable metrics-server`: Enable the metrics-server in Minikube.
- `minikube addons enable ingress`: Enable ingress for routing services in Minikube.
- `minikube image list`: List all images in Minikube.
- `minikube image pull <image-name>`: Pull an image to Minikube.
- `minikube image rm <image-name>`: Remove an image from Minikube.
- `minikube image list --format table`: List images in a table format.

## Kubectl Commands

- `kubectl get all --all-namespaces`: Get all resources in all namespaces.
- `kubectl get all --all-namespaces -o wide`: Get all resources with more details.
- `kubectl cluster-info`: Get information about the cluster.
- `kubectl cluster-info --context <cluster-name>`: Get info for a specific cluster context.
- `kubectl get nodes`: Get information about worker nodes.
- `kubectl run <pod-name> --image=<image-name>`: Run a pod with a specific image.
- `kubectl get namespace | ns`: Get namespaces.
- `kubectl get pods`: List all pods.
- `kubectl get pods -n <namespace>`: List pods in a specific namespace.
- `kubectl create ns <namespace-name>`: Create a new namespace.
- `kubectl delete pod <pod-name>`: Delete a specific pod.
- `kubectl run <pod-name> --image=<image-name> -n <namespace>`: Run a pod in a specific namespace.
- `kubectl delete pod <pod-name> -n <namespace>`: Delete a pod in a specific namespace.
- `kubectl delete ns <namespace-name>`: Delete a namespace.
- `kubectl apply -f <filename>.yml`: Apply a configuration file (pod, deployment, etc.).
- `kubectl exec -it <pod-name> -n <namespace> -- bash`: Execute a command in a pod.
- `kubectl scale deployment <deployment-name> -n <namespace> --replicas=<count>`: Scale a deployment.
- `kubectl set image deployment/<deployment-name> -n <namespace> <container-name>=<image-name>`: Update the image of a deployment.
- `kubectl get deployment -n <namespace>`: Get deployments in a specific namespace.
- `kubectl get replicasets -n <namespace>`: Get replica sets in a specific namespace.
- `kubectl get service | svc`: List all services.
- `kubectl apply -f ingress.yml`: Apply an ingress configuration file.
- `kubectl get ingress/ing`: Get all ingress controllers.
- `kubectl taint node <node-name> <key>=<value>:<effect>`: Taint a node.
- `kubectl top node/pod`: View resource metrics for nodes or pods.
- `kubectl get secrets -n <namespace>`: Get secrets in a specific namespace.
- `kubectl auth whoami`: Get the current authenticated user.
- `kubectl auth can-i <action> <resource>`: Check if a user has permission for a specific action.
  
## Helm Commands

- `helm version`: Get the current version of Helm.
- `helm create <project-name>`: Create a new Helm chart project.
- `helm package .`: Package the current Helm project into a `.tgz` file.
- `helm install <release-name> <chart-name>`: Install a Helm chart in your Kubernetes cluster.
- `helm uninstall <release-name>`: Uninstall a Helm release.
- `helm install <release-name> <chart-name> -n <namespace> --create-namespace`: Install a Helm chart in a specific namespace and create the namespace if it doesn't exist.
- `helm upgrade <release-name> <chart-path> -n <namespace>`: Upgrade an existing Helm release.
- `helm rollback <release-name> <revision> -n <namespace>`: Rollback a Helm release to a previous revision.
- `helm repo list`: List all Helm repositories.
- `helm list -n <namespace>`: List all releases in a specific namespace.
- `helm install mongodb-helm oci:registry-1.docker.io/bitnamicharts/mongodb -n <namespace>`: Install MongoDB using a Helm chart from an external registry.

## Core Kubernetes Concepts

- **Monolithic vs Microservices**: Monolithic is a single service, while microservices are multiple independent services working together.
- **Node**: A node is a machine (VM or physical) in your Kubernetes cluster.
- **Pod**: A pod is the smallest deployable unit in Kubernetes, running one or more containers.
- **Deployment**: A Kubernetes Deployment provides declarative updates for Pods and ReplicaSets.
- **Service**: A service in Kubernetes is an abstraction that defines a logical set of pods and enables network access to them.
- **Namespace**: A Kubernetes namespace provides a way to divide cluster resources between multiple users.
- **StatefulSet**: A StatefulSet is used for managing stateful applications where the order of pod deployment matters.
- **ConfigMap**: A Kubernetes ConfigMap is used to store non-sensitive configuration data in key-value pairs.
- **Secrets**: A Kubernetes Secret is used to store sensitive information such as passwords or API keys in a base64 encoded format.
- **Persistent Volumes (PV) & Persistent Volume Claims (PVC)**: Used for storage in Kubernetes, enabling persistent storage even after pods are destroyed.
- **Horizontal Pod Autoscaler (HPA)**: Automatically scales the number of pods in a deployment based on observed CPU utilization or other select metrics.
- **Vertical Pod Autoscaler (VPA)**: Adjusts the CPU and memory requests for containers based on usage.
- **Taints & Tolerations**: Taints allow nodes to repel certain pods, and tolerations allow pods to be scheduled on tainted nodes.
- **Ingress**: Ingress exposes HTTP and HTTPS routes from outside the cluster to services within the cluster.

## Kubernetes Probes

- **Readiness Probe**: Determines if a pod is ready to handle traffic.
- **Liveness Probe**: Determines if a pod is alive or dead.
- **Startup Probe**: Determines if a pod is starting or still initializing.

## Cluster Dashboard

- **To install Kubernetes Dashboard**:
  ```bash
  kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.7.0/aio/deploy/recommended.yaml
  ```
  
- **Create an Admin User for Dashboard**:
  ```bash
  kubectl apply -f dashboard-admin-user.yml
  ```

- **Get Token to Login**:
  ```bash
  kubectl -n kubernetes-dashboard create token admin-user
  ```

- **Access the Dashboard**:
  ```bash
  kubectl proxy
  ```

  Visit: [http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/](http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/)

