# Estándar de ejecución

Clasifica cada iniciativa antes de cambiar código. Si aparece complejidad nueva, eleva su clasificación; no la reduzcas silenciosamente.

## Spike

Úsalo para responder una duda de viabilidad.

- Define la pregunta, límite de tiempo/coste y evidencia que respondería la duda.
- El resultado es una recomendación, no código de producción.
- Si se decide construir, abre una iniciativa nueva y clasifícala de nuevo.

## Cambio acotado (`bounded`)

Úsalo cuando ya existe un flujo claro en el proyecto y el cambio es localizado.

- Registra un diseño breve, los archivos afectados y el criterio de aceptación.
- Agrega una prueba de regresión cuando cambie comportamiento.
- Verifica el cambio con el comando o prueba apropiada antes de liberarlo.

## Cambio arquitectural (`architectural`)

Úsalo para sistemas nuevos, subsistemas, integraciones, cambios de datos, permisos o interfaces que otros componentes consumen.

- Requiere especificación, alternativas, ADR si la decisión es difícil de revertir y plan de implementación.
- Divide el trabajo en entregables verificables.
- Requiere revisión independiente antes de liberar si afecta seguridad, datos, migraciones o integraciones.

## Pruebas y revisión según riesgo

- Aplica TDD a reglas de negocio, cálculos, autorización, APIs, transformaciones de datos y bugs reproducibles.
- Para copy, configuración o cambios visuales simples, usa la verificación proporcional: build, prueba manual o E2E cuando aplique.
- No uses pruebas artificiales solo para cumplir un ritual.
- Una corrección comienza con evidencia y causa raíz; después de tres hipótesis no confirmadas, reabre el diseño o la arquitectura antes de intentar otro parche.
