# Module: data (referencia)

Propósito: bases de datos y caché para cargas transaccionales con alta disponibilidad.

## Entradas (Inputs)
| Nombre | Tipo | Descripción | Req | Default |
|---|---|---|---|---|
| engine | string | Motor (postgresql) | sí | postgresql |
| capacity | string/number | Capacidad/Clase | sí | — |
| multi_az | bool | Alta disponibilidad | no | true |
| backup_retention | number | Retención de backups (días) | no | 7 |
| pitr_enabled | bool | Point-in-time recovery | no | true |
| redis_node_type | string | Tipo de nodo Redis | no | cache.t3.micro |
| tags | map(string) | Tags obligatorios | sí | — |

## Salidas (Outputs)
| Nombre | Descripción |
|---|---|
| aurora_cluster_arn | ARN del clúster |
| aurora_writer_endpoint | Endpoint escritor |
| aurora_reader_endpoint | Endpoint de lectura |
| redis_endpoint | Endpoint de Redis |

## Ejemplo de uso (ilustrativo)
```hcl
module "data" {
	source           = "./modules/data"
	engine           = "postgresql"
	capacity         = "db.r6g.large"
	multi_az         = true
	backup_retention = 7
	pitr_enabled     = true
	redis_node_type  = "cache.t3.micro"
	tags             = var.tags
}
```

## Configuración sugerida
- Aurora PostgreSQL con cluster Multi‑AZ; habilitar PITR y métricas de `replica_lag`.
- Redis Multi‑AZ como read‑through cache; TTL con jitter para evitar thundering herd.
- Cifrado KMS para RDS/Redis; secretos de credenciales en Secrets Manager.

Notas:
- Considerar `query routing` para lecturas pesadas hacia readers.
