# build-container-image

A composite action that builds, pushes, signs, and attests a container image.

## Usage

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    permissions:
      artifact-metadata: write
      attestations: write
      contents: read
      id-token: write
      packages: write
    steps:
      - uses: den4200/shared-workflows/actions/build-container-image@main
        with:
          password: ${{ github.token }}
          # Optional:
          # image: org/image-name
          # username: my-username
          # target: default
          # registry: ghcr.io
          # default-branch: main
          # vars: |
          #   {
          #     "NPM_TOKEN": "${{ secrets.NPM_TOKEN }}"
          #   }
```

## Inputs

| Name             | Required | Default                | Description                                     |
| ---------------- | -------- | ---------------------- | ----------------------------------------------- |
| `password`       | Yes      | —                      | Container registry password                     |
| `image`          | No       | `${{ github.repository }}` | Full image name (e.g. org/repo)             |
| `username`       | No       | `${{ github.actor }}`  | Container registry username                     |
| `target`         | No       | `default`              | Docker Bake build target                        |
| `registry`       | No       | `ghcr.io`              | Container registry                              |
| `default-branch` | No       | repo default           | Default branch reference                        |
| `vars`           | No       | `{}`                   | Additional environment variables in JSON format |

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
