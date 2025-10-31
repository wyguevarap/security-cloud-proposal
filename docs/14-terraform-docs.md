# 14 — Documentación automática con terraform-docs

Este repositorio es documental (sin `.tf`), pero recomendamos usar `terraform-docs` en el repo de IaC real para generar README de módulos con Inputs/Outputs/Providers/Resources.

## ¿Qué es terraform-docs?
Herramienta que escanea módulos de Terraform y genera documentación estandarizada (Markdown/Asciidoc, etc.).

## Instalación local (opcional)
- macOS (Homebrew):
```bash
brew install terraform-docs
```
- Binario:
```bash
curl -sSLo /usr/local/bin/terraform-docs \
  https://github.com/terraform-docs/terraform-docs/releases/download/v0.19.0/terraform-docs-v0.19.0-darwin-amd64
chmod +x /usr/local/bin/terraform-docs
```

## Uso básico
Dentro del módulo (que contenga `.tf`):
```bash
terraform-docs markdown table . > README.md
```

## Configuración por archivo `.terraform-docs.yml` (ejemplo)
> No incluir en este repo; usar en el repo de IaC real.
```yaml
formatter: markdown table
sort:
  enabled: true
  by: name
sections:
  hide:
    - requirements
    - providers
    - modules
    - resources
settings:
  anchor: true
  default: true
  escape: false
```

## Integración en CI (opcional)
- Pre-commit hook con `pre-commit-terraform` o job de GitHub Actions que ejecute `terraform-docs` y verifique cambios.
- Recomendación: fallar el pipeline si el README del módulo no está actualizado tras cambios de inputs/outputs.
- Ejemplo funcionando: en el repo demo se incluyó un workflow en `.github/workflows/terraform-docs.yml` que genera y empuja el `README.md` del módulo en cada PR.

## Convención aplicada en este repo
- Cada `modules/*/README.md` ya sigue la estructura típicamente generada por `terraform-docs`: Inputs, Outputs, Ejemplo de uso y Notas.
- En un repo activo, reemplaza estas tablas manuales por la salida real de `terraform-docs`.

## Demo práctica
Se creó un repo de ejemplo con un módulo mínimo y README generado por `terraform-docs`:
- https://github.com/wyguevarap/terraform-docs-sample

Comando usado para generar README:
```bash
terraform-docs markdown table modules/network > modules/network/README.md
```
