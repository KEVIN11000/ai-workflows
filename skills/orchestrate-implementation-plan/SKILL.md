---
name: Orchestrate Implementation Plan
description: Guía paso a paso para ejecutar un plan de implementación leyendo el documento y despachando al Agents Orchestrator.
---

# Habilidad: Ejecutar Plan de Implementación mediante el Orquestador

Cuando el usuario aprueba un `implementation_plan.md` y da luz verde para programar los cambios, **tienes estrictamente prohibido programar el código tú mismo**. Debes usar esta habilidad para delegar el trabajo.

## Paso 1: Leer el Plan
Si no tienes el contexto completo del plan de implementación en tu memoria inmediata, usa `view_file` para leer el archivo `implementation_plan.md` y entender qué se debe modificar.

## Paso 2: Invocar o Configurar al Orquestador
Debes invocar al subagente orquestador. 
- **Rol:** Tech Lead / Orchestrator
- **Modelo:** `inherit` o `pro`

Si el subagente no ha sido definido en la sesión, defínelo usando `define_subagent` con un prompt de sistema que le indique:
*"Eres el AgentsOrchestrator basado en la metodología de agency-agents. Debes coordinar a desarrolladores y QA para completar el plan de implementación. No permitas que una tarea pase a producción sin ser verificada por el QA Engineer."*

## Paso 3: Inyectar el Plan como Contexto
En el `Prompt` de invocación de `invoke_subagent`, entrégale al orquestador la lista exacta de tareas (ej: Tarea 1: refactorizar X. Tarea 2: inyectar dependencias en Y).
Instruye al orquestador a que despache subagentes de desarrollo para hacer las escrituras (`write_to_file`, `replace_file_content`) y un subagente de calidad (`qa_engineer`) para que verifique que el código compila y cumple los requisitos.

## Paso 4: Monitoreo y Reporte Transparente
Tu única labor durante la ejecución del plan es mantener al USUARIO informado. A medida que el Orquestador envíe reportes de avance a tu bandeja, deberás parafrasearlos (o citarlos textualmente respetando el formato `🗣️ [Subagente: Orquestador]`) y enviárselos al usuario para que sepa en qué paso del "Dev-QA Loop" va el equipo.
