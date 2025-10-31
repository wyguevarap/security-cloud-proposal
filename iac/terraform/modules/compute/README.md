# Module: compute (referencia)

Propósito: desplegar servicios en ECS Fargate detrás de NLB interno.

Entradas sugeridas:
- `service_name` (string)
- `desired_count_per_az` (number)
- `cpu`/`memory` (number)
- `image` (string)
- `env_vars` (map(string))
- `secrets` (list(object))
- `target_group_health` (object)
- `tags` (map(string))

Configuración sugerida:
- Mínimo 1 tarea por AZ (capacidad de base) + autoscaling por CPU/mem/latencia.
- Health check del target group acorde a SLOs (p95 y timeout/backoff razonables).
- Variables vía SSM y secretos en Secrets Manager (no embebidos en la tarea).
- Activar circuit breaker y deployment configuration segura (porcentaje y tiempos).

Notas:
- No publica ALB; el tráfico llega por VPC Link → NLB.
