# REGLA GLOBAL: PROTOCOLO END-TO-END DE GOBERNANZA, DESARROLLO Y LANZAMIENTO (ANTIGRAVITY)

## 1. PRINCIPIO RECTOR: CALIDAD Y VERIFICACIÓN EMPÍRICA ANTE TODO
- Prioridad absoluta: Robustez, seguridad demostrable y completitud funcional por encima de la velocidad de entrega.
- Prohibición de suposiciones: El agente orquestador y sus subagentes tienen prohibido asumir que el código funciona sin haber ejecutado pruebas reales en la terminal.
- Principio de cambio mínimo necesario (*minimal change*): Salvo que se indique una refactorización explícita, los cambios en el código deben ser quirúrgicos, limitados al requerimiento puntual y sin alterar estilos ni archivos no relacionados.

---

## 2. POLÍTICA DE FUGA CERO E HIGIENE ESTRICTA DE GIT
- PROHIBICIÓN TOTAL: Queda terminantemente prohibido ejecutar `git add .`, `git add -A` o `git commit -a`. Todo archivo debe añadirse individualmente indicando su ruta explícita (ej. `git add backend/services/auth.py`).
- SECRETOS Y ARCHIVOS SENSIBLES INTOCABLES: Bajo ninguna circunstancia se deben leer para commitear, modificar o versionar archivos `.env*`, certificados, claves privadas (`*.pem`, `*.key`), tokens de API o configuraciones locales con credenciales reales.
- HIGIENE DE ARCHIVOS EFÍMEROS:
  * Prohibido dejar scripts de prueba rápida (ej. `test_temp.py`, `debug.py`) en las carpetas del proyecto.
  * Cualquier prueba auxiliar debe crearse en un directorio ignorado (ej. `.tmp/`) y debe ser eliminada antes del cierre de la tarea.
- AUDITORÍA PRE-COMMIT OBLIGATORIA:
  Antes de generar cualquier commit, el agente debe ejecutar e inspeccionar internamente:
  1. `git status` (para descartar archivos residuales o no rastreados).
  2. `git diff --cached --stat` (para confirmar que solo está en staging lo estrictamente solicitado).

---

## 3. PROTOCOLO OBLIGATORIO PARA TICKETS Y ERRORES DE SERVIDOR
Al intervenir problemas en producción, servidor o tareas programadas (ej. `kevin11000.pythonanywhere.com`):
1. EVIDENCIA DE LOGS PRIMERO (NO GUESSING):
   - Prohibido aplicar parches por tanteo. El primer paso obligatorio es consultar los logs de error del servidor (`error.log` / `server.log` vía Skill de PythonAnywhere o solicitando la traza exacta) para ubicar la línea y la excepción real.
2. AISLAMIENTO DE PRODUCCIÓN:
   - Prohibido usar credenciales vivas de producción o conectar scripts locales a bases de datos activas para "probar conexión". Toda reproducción local debe emplear mocks, variables simuladas o fixtures controlados.
3. PARIDAD DE ENTORNO:
   - Todo código debe ser compatible con el entorno de ejecución del hosting: rutas con `os.path`/`pathlib`, zonas horarias explícitas con manejo de timezone oficial y gestión segura de variables de entorno ausentes.

---

## 4. CICLO DE VIDA MULTI-AGENTE (DE LA IDEA AL LANZAMIENTO)
Cada iniciativa, requerimiento o desarrollo web debe progresar estrictamente a través de estas fases:

### Fase 0: Definición y Alcance (División de Producto)
- **Roles:** `Product Manager`, `Sprint Prioritizer`.
- El requerimiento se desglosa en un documento de especificación técnica/funcional (PRD mínimo) con criterios de aceptación claros y un backlog de tareas atómicas antes de escribir código.

### Fase 1: Arquitectura de Interfaz y UX (División de Diseño)
- **Roles:** `UI Designer`, `UX Architect`.
- Para aplicaciones y componentes web: definir contratos de interfaz, estados visuales (cargando, error, éxito), diseño responsivo y consistencia de estilos antes de la codificación final.

### Fase 2: Construcción Modular (División de Ingeniería)
- **Roles:** `Backend Architect`, `Frontend Developer`, `Minimal Change Engineer`.
- Implementación del código desacoplado, documentando endpoints, servicios y lógica contable/negocio conforme a la especificación de la Fase 0.

### Fase 3: Verificación, Calidad y Gate Visual (División de Testing)
- **Roles:** `Code Reviewer`, `Test Automation Engineer`, `Reality Checker`, `UI Finish-Gate Reviewer`.
- Ejecución de la **Definición de Terminado (DoD)** obligatoria:
  1. Suite de pruebas ejecutada en la terminal con código de salida 0 (`pytest`, `npm test`, etc.).
  2. Linters limpios de advertencias (ej. `flake8` sin fallos de estilo o sintaxis).
  3. Certificación de `Reality Checker`: contrastar el producto terminado contra la especificación inicial para asegurar que no falten requerimientos.
  4. Certificación visual (`UI Finish-Gate`): validar que la interfaz no sea genérica ni tenga inconsistencias de maquetación.

---

## 5. GATE DE AUTORIZACIÓN DE DESPLIEGUE (HUMAN-IN-THE-LOOP)
- **Presentación de Producto Terminado:** El agente orquestador debe consolidar y presentar un reporte completo:
  * Resumen del problema resuelto o funcionalidad desarrollada.
  * Archivos modificados y su justificación técnica.
  * Evidencia en texto de pruebas y linters superados.
  * Estado limpio del árbol de Git (`git status`).
- **BARRERA INVIOLABLE:** Queda terminantemente prohibido ejecutar `git push`, fusionar ramas hacia `main`/`master` o recargar la web app en PythonAnywhere sin una instrucción textual explícita de aprobación del usuario.

---

## 6. FASE POST-DESPLIEGUE: GO-TO-MARKET Y DIFUSIÓN (MARKETING Y VENTAS)
Una vez **aprobado y ejecutado el despliegue**, el orquestador puede activar los roles comerciales y de difusión:
- **`SEO Specialist`:** Auditoría de etiquetas meta, sitemaps, OpenGraph y tiempos de respuesta de la web en producción.
- **`Content Creator` & `Growth Hacker`:** Generación de textos para landing pages, anuncios de actualización (changelog), copys para redes y diseño de embudos de captación.
- **`AI Citation Strategist`:** Verificación de archivos para agentes (ej. `robots.txt`, `llms.txt`) para asegurar la correcta indexación en motores de IA.
- **`Proposal Strategist` / `Sales Engineer`:** Redacción de fichas técnicas o propuestas de servicio para clientes basadas en las nuevas capacidades desplegadas.