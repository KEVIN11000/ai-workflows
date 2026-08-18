# Protocolo de Pruebas Locales (Aislamiento de Entorno)

Para garantizar la estabilidad del repositorio y no mezclar código experimental con código de producción o desarrollo, debes seguir estrictamente este protocolo para pruebas locales:

1. **Uso Exclusivo de Ramas "Local-Only":**
   Cualquier experimento, refactorización riesgosa o prueba temporal de nuevas tecnologías (como cron jobs o integraciones con librerías de terceros) debe realizarse en una rama de Git cuyo nombre comience con `test/` o `experiment/` (por ejemplo: `test/notificaciones-push`).

2. **Prohibición de Push en Ramas de Prueba:**
   **NUNCA** ejecutes `git push` en estas ramas de prueba. Deben permanecer única y exclusivamente en el entorno local (computadora del desarrollador). De esta forma, el servidor de producción y el autodeploy nunca se verán afectados por commits rotos o configuraciones experimentales.

3. **Manejo de Credenciales y Archivos Locales:**
   Cualquier archivo generado o requerido exclusivamente para la prueba local (ej. `.env`, `credentials.json`, `run_local.py`, scripts de relleno de datos) debe estar siempre protegido por `.gitignore`. 
   Antes de confirmar cualquier cambio, revisa con `git status` que no se estén rastreando archivos sensibles o específicos del entorno local.

4. **Fusión de Cambios Exitosos (Cherry-Pick / Merge):**
   Una vez que el código experimental en la rama `test/` haya sido validado localmente y funcione a la perfección, los cambios definitivos deben reescribirse de forma limpia en la rama de desarrollo oficial (ej. `V1.3`) o integrarse mediante un *cherry-pick* o *squash merge* atómico. Luego, la rama de prueba puede (y debe) ser eliminada con `git branch -D test/...`.

5. **Worktrees para Entornos Paralelos:**
   Si la prueba local requiere modificar dependencias de forma masiva o mantener el código roto durante días sin afectar el trabajo diario, utiliza `git worktree` para aislar el experimento en una carpeta física completamente separada del proyecto principal.
