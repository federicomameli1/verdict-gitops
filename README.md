# verdict-gitops

GitOps repository for [Verdict](https://github.com/federicomameli1/challenge-app).

Argo CD watches this repo and syncs the Verdict Helm chart to the `verdict` namespace on the mgmt cluster.

## Structure

```
environments/
  mgmt/
    values.yaml   # image tag updated automatically by CI on every push to main
```

## How it works

1. A push to `main` in the Verdict repo triggers the CI pipeline.
2. CI builds the Docker image, pushes it to GHCR, then commits the new image tag to `environments/mgmt/values.yaml`.
3. Argo CD detects the change and syncs the Helm release on the mgmt cluster.
