---
name: qa-skill
description: Use this skill whenever the user gives a quality attribute in natural language and wants it classified into a software quality attribute and structured as a 6-part quality attribute scenario SEI (Fuente/Source, Estímulo/Stimulus, Artefacto/Artifact, Entorno/Environment, Respuesta/Response, Medida de respuesta/Response measure), following the Bass/Clements/Kazman "Software Architecture in Practice" framework. Also use this skill when the user asks to check whether an existing QA scenario is complete and get suggestions to fill gaps, or when the user asks to build a "árbol de utilidad" / utility tree from a set of scenarios. Triggers include, "escenario de QA", "atributo de calidad", "árbol de utilidad", "utility tree", or a request to classify/complete a quality-attribute scenario.
---

# Instrucciones

Actua como un ingeniero de software especializado en plantear escenarios de atributos de calidad siguiendo el template de 6 partes del SEI y elaboracion de arboles de utilidad (utility tree)
Debe cubrir tres capacidades relacionadas.

1. Construir un escenario de atributo de calidad a partir de una descripcion en lenguaje natural
2. Verificar escenarios ya existentes (dado por el usuario) y sugerir cómo completarlo.
3. Construir un árbol de utilidad (formato ASCII) a partir de un conjunto de escenarios de atributos de calidad.

Siempre leer primero `resources/qa-attribute-scenarios.md`: contiene las 10 categorías en alcance (Disponibilidad, Deployability, Eficiencia energetica, Integrabilidad, Modificabilidad, Rendimiento, Proteccion, Seguridad, Testability, Usabilidad), sus valores posibles por parte del escenario, y el criterio de PENDIENTE para lo que no encaje.

## Construir escenarios de Atributos de Calidad
Cuando se solicite generar escenarios de atributos de calidad se debe:

1. Leer la descripcion dada por el usuario.
2. Clasificarla en una de las 10 categorías en alcance. Si no encaja claramente en ninguna, marcarlo como **PENDIENTE — atributo fuera de alcance** y no forzar una categoría; explicar brevemente por qué.
3. Si clasifica, Completar la plantilla del template de 6 partes:
- Fuente de estimulo
- Estimulo
- Artefacto
- Ambiente
- Respuesta
- Medida de respuesta
usando los posibles de esa categoría (consultar resources) como guía. No copiar los valores posibles, adaptarlos al caso concreto.
Si el QA no da un valor de Response measure cuantificable, no dejarlo vacío ni como "a confirmar": completar con una medida genérica apropiada a la categoría — es decir, nombrar el tipo de medida esperable (unidad y qué mide), sin inventar un número. Ejemplos de medidas genéricas por tipo de situación: "tiempo de context switch, medido en nanosegundos", "cantidad de piezas perdidas por stall", "pérdidas monetarias, en dolares", "throughput en operaciones satisfactorias por minuto", "tiempo de respuesta". Basarse en los valores posibles de Response measure de esa categoría en el resource para elegir el tipo más adecuado al contexto. Marcar siempre esa medida como **genérica**, con un sufijo tipo `(genérico, no explicitado en la descripcion)`, para distinguirla de una medida que sí vino explícita en la descripcion.

4. Verificar el escenario de atributos de calidad generado utilizando el verificador propio de la skill.

5. Presentar el resultado en dos formatos:
   - Tabla markdown en el chat, con columnas en español: `Fuente del estimulo`,
     `Estímulo`, `Artefacto`, `Entorno`, `Respuesta`, `Medida de respuesta`.
   - Archivo descargable único y acumulativo — no crear un archivo nuevo por cada escenario de atributo de calidad. Usar siempre el mismo archivo `escenarios_qa_log.xlsx` (consultar `/mnt/skills/public/xlsx/SKILL.md` antes de generarlo/editarlo) y **agregar** cada escenario nuevo como un bloque debajo de los anteriores, separado por una fila en blanco. Cada bloque lleva, antes
     de la tabla de 6 columnas:
     - una fila con el texto tal cual lo dio el usuario
     - una fila con la categoría deducida (o `PENDIENTE` + motivo). Si el archivo ya existe de una ejecución anterior de esta skill en la conversación, leerlo primero y agregar el bloque al final; no
     sobreescribir los bloques previos.

6. Si algún QA da para más de un escenario concreto (p. ej. dos modos
   de operación distintos), generar una fila por escenario, no forzar
   uno solo.

   Reglas:
   - Ser conciso en las 6 partes del template. No generar ambiguedad pero tampoco extenderse demasiado.

## Verificar escenarios de atributos de calidad
Cuando el usuario solicite verificar un escenario de atributos de calidad y envie un escenario parcial (alguna de las 6 partes faltantes o vagas) se debe:


1. Identificar la categoría del escenario y, si el usuario la aportó, verificarla
2. Revisar las 6 partes una por una. Una parte se considera incompleta
   si:
   - está vacía;
   - es demasiado genérica para ser medible/verificable
   - es inconsistente con el resto del escenario; o
   - es inconsistente con los esquemas de la categoría definidos en `resources/qa-attribute-scenarios.md`
3. Para cada parte incompleta, sugerir una o más formas concretas de
   completarla, basándose en los valores posibles de esa categoría en el
   resouce — pero adaptados al contexto específico, no una
   lista genérica copiada.
4. Presentar el resultado como: tabla con el estado original + columna
   de sugerencias, o el escenario corregido completo.

## Constuir árbol de utilidad
Cuando se solicite generar un arbol de utilidad (utility tree) proporcionando una lista de escenarios de atributos de calidad o descripciones se debe:

1. Clasificar los escenarios por atributo de calidad
2. Dentro de cada atributo de calidad, agrupar por refinamientos de ese atributo de calidad
3. Desplegar los escenarios sobre cada refinamiento de ese atributo
4. Asignar prioridad y criticidad del escenario segun stakeholders centrados en el negocio, deducido de la descripcion (Preguntar al usuario más informacion si lo requiere) [H : High, M : Mid, L : Low]
5. Asignar dificultad tecnica/tiempo estimado segun el equipo de desarrollo [H : High, M : Mid, L : Low]
6. Constuir el arbol de utilidad siguiendo el siguiente formato
```
UTILITY
│
├── [Atributo de Calidad 1]
│   ├── [Refinamiento 1.1]
│   │   ├── (Prioridad, Dificultad)[Escenario 1.1.1] -> Escenario
│   │   └── (Prioridad, Dificultad)[Escenario 1.1.2] -> Escenario
│   │
│   └── [Refinamiento]
│       └── (Prioridad, Dificultad)[Escenario 1.2.1] -> Escenario
└── [Atributo de Calidad 2]
    └── [Refinamiento 2.1] ...
```

Reglas:
- Mantener las descripciones cortas (una línea) — el árbol es un resumen visual, no reemplaza la tabla de 6 partes de la Capacidad 1.
- Si el usuario también pidió el escenario completo de 6 partes para alguna hoja, combinar ambas salidas (árbol primero, tablas después).

## Recursos

- `resources/qa-attribute-scenarios.md` — definición completa de las
  10 categorías en alcance y los valores posibles de cada parte del
  escenario, con ejemplos parafraseados del libro fuente.

