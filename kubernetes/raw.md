Minikube 
minikube start 
Minikube delete 
Minikube stop 
Minikube logs 
minikube service react-app-service
minikube addons enable metrics-server = to enable metrice server in minikube server
minikube addons enable ingress 
minikube image list 
minikube image pull imageName 
minikube image rm imageName 
minikube image list --format table 
Kubectl 
kubectl get all --all-namespaces = to get all resources
kubectl get all --all-namespaces -o wide = to get all resources with more details 
kubectl cluster-info = to get cluster info 
kubectl cluster-info --context clusterName = to get info 
kubectl get nodes = to get worker node info 
kubectl run node --image=node:latest = to run node pods 
kubectl get namespace Or ns = to get namespace 
kubectl get pods = to get pods 
kubectl get pods -n namespace = to get pods of particular ns
kubectl create ns addifly = to create a namespace named addilfy 
kubectl run nginx --image=nginx:latest = to run nginx pods
kubectl delete pod nginx = to delete the pods of nginx
kubectl run nginx --image=nginx:latest -n nginx = to run nginx pods in namespace nginx
kubectl delete pod nginx -n nginx = to delete pods 
kubectl delete ns nginx = to delete namespce 
kubectl apply/create -f namespace.yml = to create a namespace 
kubectl apply/create -f pod.yml = to create a pod 
kubectl exec -it nginx -n nginx -- bash = to interact with pod
kubectl delete -f namespace.yml = to delete a namespace 
kubectl apply -f deployment.yml = to developy 
kubectl get deployment = to get deployment
 kubectl get deployment -n node = to get deployment in namespace named node 
kubectl scale deployment/depolement-Name -n node --replicas=12 = to scale deployment to 12  
kubectl get pods -n node -o wide = for more information 
kubectl set image deployment/depolement-Name -n node nginx=nginx:1.27.3 = to update the image to use 1.27.3 image of pods
kubectl apply -f replica.yml = to apply replica file 
kubectl get replicasets -n node = to get replicasets in node namespace 
kubectl scale replicasets/depolement-Name -n node --replicas=12 = to scale replicasets to 12 
kubectl apply -f job.yml = to apply job yml file 
kubectl logs pod/pod-Name -n node = to get logs of pod 
kubectl apply -f cron-job.yml = to apply cron job yml file
kubectl get cronjob -n node = to get cronjob in node namespace 
kubectl logs pods/pods-name -n node = to get logs of cronjob 
kubectl describe pod/pod-Name -n node = to describe logs of pod in namespace node 
kubectl apply -f pv.yml = to apply pv yml file
kubectl apply -f pvc.yml = to apply pvc yml file
kubectl apply -f service. yml = to apply service yml file
kubectl port-forward service/service-Name -n node 80:80 --address=0.0.0.0 = to forward port to local machine 
kubectl get all -n node = to get all resource 
kubectl get service or svc = to get all services 
kubectl apply -f ingress.yml = to apply ingress yml file
kubectl get ingress/ing = to get all ingress controller 
kubectl get nodes = to get all worker node 
kubectl taint node NODE-WORKER-NAME prod=true:NoSchedule = to taint a worker node in k8s 
kubectl taint node NODE-WORKER-NAME prod=true:NoSchedule- = to untainted a worker node in k8s
kubectl top node/pod = this commad give list of metrics 
kubectl get pods -n kube-system = to check pod in ns kube system 
kubectl get hpa -n apache = to check hpa autoscaling in apache namespace Or usage 
kubectl get vpa -n apache = to check vpa autoscaling in apache namespace  Or usage 
kubectl delete -f dot = to delete all resources 
kubectl auth whoami = to check who am I 
kubectl auth can-i any cmd = to check I can do or not 
kubectl get role = to check type of role in ns Or cluster 
kubectl get serviceaccount = to check which svcacc 
kubectl auth can-i get pods --as=user -n NameSpace = to check permission of user 
kubectl exec -it podName -n addifly -- bash = to interact with pod 
kubectl get all -n ns -o wide = for more info 
kubectl get secrets -n name = to get all secret 
helm package manager 
helm version 
helm create project = to create a helm package 
helm package dot = to create a helm package 
one level up 
helm package project name = to create a helm package
helm install dev-project helm-project-name = to run the helm project 
helm uninstall dev-project =  to delete the helm project
helm install dev-project helm-project-name -n namespace ---create-namespace = to run the helm project in namespace 
helm upgrade project-name  ./apache-package -n prod-apache = to upgrade the helm projects 
helm rollback prd-apache 1 -n namespace = to rollback helm revision of pods 
helm can add external image to run 
helm install mongodb-helm oci:registery-1.docker.io/bitnamicharts/mongodb -n mongo = to run monodb in namespace mongo via helm 
helm repo list = to get list of repo 
helm list -n mongo = to get list in mongo namespace
kubectl get pod init-pod -c main-container 




