- In all interactions and commit messages, be extremely concise and sacrifice grammar for the sake of concision.

## Plan

- Make the plan extremely concise. Sacrifice grammar for the sake of concision.
- At the end of the plan, give me a list of unresolved questions to answer, if any.

## What This Repo Is

A GitOps repository for a Kubernetes cluster. ArgoCD watches this repo and automatically applies changes to the cluster. Changes take effect when pushed to `main`.

## How Deployments Work

This repo uses the **App-of-Apps** pattern:

1. `root-app.yml` is manually applied once to bootstrap ArgoCD. It watches the `apps/` directory.
2. Each file in `apps/` is an ArgoCD `Application` manifest pointing to a subdirectory under `manifests/`.

**To add a new application:**
1. Create `manifests/<app-name>/` with Kubernetes manifests.
2. Create `apps/<app-name>-app.yml` as an ArgoCD `Application` pointing to that path.
3. Push to `main` — ArgoCD picks it up automatically.
