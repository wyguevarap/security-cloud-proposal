# 09 — Matriz de cobertura de requisitos

> Propósito: trazar cada requerimiento típico de una prueba de Arquitectura de Seguridad Cloud con los artefactos de este repositorio. Ajusta/añade filas según el enunciado específico.

| Dominio | Requerimiento típico | Cubierto en |
|---|---|---|
| Perímetro y entrada | WAF/DDoS, protección Bot, rate-limit, TLS 1.2+ | `01-architecture-tobe.md` (perímetro dual), `SECURITY.md` |
| Red | VPC privada, subredes por AZ, endpoints VPC, sin exposición pública | `01-architecture-tobe.md`, `SECURITY.md` |
| Balanceo y HA | Multi‑AZ, health checks, failover controlado | `01-architecture-tobe.md`, `06-runbooks.md` |
| Cómputo | Inmutabilidad, autoscaling, despliegues seguros | `01-architecture-tobe.md`, `03-cicd-github-actions.md` |
| Datos | Cifrado at‑rest, Aurora Multi‑AZ, PITR, caché con TTL | `01-architecture-tobe.md`, `SECURITY.md` |
| Certificados y secretos | TLS con ACM; secretos en Secrets Manager; parámetros en SSM | `01-architecture-tobe.md`, `SECURITY.md` |
| Identidad | OIDC para CI/CD, mínimo privilegio, separación de funciones | `03-cicd-github-actions.md`, `SECURITY.md` |
| IaC | Terraform modular, estado remoto con lock, lint/security gates | `02-terraform-approach.md`, `04-governance-and-policies.md` |
| CI/CD | Plan en PR, apply protegido, evidencias, rollback | `03-cicd-github-actions.md`, `06-runbooks.md` |
| Observabilidad | Métricas, logs, trazas, sintéticos, alertas | `07-observability.md` |
| Gobernanza | Tags obligatorios, políticas mínimas, auditoría | `04-governance-and-policies.md`, `SECURITY.md` |
| Cumplimiento | Alineación con marcos (CIS/NIST/ISO), trazabilidad | `08-references.md`, `04-governance-and-policies.md` |

## Notas de adecuación
- Cloud agnóstico por diseño (ejemplos en AWS). Si el enunciado exige Azure/GCP, sustituir servicios equivalentes:
  - API GW ⇄ Azure API Management / GCP API Gateway
  - ECS Fargate ⇄ Azure Container Apps/AKS / GKE Autopilot
  - Aurora ⇄ Azure Database for PostgreSQL (HA) / Cloud SQL HA
  - CloudWatch/X‑Ray ⇄ Azure Monitor/App Insights / Cloud Operations Suite
- Añadir cualquier requerimiento específico del cliente (por ejemplo, residencia de datos, claves administradas por el cliente, SSO corporativo, integración con SIEM externo) y enlazarlo a la sección correspondiente.
