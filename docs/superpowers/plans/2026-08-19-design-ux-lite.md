# AI Engineering Kit v1.2 Lite — Design & UX Layer Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Añadir una capa de Design & UX opcional y proporcional que eleve la calidad de interfaces sin convertir el template en una biblioteca de estilos ni añadir ceremonias a trabajo sin UI.

**Architecture:** El estándar `design-quality.md` define mínimos de calidad independientes del estilo. `design-brief.md` concentra discovery UX y dirección visual opcional; `reference-pack.md` registra referencias y originalidad sólo cuando agrega valor. La plantilla de verificación existente incorpora una sección UI condicional y el README explica cuándo activar cada artefacto.

**Tech Stack:** Markdown y YAML existentes; sin dependencias, scripts, automatización ni código ejecutable.

**Spec:** `docs/superpowers/specs/2026-08-19-design-ux-lite-design.md`

## Global Constraints

- Crear exactamente un estándar y dos plantillas nuevas.
- No añadir `design-presets/`, `visual-direction.md`, `design-verification.md`, skills de terceros, scripts ni dependencias.
- La capa no aplica a backend, APIs, datos, infraestructura o cambios sin UI.
- Los sistemas de diseño y marca existentes prevalecen sobre cualquier orientación del kit.
- La verificación de diseño debe vivir como sección condicional de `templates/verification.md`.
- Cada artefacto nuevo debe incluir propósito, inputs, outputs, uso y la sección breve de cambio upstream requerido.

---

## File Structure

- Create: `standards/design-quality.md` — mínimos de calidad UX/UI independientes de estilo.
- Create: `templates/design-brief.md` — brief único para UX y dirección visual opcional.
- Create: `templates/reference-pack.md` — registro opcional de referencias, licencia y originalidad.
- Modify: `templates/verification.md` — añadir comprobaciones condicionales de UI, sin duplicar el documento.
- Modify: `template/.ai/workflow.yaml` — documentar reglas de activación sin añadir etapas universales.
- Modify: `README.md` — explicar propósito, alcance, activación y decisiones aplazadas de v1.2 Lite.

### Task 1: Crear el estándar de calidad de diseño

**Files:**
- Create: `standards/design-quality.md`

**Interfaces:**
- Consumes: criterios de aceptación de `templates/specification.md` y decisiones UX de `templates/design-brief.md`.
- Produces: lista de mínimos que `templates/verification.md` debe evidenciar cuando exista UI.

- [x] **Step 1: Escribir `standards/design-quality.md`**

Incluir alcance condicional, responsabilidades, requisitos de responsive, semántica, contraste, teclado, estados, motion seguro, rendimiento, contenido realista, no engaño y claims respaldados. Declarar de forma explícita que no prescribe paleta, fuente, framework ni estilo.

- [x] **Step 2: Verificar estructura y prohibiciones**

Run: `rg -n 'responsive|teclado|prefers-reduced-motion|claims|tipograf|paleta|framework' standards/design-quality.md`

Expected: cada mínimo y el límite de no prescribir estilo aparecen en el archivo.

### Task 2: Crear artefactos de discovery UX y referencias

**Files:**
- Create: `templates/design-brief.md`
- Create: `templates/reference-pack.md`

**Interfaces:**
- Consumes: problema, ICP, propuesta de valor, objetivo de negocio, evidencia, métricas y restricciones de discovery/idea-validation/specification.
- Produces: requisitos UX, dirección visual opcional y referencias aptas para `templates/implementation-plan.md` y `templates/verification.md`.

- [x] **Step 1: Escribir `templates/design-brief.md`**

Definir propósito, cuándo usarlo, inputs y outputs. Incluir secciones para objetivo de usuario, acciones, contexto, journey, jerarquía, contenido, objeciones, estados, accesibilidad y criterios UX. Añadir bloque de landing y bloque opcional de dirección visual. Añadir el bloque corto de cambio upstream requerido.

- [x] **Step 2: Escribir `templates/reference-pack.md`**

Definir propósito, cuándo usarlo, inputs y outputs. Añadir una tabla por referencia con fuente, motivo, patrones a aprender, elementos a no copiar, licencia/uso y consideraciones de originalidad. Añadir el bloque corto de cambio upstream requerido.

- [x] **Step 3: Verificar campos requeridos**

Run: `rg -n 'Objetivo del usuario|Estados|Dirección visual|Cambio upstream requerido' templates/design-brief.md && rg -n 'Fuente|Patrones|no copiar|licencia|originalidad|Cambio upstream requerido' templates/reference-pack.md`

