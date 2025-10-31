# 05 — Decisiones y trade‑offs

| Problema | Alternativas | Decisión | Riesgo residual / Mitigación |
|---|---|---|---|
| Base de datos consistente | RDS estándar / Aurora / DynamoDB | **Aurora PG Multi‑AZ** | Coste ↑ (~20%) / Lag leve → *query routing* + monitoreo |
| Cómputo elástico | EC2 ASG / EKS / ECS | **ECS Fargate** | *Cold start* en picos → *warm tasks* + *autoscaling thresholds* |
| Perímetro y entrada | Solo WAF / Solo Cloudflare / Dual | **Modelo dual** | Doble gestión de reglas → IaC unificada (no incluida) |
| Balanceo interno | ALB (L7) / NLB (L4) | **NLB (L4)** | Menor visibilidad L7 → X‑Ray + métricas CW |
| Carga en DB | Redis / DAX / Ninguno | **Redis Multi‑AZ** | Consistencia eventual → TTL + *jitter* + *write‑around* |
| Logs y costo | CloudWatch / OpenSearch / S3 | **S3 + Lifecycle** | Búsqueda lenta en frío → export temporal a OpenSearch |
| Secretos | Param Store / Secrets / Vault | **Secrets Manager** | Fallos de rotación → *grace period* + *retries* |
| Identidad CI/CD | Keys / Runners / OIDC | **OIDC** | Trust mal configurado → validación inicial |
| Multi‑entorno | Una cuenta / Multi‑cuenta | **Organizations + CT** | Overhead admin → módulos delegados |
| Monitoreo | Solo CW / 3rd party | **CW + X‑Ray + Synthetics** | Costo logs ↑ → retención y filtros |
