# Helm Documentation

## What is Helm?
Helm is a package manager for Kubernetes that simplifies application deployment, management, and versioning. It helps package Kubernetes resources into Helm charts, making it easy to deploy and maintain complex applications.

## Why Use Helm?
- ✅ **Simplifies Kubernetes Deployments** – Avoids writing large YAML files.
- ✅ **Templates Kubernetes Manifests** – Uses reusable templates.
- ✅ **Manages Dependencies** – Handles dependencies between Kubernetes resources.
- ✅ **Supports Rollbacks** – Easily revert to a previous version.
- ✅ **Customizable Deployments** – Override default values using `values.yaml`.

## Structure of a Helm Chart
A Helm chart is a collection of files that define a Kubernetes application. The basic structure of a Helm chart looks like this:

my-chart/
│── Chart.yaml           # Metadata about the chart (name, version, description)
│── values.yaml          # Default configuration values
│── templates/           # Contains Kubernetes manifest templates
│   ├── deployment.yaml  # Deployment template
│   ├── service.yaml     # Service template
│   ├── ingress.yaml     # Ingress template (optional)
│   ├── _helpers.tpl     # Reusable template functions
│── charts/              # Dependencies (optional)
│── README.md            # Documentation for the chart

### Key Files Explained
- **`Chart.yaml`** → Defines the chart name, description, and version.
- **`values.yaml`** → Contains configurable values (can be overridden).
- **`templates/`** → Holds Kubernetes YAML templates using Helm's templating engine.
- **`_helpers.tpl`** → Contains reusable template functions.
- **`charts/`** → Stores dependencies (if any).

## Commonly Used Helm Commands

### 1. Installing Helm
Install Helm (if not already installed):
```sh
curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash

Adding & Managing Helm Repositories

# helm repo add bitnami https://charts.bitnami.com/bitnami  # Add a repo
helm repo update                                           # Update the repo
helm search repo nginx                                     # Search for a chart

helm install my-app bitnami/nginx        # Install a chart
helm list                                # List installed releases
helm status my-app                       # Get the status of a release

helm upgrade my-app bitnami/nginx --set service.type=ClusterIP  # Upgrade release
helm rollback my-app 1                                         # Rollback to version 1

helm upgrade my-app bitnami/nginx --set service.type=ClusterIP  # Upgrade release
helm rollback my-app 1                                         # Rollback to version 1
