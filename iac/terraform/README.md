# Terraform — Estructura de referencia (sin HCL)

Este árbol define solo carpetas y archivos guía para ilustrar la organización propuesta. No incluye código `.tf` ni YAML.

## Estructura

```
iac/terraform/
├─ modules/
│  ├─ network/
│  ├─ security/
│  ├─ compute/
│  ├─ data/
│  ├─ observability/
│  └─ iam/
├─ live/
│  ├─ dev/
│  ├─ test/
│  └─ prod/
├─ global/
│  └─ bootstrap/
└─ policies/
```

## Convenciones
- Un módulo por dominio (entradas/salidas definidas, sin acoplamiento cruzado).
- Estados remotos aislados por dominio/entorno (backend S3 + lock DynamoDB; definido en cada `live/*`).
- Versionado semántico de módulos; PRs con gates (fmt/validate/lint/security/cost/OPA) en `docs/03-cicd-github-actions.md`.

## Archivos base esperados (documentados en `base-files.md`)
- `versions.tf` — versiones de Terraform y providers.
- `providers.tf` — proveedores y aliases.
- `backend.tf` — configuración del backend remoto (solo en `live/*`).
- `main.tf` — recursos/composición del módulo.
- `variables.tf` — entradas tipadas con `validation`.
- `outputs.tf` — salidas estables.

> Nota: este repositorio no contiene `.tf` reales; los esqueletos están en Markdown para propósitos ilustrativos.
