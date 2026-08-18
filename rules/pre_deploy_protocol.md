---
name: Pre-Deploy Protocol
description: 4 gates obligatorios antes de cualquier push a Main-stable. Previene que código roto llegue a producción.
trigger: always_on
---

# Protocolo Pre-Deploy — 4 Gates Obligatorios

Antes de ejecutar `git push origin Main-stable`, DEBES completar estos 4 gates en orden. Si alguno falla, el push se BLOQUEA hasta corregir.

## Gate 1 — Verificación de Migraciones
Después de cualquier refactor que renombre, elimine o mueva funciones/clases/imports, ejecutar grep exhaustivo sobre TODOS los archivos `.py` del proyecto:
```
Select-String -Path "*.py" -Pattern "nombre_eliminado" -Recurse
```
**Criterio:** 0 resultados. Si hay resultados → corregir antes de continuar.

## Gate 2 — Import Smoke Test
Importar CADA módulo del proyecto para detectar `ImportError`, `NameError` o `AttributeError`:
```
python -c "from flask_app import app; from com.bot import GAMMA; from logic.logic import ConexionSheets; from logic.financiero import AgenteFinanciero; from logic.cron_jobs import resumen_semanal, notificacion_clima, rotar_logs; from logger_config import setup_logger; print('OK')"
```
**Criterio:** Imprime `OK` sin errores.

## Gate 3 — Code Reviewer con Alcance COMPLETO
Invocar al Code Reviewer con la lista COMPLETA de archivos `.py` del proyecto (no solo los modificados). El reviewer DEBE emitir un artefacto `code_review_vX.Y.Z.md`. Hallazgos 🔴 bloquean el deploy.

## Gate 4 — Prueba Local
Levantar el bot con `run_bot.py` (polling local) y verificar que los comandos principales responden. Para lógica exclusiva de `flask_app.py`, levantar servidor Flask local temporal. NUNCA tocar el webhook de producción.

## Protocolo de Hotfix
En emergencias: Gates 1 y 2 son obligatorios pre-deploy. Gate 3 puede ser post-deploy (dentro de 24h). Gate 4 del endpoint afectado como mínimo.
