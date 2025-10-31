# Arquitectura de Seguridad Cloud — Artefactos Ilustrativos (sin HCL/YAML)

Este repositorio **no contiene código** de infraestructura ni pipelines. Está pensado como **complemento documental** para la propuesta de arquitectura (TO‑BE), demostrando criterio profesional en **resiliencia, seguridad, automatización y gobernanza**.

> **Objetivo:** ofrecer artefactos de referencia —diagramas, decisión de diseño, flujos operativos y lineamientos IaC/CI-CD— para evaluación técnica.  
> **Alcance:** documentación ejecutiva y técnica, *code-free* (solo Markdown y Mermaid).

## Contenido
- `docs/` — Explicación técnica por dominios (TO‑BE, IaC con Terraform, CI‑CD con GitHub Actions, Gobierno, Observabilidad, Runbooks) y matriz de cobertura de requisitos. Revisa el índice en `docs/README.md`.
- `diagrams/` — Diagramas Mermaid (`.mmd`) para arquitectura y pipelines.
- `iac/terraform/` — Estructura de referencia de IaC (carpetas y esqueletos en Markdown, sin `.tf`).
- `assets/` — Anexos (PNG/PDF). Ver índice en `docs/12-anexos.md`.
- `SECURITY.md` — Lineamientos mínimos de seguridad.
- `CONTRIBUTING.md` — Forma de contribuir a los artefactos.
- `CODEOWNERS` — Responsables por dominio (ejemplo).
- `LICENSE` — MIT.

Para una vista detallada de la estructura, consulta `docs/13-estructura-del-repo.md`.

## Visualizar diagramas Mermaid
Puedes ver los `.mmd` directamente en GitHub o pegarlos en el editor de Mermaid (https://mermaid.live).

## Resumen ejecutivo
- **Perímetro dual:** Cloudflare (edge) y WAF+Shield (nativo AWS) para defensa en profundidad.
- **Entrada API:** API Gateway privado + VPC Link → NLB interno (L7→L4) con *rate‑limit* y contratos centralizados.
- **Cómputo inmutable:** ECS Fargate multi‑AZ con *autoscaling*, *circuit breaker* y capacidad mínima por zona.
- **Datos resilientes:** Aurora PostgreSQL Multi‑AZ (writer/reader, PITR) + Redis Multi‑AZ como *read‑through cache*.
- **Red duplicada por AZ:** subredes, NAT GW, endpoints, targets y tareas simétricos por zona.
- **Observabilidad 360°:** CloudWatch, X‑Ray, CloudTrail a S3 cifrado; *Synthetics/health checks* por servicio.
- **Gobernanza IaC:** Terraform modular (estado remoto S3 + lock DynDB), OIDC con GitHub, *policy‑as‑code* (tflint, tfsec/Checkov, OPA), *drift detection* y *Infracost*.
- **CI‑CD GitHub Actions:** `plan` en PR (artefactos + puertas de calidad), `apply` en rama protegida con aprobaciones y OIDC por *job*.
- **Trade‑offs conscientes:** +HA (+coste), consistencia eventual controlada en caché, complejidad mitigada con IaC y runbooks.

> **SLOs guía:** disponibilidad 99.95 %, **RPO ≤ 5 min**, **TTR/MTTR ≤ 30/10 min** (recuperación).

## Cómo presentar (rápido)
- Comienza por `docs/README.md` (índice + mapa de navegación).
- Muestra los diagramas: `diagrams/architecture-tobe.mmd` y `diagrams/cicd-sequence.mmd` (visualízalos en https://mermaid.live si es necesario).
- Recorre la matriz `docs/09-requirements-matrix.md` para evidenciar cobertura del enunciado.
- Si piden anexos, apunta a `docs/12-anexos.md` y a la carpeta `assets/` (imagen y PDFs).

## Qué NO incluye
- No hay código de infraestructura (`.tf`) ni pipelines (`.yml/.yaml`).
- No se automatiza Cloudflare ni WAF en este repo (solo se describe el patrón y controles).

## Sugerencias de configuración clave
- Nombres y etiquetas: `<org>-<dominio>-<env>-<region>`, tags obligatorias: `CostCenter`, `Owner`, `Environment`, `DataClass`, `RTO`, `RPO`.
- Backend de estado: S3 cifrado + DynamoDB para lock por entorno/cuenta (`iac/terraform/global/bootstrap/`).
- OIDC GitHub→AWS: roles por job (Plan/Apply/Drift), sesiones ≤ 1h, boundaries por repo/branch/entorno.
- Retención de logs y archivado: 30–90 días en CloudWatch, export a S3 con lifecycle a Glacier.
