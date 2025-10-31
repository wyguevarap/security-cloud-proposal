# 01 — Arquitectura TO‑BE

## Diagrama de alto nivel
```mermaid
flowchart LR
  user[Usuarios / Clientes] --> cf[Cloudflare (Edge)]
  user --> waf[WAF + Shield (Nativo AWS)]
  cf --> r53[Route 53 Health Checks / Failover]
  waf --> r53

  r53 --> apigw[API Gateway (Privado)]
  apigw --> vpclink[VPC Link]
  vpclink --> nlb[NLB (L4 Interno)]

  nlb --> ecs1[ECS Fargate (AZ-A)]
  nlb --> ecs2[ECS Fargate (AZ-B)]
  nlb --> ecs3[ECS Fargate (AZ-C)]

  subgraph Data
    aurora[(Aurora PostgreSQL Multi-AZ)]
    redis[(Redis Multi-AZ / ElastiCache)]
  end

  ecs1 --> redis
  ecs2 --> redis
  ecs3 --> redis
  ecs1 --> aurora
  ecs2 --> aurora
  ecs3 --> aurora

  subgraph Network
    subnets[Subredes privadas por AZ]
    nat[NAT Gateways por AZ]
    endpoints[Endpoints VPC]
  end

  apigw -.logs/metrics/traces.-> cw[(CloudWatch/X-Ray)]
  ecs1 -.logs/metrics.-> cw
  ecs2 -.logs/metrics.-> cw
  ecs3 -.logs/metrics.-> cw
  cw -.archive.-> s3[(S3 Cifrado + Lifecycle)]
```

### Servicios de soporte y seguridad
- Certificados TLS con **ACM** terminando en Cloudflare/API GW según dominio; rotación automatizada.
- Gestión de secretos en **Secrets Manager** y parámetros no sensibles en **SSM Parameter Store**.
- Identidades y permisos con **IAM** (mínimo privilegio; roles por job/entorno en CI/CD).
- **CloudTrail** para auditoría de APIs con export a S3 cifrado y retención con lifecycle.
- Observabilidad con **CloudWatch** y **X‑Ray**; correlación de trazas.

### Notas de diseño (alineación con To‑Be)
- La entrada expone dominios en Route 53; se protege en el edge con Cloudflare y en el perímetro nativo con WAF+Shield.
- **API Gateway es privado**; el enrutamiento hacia servicios internos se realiza por **VPC Link** a un **NLB** interno. No se publican ALB.
- Subredes separadas por función (front público, aplicación privada, datos privados), simétricas en AZ‑A/AZ‑B (y AZ‑C si aplica).
- **ECS Fargate** ejecuta contenedores inmutables detrás del NLB; comunicación a **Aurora** (writer/reader) y **Redis** para alivio de lectura.
- **IGW/NAT** existen para egress controlado (parches, repos de contenedores, etc.), no para tráfico de entrada de la API privada.

## Cambios clave vs AS‑IS
- Sustituye ALB públicos por **API GW privado + VPC Link + NLB**.
- **Cómputo inmutable** (ECS Fargate) con *autoscaling* y *circuit breaker*.
- **Datos**: Aurora Multi‑AZ (PITR) + **Redis** como *read‑through cache*.
- **Red**: duplicación por AZ (subredes, NAT, endpoints, *targets*).
- **Observabilidad**: centralización y *health checks* por ruta crítica.

## Resiliencia y HA
- **Failover** controlado por Route 53 (health checks) y NLB multi‑AZ.
- **RPO ≤ 5 min**: réplica Aurora + PITR; caché con TTL y *jitter*.
- **TTR ≤ 30 min**: runbooks de *redeploy/failover* y verificación sintética.
