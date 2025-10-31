# 13 — Estructura del repositorio (guía rápida)

Este documento explica la finalidad de cada carpeta/archivo para que el lector identifique dónde está cada artefacto.

## Árbol general

```
security-cloud-proposal/
├─ README.md                    # Visión general y cómo presentar
├─ SECURITY.md                  # Lineamientos mínimos de seguridad
├─ CONTRIBUTING.md              # Guía de contribución (docs/diagramas)
├─ CODEOWNERS                   # Responsables por dominio
├─ diagrams/                    # Diagramas Mermaid
│  ├─ architecture-tobe.mmd     # Arquitectura de referencia
│  └─ cicd-sequence.mmd         # Secuencia CI/CD
├─ docs/                        # Documentación por dominio
│  ├─ 00-overview.md
│  ├─ 01-architecture-tobe.md
│  ├─ 02-terraform-approach.md
│  ├─ 03-cicd-github-actions.md
│  ├─ 04-governance-and-policies.md
│  ├─ 05-decisions-tradeoffs.md
│  ├─ 06-runbooks.md
│  ├─ 07-observability.md
│  ├─ 08-references.md
│  ├─ 09-requirements-matrix.md
│  ├─ 10-presentacion-ejecutiva.md
│  ├─ 11-checklist-evaluacion.md
│  ├─ 12-anexos.md              # Enlaces a PNG y PDFs en assets/
│  └─ README.md                 # Índice de documentación
├─ iac/terraform/               # Estructura de referencia (sin .tf)
│  ├─ modules/                  # Módulos por dominio (README)
│  ├─ live/                     # Composición por entorno (README)
│  ├─ global/bootstrap/         # Estado remoto S3+DynDB (README)
│  ├─ policies/                 # Policy-as-code conceptual (README)
│  ├─ base-files.md             # Esqueletos de archivos .tf (en MD)
│  └─ README.md
└─ assets/                      # Anexos (imagen y PDFs)
   ├─ arquitectura-tobe.png
   ├─ propuesta-solucion.pdf
   └─ prueba-tecnica.pdf
```

## Sugerencias de navegación
- Si evalúas arquitectura: empieza por `docs/01-architecture-tobe.md` y `diagrams/architecture-tobe.mmd`.
- Si evalúas IaC/CI: visita `docs/02-terraform-approach.md` y `docs/03-cicd-github-actions.md`, junto con `iac/terraform/`.
- Para ver cobertura del enunciado: `docs/09-requirements-matrix.md`.
- Para operación/observabilidad: `docs/06-runbooks.md` y `docs/07-observability.md`.
