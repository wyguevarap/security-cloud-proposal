# 07 — Observabilidad

## Métricas clave
- API: latencia P50/P95, tasa de errores 4xx/5xx, *rate‑limit hits*.
- ECS: CPU/mem, *task failures*, *restart count*, *circuit breaker trips*.
- Aurora: conexiones, *replica lag*, *deadlocks*, IOPS/latencia.
- Redis: *hit ratio*, *evictions*, latencia, conexiones.
- NLB/API GW: *healthy targets*, *TLS handshake errors*.
- Red: egress por NAT, endpoints VPC por AZ.
- Logs: CW Logs estructurados; correlación con `trace_id` (X‑Ray).

## Synthetics y salud
- Rutas críticas con *canary checks*; tolerancias por SLO; alertas multi‑canal.
