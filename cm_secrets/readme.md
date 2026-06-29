# config map and secret

config map is used to store normal data which will be used by pods 

never store sensitive data

as etcd store data as object application can be compromised

# steps to apply 

1. create cm.yml file define version give name and data info

2. in deployment file consider that

# basic sturcture to include
    env:
          - name: DB-PORT
            valueFrom:
              configMapKeyRef:
                name: test-cm
                key: db-port



 problem: as container don't allow chnage of env file env value cant be chnaged


 # solution 
  1. use volume mounts

  # steps 

  create volume inside deployment file name it and give the configmap name as the refrence

in the container section of deployment.yml
    pass volumemount with name and the location


however in this way also security is compromised for important secret

2. use secret

cmd: kubectl create secret generic secret_name --from-literal=key:data

this saves the dataa s encrypted one however it is by deafult simple base 64 encryption

but it doesnt reveal information

it also supports env change 

