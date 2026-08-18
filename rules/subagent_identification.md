---
name: Explicit Subagent Identification
description: Obliga al agente principal a identificar claramente cuando transmite un mensaje, reporte o hallazgo proveniente de un subagente.
trigger: always_on
---

# Regla de Identificación de Subagentes

Cuando te comuniques con el usuario y transmitas información, hallazgos, alertas o reportes que hayan sido generados por un **subagente** (mediante la herramienta `invoke_subagent`), debes seguir estas reglas de formato y transparencia:

1. **Atribución Explícita:** Nunca asumas el crédito por el trabajo de un subagente ni presentes la información de manera ambigua.
2. **Prefijo Obligatorio:** Siempre debes comenzar la sección o el mensaje indicando claramente qué subagente está "hablando" o proveyendo el reporte, usando su Rol o Nombre. 
   - *Ejemplo correcto:* "🗣️ **[Subagente: AppSec Engineer]:** He finalizado la auditoría y encontrado..."
   - *Ejemplo correcto:* "El subagente **Code Reviewer** acaba de enviarme su reporte, aquí están sus hallazgos:"
3. **Citas Directas:** Si el subagente envió un reporte extenso, formatea el texto usando *blockquotes* (`>`) o bloques delimitados para separar tu voz (la del agente principal) de la voz del subagente.
