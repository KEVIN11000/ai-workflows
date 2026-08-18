# Plan de Implementación – Prioridad Baja (Fase_Fenix)

## Acciones propuestas (pendientes de aprobación)

| Ítem | Acción | Descripción detallada | Responsable | Estimado |
|------|--------|------------------------|-------------|----------|
| **B1** | **Completar documentación (README)** | - Incluir pasos de configuración de credenciales de Google y variables de entorno.
- Añadir diagramas de arquitectura y flujo de datos.
- Detallar proceso de despliegue y pruebas. | Equipo Docs | 2 días |
| **B2** | **Crear suite completa de pruebas unitarias e integración** | - Mockear `gspread` y `googleapiclient`.
- Cobertura objetivo >90 %.
- Incluir pruebas de seguridad (validación de `CHAT_ID`, sanitización). | QA | 1‑2 semanas |
| **B3** | **Añadir docstrings estilo Google/NumPy** | - Documentar todas las clases y funciones públicas.
- Generar documentación automática con Sphinx. | Desarrolladores | 2‑3 días |
| **B4** | **Configurar CI/CD (GitHub Actions)** | - Añadir workflow que ejecute lint, mypy, pruebas y análisis de seguridad.
- Configurar despliegue a entorno de staging. | DevOps | 3 días |

Estas tareas completarán la profesionalización del proyecto y facilitarán su mantenimiento a largo plazo.
