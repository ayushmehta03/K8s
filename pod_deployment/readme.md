# K8s Pods

Pod is the smallest deployale unit in k8s


executed inside pod.yml file -> it is basically the deination of how to run a container


pod can run either a single or multiple contaienrs
side car or init containers which supports the actual container


if a pod runs multiple container they get advantage of shared network and shared storage 



# steps to create delete get info about pods using minkube

1. install kubectl -> cli tool for kubernetes

2. install minikube -> used locally provides 1 master and 1 worker node for learning purpose

# cmd to execute

1. minikube start (creates a vm for single node k8s cluster) by default it uses docker driver

2. kubectl get nodes (give the info about the node cluster)

3. create a pod.yml file 

4. kubectl create -f pod.yml (creates pod)

5. kubectl get pods (give the pod information ) || kubectl get pods -o wide (details info)

6. kubectl delete pod pod_name (deletes the running pod)

7. kubectl describe pod pod_name (give status of everything inside a pod, helps in debuging)

8. kubectl logs pod_name (gives log of the application)


# add:

to acheive auto scaling auto healing we use wrapper deployment 