# Module: security (referencia)

Propósito: controles de perímetro nativo (WAF/Shield) y parámetros de TLS.

## Entradas (Inputs)
| Nombre | Tipo | Descripción | Requerido | Default |
|---|---|---|---|---|
| waf_ruleset_ids | list(string) | Conjunto de reglas WAF a aplicar | no | [] |
| shield_advanced | bool | Activar AWS Shield Advanced | no | false |
| cloudflare_zone_id | string | Zona Cloudflare (referencial) | no | "" |
| tls_policy | string | Política TLS mínima | no | TLSv1.2 |
| allowed_cidrs_admin | list(string) | Rangos admin permitidos | no | [] |
| tags | map(string) | Tags obligatorios | sí | — |

## Salidas (Outputs)
| Nombre | Descripción |
|---|---|
| waf_web_acl_arn | ARN de la WebACL creada |
| shield_subscription | Estado de Shield Advanced |

## Ejemplo de uso (ilustrativo)
```hcl
module "security" {
	source            = "./modules/security"
	waf_ruleset_ids   = ["common-threats", "bot-control"]
	shield_advanced   = true
	tls_policy        = "TLSv1.2_2021"
	allowed_cidrs_admin = ["203.0.113.0/24"]
	tags = var.tags
}
```

## Configuración sugerida
- Reglas equivalentes en Cloudflare y WAF (mitigar desalineación gestionando IaC desde un único origen, no incluido aquí).
- TLS 1.2+ extremo a extremo; certificados en ACM.
- Lista explícita de rangos admin permitidos para accesos operativos (solo egress o bastión si aplica).

Notas:
- La configuración de Cloudflare está fuera del alcance de este repo (referencia conceptual).
