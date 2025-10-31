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

## Diagrama — Organización IaC
```mermaid
flowchart TD
	A[iac/terraform] --> B[modules]
	A --> C[live]
	A --> D[global/bootstrap]
	A --> E[policies]

	B --> B1[network]
	B --> B2[security]
	B --> B3[compute]
	B --> B4[data]
	B --> B5[observability]
	B --> B6[iam]

	C --> C1[dev]
	C --> C2[test]
	C --> C3[prod]

	click B1 "../iac/terraform/modules/network/README.md" "network"
	click B2 "../iac/terraform/modules/security/README.md" "security"
	click B3 "../iac/terraform/modules/compute/README.md" "compute"
	click B4 "../iac/terraform/modules/data/README.md" "data"
	click B5 "../iac/terraform/modules/observability/README.md" "observability"
	click B6 "../iac/terraform/modules/iam/README.md" "iam"
```

## Sugerencias de configuración
- Backend S3: `bucket = <org>-tfstate`, `key = <stack>/<env>/terraform.tfstate`, `dynamodb_table = <org>-tf-locks`, `encrypt = true`.
- Nombres consistentes: `<org>-<dominio>-<env>-<region>` para recursos y etiquetas `Name`.
- Tags obligatorias: `CostCenter`, `Owner`, `Environment`, `DataClass`, `RTO`, `RPO` (ver `docs/04-governance-and-policies.md`).
- IAM CI/CD: OIDC GitHub→AWS con roles por job (`PlanRole`, `ApplyRole`, `DriftRole`) y sesiones ≤ 1h.
- Retención de logs: 30–90 días en CloudWatch; archivado a S3 con lifecycle a Glacier.
- Lint/Seguridad/Coste: `tflint`, `tfsec/Checkov`, `OPA/Conftest`, `Infracost` como gates en PR.

## Separación de responsabilidades (ejemplo)
- `modules/*`: implementación reusable por dominio.
- `live/*`: composición por entorno (define backend y variables del stack).
- `global/bootstrap`: artefactos únicos (S3/DynamoDB/KMS) para estado remoto.
- `policies/`: reglas conceptuales de cumplimiento (OPA/Conftest) a aplicar en CI.

> Ver `docs/04-governance-and-policies.md` para políticas mínimas.
