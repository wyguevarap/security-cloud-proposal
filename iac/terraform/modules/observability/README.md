# Module: observability (referencia)

Propósito: telemetría unificada (logs/métricas/trazas) y sintéticos.

## Entradas (Inputs)
| Nombre | Tipo | Descripción | Req | Default |
|---|---|---|---|---|
| log_retention_days | number | Días de retención en CloudWatch | no | 30 |
| metrics_namespaces | list(string) | Namespaces para métricas personalizadas | no | [] |
| synthetics_endpoints | list(object) | Canaries para rutas críticas | no | [] |
| alarm_endpoints | list(object) | Destinos de alarma (SNS, etc.) | no | [] |
| tags | map(string) | Tags obligatorios | sí | — |

## Salidas (Outputs)
| Nombre | Descripción |
|---|---|
| dashboard_urls | URLs de dashboards creados |
| log_groups | Nombres de log groups |

## Ejemplo de uso (ilustrativo)
```hcl
module "observability" {
	source              = "./modules/observability"
	log_retention_days  = 60
	metrics_namespaces  = ["app/api"]
	synthetics_endpoints = [
		{ name = "health", url = "https://example.com/health", interval = 5 }
	]
	tags = var.tags
}
```

## Configuración sugerida
- Logs estructurados en JSON con `trace_id` para correlación con X‑Ray.
- Retención 30–90 días en CloudWatch; export y archivado en S3 con lifecycle.
- Canaries en rutas críticas con tolerancias alineadas a SLOs.
- Dashboards por dominio (API, ECS, DB, Redis, NLB/API GW).
