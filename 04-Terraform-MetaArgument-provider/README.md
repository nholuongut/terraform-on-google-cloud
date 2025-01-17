# Title: GCP Google Cloud Platform - Terraform Meta-Argument Provider

![](https://i.imgur.com/waxVImv.png)
### [View all Roadmaps](https://github.com/nholuongut/all-roadmaps) &nbsp;&middot;&nbsp; [Best Practices](https://github.com/nholuongut/all-roadmaps/blob/main/public/best-practices/) &nbsp;&middot;&nbsp; [Questions](https://www.linkedin.com/in/nholuong/)
<br/>

# # Description:
- Learn Terraform Meta-Argument Provider

## Step-01: Introduction
- Learn [Terraform Meta-Argument Provider](https://developer.hashicorp.com/terraform/language/meta-arguments/resource-provider)

## Step-02: c1-versions.tf
```hcl
# Terraform Settings Block
terraform {
  required_version = ">= 1.8"
  required_providers {
    google = {
      source = "hashicorp/google"
      version = ">= 5.34.0"
    }
  }
}

# Terraform Provider-1: us-central1
provider "google" {
  project = "gcplearn9"
  region = "us-central1"
  alias = "us-central1"    
}

# Terraform Provider-2: europe-west1
provider "google" {
  project = "gcplearn9"
  region = "europe-west1"
  alias = "europe-west1"  
}
```

## Step-03: c3-vpc.tf
```hcl
# Resource: VPC
resource "google_compute_network" "myvpc" {
  project = "gcplearn9"
  name = "vpc1"
  auto_create_subnetworks = false   
}

# Resource: Subnet1
resource "google_compute_subnetwork" "mysubnet1" {
  provider = google.us-central1   # Define provider to use
  name = "subnet1"
  ip_cidr_range = "10.128.0.0/20"
  network = google_compute_network.myvpc.id 
}

# Resource: Subnet2
resource "google_compute_subnetwork" "mysubnet2" {
  provider = google.europe-west1   # Define provider to use
  name = "subnet2"
  ip_cidr_range = "10.132.0.0/20"
  network = google_compute_network.myvpc.id 
}
```

## Step-04: Execute Terraform Commands
```t
# Terraform Initialize
terraform init

# Terraform Validate
terraform validate

# Terraform Plan
terraform plan

# Terraform Apply
terraform apply
Observation: 
1. Subnets will be created in both regions
```

## Step-05: Clean-Up
```t
# Terraform Destroy
terraform destroy --auto-approve
[or]
terraform apply --destroy --auto-approve
```

![](https://i.imgur.com/waxVImv.png)
# 🚀 I'm are always open to your feedback.  Please contact as bellow information:
### [Contact Me]
* [Name: Nho Luong]
* [Skype](luongutnho_skype)
* [Github](https://github.com/nholuongut/)
* [Linkedin](https://www.linkedin.com/in/nholuong/)
* [Email Address](luongutnho@hotmail.com)
* [PayPal.me](https://www.paypal.com/paypalme/nholuongut)

![](https://i.imgur.com/waxVImv.png)
![](Donate.png)
[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/nholuong)

# License
* Nho Luong (c). All Rights Reserved.🌟