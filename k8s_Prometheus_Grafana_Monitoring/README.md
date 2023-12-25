# Kubernetes Monitoring with Prometheus and Grafana

This lab provides a step-by-step guide on setting up monitoring for a Kubernetes cluster using Prometheus and Grafana. The demonstration utilizes a Kakoda Kubernetes cluster.

**Commands Used:**

This commands were used to download and install both prometheus and grafana, and forward port to view details in grafana.

```bash
wget https://get.helm.sh/helm-v3.13.tar.gz
tar -xf helm-v3.13.tar.gz
sudo mv linux-amd64/helm /usr/local/bin/helm

helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
helm install prometheus prometheus-community/prometheus

helm repo add grafana https://grafana.github.io/helm-charts
helm repo update
helm install grafana grafana/grafana

kubectl get pods -n default
kubectl get all -n default

kubectl port-forward svc/grafana 3000:3000

kubectl get secret grafana -n default -o jsonpath='{.data.admin-password}' | base64 -d
grafana-cli login localhost:3000 admin <password>

grafana-cli data source create prometheus http://prometheus-server:9090
grafana-cli dashboard import https://grafana.com/api/dashboards/11193
grafana-cli dashboard list
grafana-cli dashboard delete 11193
```
