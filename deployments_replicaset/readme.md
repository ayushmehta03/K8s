# deployment wrapper in k8s

# diff between container,pods and deployment

# container

runs on command
single host nature
ephemeral in nature

# pods

can run single or multiple containers

contains running specifaction of container 

instead of cli uses yaml file which contains info about network volume


# deployment

works on the top of pods

used in production 

supports auto healing and auto scaling


# how deployment works

deployment is also specified in yaml file

1. deployment creates replicasets
2. replica sets are controllers writeen in golang, replicasets ensures that the actual and desired state are same 
3. these replicasets create pods

# how it supports auto healing and auto scaling

if any pod is deleted it is parallely created again with the termination, this is not avilable while using pods for deployment

to autoscale just increase the replicaset count in deployment.yaml


# commands 

1. kubectl get all -> lisr all the resources in the namespace
2. kubectl get all -A -> list all the resources from all namespaces
3. kubectl apply -f deployment.yml -> execute deployment file
4. kubectl get pods -w (watch the behaviour of nodes)
5. kubectl scale deployment <deployment-name> --replicas=0 -> to delete all the created pods






