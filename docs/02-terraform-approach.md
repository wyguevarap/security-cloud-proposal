# 02 — Enfoque Terraform (sin HCL)

## Diseño modular
- Módulos por dominio: `network/`, `security/`, `compute/`, `data/`, `observability/`, `iam/` (ver `iac/terraform/modules/`).
- Variables normalizadas (`env`, `region`, `tags`), *defaults* seguros (sin acceso público, cifrado on, retención logs).

## Estado y bloqueo
- Backend S3 cifrado + **lock en DynamoDB** por entorno/cuenta (ver `iac/terraform/global/bootstrap/`).
- Estados **aislados por dominio** para reducir *blast radius*.

## Seguridad IaC (*shift-left*)
- `tflint`, `tfsec/Checkov`, `OPA/Conftest`, `Infracost` en PR.
- **OIDC** GitHub→AWS, sin llaves permanentes; *least privilege* por *job*.

## Reutilización y *drift*
- Versionado semántico de módulos; `plan` programado para detectar *drift* (issue automático).

## Estructura de referencia
- Árbol propuesto y esqueletos en `iac/terraform/`.
- Archivos base documentados en `iac/terraform/base-files.md` (no se incluyen `.tf` activos en este repo).

> Ver `docs/04-governance-and-policies.md` para políticas mínimas.
