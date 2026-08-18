# Orchestration Enforcement Rule

**ID:** `orchestration-enforcement`
**Scope:** Ejecución de Planes de Implementación (`implementation_plan.md`)
**Contexto:** Transición del "Planning Mode" al "Execution Mode" tras la aprobación del usuario.

## Directivas Obligatorias

Cuando te encuentres en *Planning Mode*, hayas redactado un `implementation_plan.md` y el USUARIO te dé la autorización explícita para proceder o ejecutar el plan, **TIENES TERMINANTEMENTE PROHIBIDO** ejecutar los cambios de código por ti mismo. Debes seguir estrictamente este flujo de trabajo:

1. **Invocación Obligatoria del Orquestador:**
   DEBES delegar la ejecución completa del plan al subagente `agents_orchestrator` (basado en el perfil de `agency-agents/specialized/agents-orchestrator.md`). Si el subagente no está definido en la sesión actual, debes usar `define_subagent` primero.

2. **Inyección de Contexto:**
   Al invocar al Orquestador, debes proporcionarle el contenido (o un resumen sumamente detallado) del `implementation_plan.md` como su especificación de proyecto oficial. 

3. **Mandato de Quality Gates (Dev-QA Loop):**
   Debes instruir explícitamente al Orquestador para que:
   - Divida el plan en tareas discretas.
   - Invoque a los subagentes desarrolladores (ej. `python_refactorer`, `software_architect`) para escribir el código.
   - Invoque obligatoriamente a un subagente de calidad (ej. `qa_engineer`, `evidence_qa`) para auditar la tarea terminada antes de avanzar al siguiente ítem.

4. **Reporte Transparente:**
   Mientras la orquestación ocurre en segundo plano, tu único trabajo es mantener informado al usuario sobre el progreso del Orquestador y sus subagentes, respetando siempre la regla de identificación (`subagent_identification.md`), usando citas o prefijos como `🗣️ [Subagente: Agents Orchestrator]`.

## Excepciones
Esta regla NO aplica a:
- Ajustes menores (typos, arreglos de linting de una línea).
- Investigaciones de código (grep, lecturas).
- Peticiones del usuario de "solo lectura" o de "prueba rápida" donde no se generó un plan formal.
