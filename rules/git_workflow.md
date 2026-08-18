# Flujo de Trabajo Estricto de Git

A partir de ahora, adopta el siguiente flujo de trabajo estricto de Git para este proyecto:
1. NUNCA hagas commits directamente sobre la rama `Main-stable`. Esa rama representa el entorno de Producción y debe estar blindada.
2. Toda la programación, refactorización y resolución de bugs debe realizarse obligatoriamente en ramas de desarrollo (como `V1.2`) o en ramas temporales de características (feat/*).
3. Mantén los commits usando el formato "Conventional Commits" de forma atómica y descriptiva.
4. Cuando el trabajo esté completado y verificado en la rama de desarrollo, recién entonces haz un checkout a `Main-stable` y ejecuta un `git merge` para absorber los cambios. Nunca a la inversa.
