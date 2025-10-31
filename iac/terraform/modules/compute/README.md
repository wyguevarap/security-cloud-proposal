# Module: compute (referencia)

Propósito: desplegar servicios en ECS Fargate detrás de NLB interno.

## Entradas (Inputs)
| Nombre | Tipo | Descripción | Req | Default |
|---|---|---|---|---|
| service_name | string | Nombre lógico del servicio | sí | — |
| desired_count_per_az | number | Tareas por AZ | no | 1 |
| cpu | number | CPU por tarea | sí | — |
| memory | number | Memoria por tarea | sí | — |
| image | string | Imagen del contenedor | sí | — |
| env_vars | map(string) | Variables de entorno | no | {} |
| secrets | list(object) | Secretos inyectados | no | [] |
| target_group_health | object | Umbrales de health check | no | {interval=30,healthy_threshold=3} |
| tags | map(string) | Tags obligatorios | sí | — |

## Salidas (Outputs)
| Nombre | Descripción |
|---|---|
| service_arn | ARN del servicio ECS |
| target_group_arn | ARN del TG asociado |

## Ejemplo de uso (ilustrativo)
```hcl
module "compute" {
	source               = "./modules/compute"
	service_name         = "api"
	desired_count_per_az = 1
	cpu                  = 512
	memory               = 1024
	image                = "123456789012.dkr.ecr.us-east-1.amazonaws.com/api:1.0.0"
	env_vars = {
		LOG_LEVEL = "info"
	}
	secrets = [
		{ name = "DB_URL", valueFrom = "arn:aws:secretsmanager:...:secret:db-url" }
	]
	target_group_health = { interval = 30, healthy_threshold = 3 }
	tags = var.tags
}
```

## Configuración sugerida
- Mínimo 1 tarea por AZ (capacidad de base) + autoscaling por CPU/mem/latencia.
- Health check del target group acorde a SLOs (p95 y timeout/backoff razonables).
- Variables vía SSM y secretos en Secrets Manager (no embebidos en la tarea).
- Activar circuit breaker y deployment configuration segura (porcentaje y tiempos).

Notas:
- No publica ALB; el tráfico llega por VPC Link → NLB.
