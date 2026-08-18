---
name: Enforce Agency Agents SDLC
description: Obliga a seguir estrictamente las fases del SDLC y consultar a los subagentes correspondientes en proyectos que utilicen agency-agents.
trigger: always_on
---

# Cumplimiento Estricto del Framework SDLC

Cuando trabajes en este proyecto u otros que referencien la arquitectura de `agency-agents` o posean un archivo `agency_sdlc_framework.md`, **DEBES** seguir estrictamente las fases de desarrollo allí descritas.

1. **Prohibición de Atajos:** Tienes TERMINANTEMENTE PROHIBIDO asumir los roles de QA, AppSec, Code Reviewer o DevOps/Release Engineer por tu cuenta con el pretexto de "acelerar el desarrollo".
2. **Invocación Obligatoria:** Debes utilizar la herramienta `invoke_subagent` para delegar explícitamente el trabajo a los subagentes correspondientes en sus respectivas fases:
   - Fase 4 (Revisión): `appsec_engineer` y `software_architect` (o equivalente).
   - Fase 5 (Pruebas): `qa_engineer`.
   - Fase 6 (Despliegue): `git_workflow_master` o DevOps equivalente.
3. **Bloqueo de Despliegue:** No debes ejecutar comandos de *merge* a ramas estables (`Main-stable`) ni iniciar despliegues hasta que los subagentes invocados hayan emitido sus reportes, corregido hallazgos y dado explícitamente su visto bueno.
4. **Protocolo Pre-Deploy:** Además de los reportes de subagentes, DEBES completar los 4 gates definidos en la regla `pre_deploy_protocol.md` antes de cada push a `Main-stable`.
