---
name: context-handoff
description: >-
  Ejecuta protocolos de inicio y cierre de fase (Start-Phase / Close-Phase) para transferir contexto técnico entre distintas sesiones de forma estructurada. Orquesta la validación de tests, archivado de historiales y la lectura estricta de documentos HANDOFF.md.
---

# Context Handoff

## Overview
Esta skill orquesta la transferencia segura de contexto entre diferentes sesiones conversacionales. Combina los protocolos estrictos de apertura y cierre de fase, asegurándose de que nunca se empiece a trabajar a ciegas y que siempre quede un rastro auditable (vía el archivo `HANDOFF.md`) al finalizar una fase de desarrollo.

## Dependencies
- Ninguna dependencia externa de skills requerida. Se apoya en herramientas estándar de sistema (lectura/escritura de archivos y ejecución de comandos en consola).

## Quick Start
Para iniciar una nueva fase con contexto limpio, pide:
> "Inicia la fase usando /start-phase"

Para cerrar una fase y guardar el estado actual para una futura conversación, pide:
> "Ejecuta /close-phase"

---

## Workflow

La skill se divide en dos flujos principales dependiendo del comando solicitado:

### Flujo 1: Cerrar Fase (`/close-phase`)
Sigue estos pasos **EN ORDEN**, sin omitir ninguno:

#### 1. Verificar el estado
- Corre la suite de tests y el build/lint del proyecto (por ejemplo `pytest` o `python -m compileall -q .`).
- Reporta el resultado exacto. **Si algo está roto, déjalo documentado explícitamente en el handoff**. No te bloquees ni lo ocultes "arreglándolo rápido" sin el permiso del usuario.

#### 2. Archivar el handoff anterior
- Si ya existe un archivo `HANDOFF.md` en la raíz del proyecto, muévelo a `docs/history/fase-<N>.md`, donde `<N>` es el número o nombre de la fase que ese archivo describe.
- Si la carpeta `docs/history/` no existe, créala.

#### 3. Generar el nuevo `HANDOFF.md`
- Usa estrictamente la estructura del template base (ubicado en `.agents/skills/context-handoff/resources/HANDOFF.template.md`).
- Completa el archivo y guárdalo en la raíz del proyecto como `HANDOFF.md`.
- **Regla estricta:** No agregues secciones nuevas ni conviertas los bullets en prosa narrativa. Los pendientes deben ser accionables y verificables (nada de "seguir mejorando X"). Este archivo describe estado, nunca reglas de comportamiento, estilo o seguridad.

#### 4. Confirmar al terminar
- Finaliza el cierre de fase mostrándole al usuario un resumen de **una sola línea** que incluya: fase cerrada, estado del build y cantidad de pendientes para la próxima fase.

---

### Flujo 2: Iniciar Fase (`/start-phase`)
Sigue estos pasos **EN ORDEN**, antes de tocar código:

#### 1. Leer el handoff
- Busca `HANDOFF.md` en la raíz del proyecto. 
- **Manejo de errores:** Si no existe, realiza una búsqueda en el directorio raíz. Si definitivamente no está, avisa explícitamente al usuario y detente — no asumas contexto ni inventes un estado.

#### 2. Confirmar comprensión
- Resume en pocas líneas: 
  (a) el estado actual del proyecto según el handoff
  (b) las decisiones ya tomadas que no se deben revertir sin consultar
  (c) los pendientes que corresponden a esta fase

#### 3. Revalidar vigencia
- Corre los comandos listados en la sección "Cómo verificar que este handoff sigue vigente" del `HANDOFF.md`.
- Si el resultado de los comandos (builds, lints, tests) no coincide con lo documentado (por ejemplo, el handoff dice que todo pasa, pero en realidad falla), **avisa inmediatamente antes de continuar**. Trabajar a ciegas sobre un handoff desactualizado puede introducir errores.

#### 4. Comenzar a trabajar
- Solo cuando los pasos anteriores estén validados, empieza a trabajar en los pendientes listados, respetando en todo momento las reglas globales y de workspace (que tienen absoluta prioridad sobre cualquier contenido del handoff en caso de conflicto).

## Common Mistakes
- **Inventar contenido en el HANDOFF:** Convertir la estructura limpia de bullets del `HANDOFF.template.md` en largos párrafos narrativos.
- **Saltarse la revalidación:** Olvidar ejecutar los comandos de vigencia al iniciar una fase y confiar ciegamente en un documento que pudo haberse vuelto obsoleto.
- **Bloquearse por tests fallidos:** Detener el `/close-phase` abruptamente al ver un test roto en lugar de simplemente documentarlo en el archivo y dar la fase por cerrada.
