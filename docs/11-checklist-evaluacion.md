# 11 — Checklist de evaluación

Usa esta lista para verificar rápidamente que la propuesta cumple los puntos clave.

- [ ] Perímetro con defensa en profundidad (edge + nativo) y TLS 1.2+ extremo a extremo.
- [ ] API de entrada privada (API GW privado + VPC Link + NLB) sin ALB públicos.
- [ ] Multi‑AZ simétrico (subredes, NAT, endpoints, targets) y health checks.
- [ ] Cómputo inmutable con autoscaling y circuit breaker.
- [ ] Datos con HA (Aurora Multi‑AZ), PITR y caché Redis con TTL y jitter.
- [ ] Cifrado at‑rest (KMS) y in‑transit; S3 Block Public Access.
- [ ] IAM mínimo privilegio, separación de funciones (plan/apply/drift).
- [ ] OIDC GitHub→AWS sin llaves permanentes; permisos por job y entorno.
- [ ] Terraform modular con backend remoto + lock; gates: fmt/validate/lint/security/cost/OPA.
- [ ] Plan en PR con artefactos; apply en main con aprobaciones y checksum del plan.
- [ ] Observabilidad 360°: métricas, logs, trazas, sintéticos; retención y lifecycle.
- [ ] Runbooks de failover, degradación de DB y rollback IaC.
- [ ] Matriz de requisitos actualizada y referencias a marcos (CIS/NIST/ISO).
