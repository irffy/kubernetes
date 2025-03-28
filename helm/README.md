# Helm for Kubernetes - Comprehensive Guide

## Introduction
**Helm** is a package manager for Kubernetes that simplifies application deployment, management, and versioning through reusable packages called **charts**.

## Key Features
- ✅ Simplifies Kubernetes Deployments
- ✅ Templates Kubernetes Manifests
- ✅ Manages Dependencies
- ✅ Supports Rollbacks
- ✅ Customizable Deployments

## Helm Chart Structure
A typical Helm chart structure:

```bash
my-chart/
├── Chart.yaml           # Metadata (name, version, description)
├── values.yaml          # Default configuration values
├── templates/           # Kubernetes manifest templates
│   ├── deployment.yaml  
│   ├── service.yaml     
│   ├── ingress.yaml     
│   └── _helpers.tpl     # Reusable template functions
└── charts/              # Dependencies (optional)
```

## Essential Commands

### Installation
```shell
# Install Helm
curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
```

### Repository Management
```shell
helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo update
helm search repo nginx
```

### Release Management
```shell
# Install chart
helm install my-app bitnami/nginx

# List releases
helm list

# Check status
helm status my-app

# Uninstall
helm uninstall my-app
```

### Customization
```shell
# Override values file
helm install my-app bitnami/nginx -f values.yaml

# Set individual values
helm install my-app bitnami/nginx --set service.type=LoadBalancer
```

### Chart Development
```shell
# Create new chart
helm create my-chart

# Validate chart
helm lint my-chart

# Package chart
helm package my-chart
```

## Troubleshooting
```shell
helm get manifest my-app    # View generated manifests
helm get values my-app      # Show configured values
helm history my-app         # View release history
```

## Best Practices
1. Use semantic versioning in Chart.yaml
2. Document all configurable values in values.yaml
3. Use _helpers.tpl for shared template logic
4. Test charts with `helm template` before deployment
5. Regularly update chart dependencies

---

> **Pro Tip**: Always run `helm lint` and `helm template` to validate charts before deployment.
