# Verificación

## Cambio evaluado

Solo si el plan indica **adoptado**, completa aquí o enlaza el registro existente:

- Referencia de tarea y responsable:
- Versión evaluada (commit si hay Git) y riesgo (bajo/medio/alto):
- Para cada criterio, usa la tabla inferior: anota la observación concreta y enlaza una comprobación reproducible; omite secretos y datos reales de clientes.
- Riesgo medio/alto: por criterio crítico identifica el defecto plausible, el caso rechazado y el caso correcto aceptado. Para CI/lint cambiado, adjunta el resultado del control efectivo en ambos casos.
- Cambio crítico: revisor distinto del implementador, versión revisada, comprobación propia, veredicto y hallazgos abiertos con gravedad. Un nuevo commit exige renovar la revisión de lo afectado.

## Criterios de aceptación

| Criterio | Resultado observado | Comprobación reproducible o referencia |
| --- | --- | --- |
|  |  |  |

## Comprobaciones frescas

| Comprobación | Resultado | Evidencia / comando |
| --- | --- | --- |
|  |  |  |

## Calidad de diseño (si aplica)

| Comprobación | Resultado | Evidencia / viewport / herramienta |
| --- | --- | --- |
| Jerarquía y contenido realista |  |  |
| Desktop, tablet o mobile relevantes |  |  |
| Estados loading, empty, error, success y disabled pertinentes |  |  |
| Navegación por teclado, foco, semántica y contraste |  |  |
| `prefers-reduced-motion`, interacción y feedback |  |  |
| Overflow, imágenes, fuentes y rendimiento |  |  |
| Claims, assets y originalidad |  |  |

Si una comprobación no aplica, indica el motivo. Para cambios pequeños, documenta sólo los checks afectados; para flujos o landings nuevos, conserva capturas o resultados de herramientas cuando aporten evidencia.

## Release y operación

- Build / lint / type-check:
- Migración o compatibilidad:
- Rollback:
- Secretos, permisos y datos:
- Logs, métricas, alertas o runbook:

## Riesgos conocidos

## Decisión de liberación

Con el método adoptado, distingue: **aprobación** (persona, decisión y versión), **integración** (referencia al merge o equivalente) y **despliegue** (entorno, versión y evidencia). Marca «no consta» donde falte evidencia.

`go` | `go-with-risk` | `no-go`
