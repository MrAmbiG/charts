# NSFW JS Helm Chart

A Helm chart for deploying NSFW JS content detection service on Kubernetes.

## Description

This chart deploys the `andresribeiroo/nsfwjs:1.6` Docker image which provides a machine learning-based NSFW (Not Safe For Work) content detection service.

## Installation

```bash
# Add the chart repository
helm repo add mrambig https://mrambig.github.io/charts
helm repo update

# Install the chart in default namespace
helm install nsfwjs mrambig/nsfwjs

# Install in a specific namespace
helm install nsfwjs mrambig/nsfwjs --namespace nsfwjs-prod

# Install and create namespace if it doesn't exist
helm install nsfwjs mrambig/nsfwjs --namespace nsfwjs-prod --create-namespace

# Install with custom values
helm install nsfwjs mrambig/nsfwjs -f values.yaml --namespace production

# Install in different environments
helm install nsfwjs-dev mrambig/nsfwjs --namespace development
helm install nsfwjs-staging mrambig/nsfwjs --namespace staging
helm install nsfwjs-prod mrambig/nsfwjs --namespace production
```

## Configuration

The following table lists the configurable parameters and their default values:

| Parameter | Description | Default |
|-----------|-------------|---------|
| `replicaCount` | Number of replicas | `1` |
| `namespace.name` | Namespace name (overrides helm --namespace) | `""` |
| `namespace.create` | Create namespace if it doesn't exist | `false` |
| `namespace.labels` | Labels to add to namespace | `{}` |
| `namespace.annotations` | Annotations to add to namespace | `{}` |
| `image.repository` | Image repository | `andresribeiroo/nsfwjs` |
| `image.tag` | Image tag | `1.6` |
| `image.pullPolicy` | Image pull policy | `IfNotPresent` |
| `service.type` | Service type | `ClusterIP` |
| `service.port` | Service port | `8080` |
| `ingress.enabled` | Enable ingress | `true` |
| `ingress.className` | Ingress class name | `nginx` |
| `ingress.hosts[0].host` | Ingress hostname | `nsfwjs.local` |
| `resources` | Resource limits/requests | `{}` |
| `autoscaling.enabled` | Enable HPA | `false` |
| `healthCheck.enabled` | Enable health checks | `true` |
| `healthCheck.path` | Health check path | `/health` |

## Usage

After installation, the NSFW JS service will be available at the configured endpoint. You can test it by sending POST requests to the `/predict` endpoint with image data.

Example:
```bash
curl -X POST http://your-service-url/predict \
  -H "Content-Type: application/json" \
  -d '{"imageUrl": "https://example.com/image.jpg"}'
```

## Uninstalling

```bash
helm uninstall nsfwjs
```

## Values

See [values.yaml](values.yaml) for the full list of configurable parameters.
