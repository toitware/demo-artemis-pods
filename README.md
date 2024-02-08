# Showcase: Pod development with Artemis

This repository demonstrates how development with Artemis can be done in
combination with GitHub actions.

## Setup

We assume two repositories:
1. https://github.com/toitware/demo-artemis-pods: this repository.
2. https://github.com/toitware/demo-artemis-fleet: the fleet repository.

Development of the code (pods) is done in this repository. Deployment and
management of the fleet is done in the fleet repository.

## Idea

The source code and pod-specification of pods live in this repository.
At every commit a GitHub action is triggered that builds the pod and
uploads it to the *development* fleet. This can be used to deploy the
pod to a small set of test-devices.

When the pod is ready for production the pod is also uploaded to the
production fleet. This is typically done as part of a release, or
with a workflow-dispatch. At this point the pod is not yet released, but
can now be used by the production fleet.

Note: the `fleet.json` uses the `latest` and `latest-main` tags.
The `latest` tag is updated for each push, whereas `latest-main` is only
added for pods built when a new version is committed to the main branch.

## GitHub actions

The [GitHub action in this repository](.github/workflows/ci.yml) shows
how to build and upload a pod to a fleet. It is designed to be copied
into other repositories.
