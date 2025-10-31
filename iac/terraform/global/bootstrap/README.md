# global/bootstrap (referencia)

Recursos globales compartidos (creados una sola vez):
- S3 bucket para `tfstate` (cifrado, bloqueo de acceso público, versionado).
- DynamoDB para `state locking`.
- KMS (opcional) para cifrar el estado.

> Planifica este stack fuera del ciclo frecuente de cambios.
