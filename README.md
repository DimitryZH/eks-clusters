# AWS EKS Clusters Configuration

This repository contains two YAML configuration files for creating and managing AWS EKS (Elastic Kubernetes Service) clusters using `eksctl`, a simple CLI tool for creating clusters on EKS. These configurations are designed for two separate environments: Development (`eks_cluster_dev.yaml`) and Production (`eks_cluster_prod.yaml`). Each configuration is tailored to meet the specific requirements of its environment, with both setups utilizing a 3-node cluster to ensure high availability and resilience.

## Integration with ArgoCD for Continuous Deployment

These Clusters are designed to facilitate the deployment of the ArgoCD application, a declarative, GitOps continuous delivery tool for Kubernetes. For more details on deploying ArgoCD within theses please refer to the dedicated GitHub repository: [Deploying ArgoCD](https://github.com/DimitryZH/argo-cd-app-terraform)

## Development Configuration: `eks_cluster_dev.yaml`

The development configuration defines a 3-node cluster named `demo-dev` in the `us-east-1` region. It specifies the use of a custom VPC and subnets for both public (Load Balancer) and private (Worker Nodes) networking components. The cluster utilizes `t3.small` instances for its managed node group, with a desired capacity of 3 nodes. Each node has 70 GB of disk space and operates within private subnets, enhancing network security. Additionally, the node group is configured with IAM policies to support image building.

## Production Configuration: `eks_cluster_prod.yaml`

The production configuration sets up a 3-node cluster named `demo-prod`, also in the `us-east-1` region. It shares the same VPC and subnet setup as the development configuration, ensuring consistency across environments. However, it differs in its use of `t3.medium` instances for the managed node group, reflecting the increased resource requirements of a production environment. The desired capacity remains at 3 nodes, but each node is allocated 80 GB of disk space. Like the development configuration, nodes are placed in private subnets and are equipped with IAM policies for image building.

## Key Differences

While both configurations are similar in structure, key differences lie in the instance types and disk sizes, reflecting the distinct needs of development and production environments. The use of a 3-node cluster in both configurations ensures high availability and resilience, making it a robust foundation for deploying Kubernetes clusters in AWS tailored to the specific needs of development and production environments.

## Usage

To deploy clusters using these configurations, follow these steps:

1. **Install `eksctl`:** Ensure that `eksctl` is installed on your system. You can find installation instructions on the [official eksctl website](https://eksctl.io/).

2. **Set up AWS Credentials:**

   - **For Ubuntu:**
     Open your terminal and set your AWS credentials and default region by running the following commands:

     ```
     export AWS_ACCESS_KEY_ID="your_access_key_id_here"
     export AWS_SECRET_ACCESS_KEY="your_secret_access_key_here"
     export AWS_DEFAULT_REGION="your_preferred_region_here"
     ```

   - **For Windows:**
     Open Command Prompt and set your AWS credentials and default region by executing the following commands:
     ```
     set AWS_ACCESS_KEY_ID= "your_access_key_id_here"
     set AWS_SECRET_ACCESS_KEY= "your_secret_access_key_here"
     set AWS_DEFAULT_REGION="your_preferred_region_here"
     ```

3. **Create a Cluster:** To create a cluster, use the following command with the appropriate configuration file:

```
eksctl create cluster -f <configuration-file.yaml>
```

4. **Delete a Cluster:** To delete a cluster, use:

```
eksctl delete cluster -f <configuration-file.yaml>
```

These steps provide a comprehensive guide for deploying Kubernetes clusters in AWS using `eksctl`, tailored to the specific needs of development and production environments.

##  Production Cluster Architecture

![production_cluster](https://github.com/DimitryZH/eks-cluster-script/assets/146372946/1eb5a92a-f0d8-403a-8a74-bf4f64888e87)
