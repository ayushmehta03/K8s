# rbac

plays major role in security

rbac stands for role based acccess control

user has their role defiend and they have limitation on actins based on the role


# types

1. service accoount
2. roles/cluster role
3. rolebinding/ cluster role binding

# k8s scenirio

k8s doesnt have feature of user management or role management they throw this responsibility on identify providers

for eg: for aws eks identifier can be iamuser

# keyclok

common tool used for rbac can be connected to github also for better feature ussage


# service account

one can create service account for their pods 

however a default one is always created wrt pods


# role binding

contains 3 components
1. service accounts -> these are the users
2. role -> specify the permission
3. role binding -> bind the permission to the user on the basis of role

# cp

 for namespace-> role binding
 for cluster -> cluster role binding
