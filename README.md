Terraform module for Kubernetes Cert Manager
==========================================

Terraform module used to create Cert Manager in Kubernetes, with auto http validation issuer. With simple syntax.

## Usage

#### For activate auto generating TLS, please add this annotation to ingress: 
    `cert-manager.io/cluster-issuer = module.cert_manager.cluster_issuer_name`

#### Terraform example
```terraform
module "cert_manager" {
  source        = "terraform-iaac/cert-manager/kubernetes"
  
  cluster_issuer_email                   = "admin@mysite.com"
  cluster_issuer_name                    = "cert-manager-global"
  cluster_issuer_private_key_secret_name = "cert-manager-private-key"
}

```

## Inputs

| Name | Description | Type | Default |  Required |
|------|-------------|------|---------|:--------:|
| namespace\_name  | Name of created namespace | `string` | `cert-manager` | no |
| cluster\_issuer\_server | The ACME server URL | `string` | `https://acme-v02.api.letsencrypt.org/directory` | no |
| cluster\_issuer\_email | Email address used for ACME registration | `string` | n/a |  yes |
| cluster\_issuer\_private\_key\_secret\_name | Name of a secret used to store the ACME account private key | `string` | `cert-manager-private-key` |  no |
| cluster\_issuer\_name | Cluster Issuer Name, used for annotations | `string` | `cert-manager` |  no |
| cluster\_issuer\_create | Create Cluster Issuer? Note: you should create your own issuer if value `false` | `bool` | `true` |  no |
| cluster\_issuer\_yaml | Create Cluster Issuer with your yaml. NOTE: some variables stop to work in case when you using this parameter | `string` | `null` |  no |
| additional\_set | Additional sets to Helm | <pre>list(object({<br>    name  = string<br>    value = string<br>    type  = string // Optional<br>  }))</pre> | `[]` |  no |

## Outputs
| Name | Description |
|------|:-----------:|
| namespace | Namespace used by cert manager |
| cluster\_issuer\_name | Created cluster issuer |
| cluster\_issuer\_server | ACME Server used by Cluster Issuer |
| cluster\_issuer\_private\_key\_name | Name of secrets, where cert manager stores private key | 

## Terraform Requirements

| Name | Version |
|------|---------|
| terraform | >= 0.13.0 |
| kubernetes | >= 1.13 |
| helm | >= 2.1.0 |
| gavinbunney/kubectl | ~> 1.11.1 |

Cert Manager Version: v1.4.0

Source: https://github.com/jetstack/cert-manager

Tutorials: https://cert-manager.io/docs/