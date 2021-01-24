# Deploy Action

This action performs login and deployment of an image to [GCR].

## Inputs

### `resource-directory`

**Required** Location of the Kubernetes deployment resources.

### `image`

**Required** The image to deploy, e.g. `foo/example-app:latest`.

### `secrets-name`

Name of the Secret resource. Default: `secrets`.

### `secrets-from-files`

Secrets from files to set (e.g. for multi-line secrets)

### `secrets`

Literal secrets to set.

### `dry-run`

[Strategy](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply) passed to `kubectl apply`. Must be `none`, `server`, or `client`. Default: `none`. 

## Outputs

None.

## Example usage

```yaml
- name: Prepare secret files
  working-directory: ./deployment
  run: echo "$FOO_PRIVATE_KEY" > ./fooPrivateKey.secret

- name: Configure and deploy
  uses: 'sendinblue/k8s-deploy-action@main'
  with:
    resource-directory: ./deployment
    image: foo/example-app:1.0.0
    secrets-name: 'example-app-secrets'
    secrets-from-files: |-
      fooPrivateKey=fooPrivateKey.secret
    secrets: |
      fooToken=abc123
```

[GCR]: https://cloud.google.com/container-registry