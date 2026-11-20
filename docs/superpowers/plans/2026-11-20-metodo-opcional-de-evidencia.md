# Método opcional de evidencia — plan de implementación

> Ejecución propuesta: superpowers:executing-plans. Marcar cada paso al verificarlo.

**Objetivo:** ofrecer el método una vez por iniciativa y poder aplicarlo a mano con los documentos habituales.

**Arquitectura:** el plan conserva la decisión; la verificación conserva la evidencia o apunta al registro existente. La guía describe cómo una CLI podría leer los mismos datos.

**Tecnología:** Markdown y enlaces relativos; sin dependencias. [Diseño aprobado](../specs/2026-11-20-metodo-opcional-de-evidencia-design.md).

## Restricciones y foco de revisión

No instalar Ghosty ni introducir Actions, comandos ficticios o una bitácora adicional. Comprobar cinco límites: silencio no equivale a consentimiento; declinar no elimina controles existentes; un cambio menor no exige pruebas avanzadas; una aprobación de otro commit no está vigente; una comprobación documental no autoriza un despliegue.

### 1. Ofrecer la opción en el plan

- [x] Añadir a `templates/implementation-plan.md` una invitación breve después de aprobar la especificación y la arquitectura aplicable. Si la iniciativa ya está en marcha, ofrecerla antes de la siguiente tarea. Registrar una sola decisión: pendiente, adoptado o declinado.
- [x] Enlazar la guía desde `standards/execution.md` y `README.md`. Indicar que declinar no modifica los controles habituales.
- [x] Recorrer una iniciativa pendiente y una declinada: ninguna activa el método ni crea otro documento. Reabrir el plan no debe repetir la pregunta ya respondida.

### 2. Registrar evidencia proporcional

- [x] Adaptar las tablas existentes de `templates/verification.md`: enlazar criterio, versión, comprobación, resultado observado y referencia. Si ya hay evidencia en un issue o PR, referenciarla sin transcribirla. No registrar secretos ni datos de clientes.
- [x] Cuando se adopte, pedir una comprobación directa para riesgo bajo y, por criterio crítico de riesgo medio o alto, un defecto plausible con evidencia de rechazo y aceptación. Si cambia el CI, la comprobación debe pasar por el CI efectivo. Para cambios críticos, registrar revisor independiente, commit, prueba propia y hallazgos.
- [x] Recorrer dos ejemplos: un cambio de texto con inspección visual y un cambio de aislamiento con dos clientes ficticios. En el segundo, cambiar el commit después de revisar debe dejar el veredicto anterior sin vigencia. Distinguir aprobación, integración y despliegue por entorno.

### 3. Documentar el adaptador opcional

- [x] Crear `docs/guias/metodo-de-evidencia.md` con un ejemplo manual y el contrato para una futura CLI. Definir entradas: decisión, riesgo, criterios aplicables, referencias, commit objetivo y revisión. La herramienta leería los registros manuales, sin exigir proveedor de issues. Explicar cómo integrar un adaptador elegido explícitamente y cómo seguir manualmente al desactivarlo.
- [x] Incluir ejemplos de entrada → salida: declinado o pendiente → «no aplica», con razones distintas; adoptado sin evidencia, revisión obsoleta o hallazgo crítico abierto → «incompleto»; cobertura documental suficiente y revisión vigente cuando aplique → «listo para decisión humana». Nunca inferir que hubo merge o despliegue a partir de este resultado.
- [x] Verificar los enlaces relativos, consistencia de estados y los casos anteriores. Revisar el diff completo: ningún cambio de runtime, protección de rama o dependencia. Confirmar únicamente los documentos del método.
