# SECURITY — Lineamientos mínimos (code‑free)

## Identidad y acceso
- **Principio del mínimo privilegio**: roles por *job* y por entorno; sesiones cortas; separación `PlanRole`/`ApplyRole`/`DriftRole`.
- **Federación OIDC (GitHub→AWS)**: sin *Access Keys* permanentes; *boundaries* por repositorio/branch/entorno; `aud` validado.
- **Segregación de cuentas**: `dev`, `test`, `prod` en OUs distintas; SCP para *guardrails* globales (no detalladas aquí).

## Datos y cifrado
- Cifrado **at‑rest** con KMS para S3, EBS, RDS/Aurora, Redis, Logs.
- Cifrado **in‑transit**: TLS 1.2+ extremo a extremo (Cloudflare/API GW/NLB/servicios).
- **S3 Block Public Access** y *bucket policies* restrictivas; *lifecycle* a Glacier para logs fríos.

## Red y perímetro
- **Perímetro dual**: Cloudflare (edge) y WAF+Shield (nativo) con reglas equivalentes gestionadas vía IaC (no incluido).
- **API privada**: API GW privado + VPC Link → NLB interno; sin ALB públicos.
- **Multi‑AZ simétrico**: subredes, endpoints, NAT GW y *targets* por zona; *health checks* y *graceful failover*.

## Observabilidad y respuesta
- Métricas, logs y trazas centralizados (CloudWatch/X‑Ray/CloudTrail → S3).
- Alarmas por colas/CPU/latencia/errores/lag; *Synthetics* por ruta crítica; paneles por dominio.
- **Runbooks** de *failover/rollback* (ver `docs/06-runbooks.md`).

> Esta guía no sustituye estándares corporativos (CIS/NIST/ISO); sirve de base para auditorías y *gap analysis*.
