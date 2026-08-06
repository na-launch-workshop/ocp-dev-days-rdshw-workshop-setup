# Launch Workshop Setup

## Introduction

This workshop is intended to be deployed through the [Red Hat Demo Platform](demo.redhat.com) with the "OpenShift Dev Day Roadshow" catalog offering.
The Launch Workshop is a customized fork of the base offering and layers on a curated developer experience with additional module content around
various programming languages (i.e. Java, .NET, Python, Node.js).

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

1. From [Red Hat Demo Platform](demo.redhat.com), provision the "OpenShift Dev Day Roadshow" catalog offering. Select "enable the workshop user
interface" and update the number of users that will be provisioned.
2. Once the cluster is provisioned, log into OpenShift GitOps.  In the app-of-apps application, update the Repo URL to
https://github.com/na-launch-workshop/ocp-dev-days-rdshw-gitops and Target Revision to `main`.
3. This workshop populates GitLab with additional entities in Developer Hub, and can be kicked off by ArgoCD redeploying a job as follows:
```
oc delete job initialize-gitlab -n gitlab
```

## Workshop Modules

The [workshop module library](https://github.com/orgs/na-launch-workshop/repositories) are prebuilt module content for the developers,
prefixed with `workshop-`.  The workshop administrators should clone from the public GitHub organization to the self-hosted GitLab
instance in the workshop cluster.

### Adding Module Content

The following are instructions to import workshop modules (Git repositories) into self-hosted GitLab:

1. The GitLab repository that was deployed contains a root user that can import Git repositories from external GitHub.  Log in with the GitLab
user named `root` and the password obtained as follows:
  ```sh
  oc get secret gitlab-secret -n gitlab -o jsonpath='{.data.GITLAB_ROOT_PASSWORD}{"\n"}'|base64 --decode; echo
  ```
3. Navigate to the `workshop` group which is an appropriate RBAC role for end users to view but not merge module content to
the main branch.  Create a new project -> Import project -> Repository by URL.  Import modules from the content library above.
4. Developer Hub automatically detects valid catalog-info.yaml files from the accompanying repositories and periodically (default: 5 minutes)
imports them and their TechDocs content.

## Development

Follow these steps:

1. Fork the [ocp-dev-days-rdshw-gitops](https://github.com/na-launch-workshop/ocp-dev-days-rdshw-gitops) repository.
2. In OpenShift GitOps, in the app-of-apps application, update the Repo URL and Target Revision to your fork.
3. In the Parameters tab, edit and update the `gitops.repoUrl` and `gitops.targetRevision` to your fork.

<details>
<summary>🤫 And finally, for end users in Developer Hub...</summary>

### 🥚 You found an easter egg!

</details>

