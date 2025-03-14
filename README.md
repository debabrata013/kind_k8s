# Kubernetes Kind (K8s in Docker)

[Kind](https://kind.sigs.k8s.io/) is a tool for running local Kubernetes clusters using Docker container "nodes." It is useful for testing Kubernetes clusters locally, CI/CD pipelines, or for developing with Kubernetes in a lightweight environment.

## Prerequisites

Before you begin, ensure the following tools are installed on your local machine:

- **Docker**: [Install Docker](https://docs.docker.com/get-docker/)
- **Kubectl**: [Install kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
- **Kind**: [Install Kind](https://kind.sigs.k8s.io/docs/user/quick-start/)

## Quick Start

### Step 1: Create a Cluster

To create a new Kubernetes cluster using Kind, run the following command:

```bash
kind create cluster
```

By default, this will create a cluster named `kind`.

### Step 2: Verify the Cluster

Once the cluster creation is complete, verify your Kubernetes cluster by running:

```bash
kubectl cluster-info --context kind-kind
```

You should see output like:

```bash
Kubernetes master is running at https://127.0.0.1:6443
```

### Step 3: Deploy a Sample Application

To deploy a simple application on your Kind cluster, use the following steps.

1. Create a deployment:

   ```bash
   kubectl create deployment nginx --image=nginx
   ```

2. Expose the application via a service:

   ```bash
   kubectl expose deployment nginx --port=80 --type=LoadBalancer
   ```

3. Check the status of the services:

   ```bash
   kubectl get services
   ```

### Step 4: Delete the Cluster

To delete the cluster after you are done testing:

```bash
kind delete cluster
```

## Configuration

You can customize your Kind cluster with a configuration file. Here’s an example of a configuration file (`kind-config.yaml`):

```yaml
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
  - role: control-plane
  - role: worker
```

Create a cluster with this configuration:

```bash
kind create cluster --config kind-config.yaml
```

## Additional Commands

- **List clusters:**

  ```bash
  kind get clusters
  ```

- **Check logs for a node:**

  ```bash
  docker logs <container-name>
  ```

- **Load a local image into the Kind cluster:**

  ```bash
  kind load docker-image <image-name>
  ```

- **Set Kubeconfig for a specific context:**

  ```bash
  export KUBEVIRT_KUBECONFIG=$(kind get kubeconfig-path --name="kind")
  ```

## Useful Links

- [Kind GitHub Repository](https://github.com/kubernetes-sigs/kind)
- [Kubernetes Documentation](https://kubernetes.io/docs/)

## Troubleshooting

If you encounter any issues, here are a few steps to troubleshoot:

- **Check Docker status**: Ensure Docker is running on your system.
- **Check node logs**: You can check individual node logs for debugging by using `docker logs <container-name>`.
- **Recreate the cluster**: If things are not working correctly, deleting and recreating the cluster can help:
  
  ```bash
  kind delete cluster
  kind create cluster
  ```