kubernetes is open source version of Brog made by google in 2014 for container orchestration handle by CNCF 
Core concept 
monolithic = one single website or services 
Mircoservices = multiple services to run a one big services
 1 node = 1 server 
multiple node = cluster 
master node (headquarters) = give task 
worker node (branch) = run dcoker container
Pod = to run docker container or multiple container 
kubernetes services 
kubernetes deployment 
kubernetes pods running 
groups or namespace separated multiple pods and there resources 
deployments in kubernetes 
label and selector and replica 
deployment have rolling update where replicaset don't have rolling update 
deamonsets are give 1 single pods in all worker node are in using if three node and then three pods 
K8s has job which do a task and get close like to say hello or make a log file 
cronjob = do work in schedule job 
k8s have mountVolumme like docker volumne to store data like PV and PVC (persitive volume claim) 
in kubernetes create a persistent volume and then claim it using persistent volume claim and then use it deployment files to use this volume 
every k8s worker node is a docker container or linux machine so exec it and get data of pvc or volume 
create a service file to show the webpage to user 
and do port forwarding like docker port mapping 
ingress = use to divide service in kis with a route two service run a same namspace to run create a ingress file and apply it 
annotation = used in nginx like port 80 for more info or not customized ingress controller code 
k8s have statefullset that are if one pods get delete with same and same volume it create a another pod to run and maintain the state of database 
k8s have configMap = that takes value like env file 
kis have secrets file = that takes value env but in base64 encodeing for privacy 
kubernetes have request and resource quota to better system usage 
Probe is request is to check that pods in running or not 
three type of probe are 
readiness = to check pod is ready or not
liveliness = to check pod in alive or dead 
startup = to check pod in starting or not 
K8s have concept of tainst and toleration 
taint = means ( taana kar n) to able for working 
toleration = means it will work as pods 
Autoscaling in kubernetes 
VPA = vertical pods autoscaling is basic become hulk or large the pod resources for more traffic best used in statefullset like database 
HPA = horizontal pods autoscaling is basic increase the number of running pods to full-fill the request 
Keda = depending to traffic it apply vpa or hpa as requirements 
Node affinity = same work as taint and tolerance and to kind affinity means find same worker to node to run the pod 
To vpa service we need to download a git project for kis github repo and same thing same thing to do 
K8s has RBAC ( role based access control) to any user creating or access control in namespace level or cluster level 
create a user file and create a permission file and create a role binding file to bind them both 
kubernetes have kis dashboard to see visually see that is happening in the k8s cluster 
steps to create k8s dashboard
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.7.0/aio/deploy/recommended.yaml 
apply this yml file for dashboard dowload 
and apply the dashboard file like this 
kubectl apply -f dashboard-admin-user.yml
now create a token to login in dashboard like this 
kubectl -n kubernetes-dashboard create token admin-user
Now create k8s proxy server
kubectl proxy
and visit this url in local machine 
http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/
In k8s we can create our custom resouce definition or crd which one yml file and another yml file to implement 
k8s have helm as package manager of kis cluster 
topic = init container and sidercar container 
init container = init container give initial container to run main container 
sidecar container = side container help main container for store log and other stuff 



 


minikube start to start the services 
minikube stop to stop the service
minikube pause to pause the services without deleting any services 
Minikube unpause to unpauss to services 
minikube status for minikube is running or not