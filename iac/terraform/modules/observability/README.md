# Module: observability (referencia)

Propósito: telemetría unificada (logs/métricas/trazas) y sintéticos.

Entradas sugeridas:
- `log_retention_days` (number)
- `metrics_namespaces` (list(string))
- `synthetics_endpoints` (list(object))
- `alarm_endpoints` (list(object))
- `tags` (map(string))

Configuración sugerida:
- Logs estructurados en JSON con `trace_id` para correlación con X‑Ray.
- Retención 30–90 días en CloudWatch; export y archivado en S3 con lifecycle.
- Canaries en rutas críticas con tolerancias alineadas a SLOs.
- Dashboards por dominio (API, ECS, DB, Redis, NLB/API GW).