Expected: los dos templates contienen todos los campos definidos por el spec.

### Task 3: Extender verificación y workflow sin nuevas etapas obligatorias

**Files:**
- Modify: `templates/verification.md`
- Modify: `template/.ai/workflow.yaml`

**Interfaces:**
- Consumes: `standards/design-quality.md`, el brief y el reference pack cuando existen.
- Produces: evidencia de calidad UI proporcional al alcance y reglas de activación del workflow.

- [x] **Step 1: Ampliar `templates/verification.md`**

Añadir una sección `Calidad de diseño (si aplica)` con una tabla de checks y evidencia. Cubrir viewports, estados pertinentes, teclado/semántica/contraste, reduced motion, overflow, contenido realista, claims y originalidad. Mantener las secciones existentes de release y riesgos.

- [x] **Step 2: Actualizar `template/.ai/workflow.yaml`**

Mantener la lista de stages v1.1 intacta. Añadir reglas que activen el brief para pantalla/flujo/landing/rediseño material, limiten `reference-pack` a referencias significativas y requieran la verificación UI sólo cuando aplique.

- [x] **Step 3: Verificar que el flujo no ganó etapas universales**

Run: `rg -n 'design-brief|reference-pack|Calidad de diseño|prefers-reduced-motion' templates/verification.md template/.ai/workflow.yaml && ! rg -n '^  - (design|visual)' template/.ai/workflow.yaml`

Expected: existen reglas y checks de diseño; no existe una etapa global `design` o `visual`.

### Task 4: Documentar v1.2 Lite en el README

**Files:**
- Modify: `README.md`

**Interfaces:**
- Consumes: estándar, templates y reglas del workflow.
- Produces: guía de adopción para quien crea un proyecto desde el template.

- [x] **Step 1: Añadir sección de Design & UX Layer v1.2 Lite**

Explicar qué resuelve, qué no resuelve, el mapa de activación por tipo de trabajo, archivos usados, prioridad del sistema de diseño existente y el flujo de artefactos cuando aplica UI.

- [x] **Step 2: Añadir decisiones aplazadas**

Registrar que presets, scripts de captura/auditoría y vendorizar skills externas se evaluarán sólo cuando haya evidencia repetida en proyectos reales.

- [x] **Step 3: Verificar enlaces y lenguaje de alcance**

Run: `rg -n 'v1\.2|Design|UX|design-quality|design-brief|reference-pack|presets' README.md`

Expected: el README comunica la capa opcional y todas las decisiones de alcance.

### Task 5: Validación final de la documentación

**Files:**
- Verify: `README.md`
- Verify: `standards/design-quality.md`
- Verify: `templates/design-brief.md`
- Verify: `templates/reference-pack.md`
- Verify: `templates/verification.md`
- Verify: `template/.ai/workflow.yaml`

**Interfaces:**
- Consumes: todos los requisitos y criterios de aceptación del spec.
- Produces: evidencia fresca para la decisión de release documental.

- [x] **Step 1: Ejecutar validaciones mecánicas**

Run: `git diff --check && rg -n 'TODO|TBD' README.md standards/design-quality.md templates/design-brief.md templates/reference-pack.md templates/verification.md template/.ai/workflow.yaml`

Expected: `git diff --check` termina sin salida; no hay placeholders.

- [x] **Step 2: Confirmar footprint y exclusiones**

Run: `test -f standards/design-quality.md && test -f templates/design-brief.md && test -f templates/reference-pack.md && test ! -e design-presets && test ! -e templates/visual-direction.md && test ! -e templates/design-verification.md && git status --short`

Expected: existen sólo los tres archivos nuevos permitidos; no existen las exclusiones; el estado Git lista exactamente los cambios esperados.

- [x] **Step 3: Revisar criterios del spec uno a uno**

Comprobar que cada criterio de aceptación de `docs/superpowers/specs/2026-08-19-design-ux-lite-design.md` tiene evidencia en los archivos modificados. Registrar cualquier excepción en `templates/verification.md` antes de liberar.

- [x] **Step 4: Commit**

```bash
git add README.md standards/design-quality.md templates/design-brief.md templates/reference-pack.md templates/verification.md template/.ai/workflow.yaml docs/superpowers/specs/2026-08-19-design-ux-lite-design.md docs/superpowers/plans/2026-08-19-design-ux-lite.md
git commit -m "feat: add lightweight design UX layer"
```
