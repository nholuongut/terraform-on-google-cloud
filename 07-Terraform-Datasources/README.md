# Title: GCP Google Cloud Platform - Terraform Datasources

![](https://i.imgur.com/waxVImv.png)
### [View all Roadmaps](https://github.com/nholuongut/all-roadmaps) &nbsp;&middot;&nbsp; [Best Practices](https://github.com/nholuongut/all-roadmaps/blob/main/public/best-practices/) &nbsp;&middot;&nbsp; [Questions](https://www.linkedin.com/in/nholuong/)
<br/>
# Description: 
- Learn Terraform Datasources on Google Cloud Platform

## Step-01: Introduction
- Learn [Terraform Datasources](https://developer.hashicorp.com/terraform/language/data-sources)

## Step-02: c5-datasource.tf
```hcl
# Terraform Datasources
data "google_compute_zones" "available" {    
  status = "UP"
}

# Output value
output "compute_zones" {
  description = "List of compute zones"
  value = data.google_compute_zones.available.names
}
```

## Step-03: c6-01-vminstance.tf
```hcl
# Resource Block: Create a single Compute Engine instance
resource "google_compute_instance" "myapp1" {
  # Meta-Argument: count
  count = 2
  name         = "myapp1-vm-${count.index}"
  machine_type = var.machine_type
  zone         = data.google_compute_zones.available.names[count.index]
  tags        = [tolist(google_compute_firewall.fw_ssh.target_tags)[0], tolist(google_compute_firewall.fw_http.target_tags)[0]]

  boot_disk {
    initialize_params {
      image = "debian-cloud/debian-12"
    }
  }

  # Install Webserver
  metadata_startup_script = file("${path.module}/app1-webserver-install.sh")

  network_interface {
    subnetwork = google_compute_subnetwork.mysubnet.id   
    access_config {
      # Include this section to give the VM an external IP address
    }
  }
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
```

# Step-05: Verify VM Instances
- Go to Google Cloud -> Compute Engine -> VM Instances
- **Observation:** VM Instances will be created in two different zones in a region

## Step-06: Clean-Up
```t
# Terraform Destroy
terraform destroy -auto-approve
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