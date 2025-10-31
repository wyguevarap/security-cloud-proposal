# Esqueletos de archivos base (solo referencia)

A continuación se describen los esqueletos típicos. Copia/ajusta en un repo de IaC real; aquí se muestran como ejemplo, no se incluyen `.tf` activos.

## versions.tf (ejemplo)
```hcl
terraform {
  required_version = ">= 1.6.0"
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = ">= 5.0"
    }
  }
}
```

## providers.tf (ejemplo)
```hcl
provider "aws" {
  region = var.region
}
```

## backend.tf (solo en `live/*`) (ejemplo)
```hcl
terraform {
  backend "s3" {
    bucket         = "<org>-tfstate"
    key            = "<stack>/<env>/terraform.tfstate"
    region         = "<region>"
    dynamodb_table = "<org>-tf-locks"
    encrypt        = true
  }
}
```

## variables.tf (ejemplo)
```hcl
variable "env" {
  type        = string
  description = "Entorno: dev|test|prod"
  validation {
    condition     = contains(["dev", "test", "prod"], var.env)
    error_message = "env inválido"
  }
}

variable "tags" {
  type        = map(string)
  description = "Conjunto de tags obligatorios"
}
```

## outputs.tf (ejemplo)
```hcl
output "vpc_id" {
  value       = aws_vpc.this.id
  description = "ID de la VPC creada"
}
```

## main.tf (ejemplo de módulo network)
```hcl
module "vpc" {
  source = "./modules/network"
  env    = var.env
  tags   = var.tags
}
```
