# Kubernetes Cluster Configuration with `kind`

This file defines the configuration for a Kubernetes cluster using `kind` (Kubernetes IN Docker), a tool for running Kubernetes clusters locally in Docker containers. The configuration is written in YAML and specifies the roles of the nodes in the cluster.

## Description

The `kind` tool allows you to quickly spin up a multi-node Kubernetes cluster on your local machine for testing and development purposes. In the configuration below, we define a simple cluster with one control-plane node and two worker nodes.

The configuration specifies:

- **kind**: The cluster type (in this case, a Kubernetes cluster using `kind`).
- **apiVersion**: The API version for the `kind` configuration.
- **nodes**: A list of nodes that make up the cluster. The nodes are categorized by their roles.

The roles of the nodes are:
- **control-plane**: This is the primary node that manages the cluster and schedules workloads.
- **worker**: These nodes are responsible for running the application workloads.

## `kind` Kubernetes Cluster Configuration

```yaml
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
  - role: control-plane
  - role: worker
  - role: worker


## Breakdown of the Configuration
- **kind**: Cluster: Specifies that this is a Kubernetes cluster configuration.
- **apiVersion**: kind.x-k8s.io/v1alpha4: Defines the API version of kind to be used for this configuration.
nodes:
- **role: control-plane**: This defines the node that will act as the control plane in the Kubernetes cluster.
- **role: worker**: These define the worker nodes that will run the applications and workloads in the cluster.

## How to Use This Configuration
Install kind: Before applying this configuration, make sure that kind is installed on your local machine. You can follow the installation instructions in the official kind documentation.

Create the Cluster: Save this YAML file as `kind-cluster.yaml` and use the following command to create the cluster:

`kind create cluster --config kind-cluster.yaml`
Verify the Cluster: Once the cluster is created, you can verify that the nodes are set up correctly by running:


`kubectl get nodes`
This will display the nodes in your Kubernetes cluster, including the control plane and worker nodes.

Access the Cluster: You can now use kubectl to interact with your Kubernetes cluster. For example, you can deploy applications, view logs, or scale workloads.