# AI Engineering Kit v1.2 Lite — Design & UX Layer

## Objetivo

Elevar la calidad de UX/UI de productos construidos con IA sin convertir el kit en un sistema de diseño rígido, una biblioteca de estilos ni una cadena obligatoria de documentación para toda iniciativa.

La capa se activa sólo cuando el alcance incluye una interfaz relevante. Se mantiene opcional, proporcional al riesgo visual y compatible con los artefactos v1.1.

## Problema que resuelve

Sin un contrato de diseño, una petición visual ambigua puede hacer que el agente cambie a la vez producto, jerarquía, estética y comportamiento. Eso produce iteraciones costosas, interfaces genéricas, estados incompletos y claims comerciales no respaldados.

El kit debe separar responsabilidades:

```text
Producto / estrategia -> UX -> dirección visual -> implementación -> verificación
```

Cada capa consume decisiones aprobadas de la anterior. Un cambio que afecte una decisión upstream debe declararse y aprobarse; no se aplica de forma silenciosa.

## Principios de diseño

1. **Proporcionalidad.** Ningún artefacto de diseño aplica a backend, APIs, infraestructura o cambios internos sin UI.
2. **No duplicación.** El `design-brief` consume problema, ICP, propuesta de valor, objetivo de negocio, evidencia, métricas y restricciones ya definidos por discovery, validación y specification.
3. **Una fuente de verdad.** El sistema de diseño y la marca existentes del proyecto prevalecen sobre defaults del kit.
4. **Evidencia sobre gusto.** Referencias, requisitos y capturas verificables reemplazan instrucciones vagas como “hazlo premium”.
5. **Originalidad y veracidad.** Las referencias enseñan principios; no se copian composiciones distintivas. Las afirmaciones de producto no se inventan.
6. **Mínimo mantenible.** La versión inicial evita presets, automatizaciones, dependencias, galerías de assets y skills de terceros vendorizadas.

## Alcance

### Nuevos archivos

```text
standards/design-quality.md
templates/design-brief.md
templates/reference-pack.md
```

También se amplía `templates/verification.md` con una sección opcional de calidad de diseño, en vez de crear un segundo documento de verificación.

### `standards/design-quality.md`

Estándar aplicable sólo a trabajo con UI. Define mínimos independientes del estilo:

- comportamiento responsive;
- estructura semántica, contraste y navegación por teclado;
- estados loading, empty, error, success y disabled cuando sean pertinentes;
- jerarquía y espaciado coherentes;
- seguridad de motion (`prefers-reduced-motion`);
- rendimiento y contenido realista;
- ausencia de patrones engañosos y claims sin respaldo.

No define tipografías, paletas, radios, frameworks CSS ni una estética predeterminada.

### `templates/design-brief.md`

Artefacto requerido para una pantalla o flujo nuevo, rediseño material o landing de producción. Incluye:

- objetivo del usuario, acción primaria/secundarias y contexto de entrada;
- journey, jerarquía de información, contenido, objeciones y fricción;
- estados de UI y criterios UX de aceptación;
- para landings: oferta, audiencia, CTA, evidencia y contexto de tráfico;
- sección **dirección visual** opcional: atributos de marca, referencias, principios de layout, tipo/color/espaciado, componentes, motion y “evitar”.

La dirección visual se mantiene dentro del brief en v1.2 Lite para evitar que dos documentos se desincronicen.

### `templates/reference-pack.md`

Artefacto opcional cuando hay referencias externas significativas. Para cada referencia registra fuente, motivo, patrones que se quieren aprender, elementos que no se copiarán y consideraciones de originalidad/licencia.

No exige recopilar inspiración para cambios menores ni autoriza reproducir una interfaz de terceros.

### Verificación existente

`templates/verification.md` añadirá una sección **Calidad de diseño (si aplica)**. Pedirá evidencia proporcional: viewport probado, estados relevantes, navegación por teclado, contraste/semántica, reduced motion, overflow, contenido realista, claims y originalidad. Para un cambio pequeño bastará una comprobación concreta; para una landing o flujo nuevo se documentarán capturas y herramientas usadas cuando existan.

## Activación por tipo de trabajo

| Trabajo | Capa v1.2 Lite |
| --- | --- |
| Backend, API, datos, infraestructura o cambio sin UI | no aplica |
| Ajuste localizado en UI existente | sección de diseño en `verification.md` |
| Nueva pantalla, flujo o cambio visual material | `design-brief.md` + sección de verificación |
| Landing, rediseño o identidad visual nueva | `design-brief.md` + `reference-pack.md` si aporta valor + sección de verificación |

El agente puede recomendar subir de nivel si descubre riesgo visual, accesibilidad, marca, legal/comercial o un cambio de journey significativo; no debe crear artefactos por defecto.

## Decisiones explícitamente aplazadas

### Design presets

No se incorporan presets `clean-saas`, `fintech`, `enterprise` u otros en v1.2 Lite. Mantener siete familias exige revisar tokens, ejemplos, referencias, accesibilidad y compatibilidad con marcas existentes. Además, puede producir homogeneidad visual.

Se evaluarán después de que varios proyectos del kit demuestren patrones reutilizables. Si se añaden, serán defaults modificables y nunca sustituirán un sistema de diseño existente.

### Artefactos separados de dirección visual y verificación

No se crea `visual-direction.md` ni `design-verification.md` en esta versión. Sus responsabilidades viven en el brief y en la verificación existente para limitar la carga documental.

### Automatización y skills upstream

No se copian los repositorios externos de skills ni se añaden scripts de screenshots, Lighthouse, tokens o generación de assets. Se usan como referencias de prácticas; cualquier automatización futura requiere evidencia de que aporta valor repetible.

## Cambio upstream controlado

Los artefactos que introduzca la capa de diseño incluyen una sección breve:

```md
## Cambio upstream requerido

- Decisión afectada:
- Propuesta:
- Motivo e impacto:
- Aprobación requerida: sí / no
```

No se crea un archivo adicional. La sección documenta casos en los que UX o implementación detectan que debe cambiarse una decisión de producto, arquitectura o especificación.

## Integración con el flujo actual

```text
discovery -> idea-validation -> specification
                                -> architecture -> implementation-plan
                                -> implementation -> verification -> release

                       (si UI aplica)
                       design brief -> reference pack opcional
                       -> requisitos UX/visuales en implementation plan
                       -> calidad de diseño en verification
```

La capa de diseño no añade una etapa universal al `workflow.yaml`. El workflow se documenta mediante reglas de activación y enlaces a los artefactos para preservar la simplicidad del pipeline principal.

## Criterios de aceptación

- El template incorpora como máximo un estándar y dos plantillas nuevas.
- Ningún documento de diseño es obligatorio para trabajo sin UI.
- El brief no duplica discovery ni specification y declara sus inputs upstream.
- La dirección visual y los cambios upstream se documentan sin crear archivos adicionales.
- La verificación existente cubre calidad de diseño sólo cuando aplica.
- No se añaden presets, dependencias, scripts ni skills externas al repositorio.
- El README explica activación por impacto visual, la prioridad de los sistemas existentes y las decisiones aplazadas.
