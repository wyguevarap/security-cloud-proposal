# Índice de documentación

Guía de lectura para evaluar rápidamente la propuesta.

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

Diagramas (Mermaid):
- Arquitectura: `../diagrams/architecture-tobe.mmd`
- Pipeline CI/CD: `../diagrams/cicd-sequence.mmd`

Consejo para la revisión:
1) Revisa `09-requirements-matrix.md` y ve abriendo cada enlace. 2) Valida SLOs y supuestos en `00-overview.md`. 3) Confirma resiliencia/seguridad en `01-architecture-tobe.md` y `SECURITY.md`. 4) Cierra con `06-runbooks.md` (operabilidad).
