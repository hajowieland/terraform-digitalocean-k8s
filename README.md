# Terraform Kubernetes on Digital Ocean

This repository contains the Terraform module for creating a Kubernetes Cluster on Digital Ocean.

It uses the latest available Digital Ocean Kubernetes slug version available and creates a kubeconfig file at completion.

#### Link to my comprehensive blog post (beginner friendly):
[https://napo.io/posts/terraform-kubernetes-multi-cloud-ack-aks-dok-eks-gke-oke/#digital-ocean](https://napo.io/posts/terraform-kubernetes-multi-cloud-ack-aks-dok-eks-gke-oke/#digital-ocean)


<p align="center">
<img alt="Digital Ocean Logo" src="https://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/DigitalOcean_logo.svg/240px-DigitalOcean_logo.svg.png">
</p>


- [Terraform Kubernetes on Digital Ocean](#Terraform-Kubernetes-on-Digital-Ocean)
- [Requirements](#Requirements)
- [Features](#Features)
- [Notes](#Notes)
- [Defaults](#Defaults)
- [Runtime](#Runtime)
- [Terraform Inputs](#Terraform-Inputs)
- [Outputs](#Outputs)


## Requirements

You need a [Digital Ocean account](https://m.do.co/c/b40b1325cb18) and a [Personal access token](https://cloud.digitalocean.com/account/api/tokens).


## Features

* Always uses latest available Kubernetes version on Digital Ocean
* Kubernetes Cluster with 1 + 2 = *3* worker nodes (default node pool + additional node pool)
* **kubeconfig** file generation at completion


## Notes

* The resources will be created in your default Digital Ocean project
* If you want to add/remove worker nodes, just edit the `do_k8s_nodepool_size` variable
* It can take 2-3 minutes after Terraform completes until the Kubernetes nodes are available
* `export KUBECONFIG=./kubeconfig_do` in repo root dir to use the generated kubeconfig file
* The `enable_digitalocean` is used in the hajowieland/terraform-kubernetes-multi-cloud module

## Defaults

See tables at the end for a comprehensive list of inputs and outputs.


* Default region: **fra1** _(Frankfurt, Germany)_
* Default Kubernetes version: **1.14.2-do.0**
* Default Node type: **s-1vcpu-2gb** _(1x vCPU, 2GB memory)_
* Default main pool size: **1**
* Default additional node pool size: **2**


## Runtime

Runtime `terraform apply`:

~5-7min

```
2.56s user
0.89s system
7:16.37 total
```

```
2.38s user
0.75s system
5:15.77 total
```


## Terraform Inputs

| Name | Description | Type | Default | Required |
|------|-------------|:----:|:-----:|:-----:|
| enable_digitalocean | Enable / Disable Digital Ocean | bool | true | yes |
| random_cluster_suffix | Random 6 byte hex suffix for cluster name | string |  | yes |
| do_k8s_nodes | Worker nodes | int | 2 | yes |
| do_token | Digital Ocean Personal access token | string | DUMMY | **yes** |
| do_region | Digital Ocean region | string | fra1 | yes |
| do_k8s_name | Digital Ocean Kubernetes cluster name | string | k8s-do | yes |
| do_k8s_pool_name | Digital Ocean Kubernetes default node pool name | string | k8s-nodepool-do | yes |
| do_k8s_nodes | Digital Ocean Kubernetes default node pool size | number | 1 | yes |
| do_k8s_node_type | Digital Ocean Kubernetes default node pool type | string | s-1vcpu-2gb | yes |
| do_k8s_nodepool_type | Digital Ocean Kubernetes additional node pool type | string | s-1vcpu-2gb | yes |
| do_k8s_nodepool_size | Digital Ocean Kubernetes additional node pool size | number | 2 | yes |




## Outputs

| Name | Description |
|------|-------------|
| kubeconfig_path_do | Kubernetes kubeconfig file |
