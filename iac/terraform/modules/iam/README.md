# Module: iam (referencia)

Propósito: federación OIDC GitHub→AWS y roles por job con mínimo privilegio.

Entradas sugeridas:
- `oidc_provider_url` (string)
- `repo` (string)
- `branch` (string)
- `env` (string)
- `roles` (object): PlanRole/ApplyRole/DriftRole
- `tags` (map(string))

Configuración sugerida:
- Trust policy restringida por `sub` (repo, branch, path) y `aud` (sts.amazonaws.com).
- Permisos por rol:
	- PlanRole: solo lectura de estado y `terraform plan`.
	- ApplyRole: mutación controlada y lock de DynamoDB.
	- DriftRole: lectura para `plan` programado.
- Sesiones ≤ 1h; uso de boundaries y condition keys donde aplique.
