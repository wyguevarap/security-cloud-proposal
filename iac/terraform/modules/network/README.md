# Module: network (referencia)

Propósito: VPC y componentes de red mínimos para arquitectura privada con API Gateway privado + VPC Link + NLB.

## Requisitos (conceptual)
- AWS provider ≥ 5.x

## Entradas (Inputs)
| Nombre | Tipo | Descripción | Requerido | Valor por defecto |
|---|---|---|---|---|
| env | string | Entorno: dev/test/prod | sí | — |
| region | string | Región AWS | sí | — |
| cidr_block | string | CIDR principal de la VPC | sí | — |
| az_count | number | Número de AZ a utilizar | no | 2 |
| enable_nat_per_az | bool | NAT por AZ para HA | no | true |
| tags | map(string) | Tags obligatorios | sí | — |

## Salidas (Outputs)
| Nombre | Descripción |
|---|---|
| vpc_id | ID de la VPC |
| public_subnets | IDs de subredes públicas (front) |
| private_app_subnets | IDs de subredes privadas de aplicación |
| private_data_subnets | IDs de subredes privadas de datos |
| nat_gw_ids | NAT Gateways por AZ |
| endpoints | Endpoints VPC creados |

## Ejemplo de uso (ilustrativo, no se incluye `.tf` en este repo)
```hcl
module "network" {
	source              = "./modules/network"
	env                 = var.env
	region              = var.region
	cidr_block          = "10.0.0.0/16"
	az_count            = 2
	enable_nat_per_az   = true
	tags = {
		Owner        = "platform"
		Environment  = var.env
		CostCenter   = "1234"
		DataClass    = "internal"
		RTO          = "30m"
		RPO          = "5m"
	}
}
```

## Configuración sugerida
- Subredes por función y AZ: `front-public`, `app-private`, `data-private`.
- NAT por AZ para resiliencia (coste ↑; evaluar si el egress es crítico).
- Endpoints VPC para servicios internos (S3, STS, ECR, Secrets/SSM).

## Dependencias
- Ninguna estricta; típicamente se crea antes que `compute`/`data`.

Notas:
- No expone ALB públicos. El tráfico de entrada pasa por API Gateway privado → VPC Link → NLB interno.
