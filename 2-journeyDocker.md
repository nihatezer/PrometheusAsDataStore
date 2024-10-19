# README: Using Prometheus as a Datasource for Grafana in a Minikube Environment with GitHub Codespaces

## Overview

This README provides step-by-step instructions to set up Prometheus as a data source for Grafana in a Minikube environment, running inside a GitHub Codespaces environment. Prometheus will scrape metrics from services running in the Kubernetes cluster, and Grafana will visualize those metrics.

## Prerequisites

1. **GitHub Codespaces**: A GitHub account with Codespaces enabled.
2. **Docker**: Installed locally (required by Minikube).
3. **Minikube**: Installed and running inside GitHub Codespaces.
4. **kubectl**: Installed and configured to interact with Minikube.
5. **Helm**: For managing Prometheus and Grafana installations.

## Setup Instructions

### 1. Setting Up Minikube in Codespaces

Start by creating a Codespace and opening a terminal.

1. **Install Minikube in Codespaces:**
   ```bash
   curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
   sudo install minikube-linux-amd64 /usr/local/bin/minikube
   ```

2. **Start Minikube with Docker driver:**
   ```bash
   minikube start --driver=docker
   ```

3. **Verify Minikube is running:**
   ```bash
   minikube status
   ```

### 2. Install Prometheus Using Helm

1. **Add Prometheus Helm repository:**
   ```bash
   helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
   helm repo update
   ```

2. **Install Prometheus:**
   ```bash
   helm install prometheus prometheus-community/prometheus \
     --namespace monitoring --create-namespace
   ```

3. **Verify Prometheus pods are running:**
   ```bash
   kubectl get pods -n monitoring
   ```

4. **Access Prometheus Dashboard (optional):**
   ```bash
   minikube service prometheus-server -n monitoring
   ```

### 3. Install Grafana Using Helm

1. **Add Grafana Helm repository:**
   ```bash
   helm repo add grafana https://grafana.github.io/helm-charts
   helm repo update
   ```

2. **Install Grafana:**
   ```bash
   helm install grafana grafana/grafana \
     --namespace monitoring
   ```

3. **Get Grafana admin password:**
   ```bash
   kubectl get secret --namespace monitoring grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo
   ```

4. **Expose Grafana service:**
   ```bash
   minikube service grafana -n monitoring
   ```

### 4. Configuring Prometheus as a Data Source in Grafana

1. **Access Grafana UI:**
   - Open the URL provided by `minikube service grafana -n monitoring` in your browser.
   - Log in with username `admin` and the password retrieved in the previous step.

2. **Add Prometheus as a data source:**
   - Go to **Configuration** > **Data Sources**.
   - Click **Add data source** and select **Prometheus**.
   - Enter the following details:
     - **URL**: `http://prometheus-server.monitoring.svc.cluster.local:80`
   - Click **Save & Test** to verify the connection.

### 5. Creating Dashboards in Grafana

1. After adding Prometheus as a data source, you can create a new dashboard by navigating to:
   - **Dashboards** > **New Dashboard** > **Add Query**.
   - Select **Prometheus** as the data source and choose the metrics you want to visualize.

2. You can use pre-built dashboards by importing templates from the Grafana dashboard marketplace or using built-in dashboards from Prometheus.

### 6. Stopping and Cleaning Up

1. **Stop Minikube:**
   ```bash
   minikube stop
   ```

2. **Delete Minikube Cluster:**
   ```bash
   minikube delete
   ```

3. **Remove Helm Releases:**
   ```bash
   helm uninstall prometheus -n monitoring
   helm uninstall grafana -n monitoring
   ```

## Troubleshooting

- **Minikube issues:** If Minikube has trouble starting, ensure Docker is running correctly inside the Codespace and that you are using the correct driver (`--driver=docker`).
- **Prometheus connection issues in Grafana:** Double-check the Prometheus URL is correct, especially the namespace (`monitoring`) and port (`80`).
- **Accessing services in Minikube:** Use `minikube service <service-name> -n <namespace>` to open service URLs directly in the browser.

## Conclusion

By following these steps, you now have Prometheus running as a data source for Grafana in a Minikube cluster hosted in GitHub Codespaces. This setup allows you to scrape, visualize, and monitor your Kubernetes environment efficiently.
