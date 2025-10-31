# 04 — Gobernanza y políticas (code‑free)

## Controles mínimos obligatorios
- **Tags**: `CostCenter`, `Owner`, `Environment`, `DataClass`, `RTO`, `RPO`.
- **Cifrado** en reposo (KMS) y tránsito (TLS 1.2+).  
- **S3 Block Public Access**.  
- **IAM** de mínimo privilegio; separación de funciones (plan/apply/drift).

## Policy‑as‑Code (conceptual)
- Reglas OPA/Conftest: naming, tags, cifrado, versiones mínimas, bloqueo público.
- `tfsec/Checkov`: exposición pública, puertos abiertos, recursos sin cifrado.
- *Gates* obligatorias en PR y **bloqueo** del `apply` en caso de incumplimiento.

## Auditoría y trazabilidad
- Artefactos de `plan`, reportes y metadatos de pipelines almacenados 90 días.
- Export a S3 `audit-logs/ci` (JSON) y tablero de cambios.
