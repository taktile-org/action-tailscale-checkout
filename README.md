# Tailscale and Checkout Action

This Taktile internal GitHub Action sets up Tailscale and checks out your repository, enabling secure networking for your GitHub Actions workflows.

## Features

- Sets up Tailscale in your GitHub Actions workflow
- Checks out your repository 
- Ensures reliable connectivity to GitHub and AWS services
- Configures Tailscale with appropriate tags for CI environments

## Prerequisites

- A Tailscale account
- Tailscale OAuth credentials (client ID and secret)

## Usage

Add this action to your workflow:

```yaml
steps:
  - name: Setup Tailscale and Checkout
    uses: your-org/action-tailscale-checkout@main
    with:
      tailscale-oauth-client-id: ${{ secrets.TAILSCALE_OAUTH_CLIENT_ID }}
      tailscale-oauth-client-secret: ${{ secrets.TAILSCALE_OAUTH_CLIENT_SECRET }}
```

## Inputs

| Input                       | Description                   | Required |
|-----------------------------|-------------------------------|----------|
| `tailscale-oauth-client-id` | Tailscale OAuth client ID     | Yes      |
| `tailscale-oauth-client-secret` | Tailscale OAuth client secret | Yes  |

## Example Workflow

```yaml
name: Build with Tailscale

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Setup Tailscale and Checkout
        uses: your-org/action-tailscale-checkout@main
        with:
          tailscale-oauth-client-id: ${{ secrets.TAILSCALE_OAUTH_CLIENT_ID }}
          tailscale-oauth-client-secret: ${{ secrets.TAILSCALE_OAUTH_CLIENT_SECRET }}
      
      - name: Build project
        run: |
          # Your build commands here
          # Tailscale is now configured and the repository is checked out
```

## How It Works

1. Sets up Tailscale using the official Tailscale GitHub Action
2. Waits for GitHub and AWS connectivity to ensure network stability
3. Checks out your repository using actions/checkout
