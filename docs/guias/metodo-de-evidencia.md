# Método opcional de evidencia

El [plan](../../templates/implementation-plan.md) conserva la elección por iniciativa. La [verificación](../../templates/verification.md) enlaza el registro de cada tarea. Si ya existe un issue con los resultados, conserva allí los detalles. Una persona decide la liberación; una suite verde por sí sola no demuestra un requisito.

## Aplicación manual

Para riesgo bajo, basta una observación directa de la versión: por ejemplo, una captura de la pantalla confirma que el nuevo texto cabe en móvil. Para riesgo medio o alto, pregunta por cada criterio crítico: «Si este comportamiento fuera incorrecto, ¿qué lo detectaría?». Usa pruebas de propiedades, mutación, casos adversos o carga solo cuando respondan a esa pregunta.

Ejemplo de riesgo alto, con datos ficticios: A recupera su documento; al consultar como B, el documento no llega al contexto enviado al modelo. Conserva el identificador de la ejecución que rechazó una fixture con contexto mezclado y el de la ejecución que aceptó el contexto correcto. Si el control cambiado es el CI, verifica además que el job requerido bloquea el caso malo y acepta el bueno; no basta con ejecutar la prueba localmente.

En un cambio crítico, el revisor independiente parte del criterio y del diff, hace una comprobación propia y registra versión, resultado y hallazgos. El implementador corrige, el revisor verifica lo afectado en la nueva versión y la persona responsable decide. Ninguno de esos pasos acredita por sí mismo un despliegue.

## Contrato para una CLI futura

No hay CLI incluida. Si el proyecto elige automatizar, configura explícitamente el adaptador con la ruta al plan, la referencia al registro de verificación y la versión objetivo. Debe leer esos mismos registros, resolver sus referencias autorizadas y emitir **estado + motivos**. No mantener otra base de tareas ni inferir aceptación a partir de un campo vacío. Para desactivarlo, retira su invocación y sigue con los mismos registros a mano. Instalar herramientas, publicar evidencia o exigir un check de rama son decisiones separadas.

| Entrada de ejemplo | Resultado documental |
| --- | --- |
| Decisión pendiente o ausente | no aplica: no hay consentimiento |
| Decisión declinada | no aplica: el equipo eligió el flujo habitual |
| Adoptado; criterio sin resultado observable o referencia inaccesible | incompleto: falta evidencia verificable |
| Adoptado; evidencia de v1 para un cambio en v2, incluso de riesgo bajo | incompleto: la versión evaluada debe coincidir con la objetivo |
| Adoptado; riesgo medio/alto, criterio crítico sin caso rechazado | incompleto: control no contrastado |
| Adoptado; cambio crítico en v2, revisión de v1 o hallazgo crítico abierto | incompleto: renovar revisión o resolver el hallazgo |
| Adoptado; riesgo bajo, versión y captura que acredita el criterio | listo para decisión humana |
| Adoptado; criterio crítico con ambos casos, revisión independiente favorable de la versión objetivo, sin bloqueantes | listo para decisión humana |

En todas las rutas de adopción comprueba tarea, responsable, versión, riesgo, criterios y evidencia antes de declarar el registro listo. Una decisión desconocida, una revisión requerida ausente o un veredicto desfavorable deja el resultado incompleto. El adaptador verifica la documentación; no certifica que un test sea correcto, ni aprueba, integra o despliega.
