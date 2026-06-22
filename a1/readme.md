# def and arhictecture

# major problems of docker


1. Ephermeral nature short life 

2. single host nature 

3. no auto scaling support

4. no auto healing support


docker is a simple application doesnt support enterprise level demands

kubernetes solves all these 4 problems :

1.serves as cluster i.e group of nodes supports master slave architecture

2. replication controller 

3. auto healing supports starts container before the breaking of previous one

4. it ans enterprise level container orchstration platform



# Architecture 


ptr: kubernetes works as cluster ie. master and worker appraoch

it is divided into two groups

control plane -> servers on the master node

data plane -> serves on the worker node


# control-plane

1. API server: 
            it is the heart of kubernetes 
            exposes kubernetes to the real world
            takes the action to perform

2. Scheduler:
            scheduling process or reources
            acts on the action taken by the api server

3.  ETCD
            key value pair
            cluster related info save
            brain of kubernetes



# data-plane


1. container run time :
                runs the container like java run time run the java application

2. kubelet:
                ensures that conatiner runs 
                if it is not running informs to the api server
                serves in auto healing process

3. kube proxy
            provides networking,ip addr and basic load balancing
            works on the ip table for networking config
            serves in the auto scaling 



    # controller manager 

        ensures that the controllers are always running
        for eg we have replica set for auto scaling it ensures replica set is valid and running always


    # cloud controller manager

        open soruce 

        to link your cluster to a cloud provider's API

        seperate code from core kubernetes


        


