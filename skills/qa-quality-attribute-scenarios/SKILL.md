---
name: qa-quality-attribute-scenarios
description: Use this skill whenever the user gives a non-functional requirement (RNF) in natural language and wants it classified into a software quality attribute and structured as a 6-part quality attribute scenario (Fuente/Source, Estímulo/Stimulus, Artefacto/Artifact, Entorno/Environment, Respuesta/Response, Medida de respuesta/Response measure), following the Bass/Clements/Kazman "Software Architecture in Practice" framework. Also use this skill when the user asks to check whether an existing QA scenario is complete and get suggestions to fill gaps, or when the user asks to build a "árbol de utilidad" / utility tree from a set of RNFs. Triggers include: "escenario de QA", "atributo de calidad", "RNF", "requerimiento no funcional", "árbol de utilidad", "utility tree", or a request to classify/complete a quality-attribute scenario.
---

# QA Quality Attribute Scenarios

Esta skill cubre tres capacidades relacionadas. Identificar cuál pidió el
usuario antes de actuar:

1. **Clasificar + construir** un escenario nuevo a partir de un RNF en
   lenguaje natural.
2. **Chequear completitud** de un escenario ya existente (dado por el
   usuario) y sugerir cómo completarlo.
3. **Construir un árbol de utilidad** (formato ASCII) a partir de un
   conjunto de RNFs.

Siempre leer primero `references/qa-attribute-scenarios.md`: contiene las
6 categorías en alcance (Disponibilidad, Interoperabilidad, Escalabilidad,
Performance, Seguridad, Usabilidad), sus valores posibles por parte del
escenario, y el criterio de PENDIENTE para lo que no encaje.

## Capacidad 1 — Clasificar y construir un escenario

Pasos:
1. Leer el RNF dado por el usuario.
2. Clasificarlo en una de las 6 categorías en alcance. Si no encaja
   claramente en ninguna, marcarlo como **PENDIENTE — atributo fuera de
   alcance** y no forzar una categoría; explicar brevemente por qué.
3. Si clasifica, instanciar las 6 partes del escenario usando los valores
   posibles de esa categoría (consultar el reference) como guía, con
   contenido específico derivado del RNF — no copiar los valores posibles
   tal cual, adaptarlos al caso concreto.
3.b. **Si el RNF no da un valor de Response measure cuantificable**
   (situación frecuente en ejercicios), no dejarlo vacío ni como
   "a confirmar": completar con una **medida genérica apropiada a la
   categoría** — es decir, nombrar el *tipo* de medida esperable (unidad
   y qué mide), sin inventar un número. Ejemplos de medidas genéricas por
   tipo de situación: "tiempo de context switch, medido en nanosegundos",
   "cantidad de piezas perdidas por stall", "pérdidas monetarias, en
   pesos", "throughput en operaciones satisfactorias por minuto", "tiempo
   de respuesta". Basarse en los valores posibles de Response measure de
   esa categoría en el reference para elegir el tipo más adecuado al
   contexto del RNF. Marcar siempre esa medida como **genérica**, con un
   sufijo tipo `(genérico, no explicitado en el RNF)`, para distinguirla
   de una medida que sí vino explícita en el RNF.
4. Presentar el resultado en dos formatos (el usuario pidió ambos):
   - **Tabla markdown en el chat**, con columnas en español: `Fuente`,
     `Estímulo`, `Artefacto`, `Entorno`, `Respuesta`, `Medida de respuesta`.
   - **Archivo descargable único y acumulativo** — no crear un archivo
     nuevo por cada RNF (satura la bandeja de descargas). Usar siempre el
     mismo archivo `escenarios_qa_log.xlsx` (consultar
     `/mnt/skills/public/xlsx/SKILL.md` antes de generarlo/editarlo) y
     **agregar** cada escenario nuevo como un bloque debajo de los
     anteriores, separado por una fila en blanco. Cada bloque lleva, antes
     de la tabla de 6 columnas:
     - una fila con el **RNF original** (texto tal cual lo dio el usuario), y
     - una fila con la **categoría deducida** (o `PENDIENTE` + motivo).
     Si el archivo ya existe de una ejecución anterior de esta skill en la

     conversación, leerlo primero y agregar el bloque al final; no
     sobreescribir los bloques previos.
