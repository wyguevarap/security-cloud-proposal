# Policy-as-Code (referencia)

Ejemplos de controles (conceptuales) a implementar con OPA/Conftest o validadores equivalentes:
- Tags obligatorios presentes (`CostCenter`, `Owner`, `Environment`, `DataClass`, `RTO`, `RPO`).
- Cifrado at-rest habilitado en S3/EBS/RDS/ElastiCache/Logs.
- Bloqueo de acceso público en S3.
- Recursos públicos prohibidos salvo excepciones justificadas.
- Versiones mínimas de providers y Terraform.

> Este repo no incluye Rego ni reglas ejecutables; es una guía para la organización de las políticas.
