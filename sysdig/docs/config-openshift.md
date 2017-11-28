##  Install and configure Sysdig agent on OpenShift as a DaemonSet

In order to automate the agent deployment and configuration a [Template](../templates/sysdig-agent-template.yaml) is provided. Follow the steps below in order to deploy it.

### 1. Install kernel-devel package on all your OCP nodes

  ```bash
  yum -y install kernel-devel-$(uname -r)
  ```

### 2. Create a project in which to host Sysdig agent

  ```bash
  oc new-project <project>
  ```

### 3. Deploy DaemonSet and all required objects from the template

```bash
oc process -f templates/sysdig-agent-template.yaml \
  -p NAMESPACE="<project name from previous step>"
  -p SYSDIG_KEY="<your Sysdig Cloud Access Key>" \
  -p CLUSTER_TAG="<name to tag your cluster with>" \
  | oc create -f-
