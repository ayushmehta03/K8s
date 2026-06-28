# k8s custom controllers

used to add new resources to the kuberntes cluster

for example by default we have service deployment configmap scretes etc

but some extension is required then custom controller is used

# components

Crd -> custom resource defination
Cr-> custom resource
Custom controller


# work flow

1. lets breakdown the wf of deployment which is a deafut controller

user wrtites custom deploymet file kuberntes has something as tempelate which is resoruce defination and if user enters some field which are not define dit will thorw error and if verified the controller comes in action starts creating replicasets pods etc... basically performs action


2. now for custom controllers

first the resource will be deployed it will have a custom resrouce defination which will match and validate then the custom controller will perform actions 



# baisc architecture

cUSTOM rESOURCE-> K8sCluster <--- Custom Controller
|||||
Custom resoruce defination

