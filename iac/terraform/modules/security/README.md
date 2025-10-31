# Module: security (referencia)

Propósito: controles de perímetro nativo (WAF/Shield) y parámetros de TLS.

Entradas sugeridas:
- `waf_ruleset_ids` (list(string))
- `shield_advanced` (bool)
- `cloudflare_zone_id` (string)
- `tls_policy` (string)
- `allowed_cidrs_admin` (list(string))
- `tags` (map(string))

Configuración sugerida:
- Reglas equivalentes en Cloudflare y WAF (mitigar desalineación gestionando IaC desde un único origen, no incluido aquí).
- TLS 1.2+ extremo a extremo; certificados en ACM.
- Lista explícita de rangos admin permitidos para accesos operativos (solo egress o bastión si aplica).

Notas:
- La configuración de Cloudflare está fuera del alcance de este repo (referencia conceptual).
