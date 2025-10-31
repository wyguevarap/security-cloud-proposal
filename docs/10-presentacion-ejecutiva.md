# 10 — Presentación ejecutiva (guion sugerido)

Duración objetivo: 10–12 minutos.

1. Contexto y objetivos (1 min)
   - SLOs guía (99.95% disp., RPO ≤ 5 min, TTR ≤ 30 min) y alcance.
2. Arquitectura TO‑BE (4 min)
   - Perímetro dual (Cloudflare + WAF/Shield), API privada (API GW + VPC Link + NLB), cómputo inmutable (ECS Fargate) y datos (Aurora+Redis).
   - Resiliencia Multi‑AZ, health checks y failover.
3. Seguridad y Gobernanza (2 min)
   - Cifrado at‑rest/in‑transit, tagging, S3 BPA, IAM mínimo privilegio, auditoría.
   - Policy‑as‑code y gates obligatorias.
4. IaC y CI/CD (2 min)
   - Terraform modular, estado remoto S3+DynDB, OIDC GitHub→AWS.
   - Plan en PR, apply protegido en main, artefactos firmados.
5. Operación y observabilidad (1–2 min)
   - Métricas/logs/trazas, sintéticos críticos, runbooks de failover/rollback.
6. Riesgos y mitigaciones (1 min)
   - Coste/Complejidad/Consistencia eventual → controles y automatización.

Anexos útiles para preguntas:
- `05-decisions-tradeoffs.md` — decisiones y mitigaciones.
- `06-runbooks.md` — respuesta operativa.
- `09-requirements-matrix.md` — cobertura del enunciado.
