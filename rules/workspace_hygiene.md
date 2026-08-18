# Workspace Hygiene & Global Resource Priority

**ID:** `workspace-hygiene`
**Scope:** Gestión de archivos, búsqueda de perfiles de agentes y prevención de copias redundantes.

## Directivas Obligatorias

Para preservar la limpieza del disco y mantener la Separación de Responsabilidades (Separation of Concerns), debes adherirte estrictamente a las siguientes normas de higiene de espacio de trabajo:

1. **Prohibición de Clonación Compulsiva:**
   **NUNCA** ejecutes `git clone` para descargar repositorios de metodologías, frameworks de agentes (ej. `agency-agents` o `ai-workflows`) o herramientas similares dentro del espacio de trabajo del proyecto activo (ej. dentro de la carpeta del código fuente) o en carpetas temporales (`scratch/`), a menos que el usuario lo solicite explícitamente.

2. **Priorizar Rutas Globales:**
   Cuando necesites leer reglas, perfiles de subagentes o instrucciones que pertenezcan a frameworks globales:
   - Busca **primero** en las instalaciones globales de tu entorno (por ejemplo, en `C:\Users\kpera\.gemini\agency-agents` o el directorio equivalente donde residan las configuraciones).
   - Utiliza referencias de lectura (`view_file` o búsquedas de texto) usando **rutas absolutas** hacia esos repositorios centrales.

3. **Referenciar en lugar de Replicar:**
   Bajo ninguna circunstancia debes copiar o duplicar los archivos de reglas y agentes (`.md`) hacia las carpetas locales del proyecto actual. El repositorio del proyecto debe mantenerse 100% puro (exclusivo para código fuente de la aplicación).

4. **Autolimpieza Activa:**
   Si por algún motivo excepcional se requiere descargar un repositorio temporal para extraer un recurso, debes eliminarlo inmediatamente después de terminar su uso para no acumular basura en disco.
