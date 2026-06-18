# VPC Module

Creates a production-ready VPC with public and private subnets across multiple availability zones.

## Features

- VPC with DNS support enabled
- Public subnets with Internet Gateway
- Private subnets with optional NAT Gateway
- Route tables with proper associations
- One NAT Gateway per AZ for high availability (when enabled)

## Usage

```hcl
module "vpc" {
  source = "github.com/Suseendran-angamuthu/infra-modules//modules/vpc?ref=v1.0.0"

  name               = "my-project"
  cidr_block         = "10.0.0.0/16"
  availability_zones = ["us-east-1a", "us-east-1b"]
  enable_nat_gateway = true

  tags = {
    Environment = "dev"
    Project     = "my-project"
  }
}
```

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|----------|
| name | Name prefix for all resources | string | - | yes |
| cidr_block | CIDR block for the VPC | string | "10.0.0.0/16" | no |
| availability_zones | List of AZs to use | list(string) | - | yes |
| enable_nat_gateway | Enable NAT Gateway (costs money) | bool | false | no |
| tags | Additional tags | map(string) | {} | no |

## Outputs

| Name | Description |
|------|-------------|
| vpc_id | The ID of the VPC |
| vpc_cidr_block | The CIDR block of the VPC |
| public_subnet_ids | List of public subnet IDs |
| private_subnet_ids | List of private subnet IDs |
| internet_gateway_id | The ID of the Internet Gateway |
| nat_gateway_ids | List of NAT Gateway IDs |
| public_route_table_id | The ID of the public route table |
| private_route_table_ids | List of private route table IDs |

## Cost Note

NAT Gateways cost ~$32/month per AZ plus data transfer. Set `enable_nat_gateway = false` for dev/test environments where private subnets don't need internet access.
