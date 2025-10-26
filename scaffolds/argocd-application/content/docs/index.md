# ${{ values.name }}

## Overview

${{ values.description }}

## Application Details

- **Name**: `${{ values.name }}`
- **Owner**: `${{ values.owner }}`
- **System**: `${{ values.system }}`
{%- if values.hostName %}
- **URL**: [https://${{ values.hostName }}](https://${{ values.hostName }})
{%- endif %}

## Links

- [GitHub Repository](${{ values.githubUrl }})
- [External Documentation](${{ values.documentationUrl }})

## Deployment Configuration

{%- if values.isHelm %}

### Helm Deployment

This application is deployed using a Helm chart with the following configuration:

- **Repository**: `${{ values.helmRepoUrl }}`
- **Chart Name**: `${{ values.chartName }}`
- **Chart Version**: `${{ values.chartVersion }}`
- **Values URL**: [${{ values.chartValuesUrl }}](${{ values.chartValuesUrl }})

{%- endif %}
{%- if values.isKustomize %}

### Kustomize Deployment

This application is deployed using Kustomize manifests with the following configuration:

- **Docker Image**: `${{ values.dockerImage }}`
- **Docker Tag**: `${{ values.dockerTag }}`
- **Container Port**: `${{ values.dockerPort }}`
- **Hostname**: `${{ values.hostName }}`

The deployment includes:
- Kubernetes Deployment
- Service (exposing port ${{ values.dockerPort }})
- HTTPRoute for ingress
- ServiceAccount

{%- endif %}

## ArgoCD

This application is managed by ArgoCD and deployed to the `${{ values.name }}` namespace.

**Sync Policy**:
- Auto-prune: Enabled
- Self-heal: Enabled
- Create namespace: Enabled

## Monitoring & Observability

This application is configured with:
- Kubernetes label selector: `backstage.io/kubernetes-id=${{ values.name }}`
- ArgoCD app name: `${{ values.name }}`
- Grafana alert label selector: `name=${{ values.name }}`
