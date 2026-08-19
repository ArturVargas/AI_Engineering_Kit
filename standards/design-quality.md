# Estándar de calidad de diseño

## Cuándo aplica

Este estándar aplica cuando una iniciativa crea o modifica una interfaz visible para usuarios. No aplica a backend, APIs, datos, infraestructura ni cambios internos sin UI.

Es un mínimo de calidad, no una dirección estética. El sistema de diseño, marca y convenciones existentes del proyecto siempre prevalecen.

## Mínimos de calidad

- **Jerarquía y contenido:** la acción principal, el contenido y los estados importantes se entienden con contenido realista, no solo con lorem ipsum o datos ideales.
- **Responsive:** la interfaz funciona en los viewports relevantes para el producto; no debe ocultar, solapar ni desbordar contenido de forma inesperada.
- **Semántica y accesibilidad:** usa HTML semántico, contraste suficiente, nombres accesibles y navegación por teclado donde corresponda.
- **Estados completos:** considera `loading`, `empty`, `error`, `success` y `disabled` cuando el flujo los pueda presentar.
- **Interacción y motion:** proporciona feedback claro; respeta `prefers-reduced-motion` y no depende del movimiento para comunicar información esencial.
- **Rendimiento:** evita efectos, imágenes, fuentes o animaciones que degraden de forma material la carga o interacción del caso de uso.
- **Veracidad:** no usa dark patterns ni claims, métricas, testimonios, logos o resultados sin respaldo. Marca lo no verificado como `estimate`, `placeholder` o `hold`.
- **Originalidad:** las referencias informan principios de jerarquía, densidad o composición; no se reproducen elementos distintivos, assets o estructuras de terceros sin permiso.

## Límites

Este estándar no prescribe tipografía, paleta, radios, sombras, layout, framework CSS ni componentes concretos. Esas decisiones viven en el sistema existente del proyecto o, si no existe, en la sección de dirección visual del `design-brief`.

## Evidencia proporcional

Registra en `verification.md` sólo la evidencia necesaria para el riesgo:

- Un ajuste localizado puede requerir un viewport y un estado relevante.
- Una pantalla o flujo nuevo requiere los estados, breakpoints y accesibilidad pertinentes.
- Una landing, rediseño o interfaz comercial requiere además revisión de claims, contenido, originalidad y rendimiento cuando aplique.
