# kube-adm-demo
Independent deployment solution ( GKE, VBox, AWS, Play with k8s ) of two simple multi-tier applications using Kubernetes container orchestration technology

## Deployment Solutions available:

1. GKE (Google Kubernetes Engine) (Preferred and Easy)
2. AWS or any other cloud provider
3. Virtual Box (Local Deployment)
4. play-with-k8s (Remote temporary test deployment)

### Virtual Box Deployment Notes:
1. Please ensure that three or more VM's with a minimum of 1024 MB of RAM are created. (One of these will be a master and the others will be slave nodes)
2. Please ensure that intercommunication between all nodes is enabled. you can do this through Host-only adapter with minimal changes to hosts file.
3. This demo is a kubernetes cluster deployment. So we will be using [Kubeadm](https://kubernetes.io/docs/setup/independent/create-cluster-kubeadm/). Don't use MiniKube.

### Deployment Notes:
1. GKE itself is a cluster manager and orchestration system for running your Docker containers. So there is no need for you to install Kubeadm or minikube. If you are using GKE or play-with-k8s, please skip this section.
2. If you are using AWS or Virtual Box, then you need to install [Kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl) and [Kubeadm](https://kubernetes.io/docs/setup/independent/create-cluster-kubeadm/) on master node. Please note down the join command you get after you run the init command. 
3. Start the Kubeadm on master node using `kubeadm init`. Specify optional parameters to the command if you want to use a different network interface.
4. Establish a pod network to enable intercommunication between pods. There are pre-built solutions that you can take advantage of like Flannel, Weave Net, Calico etc.
5. Run the previously noted join command in each of the slave nodes to make them join the cluster.
6. Run `kubectl get nodes` to test whether the nodes you joined are now part of the cluster.
7. Now you have successfully setup a kubernetes cluster and you are good to deploy applications.

### Runnning the Demo:
1. Clone this project to the master node.
2. If you want to set up a guest book application. please go to the Guestbook folder. If you want to set up a voting app. please go to the Votingapp folder. Do not run both of them on the same cluster.
3. Run the deployment yaml file first and it's respective service file next. In kubernetes, we use the same command to set up a pod, service, replicaset and deployment. The way that kubernetes know which is which is by specifying the kind in the yaml file. 
4. The command is `kubectl create -f <deployment-file.yaml>` followed by `kubectl create -f <service-file.yaml>`. If you are using a LoadBalancer Port type and you have a load balancer configured (GKE has it pre-configured), the deployment will take some time. please wait until the deployment is running and then create its respective service.
5. You can use `kubectl get all` to see the status of the pods, deployments, replicasets etc.
6. After you have created all pods and services for a given application (Guestbook or Votingapp), you now will have a multi-tier application.

