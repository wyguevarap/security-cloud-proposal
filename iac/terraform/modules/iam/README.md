# Module: iam (referencia)

Propósito: federación OIDC GitHub→AWS y roles por job con mínimo privilegio.

## Entradas (Inputs)
| Nombre | Tipo | Descripción | Req | Default |
|---|---|---|---|---|
| oidc_provider_url | string | URL del proveedor OIDC (GitHub) | sí | — |
| repo | string | owner/repo | sí | — |
| branch | string | Rama autorizada | sí | — |
| env | string | Entorno | sí | — |
| roles | object | Definición de Plan/Apply/Drift | no | {} |
| tags | map(string) | Tags | no | {} |

## Salidas (Outputs)
| Nombre | Descripción |
|---|---|
| role_arns | ARNs de roles Plan/Apply/Drift |

## Ejemplo de uso (ilustrativo)
```hcl
module "iam" {
	source            = "./modules/iam"
	oidc_provider_url = "https://token.actions.githubusercontent.com"
	repo              = "org/repo"
	branch            = "main"
	env               = var.env
	roles             = {
		plan  = { policies = ["ReadOnlyAccess"] }
		apply = { policies = ["PowerUserAccess"] }
		drift = { policies = ["ReadOnlyAccess"] }
	}
}
```

## Configuración sugerida
- Trust policy restringida por `sub` (repo, branch, path) y `aud` (sts.amazonaws.com).
- Permisos por rol:
	- PlanRole: solo lectura de estado y `terraform plan`.
	- ApplyRole: mutación controlada y lock de DynamoDB.
	- DriftRole: lectura para `plan` programado.
- Sesiones ≤ 1h; uso de boundaries y condition keys donde aplique.
