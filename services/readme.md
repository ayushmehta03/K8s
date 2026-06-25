# k8s services


services are the add on feature given by k8s that works on the top of deployment

we were solving our issues with deployment earlier then why do we need services ??


# problem 1

while deployment provides auto healing feature by creating new pod before the termination of other pod

the problem arises when new pod is created it gets new ip address

but the user or team working doesnt get informed about chnage as there are 100s of pods running

they try to access the previous or terminated pod ip addresss which returns error 

this increase the debuuging time and is inefficinet

# solution

load balancing : insteaed of directly accessing the pods or app with ip add 

we implement a load balancer in the services which eventually distributes the traffic

no requirnemnt of ip add it will redirect to the required app with the lb algo mechanims

however this is not a complete soln

# problem 2

however we implemented load balancing but the prolem is still there how it will know the new ip address created by healing process
it will still redirect to previous ip add based on the algo

this will cause inconveniance to users and the teams


# solution 2

services uses something as label and selectors 

instead of depending upon ip add it gives label to pod 

in deployment we define label in the metadata

 in case any pod is healed again created one will also have the same label defined in deployment


 # basics structure

 deployment -> creates replicasets  -> pod1 and pod2 both having same  label 
 yaml here we define 
 label

 load balancing will use label for distribution


 # problem 3

 however we are done with the two problems but there is still one that is we are only able to access the app from kubernetes cluster

 this is a major issue in production we cant give users k8s cluster creditians and tell them to login to use app


and even the other team members will not be able to use it

# solution 3

services provided us discovery feature

it porvides us 3 functionality:
1. cluster ip
2. node port
3. load balance 


cluster ip -> used when we want to give the acces only to the internal and devops team who have kuberntes cluster access

node prot -> give access to those who are working on any node or having vpc accesss

load balancer-> give access to the external world

# how load balancer works work discovery

suppose we are using aws  will tell eks to give elastic load balancer a public ip add

that public ip add will be used for the external world access





