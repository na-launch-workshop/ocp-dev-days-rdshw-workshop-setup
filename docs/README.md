# Launch Workshop Setup

## Introduction

This workshop is intended to be deployed through the [Red Hat Demo Platform](demo.redhat.com) with the "OpenShift Dev Day Roadshow" catalog offering.  The Launch Workshop is a customized fork of the base offering and layers on a curated developer experience with additional module content around various programming languages (i.e. Java, .NET, Python, Node.js).

## Code

The base OpenShift Dev Day Roadshow consists of:
- [Cluster bootstrapper](https://github.com/rhpds/ocp-dev-days-rdshw-automation)
- [Helm charts and ArgoCD manifests](https://github.com/rhpds/ocp-dev-days-rdshw-gitops)
- [Showroom](https://github.com/rhpds/ocp-dev-days-rdshw-showroom)

The Launch Workshop is a fork of the base offering:
- [Cluster bootstrapper](https://github.com/na-launch-workshop/ocp-dev-days-rdshw-automation)
- [Helm charts and ArgoCD manifests](https://github.com/na-launch-workshop/ocp-dev-days-rdshw-gitops)
- [Showroom](https://github.com/na-launch-workshop/ocp-dev-days-rdshw-showroom)

## Provisioning

Follow these steps to provision the Launch workshop:

1. From [Red Hat Demo Platform](demo.redhat.com), provision the "OpenShift Dev Day Roadshow" catalog offering. Select "enable the workshop user interface" and update the number of users that will be provisioned.
2. Once the cluster is provisioned, log into OpenShift GitOps.  In the app-of-apps application, update the Repo URL to https://github.com/na-launch-workshop/ocp-dev-days-rdshw-gitops and Target Revision to `main`.
3. This workshop populates GitLab with additional entities in Developer Hub, and can be kicked off by ArgoCD redeploying a job as follows:
```
oc delete job initialize-gitlab -n gitlab
```

## Development

Follow these steps:

1. Fork the [ocp-dev-days-rdshw-gitops](https://github.com/na-launch-workshop/ocp-dev-days-rdshw-gitops) repository.
2. In OpenShift GitOps, in the app-of-apps application, update the Repo URL and Target Revision to your fork.
3. In the Parameters tab, edit and update the `gitops.repoUrl` and `gitops.targetRevision` to your fork.

