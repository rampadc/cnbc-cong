# Prerequisites

Delete everything you have right now. I strayed significantly from the path set out by the instructions.

1. Deploy tasks, triggers and pipeline from day-5 folder
2. Create the event listener route as described in `trigger-create-route.sh`.
3. Create a webhook in Github, set content type to `application/json`.
4. Make sure day-5 works.

# FYI

Changes to `gitops.yaml` compared to class's instructions:

- Remove unused variables
- Use GitHub personal access token instead of using the user's username and password
- `cp ../source/k8s/manifests.yaml` is changed to `cp ../source/manifests.yaml` to match output of day-5's kustomization step.

# Day 6 deltas

1. Apply new gitops task by running `oc apply -f tasks`.
2. Apply new pipeline by running `oc apply -f pipeline.yaml`.
3. Create a GitHub personal access token with `public_repo` scope - I'm only using a public repo here. Choose accordingly for your needs.
4. Create a new secret for the personal access token with `oc create secret generic git-credentials --from-literal=pat=<your-personal-access-token-here>`.
5. Create a new GitHub repo to host the `manifests.yaml` file.
6. Modify the `gitops-repo.configmap.yaml` with this new repo's details.
7. `oc apply -f gitops-repo.configmap.yaml`.
8. Run it once with `pipelinerun.yaml` to verify that everything works.
9. Assuming day-5 was deployed correctly (prereq), the existing triggers should still work.