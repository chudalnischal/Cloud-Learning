
## What is Kubernetes?
Kubernetes is an open-source container orchestration tool that automates the deployment, management, scaling, and networking of containers across a cluster. A cluster is a group of nodes that run containerized applications managed by Kubernetes. Kubernetes is often abbreviated as k8s, representing the eight letters between 'K' and 'S' in the word Kubernetes.

## Why Kubernetes is Important?
Kubernetes is essential for running containerized applications because it automates the deployment and operation of applications across clusters. It can automatically replace and reschedule containers from stopped nodes, ensuring high availability. Additionally, Kubernetes integrates with a wide range of tools and services, enhancing its functionality and usability.

## Prerequisites:
Ensure you have the following tools installed on your system:

- **Docker**: Required for creating and managing containers. [Download it here](https://www.docker.com/products/docker-desktop).
- **Kind**: A tool for running local Kubernetes clusters using Docker. [Install it from the official installation site](https://kind.sigs.k8s.io/docs/user/quick-start/).
- **Kubectl**: The command-line interface for interacting with Kubernetes clusters. [Download it from the official Kubernetes site](https://kubernetes.io/docs/tasks/tools/).

## Creating the Cluster
To create the cluster, use the following command:

```bash
kind create cluster --name <cluster-name> 
```

This command will create a single-node cluster with only the control-plane in it.


If you want to create a cluster using a YAML configuration file, use the --config flag:

```bash 
kind create cluster --name=<cluster-name> --config=<file.YAML>
```
Using a YAML file allows you to create a multi-node cluster. A multi-node cluster consists of multiple instances or machines working together to run applications.

Here is an example YAML file for creating a cluster in Kubernetes:

```bash 
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
  - role: control-plane
  - role: worker
  - role: worker
  ```
After running the following command in the terminal, your cluster will be ready

## Explanation of the YAML File:

**kind: Cluster**
This line specifies the kind of Kubernetes resource you are defining. In this case, it’s a Cluster, which indicates that you are defining the configuration for a Kind Kubernetes cluster.

**apiVersion**: kind.x-k8s.io/v1alpha4
This line specifies the API version of the Kind configuration. The v1alpha4 version is used for defining the cluster configuration in Kind. It ensures that the configuration syntax and features are compatible with this version of Kind.

**nodes**:
This section defines the nodes that will be part of the Kubernetes cluster. Each node is an instance of a machine that runs part of the cluster’s workload. The nodes can have different roles:

- **Control Plane Node (Master Node)**: Manages Kubernetes control plane components, such as the API server, scheduler, and controller manager. It is responsible for maintaining the desired state of the cluster, handling API requests, and scheduling workloads on the worker nodes.

- **Worker Nodes**: Run the application workloads (containers) and report back to the control plane. These nodes host the application's containers, which are managed by the control plane.


### Verifying the cluster
```bash 
kubectl get nodes
```
You will see a list of nodes, including the control plane and worker nodes.

The output will include:

- **Name**: The name of the node.

- **Status**: The current status of the node.

- **Roles**: The role of the node (control-plane or worker).

- **Age**: How long the node has been running.

- **Version**: The version of Kubernetes the node is using.

### Switching between the cluster
If you have created multiple clusters and want to switch between them, first list the available contexts:

```bash 
kubectl config get-contexts
```
This command shows all clusters and indicates the current context with an asterisk.

#### To switch to a different cluster, use:
```bash 
kubectl config use-context <cluster-name>
```
This command changes the context to the specified cluster.

#### Kubernetes Cluster Info
To get information about the cluster, use:
```bash
kubectl cluster-info --context <cluster-name>
```
This command provides URLs to access the control plane and CoreDNS services of your Kubernetes cluster.


This are the basic commands used in Kubernetes. 

Please navigate to the days folder to learn more abou other topic in Kubernetes. 

THANKYOU
