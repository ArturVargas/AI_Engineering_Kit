# AI Engineering Kit

Una plantilla reutilizable para trabajar con IA en producto y software de forma **visible, trazable y ligera**. No es un framework de agentes ni una aplicación que deba desplegarse: es una convención de archivos Markdown/YAML para que el humano y la IA compartan el contexto correcto en cada iniciativa.

Está inspirado en la *Interpretable Context Methodology* (ICM): un flujo complejo se divide en etapas pequeñas; cada una lee solo lo que necesita, entrega un artefacto editable y deja evidencia para la siguiente decisión.

## Qué problema resuelve

Un asistente de IA suele recibir un prompt largo, historia de chat, archivos y reglas mezcladas. Eso provoca contexto irrelevante, respuestas inconsistentes, pérdida de decisiones y correcciones repetidas.

Este kit separa tres niveles:

```text
Estándares globales reutilizables
        ↓
Contexto estable de cada proyecto
        ↓
Artefactos de una iniciativa concreta
```

Así, una IA puede revisar una arquitectura sin cargar material de marketing, o preparar una validación de producto sin recibir todo el código. El equipo puede inspeccionar, editar o rechazar cualquier salida antes de continuar.

## Cuándo usarlo

Es especialmente útil para trabajo que sea:

- **Secuencial:** una decisión alimenta a la siguiente.
- **Repetible:** el flujo se usa en múltiples iniciativas o proyectos.
- **Revisable:** una persona debe validar decisiones de producto, arquitectura o release.
- **De alto contexto:** hace falta conservar decisiones, restricciones y evidencia entre sesiones de IA.

Casos típicos:

- Validar una idea, prototipo o hipótesis antes de construir.
- Definir arquitectura, comparar alternativas y registrar ADRs.
- Preparar especificaciones e implementación de una funcionalidad.
- Revisar pruebas, seguridad, release y observabilidad.
- Analizar feedback de early users e iterar el producto.
- Adoptar IA en un proyecto existente sin perder su estado actual.

## Cuándo no usarlo

No es la herramienta principal para:

- Sistemas de producción con muchos usuarios concurrentes, colas y estado distribuido.
- Agentes que deben coordinarse en tiempo real o ramificar automáticamente muchas veces.
- Automatización totalmente desatendida donde no exista un punto razonable de revisión humana.
- Tareas triviales de un solo paso; crear un `run` para cambiar una línea de copy añade más fricción que valor.

En esos casos puede convenir código de orquestación, un sistema de colas, CI/CD o un issue sencillo. El kit documenta y guía decisiones; no sustituye esas herramientas.

## Principios

1. **Una etapa, un objetivo.** Cada artefacto responde una pregunta concreta.
2. **Contexto acotado.** Cargar solo reglas y archivos pertinentes a la etapa actual.
3. **Outputs editables.** Toda salida puede ser revisada o corregida por una persona antes de usarse.
4. **Arreglar la causa.** Si una corrección se repite, mejorar una plantilla, regla o referencia; no parchear la salida cada vez.
5. **Separar lo estable de lo temporal.** Los estándares globales no se mezclan con el contexto específico ni con los resultados de una iniciativa.
6. **Evidencia sobre opinión.** Una decisión de producto, arquitectura o release debe enlazar su evidencia.

## Flujo v1.2 Lite

```text
discovery
  → idea-validation
  → specification
  → architecture
  → implementation-plan
  → implementation
  → verification
  → release
  → observability
  → early-user-feedback
  → product-learning
```

No es una cadena obligatoria. Cada iniciativa entra por la primera etapa que necesita:

| Tipo de iniciativa | Etapa de entrada habitual |
| --- | --- |
| Idea nueva | `discovery` o `idea-validation` |
| Funcionalidad confirmada | `specification` |
| Cambio estructural o de integración | `architecture` |
| Bug o regresión | `verification` |
| Incidente en producción | `observability` o `product-learning` |
| Proyecto existente | `baseline`, luego la etapa actual |

Antes de implementar, clasifica la iniciativa:

- **`spike`:** responde una duda de viabilidad; no convierte código exploratorio en producción.
- **`bounded`:** modifica un flujo existente y localizado; requiere diseño breve y verificación proporcional.
- **`architectural`:** altera componentes, datos, integraciones o contratos; requiere especificación, alternativas y plan técnico.

La diferencia entre las fases finales importa:

- **Verification:** ¿está correctamente construido antes de liberar?
- **Observability:** ¿cómo detectamos e investigamos un problema en producción?
- **Early-user-feedback:** ¿las personas entienden, usan y valoran la solución?
- **Product-learning:** ¿qué evidencia cambia el backlog, la hipótesis o la arquitectura?

## Estructura

```text
ai-engineering-kit/
├─ standards/                 # reglas reutilizables de todos los proyectos
├─ templates/                 # formatos de artefactos
└─ template/.ai/              # contenido que vive dentro de cada proyecto
   ├─ CONTEXT.md              # identidad, restricciones y rutas del proyecto
   ├─ workflow.yaml           # versión del flujo adoptado
   ├─ references/             # dominio, arquitectura, convenciones y baseline
   ├─ adr/                    # decisiones arquitecturales persistentes
   └─ runs/                   # una carpeta por iniciativa
```

Un `run` contiene solamente los artefactos que esa iniciativa necesita:

```text
.ai/runs/2026-08-07-mejorar-busqueda/
├─ 03-specification.md
├─ 04-architecture.md
├─ 06-verification.md
└─ 08-observability.md
```

## Uso en proyectos nuevos

