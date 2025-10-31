# Índice de documentación

Esta guía te orienta sobre qué leer según el foco de evaluación.

## Núcleo
- 00 — Overview: `00-overview.md`
- 01 — Arquitectura TO‑BE (diagrama y decisiones): `01-architecture-tobe.md`
- 02 — Enfoque Terraform (modularidad, estado, seguridad shift‑left): `02-terraform-approach.md`
- 03 — CI‑CD con GitHub Actions (gates, OIDC, artefactos): `03-cicd-github-actions.md`
- 04 — Gobernanza y políticas (controles mínimos, policy‑as‑code): `04-governance-and-policies.md`
- 05 — Decisiones y trade‑offs: `05-decisions-tradeoffs.md`
- 06 — Runbooks (operación/failover/rollback): `06-runbooks.md`
- 07 — Observabilidad (métricas, logs, trazas, sintéticos): `07-observability.md`
- 08 — Referencias y glosario: `08-references.md`
- 09 — Matriz de cobertura de requisitos: `09-requirements-matrix.md`
- 12 — Anexos (imagen/PDFs): `12-anexos.md`
- 13 — Estructura del repositorio: `13-estructura-del-repo.md`

## Diagramas (Mermaid)
- Arquitectura: `../diagrams/architecture-tobe.mmd`
- Pipeline CI/CD: `../diagrams/cicd-sequence.mmd`

## Sugerencia de recorrido
1) Abre `09-requirements-matrix.md` y valida cobertura del enunciado.
2) Confirma SLOs en `00-overview.md` y arquitectura en `01-architecture-tobe.md` + `SECURITY.md`.
3) Revisa IaC/CI en `02-terraform-approach.md` y `03-cicd-github-actions.md`.
4) Cierra con `06-runbooks.md` y `07-observability.md` (operabilidad).
