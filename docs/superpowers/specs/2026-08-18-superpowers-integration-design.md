# AI Engineering Kit v1.1 — Integración de Superpowers

## Objetivo

Mejorar la ejecución de especificaciones aprobadas con artefactos persistentes para planificación, verificación de releases y análisis de causa raíz, sin duplicar las skills de Superpowers ni imponer ceremonias en cambios triviales.

## Alcance

- Añadir un estándar de ejecución que clasifique cada iniciativa como `spike`, `bounded` o `architectural`.
- Añadir un estándar de preparación para release.
- Añadir plantillas de especificación, plan de implementación y causa raíz de incidentes.
- Ampliar la plantilla de verificación para exigir evidencia fresca.
- Actualizar el flujo v1 para insertar `implementation-plan` entre arquitectura e implementación.
- Documentar en el README cómo cooperan el kit y Superpowers.

## Fuera de alcance

- Copiar skills de Superpowers al repositorio.
- Exigir worktrees, subagentes, TDD exhaustivo o code review para cambios triviales.
- Añadir scripts, dependencias, CI o automatización.
- Convertir el kit en un framework de agentes.

## Diseño

El kit sigue siendo la fuente de contexto y evidencia persistente. Superpowers sigue siendo la fuente de comportamiento del agente durante la ejecución.

```text
AI Engineering Kit                         Superpowers
spec + ADR + referencias        →          diseño, plan y ejecución disciplinada
plan persistente                →          tareas, TDD y revisión cuando aplique
evidencia de verificación       ←          comandos ejecutados y resultados frescos
incidente / causa raíz          ←          debugging sistemático
```

### Clasificación de iniciativas

| Tipo | Artefacto mínimo | Ejecución |
| --- | --- | --- |
| `spike` | hipótesis, límite de gasto/tiempo y recomendación | exploración desechable; no se promociona como producción |
| `bounded` | diseño breve, criterio de aceptación y verificación | cambio localizado; prueba de regresión si modifica comportamiento |
| `architectural` | especificación, alternativas, ADR si corresponde y plan técnico | tareas planificadas, pruebas por riesgo y revisión antes de release |

La complejidad descubierta puede elevar una iniciativa a un nivel superior; nunca se rebaja silenciosamente.

### TDD y revisión basados en riesgo

TDD es obligatorio para reglas de negocio, cálculos, autorización, APIs, transformaciones de datos y bugs reproducibles. Para copy, archivos de configuración y cambios visuales simples, se exige la verificación apropiada (por ejemplo, build, prueba manual o E2E), no una prueba artificial.

La revisión independiente se exige para cambios arquitecturales, seguridad, datos/migraciones e integraciones. Para un cambio acotado se usa cuando el riesgo o tamaño lo justifique.

### Release readiness

Antes de liberar un cambio de riesgo relevante, su verificación debe cubrir: criterios de aceptación, pruebas ejecutadas, build/lint/type-check aplicables, compatibilidad o migraciones, rollback, secretos/permisos, y señales de observabilidad necesarias.

### Incidentes y debugging

Antes de aplicar una corrección se registra reproducción, evidencia, cambios recientes, hipótesis y causa raíz. Después de tres intentos no confirmados, se reabre la arquitectura en vez de continuar acumulando parches.

## Archivos resultantes

```text
standards/execution.md
standards/release-readiness.md
templates/specification.md
templates/implementation-plan.md
templates/incident-root-cause.md
templates/verification.md                 # actualizado
template/.ai/workflow.yaml                # actualizado
README.md                                 # actualizado
```

## Criterios de aceptación

- El README explica la división de responsabilidades entre el kit y Superpowers.
- Cada nueva plantilla indica propósito, inputs, outputs y evidencia requerida.
- `workflow.yaml` declara `implementation-plan` entre `architecture` e `implementation`.
- La verificación no permite afirmar éxito sin comandos/resultados concretos.
- No se añaden dependencias, scripts ni automatizaciones.
