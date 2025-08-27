# Infra.new Helm Chart

A Helm chart for deploying the infra.new application stack on Kubernetes.

## Components

- **Infra.new Frontend**: Main React application
- **Cost Service**: Backend service for cost calculations
- **Cloud Pricing Scraper**: Job for collecting cloud pricing data
- **PostgreSQL**: Database backend

## Installation

### From Local Chart
```bash
helm install infra-new ./infra-new-chart
```

### From GitHub
```bash
helm install infra-new git+https://github.com/launchflow/infra.new-charts@main?path=infra-new-chart
```

### From GitHub with Custom Values
```bash
helm install infra-new git+https://github.com/launchflow/infra.new-charts@main?path=infra-new-chart \
  --set infranew.spaceliftApiKeyId="your-spacelift-api-key-id" \
  --set infranew.spaceliftApiKeySecret="your-spacelift-api-key-secret" \
  --set infranew.spaceliftApiKeyEndpoint="https://launchflow.app.spacelift.io" \
  --set infranew.googleVertexProject="infra-new-dev" \
  --set infranew.gcsBucketName="infra-new-dev-dev-bucket" \
  --set cloudPricingScraper.onlyFlag="gcp:catalog,gcp:machine-types"
```

## Configuration

Key configuration options in `values.yaml`:

### Required Settings
- `infranew.anthropicApiKey`: Anthropic API key for AI features
- `infranew.spaceliftApiKeyId`: Spacelift API key ID
- `infranew.spaceliftApiKeySecret`: Spacelift API key secret
- `infranew.spaceliftApiKeyEndpoint`: Spacelift API endpoint
- `infranew.gcsBucketName`: GCS bucket for chat metadata
- `infranew.googleVertexProject`: Google Cloud project for Vertex AI

### Optional Settings
- `costservice.enabled`: Enable/disable cost service (default: true)
- `cloudPricingScraper.enabled`: Enable/disable pricing scraper (default: true)
- `postgres.password`: PostgreSQL password (default: postgres)

## Usage

```bash
# Install with custom values
helm install infra-new ./infra-new-chart -f my-values.yaml

# Upgrade deployment
helm upgrade infra-new ./infra-new-chart

# Uninstall
helm uninstall infra-new
```