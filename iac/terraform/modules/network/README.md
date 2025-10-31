# Module: network (referencia)

Entradas sugeridas:
- `env` (string)
- `region` (string)
- `cidr_block` (string)
- `az_count` (number)
- `enable_nat_per_az` (bool)
- `tags` (map(string))

Salidas sugeridas:
- `vpc_id`, `public_subnets`, `private_app_subnets`, `private_data_subnets`, `nat_gw_ids`, `endpoints`

Recursos: VPC, subredes por función/AZ, NAT por AZ, endpoints VPC necesarios.
