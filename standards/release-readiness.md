# Estándar de preparación para release

No declares una iniciativa lista sin evidencia fresca en su artefacto de verificación.

## Evidencia requerida cuando aplique

- Criterios de aceptación comprobados.
- Pruebas automatizadas y comandos ejecutados, con resultado.
- Build, lint y type-check del proyecto.
- Compatibilidad, migración de datos y rollback.
- Revisión de secretos, permisos y exposición de datos.
- Observabilidad: logs, métricas, alertas o runbook para cambios operativamente relevantes.

## Decisión

Registra una de estas decisiones:

- `go`: se puede liberar con la evidencia disponible.
- `go-with-risk`: se libera con riesgos explícitos, propietario y fecha de seguimiento.
- `no-go`: falta evidencia o existe un riesgo bloqueante.

Una prueba parcial no prueba el release completo. Si una comprobación no aplica, indica por qué.
