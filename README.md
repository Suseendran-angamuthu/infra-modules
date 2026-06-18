# Infra Modules

Reusable Terraform modules for AWS infrastructure. Build once, use everywhere.

[![Terraform Validate](https://github.com/Suseendran-angamuthu/infra-modules/actions/workflows/validate.yml/badge.svg)](https://github.com/Suseendran-angamuthu/infra-modules/actions/workflows/validate.yml)

## Available Modules

| Module | Description |
|--------|-------------|
| [vpc](./modules/vpc) | VPC with public/private subnets, IGW, NAT Gateway |

## Quick Start

```hcl
module "vpc" {
  source = "github.com/Suseendran-angamuthu/infra-modules//modules/vpc?ref=v1.0.0"

  name               = "my-project"
  cidr_block         = "10.0.0.0/16"
  availability_zones = ["us-east-1a", "us-east-1b"]
  enable_nat_gateway = true

  tags = {
    Environment = "production"
    Project     = "my-project"
  }
}
```

## Prerequisites

- Terraform >= 1.5
- AWS credentials configured (any method):
  - `aws configure` (access keys)
  - AWS SSO (`aws sso login`)
  - Environment variables
  - OIDC (for CI/CD)

## Required IAM Permissions

To deploy the VPC module, your credentials need:
- `ec2:CreateVpc`, `ec2:DeleteVpc`, `ec2:DescribeVpcs`
- `ec2:CreateSubnet`, `ec2:DeleteSubnet`, `ec2:DescribeSubnets`
- `ec2:CreateInternetGateway`, `ec2:DeleteInternetGateway`
- `ec2:CreateNatGateway`, `ec2:DeleteNatGateway`
- `ec2:CreateRouteTable`, `ec2:CreateRoute`
- `ec2:AllocateAddress`, `ec2:ReleaseAddress`
- `ec2:CreateTags`

## Contributing

1. Create a feature branch
2. Make changes
3. Run `terraform fmt -recursive` and `terraform validate`
4. Submit a pull request

## License

MIT
