# ingress in k82

ingress is a feature provided by k8s which allow to implement diff load balancing algorithms and api gateway


# problems before ingress

1. while using services there was only one load baalncing algorihtm round robin it lacks security and demand
2. for exposing to the real world in services load balancer used is guven static public ip add cloud provider charges for each ip add


# enterprise level load balancer demans
1. sticky lb
2. tcl 
3. path based
4. host based
5. ratio based


# flow

user deploys ingress.yaml file and installs ingress controller whatever they want nginx through one ingress they can manage 100 services 


