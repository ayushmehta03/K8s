# k8s monitoring using prometheus and grafana


# install prometheus


1. install helm

brew install helm

2. install promethus

1. add promethus repo 

helm repo add prometheus-community https://github.io

2. update the repo

helm repo update 

3. install prometheus
helm install my-prometheus prometheus-community/prometheus


# making the prometheus server nodeport mode for grafana to access it from ip cluster

kubectl expose service prometheus-server  --type=NodePort   --target-port=9090  --name=prometheus-server-ext



// for docker driver only 

minikube service prometheus-server-ext



# install grafana

1.  helm repo add grafana https://grafana.github.io/helm-charts

2. helm repo update

3. helm install my-grafana grafana/grafana 



# making the my grafana to node port mode

kubectl expose service my-grafana --type=NodePort --target-port=3000 --name=grafana-ext


// for docker driver only 

minikue service grafana-ext

# this will launch grafana dashboard

![Grafana dASHBOARD](grafana_dashboard.png)






┌───────────────────────────────── Mac Engine ─────────────────────────────────┐
 │                                                                              │
 │  Your Mac Browser ──(Blocked Natively)───┐                                   │
 │       │                                  │                                   │
 │       │ (minikube service tunnel)        ▼                                   │
 │       ▼                            ┌─────────── Minikube (Docker Container) ┐│
 │  http://127.0.0.1:xxxxx ──────────►│  NodePort 32390                        ││
 │                                    │      │                                 ││
 │                                    │      ▼                                 ││
 │                                    │  [Grafana Pod] ───(Direct Internal)───►││
 │                                    │        URL: http://prometheus:80       ││
 │                                    └────────────────────────────────────────┘│
 └──────────────────────────────────────────────────────────────────────────────┘
