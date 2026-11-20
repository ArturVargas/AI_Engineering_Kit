# Método opcional de evidencia por iniciativa

Estado: diseño para revisión. Inspiración: [ghosty-dev](https://github.com/blissito/ghosty-dev). No requiere instalarlo.

## Decisión de adopción

Al abrir el plan de implementación, una vez aprobadas la especificación y la arquitectura que corresponda, el agente explica la opción: «Podemos vincular los criterios al commit, comprobar que las pruebas detectan el defecto que importa y dejar una revisión proporcional al riesgo. Esto añade trabajo de verificación. ¿Quieres adoptarlo para esta iniciativa?». En proyectos existentes que entren directamente en implementación, ofrecerlo al preparar la siguiente tarea. No interrumpir cada tarea para repetir la pregunta.

Registrar la elección en el plan existente: pendiente, adoptado o declinado. Sin un sí explícito no se activa. Declinar mantiene el flujo normal, incluidas las revisiones que los estándares del proyecto ya exijan. La adopción no autoriza instalar herramientas, publicar evidencia ni cambiar protecciones de ramas.

## Reglas cuando se adopta

- Un responsable de implementación y una referencia persistente por tarea (issue, ticket o run); enlazar en vez de duplicar. Esperar la notificación del CI cuando exista, sin consultas repetitivas del agente.
- Evidencia significa criterio, versión, comprobación, resultado observado y referencia reproducible. Evitar datos de clientes y secretos en las salidas. Un conteo de tests o un enlace al CI por sí solos no demuestran el criterio.
- Para riesgo bajo, basta una comprobación directa proporcional. Para riesgo medio o alto, identificar para cada criterio crítico un defecto plausible y mostrar que el control lo distingue del caso correcto. Si cambia CI o lint, verificar también el rechazo por el control efectivo, no solo por un comando local.
- Para cambios críticos, un revisor independiente parte del criterio y del diff, comprueba el comportamiento y registra hallazgos en el commit revisado. El implementador corrige; un commit posterior requiere renovar el veredicto y verificar lo afectado. Fuzzing, pruebas de propiedades, mutación, carga o evaluación adversarial se seleccionan según el modo de fallo; ninguna es universal.
- Una persona decide la liberación. Distinguir revisión aprobada, cambio integrado y versión desplegada en un entorno. Sin evidencia de despliegue no declarar que está en producción.

## Encaje en el template y extensión CLI

La implementación prevista deja la oferta en `templates/implementation-plan.md`, la sección condicional en `templates/verification.md` y un enlace desde `standards/execution.md` a una guía opcional distribuida en el Kit. El README indica cómo encontrarla. No añadir una etapa global ni otro registro de tareas.

La guía definirá el contrato para activar una CLI compatible si ya existe o implementarla desde el template: leer la decisión, riesgo, criterios, revisión y referencias desde el mismo registro manual; comprobar campos y coincidencia del commit; devolver «no aplica», «incompleto» o «listo para decisión humana» con motivos. Una revisión obsoleta o un hallazgo crítico abierto impiden este último estado. «Listo» solo valida requisitos documentales, no la veracidad de un test. La guía incluirá ejemplos de entrada y resultado para adopción declinada, evidencia insuficiente y revisión vigente. El adaptador y su integración con CI son opcionales; esta versión no entrega un binario ni un interruptor ejecutable.

## Alternativas y aceptación

Se descarta exigir el método a todos los proyectos o dejarlo únicamente en un cookbook sin punto de descubrimiento. La opción elegida combina una invitación visible con una guía consultada bajo demanda.

El diseño se cumple si una iniciativa puede declinar sin crear artefactos extra, adoptarlo sin CLI o GitHub, y automatizar después las comprobaciones documentales sin mantener un segundo registro ni cambiar el significado de sus estados.