5. Si algún RNF da para más de un escenario concreto (p. ej. dos modos
   de operación distintos), generar una fila por escenario, no forzar
   uno solo.

## Capacidad 2 — Chequear completitud de un escenario existente

El usuario puede pasar un escenario parcial (algunas de las 6 partes
completas, otras vacías o vagas) en cualquier formato (tabla, lista, texto
libre).

Pasos:
1. Identificar la categoría del escenario (si no la dio el usuario,
   inferirla del contenido).
2. Revisar las 6 partes una por una. Una parte se considera **incompleta**
   si:
   - está vacía;
   - es demasiado genérica para ser medible/verificable (esto aplica
     sobre todo a Response measure, que debe ser cuantificable);
   - es inconsistente con el resto del escenario; o
   - **es inconsistente con los esquemas de la categoría** definidos en
     `references/qa-attribute-scenarios.md` (p. ej. un valor de Artifact
     que no corresponde a los valores posibles de esa categoría, o un
     Response que no se alinea con las respuestas típicas esperadas para
     ese atributo).
3. Para cada parte incompleta, sugerir una o más formas concretas de
   completarla, basándose en los valores posibles de esa categoría en el
   reference — pero adaptados al contexto específico del RNF, no una
   lista genérica copiada.
4. Presentar el resultado como: tabla con el estado original + columna
   de sugerencias, o el escenario corregido completo — preguntar al
   usuario cuál prefiere si no lo especificó.

## Capacidad 3 — Árbol de utilidad (formato ASCII)

Estructura: `Utility` en la raíz → una rama por categoría de atributo de
calidad presente en el conjunto de RNFs → una o más hojas por categoría,
cada hoja siendo un escenario concreto con su par `(A, B)`:

- **A** = criticidad del escenario para los stakeholders. Se **deduce del
  contexto del RNF** (no se pregunta al usuario), usando señales como:
  impacto en el negocio, frecuencia de uso, consecuencia de falla,
  énfasis del RNF. Valor: `L` | `M` | `H`.
- **B** = dificultad/tiempo estimado para el equipo de desarrollo. También
  se deduce del contenido del RNF (complejidad técnica implícita,
  alcance del cambio). Valor: `L` | `M` | `H`.

Si la criticidad o la dificultad no se pueden deducir razonablemente del
RNF, **no usar `?`** — usar `H*` (con asterisco, para distinguirlo de un
H genuinamente deducido). Esto aplica en particular a User Stories épicas
o RNFs muy amplios, donde la dificultad agregada suele ser alta y hace
falta investigación adicional para desglosarla con precisión. Agregar una
nota al pie por cada `H*` explicando que el valor no se pudo deducir
directamente y se marcó como alto en forma conservadora, pendiente de
investigación.

### Formato de salida (texto plano, sin diagramas gráficos)

```
Utility
├─ <Categoría 1>
│  ├─ <nombre corto del escenario> (A, B) — <descripción breve una línea>
│  └─ <nombre corto del escenario> (A, B) — <descripción breve una línea>
├─ <Categoría 2>
│  └─ <nombre corto del escenario> (A, B) — <descripción breve una línea>
└─ <Categoría N>
   └─ <nombre corto del escenario> (A, B) — <descripción breve una línea>
```

Reglas:
- Usar los nombres de categoría en español de las 6 en alcance.
- Un RNF que no clasifica en ninguna categoría no entra al árbol; listarlo
  aparte como PENDIENTE, debajo del árbol.
- Mantener las descripciones cortas (una línea) — el árbol es un resumen
  visual, no reemplaza la tabla de 6 partes de la Capacidad 1.
- Si el usuario también pidió el escenario completo de 6 partes para
  alguna hoja, combinar ambas salidas (árbol primero, tablas después).

## Recursos

- `references/qa-attribute-scenarios.md` — definición completa de las
  6 categorías en alcance y los valores posibles de cada parte del
  escenario, con ejemplos parafraseados del libro fuente.
