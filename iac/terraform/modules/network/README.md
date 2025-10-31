# Module: network (referencia)

Propósito: VPC y componentes de red mínimos para arquitectura privada con API Gateway privado + VPC Link + NLB.

Entradas sugeridas:
- `env` (string)
- `region` (string)
- `cidr_block` (string)
- `az_count` (number)
- `enable_nat_per_az` (bool)
- `tags` (map(string))

Salidas sugeridas:
- `vpc_id`, `public_subnets`, `private_app_subnets`, `private_data_subnets`, `nat_gw_ids`, `endpoints`

Configuración sugerida:
- Subredes por función y AZ: `front-public`, `app-private`, `data-private`.
- NAT por AZ para resiliencia (coste ↑; evaluar si el egress es crítico).
- Endpoints VPC para servicios internos (S3, STS, ECR, Secrets/SSM).

Notas:
- No expone ALB públicos. El tráfico de entrada pasa por API Gateway privado → VPC Link → NLB interno.
