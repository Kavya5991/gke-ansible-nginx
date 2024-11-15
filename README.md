# Ansible Role: NGINX on GKE

This Ansible role automates the deployment of NGINX on Google Kubernetes Engine (GKE) clusters. It handles the complete setup from GKE authentication to NGINX deployment with LoadBalancer service.

## Prerequisites

- Ansible
- Google Cloud SDK
- kubectl
- Access to a GKE cluster

```bash
# Install required tools
Refer to Google's documentation to install Google Cloud CLI

# Install required collections
ansible-galaxy collection install kubernetes.core
```

## Directory Structure
```
.
├── README.md
├── ansible.cfg
├── inventory
│   └── hosts
├── playbook.yml
└── roles
    └── gke-nginx
        ├── tasks/
        ├── vars/
        ├── handlers/
        └── templates/
```

## Configuration

1. Update `roles/nginx-k8s/vars/main.yml` with your GKE details:
```yaml
gke_cluster_name: "your-cluster-name"
gke_region: "your-region"
project_id: "your-project-id"
```

2. Authenticate with Google Cloud:
```bash
gcloud auth login
gcloud config set project your-project-id
```

## Usage

Run the playbook:
```bash
ansible-playbook -i inventory/hosts playbook.yml -e "gke_cluster_name=your-cluster gke_region=your-region project_id=your-project-id"
```

## Variables

| Variable | Description | Default |
|----------|-------------|---------|
| nginx_replicas | Number of NGINX replicas | 3 |
| nginx_container_port | Container port | 80 |
| nginx_service_port | Service port | 80 |
| nginx_service_type | Service type | LoadBalancer |
