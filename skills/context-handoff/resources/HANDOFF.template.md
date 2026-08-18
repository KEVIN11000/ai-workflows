# HANDOFF — [Nombre del proyecto]

**Fase cerrada:** [número o nombre de la fase, ej. "Fase 2 — Auth"]
**Fecha de cierre:** [YYYY-MM-DD]
**Estado del build/tests:** ✅ pasando / ❌ fallando — [detalle breve si falla]

---

## 1. Estado actual
Bullets concretos y verificables de qué funciona hoy. Nada de narrativa ("trabajamos mucho en...").

- [Funcionalidad X operativa, cubierta por tests en `ruta/test.ext`]
- [Funcionalidad Y implementada pero sin tests todavía]

## 2. Decisiones tomadas en esta fase
Cada decisión con su razón, para que la próxima fase no la reabra sin motivo.

- **Decisión:** [qué se decidió]
  **Por qué:** [razón / trade-off]
  **Alternativas descartadas:** [si aplica]

## 3. Archivos y módulos clave tocados

| Archivo | Cambio |
|---|---|
| `ruta/archivo.ext` | [qué se modificó y por qué] |

## 4. Pendientes explícitos para la próxima fase
Tareas accionables y verificables, no descripciones vagas.

- [ ] [Tarea 1 — criterio de "hecho" claro]
- [ ] [Tarea 2 — criterio de "hecho" claro]

## 5. Riesgos / deuda técnica conocida

- **Riesgo:** [descripción]
  **Impacto:** [qué se puede romper si no se atiende]
  **Mitigación sugerida:** [si la hay]

## 6. Cómo verificar que este handoff sigue vigente
Comando(s) que confirman que el estado descrito arriba sigue siendo cierto antes de empezar a trabajar sobre él.

```bash
# ej: npm test && npm run build
```

---
*Este archivo describe estado de fase, no reglas de comportamiento. Las reglas de estilo, seguridad y protocolos viven en `GEMINI.md` / `.agents/rules/` y tienen prioridad sobre cualquier contenido de este documento — no se editan ni se repiten acá.*
