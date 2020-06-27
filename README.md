# Terraform Rancher
Terraform to deploy Rancher server on vSphere

# Releases
Please check the [releases](https://github.com/NetApp/ez-rancher/releases) page.

## Requirements
If you're running locally:
* [Terraform](https://www.terraform.io/downloads.html) >= 0.12
* [Kubectl](https://downloadkubernetes.com/)
* [Terraform RKE plugin](https://github.com/rancher/terraform-provider-rke)
* netcat

## Getting Started
For tfvars config file examples, refer to [tfvars examples](docs/TfvarsExamples.md)

#### Local
```bash
# create cluster
terraform apply -var-file=rancher.tfvars terraform/vsphere-rancher
# remove cluster
terraform destroy -var-file=rancher.tfvars terraform/vsphere-rancher
```

#### Docker
```bash
make image
# create cluster
docker run -it --rm -v ${PWD}/rancher.tfvars:/terraform/vsphere-rancher/terraform.tfvars -v ${PWD}/deliverables:/terraform/vsphere-rancher/deliverables terraform-rancher apply -state=deliverables/terraform.tfstate
# remove cluster
docker run -it --rm -v ${PWD}/rancher.tfvars:/terraform/vsphere-rancher/terraform.tfvars -v ${PWD}/deliverables:/terraform/vsphere-rancher/deliverables terraform-rancher destroy -state=deliverables/terraform.tfstate
```

or

```bash
make shell
# create cluster
terraform apply -var-file=terraform.tfvars -state=deliverables/terraform.tfstate
# remove cluster
terraform destroy -var-file=terraform.tfvars -state=deliverables/terraform.tfstate
```

## Notes

* `terraform apply` will create a `deliverables/` directory to save things like the kubeconfig, ssh keys, etc
* Releases will be published as container images in Github