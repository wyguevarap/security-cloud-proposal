# Module: data (referencia)

Propósito: bases de datos y caché para cargas transaccionales con alta disponibilidad.

Entradas sugeridas:
- `engine` (string: postgresql)
- `capacity` (string/number)
- `multi_az` (bool)
- `backup_retention` (number)
- `pitr_enabled` (bool)
- `redis_node_type` (string)
- `tags` (map(string))

Configuración sugerida:
- Aurora PostgreSQL con cluster Multi‑AZ; habilitar PITR y métricas de `replica_lag`.
- Redis Multi‑AZ como read‑through cache; TTL con jitter para evitar thundering herd.
- Cifrado KMS para RDS/Redis; secretos de credenciales en Secrets Manager.

Notas:
- Considerar `query routing` para lecturas pesadas hacia readers.
