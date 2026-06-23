# different distribution of kubernetes

1. EKS
2. OpenShift
3. Tanzu
4. Rancher 

these distribution provides user eperiannace and customer support


however in staging env pre prod env and production many org uses kubernetes

ranking of usage of distribution

1. openshift
2. rancher 
3. tanzu  by vmware
4. eks amazon


Kuernetes vs EKS

nothing but eks is built on top of kuernets 
incase of any issue with eks amazon will provide quick support

# KOPS

kops is an open soruce command line tool

it manages the life cycle of k8s create,upgrade ,manage,delete


# steps to implement kops

dev dependencies

python3 
aws cli
kubectl 

Install KOPS


GRant permission if using iam user on aws

EC2 Full access
s3 full acces
vpc full access
iam full access

aws configure


create s3 bukcet to store all config of cluster

cmd -> kops create cluster --name s3_bukcet info region_info volume_info 



kops update cluster --name.local


# for production

instead of local use domain

and configure route 53 aws