# terraform-google-gpu-rdma-vpc

## Description
### Tagline
This is an auto-generated module.

### Detailed
This module was generated from [terraform-google-module-template](https://github.com/terraform-google-modules/terraform-google-module-template/), which by default generates a module that simply creates a GCS bucket. As the module develops, this README should be updated.

The resources/services/activations/deletions that this module will create/trigger are:

- Create a GCS bucket with the provided name

### PreDeploy
To deploy this blueprint you must have an active billing account and billing permissions.

## Architecture
![alt text for diagram](https://www.link-to-architecture-diagram.com)
1. Architecture description step no. 1
2. Architecture description step no. 2
3. Architecture description step no. N

## Documentation
- [Hosting a Static Website](https://cloud.google.com/storage/docs/hosting-static-website)

## Deployment Duration
Configuration: X mins
Deployment: Y mins

## Cost
[Blueprint cost details](https://cloud.google.com/products/calculator?id=02fb0c45-cc29-4567-8cc6-f72ac9024add)

## Usage

Basic usage of this module is as follows:

```hcl
module "gpu_rdma_vpc" {
  source  = "terraform-google-modules/gpu-rdma-vpc/google"
  version = "~> 0.1"

  project_id  = "<PROJECT ID>"
  bucket_name = "gcs-test-bucket"
}
```

Functional examples are included in the
[examples](./examples/) directory.

<!-- BEGINNING OF PRE-COMMIT-TERRAFORM DOCS HOOK -->
## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| delete\_default\_internet\_gateway\_routes | If set, ensure that all routes within the network specified whose names begin with 'default-route' and with a next hop of 'default-internet-gateway' are deleted | `bool` | `false` | no |
| deployment\_name | The name of the current deployment | `string` | n/a | yes |
| enable\_internal\_traffic | Enable a firewall rule to allow all internal TCP, UDP, and ICMP traffic within the network | `bool` | `true` | no |
| firewall\_log\_config | Firewall log configuration for Toolkit firewall rules (var.enable\_iap\_ssh\_ingress and others) | `string` | `"DISABLE_LOGGING"` | no |
| firewall\_rules | List of firewall rules | `any` | `[]` | no |
| mtu | The network MTU (default: 8896). Recommended values: 0 (use Compute Engine default), 1460 (default outside HPC environments), 1500 (Internet default), or 8896 (for Jumbo packets). Allowed are all values in the range 1300 to 8896, inclusively. | `number` | `8896` | no |
| network\_description | An optional description of this resource (changes will trigger resource destroy/create) | `string` | `""` | no |
| network\_name | The name of the network to be created (if unsupplied, will default to "{deployment\_name}-net") | `string` | `null` | no |
| network\_profile | A full or partial URL of the network profile to apply to this network.<br>This field can be set only at resource creation time. For example, the<br>following are valid URLs:<br>- https://www.googleapis.com/compute/beta/projects/{projectId}/global/networkProfiles/{network_profile_name}<br>- projects/{projectId}/global/networkProfiles/{network\_profile\_name}} | `string` | n/a | yes |
| network\_routing\_mode | The network routing mode (default "REGIONAL") | `string` | `"REGIONAL"` | no |
| nic\_type | NIC type for use in modules that use the output | `string` | `"MRDMA"` | no |
| project\_id | Project in which the HPC deployment will be created | `string` | n/a | yes |
| region | The default region for Cloud resources | `string` | n/a | yes |
| shared\_vpc\_host | Makes this project a Shared VPC host if 'true' (default 'false') | `bool` | `false` | no |
| subnetworks\_template | Specifications for the subnetworks that will be created within this VPC.<br><br>count       (number, required, number of subnets to create, default is 8)<br>name\_prefix (string, required, subnet name prefix, default is deployment name)<br>ip\_range    (string, required, range of IPs for all subnets to share (CIDR format), default is 192.168.0.0/16)<br>region      (string, optional, region to deploy subnets to, defaults to vars.region) | <pre>object({<br>    count       = number<br>    name_prefix = string<br>    ip_range    = string<br>    region      = optional(string)<br>  })</pre> | <pre>{<br>  "count": 8,<br>  "ip_range": "192.168.0.0/16",<br>  "name_prefix": null,<br>  "region": null<br>}</pre> | no |

## Outputs

| Name | Description |
|------|-------------|
| network\_id | ID of the new VPC network |
| network\_name | Name of the new VPC network |
| network\_self\_link | Self link of the new VPC network |
| subnetwork\_interfaces | Full list of subnetwork objects belonging to the new VPC network (compatible with vm-instance and Slurm modules) |
| subnetwork\_interfaces\_gke | Full list of subnetwork objects belonging to the new VPC network (compatible with gke-node-pool) |
| subnetwork\_name\_prefix | Prefix of the RDMA subnetwork names |
| subnetworks | Full list of subnetwork objects belonging to the new VPC network |

<!-- END OF PRE-COMMIT-TERRAFORM DOCS HOOK -->

## Requirements

These sections describe requirements for using this module.

### Software

The following dependencies must be available:

- [Terraform][terraform] v0.13
- [Terraform Provider for GCP][terraform-provider-gcp] plugin v3.0

### Service Account

A service account with the following roles must be used to provision
the resources of this module:

- Storage Admin: `roles/storage.admin`

The [Project Factory module][project-factory-module] and the
[IAM module][iam-module] may be used in combination to provision a
service account with the necessary roles applied.

### APIs

A project with the following APIs enabled must be used to host the
resources of this module:

- Google Cloud Storage JSON API: `storage-api.googleapis.com`

The [Project Factory module][project-factory-module] can be used to
provision a project with the necessary APIs enabled.

## Contributing

Refer to the [contribution guidelines](./CONTRIBUTING.md) for
information on contributing to this module.

[iam-module]: https://registry.terraform.io/modules/terraform-google-modules/iam/google
[project-factory-module]: https://registry.terraform.io/modules/terraform-google-modules/project-factory/google
[terraform-provider-gcp]: https://www.terraform.io/docs/providers/google/index.html
[terraform]: https://www.terraform.io/downloads.html

## Security Disclosures

Please see our [security disclosure process](./SECURITY.md).