1. Sube este directorio a GitHub y actívalo como **Template repository**.
2. Crea el nuevo repositorio desde la plantilla.
3. Mueve `template/.ai/` a la raíz del repositorio, de modo que exista `mi-proyecto/.ai/`.
4. Completa `.ai/CONTEXT.md` y añade referencias estables en `.ai/references/`.
5. Crea un `run` para la primera iniciativa y usa solo las etapas necesarias.

## Adopción en un proyecto existente

No reconstruyas el historial ni fuerces el proyecto a recorrer todas las etapas.

1. Copia `template/.ai/` al proyecto existente.
2. Completa `.ai/references/baseline.md` con arquitectura actual, despliegue, integraciones, riesgos y deuda conocida.
3. Registra las decisiones difíciles de revertir que ya estén vigentes como ADRs breves.
4. Ejecuta la próxima iniciativa real desde la etapa correspondiente.

## Qué va en cada sitio

| Ubicación | Contenido |
| --- | --- |
| `standards/` | Reglas estables aplicables a muchos proyectos. |
| `.ai/references/` | Conocimiento estable específico de un proyecto. |
| `.ai/adr/` | Decisiones y trade-offs que deben persistir. |
| `.ai/runs/` | Inputs, evidencia y resultados de una iniciativa. |

No copies credenciales, tokens, PII ni datos sensibles a estos artefactos. Usa enlaces, identificadores o resúmenes seguros cuando necesites referenciarlos.

## Uso junto a Superpowers

El kit y Superpowers se complementan, pero no son lo mismo:

| Responsabilidad | AI Engineering Kit | Superpowers |
| --- | --- | --- |
| Contexto de producto, arquitectura y decisiones | Guarda referencias, ADRs y evidencia persistente. | Lee ese contexto para trabajar. |
| Especificación y planificación | Aporta plantillas que viajan con el proyecto. | Guía el refinamiento, aprobación y descomposición en tareas. |
| Implementación | Conserva el plan y los resultados del run. | Aplica TDD, ejecución disciplinada y revisión según riesgo. |
| Debugging y release | Registra causa raíz y evidencia de salida. | Investiga causa raíz y exige verificación fresca antes de declarar éxito. |

Superpowers no debe copiarse dentro de este repositorio: se instala en el agente. Este kit guarda los artefactos que permiten reutilizar su disciplina entre sesiones y proyectos.

Para una iniciativa de riesgo medio o alto, usa estas plantillas junto con los skills de Superpowers:

1. `templates/specification.md` para definir alcance, criterios y comportamiento ante errores.
2. `templates/implementation-plan.md` para fijar archivos, interfaces, pruebas y rollback.
3. `templates/verification.md` para registrar la evidencia fresca antes de un release.
4. `templates/incident-root-cause.md` cuando haya un fallo que requiera investigación antes de corregirlo.

Los estándares `standards/execution.md` y `standards/release-readiness.md` indican cuándo cada práctica es proporcional al riesgo. No conviertas cambios triviales en un proceso arquitectural.

## Capa opcional de Design & UX

La v1.2 Lite mejora el trabajo con interfaces sin imponer una estética ni una etapa adicional a todas las iniciativas. Evita que una petición como “hazlo más premium” cambie silenciosamente el producto, el journey y la implementación a la vez.

Cuando hay UI, la responsabilidad se separa así:

```text
Producto / estrategia → UX → dirección visual → implementación → verificación
```

Producto conserva problema, ICP, propuesta de valor y objetivo de negocio. El brief de diseño consume esas decisiones; no vuelve a hacer discovery desde cero. UX define journey, jerarquía, acciones y estados. La dirección visual sólo define cómo expresar esa experiencia y no reemplaza un sistema de diseño existente.

| Tipo de trabajo | Capa de Design & UX |
| --- | --- |
| Backend, API, datos, infraestructura o cambio sin UI | No aplica. |
| Ajuste localizado de UI existente | Sección de calidad de diseño en `verification.md`. |
| Nueva pantalla, flujo o cambio visual material | `design-brief.md` + verificación proporcional. |
| Landing, rediseño o identidad visual nueva | `design-brief.md`, `reference-pack.md` si aporta valor y verificación proporcional. |

Los artefactos son:

- `standards/design-quality.md`: mínimos de responsive, accesibilidad, estados, rendimiento, veracidad y originalidad; no define estilo.
- `templates/design-brief.md`: requisitos UX y una sección opcional de dirección visual.
- `templates/reference-pack.md`: referencias, patrones que aprender, elementos a no copiar y consideraciones de licencia/originalidad.
- `templates/verification.md`: evidencia UI cuando aplica, sin crear un segundo proceso de verificación.

Si UX o implementación necesitan cambiar una decisión ya aprobada de producto, arquitectura o especificación, documenta el cambio upstream dentro del artefacto afectado y pide aprobación. No reconstruyas silenciosamente una interfaz por una petición local.

### Qué no incluye todavía

La v1.2 Lite no incluye presets de diseño, galerías de assets, scripts de screenshots/Lighthouse, automatización de auditorías ni skills externas copiadas. Se evaluarán sólo cuando varios proyectos reales demuestren que un patrón se repite y compensa su mantenimiento.

## Evolución del kit

Versiona los cambios al kit global. Si ves que los equipos corrigen el mismo tipo de salida una y otra vez, mejora el estándar o la plantilla que la originó. No hace falta actualizar todos los proyectos de inmediato: cada proyecto puede adoptar una versión nueva del flujo cuando tenga sentido.
