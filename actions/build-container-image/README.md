# build-container-image

A composite action that builds, pushes, signs, and attests a container image.

## Usage

```yaml
jobs:
  build-push:
    runs-on: ubuntu-latest
    permissions:
      artifact-metadata: write
      attestations: write
      contents: read
      id-token: write
      packages: write
    steps:
      - uses: your-org/shared-workflows/actions/build-container-image@main
        with:
          image: ${{ github.repository }}
          username: ${{ github.actor }}
          password: ${{ github.token }}
          # Optional:
          # target: default
          # registry: ghcr.io
          # default-branch: main
          # vars: |
          #   {
          #     "NPM_TOKEN": "${{ secrets.NPM_TOKEN }}"
          #   }
```

## Inputs

| Name             | Required | Default      | Description                                     |
| ---------------- | -------- | ------------ | ----------------------------------------------- |
| `image`          | Yes      | —            | Full image name (e.g. org/repo)                 |
| `username`       | Yes      | —            | Container registry username                     |
| `password`       | Yes      | —            | Container registry password                     |
| `target`         | No       | `default`    | Docker Bake build target                        |
| `registry`       | No       | `ghcr.io`    | Container registry                              |
| `default-branch` | No       | repo default | Default branch reference                        |
| `vars`           | No       | `{}`         | Additional environment variables in JSON format |

## Required Permissions

The calling workflow must grant these permissions:

```yaml
permissions:
  artifact-metadata: write
  attestations: write
  contents: read
  id-token: write
  packages: write
```
