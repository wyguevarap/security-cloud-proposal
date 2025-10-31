# 06 — Runbooks de operación (extracto)

## Falla de una AZ
1. **Detección**: alarmas de NLB / health checks / incremento 5xx.
2. **Acción**: verificación de `target health` y *drain* en AZ afectada.
3. **ECS**: forzar *redeploy* de tareas en AZ sanas (capacidad mínima respetada).
4. **Datos**: validar *replica lag* Aurora < umbral; *failover* si writer afectado.
5. **Cierre**: *post‑mortem* con métricas adjuntas y acciones preventivas.

## Degradación en Aurora (lag/latencia)
1. Inspeccionar *replica lag* y métricas de I/O.
2. Activar *query routing* a readers para lecturas pesadas.
3. Aumentar *provisioned IOPS* (si aplica) y ajustar *pool size* Redis.
4. Evaluar *failover* y ejecutar *PITR* si hay corrupción.

## Rollback de cambio IaC
1. `git revert` del commit responsable.
2. Ejecutar `plan` validado en **test**; si es sano, promover a **prod**.
3. Notificar y adjuntar artefactos de evidencias.
