# Documentation: Publish Bicep Module to Azure Action

## Overview

The "Publish Bicep Module to Azure" action is designed to publish a specified Bicep module to an Azure container registry. This action automates the process of pushing Bicep modules to Azure, ensuring that the latest versions of your infrastructure-as-code are available in your Azure container registry.

## Inputs

Below are the inputs required for this action:

- **azureClientId**: Azure Client ID.
  - Description: Azure Client ID.
  - Required: True

- **azureTenantId**: Azure Tenant ID.
  - Description: Azure Tenant ID.
  - Required: True

- **azureSubscriptionId**: Azure Subscription ID.
  - Description: Azure Subscription ID.
  - Required: True

- **registryName**: Azure Container Registry Name.
  - Description: Azure Container Registry Name.
  - Default: 'eruza123'

- **moduleName**: Bicep Module Path.
  - Description: Bicep Module Path.
  - Required: True

- **moduleTag**: Bicep Module Tag.
  - Description: Bicep Module Tag.
  - Required: True

- **module**: Bicep Module Name.
  - Description: Bicep Module Name.
  - Required: True

## Execution

The action uses a composite run type and follows these steps:

1. **Checkout Step**: Checks out the repository using the `actions/checkout@v3` action.
2. **Azure Login**: Logs into Azure using the provided Azure Client ID, Tenant ID, and Subscription ID.
3. **Publish Bicep Module**: Publishes the Bicep module to the specified Azure container registry.

## Example Workflow

To use the "Publish Bicep Module to Azure" action in a GitHub workflow for your Git repository documentation, follow the example below:

```yaml
name: Publish Bicep Module

on:
  push:
    branches:
      - main

jobs:
  publish:
    runs-on: ubuntu-latest
    steps:
    - name: Publish Bicep Module to Azure
      uses: [YOUR_GITHUB_USERNAME]/[YOUR_REPOSITORY_NAME]@[YOUR_ACTION_VERSION]
      with:
        azureClientId: ${{ secrets.AZURE_CLIENT_ID }}
        azureTenantId: ${{ secrets.AZURE_TENANT_ID }}
        azureSubscriptionId: ${{ secrets.AZURE_SUBSCRIPTION_ID }}
        registryName: 'eruza123'
        moduleName: 'path/to/your/bicep/module.bicep'
        moduleTag: '1.0.0'
        module: 'my-bicep-module'
```

Replace `[YOUR_GITHUB_USERNAME]`, `[YOUR_REPOSITORY_NAME]`, and `[YOUR_ACTION_VERSION]` with appropriate values for your GitHub repository and action version.

Ensure that you've stored your Azure credentials (`AZURE_CLIENT_ID`, `AZURE_TENANT_ID`, and `AZURE_SUBSCRIPTION_ID`) as secrets in your GitHub repository for security reasons.

With this workflow, every time you push to the `main` branch, the specified Bicep module will be published to the Azure container registry.