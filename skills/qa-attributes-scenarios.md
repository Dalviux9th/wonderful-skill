# Atributos de calidad y escenarios generales (SAiP, 4ta ed.)

> Síntesis propia basada en las tablas de escenario general de Bass, Clements
> y Kazman, "Software Architecture in Practice" (4ta ed.), Caps. 3–14.
> Contenido parafraseado, no una transcripción del libro.
>
> **Alcance de esta skill (por ahora)**: solo se clasifican y construyen
> escenarios para las 6 categorías de abajo. Cualquier requerimiento no
> funcional que no encaje en ninguna de ellas se marca como **PENDIENTE**
> y no se fuerza a entrar en una categoría.

## Mapeo de nombres (español ↔ libro)

| Nombre usado en la skill | Capítulo del libro (nombre original) | Nota |
|---|---|---|
| Disponibilidad | Availability (Cap. 4) | Coincide 1:1 |
| Interoperabilidad | **Integrability** (Cap. 7) | El libro no tiene un capítulo "Interoperability"; el más cercano es Integrability (integrar componentes desarrollados por separado) |
| Escalabilidad | **Modifiability** (Cap. 8) | El libro no tiene capítulo "Scalability"; el más cercano conceptualmente es Modifiability (costo/facilidad de hacer cambios al sistema) |
| Performance | Performance (Cap. 9) | Coincide 1:1 |
| Seguridad | Security (Cap. 11) | Coincide 1:1 |
| Usabilidad | Usability (Cap. 13) | Coincide 1:1 |

**Otros atributos del libro (Deployability, Energy Efficiency, Safety, y
los del Cap. 14) quedan fuera de esta skill por ahora — no se clasifican.**

## El escenario de atributo de calidad (Cap. 3) — template de 6 partes

| # | Parte | Qué responde |
|---|-------|--------------|
| 1 | **Source (Fuente)** | Quién o qué origina el estímulo |
| 2 | **Stimulus (Estímulo)** | La condición/evento que llega al sistema |
| 3 | **Artifact (Artefacto)** | Qué parte del sistema es estimulada |
| 4 | **Environment (Entorno)** | Bajo qué condiciones ocurre |
| 5 | **Response (Respuesta)** | Qué hace el sistema ante el estímulo |
| 6 | **Response Measure (Medida de respuesta)** | Cómo se mide/verifica esa respuesta |

---

## 1. Disponibilidad (Availability) — Cap. 4, Tabla 4.2

- **Source**: origen interno o externo de la falla — personas, hardware,
  software, infraestructura física, entorno físico.
- **Stimulus**: ocurre una falla (fault) — omisión, caída (crash), timing
  incorrecto, o respuesta incorrecta.
- **Artifact**: procesadores, canales de comunicación, almacenamiento,
  procesos, u otros elementos del entorno del sistema afectados por la falla.
- **Environment**: operación normal, arranque, apagado, modo de reparación,
  operación degradada, operación sobrecargada.
- **Response**: evitar que la falla se convierta en fallo (failure);
  detectarla, registrarla (log), notificar a las entidades correspondientes
  (personas o sistemas), recuperarse de la falla, deshabilitar la fuente
  del evento, operar en modo degradado mientras se repara, o
  enmascarar/corregir/contener el daño.
- **Response measure**: ventana de tiempo en que el sistema debe estar
  disponible; porcentaje de disponibilidad (ej. 99.999%); tiempo de
  detección de la falla; tiempo de reparación; duración permitida en modo
  degradado; proporción o tasa de una clase de fallas que el sistema
  previene o maneja sin fallar.
- **Ejemplo del libro (parafraseado)**: un servidor de un server farm
  falla en operación normal; el sistema avisa al operador y sigue
  funcionando sin downtime.

## 2. Interoperabilidad (Integrability) — Cap. 7, Tabla 7.1

- **Source**: stakeholder de la misión/sistema, marketplace de
  componentes, o proveedor del componente.
- **Stimulus**: agregar un componente nuevo; integrar una nueva versión
  de un componente existente; o integrar componentes existentes de una
  forma nueva entre sí.
- **Artifact**: el sistema entero, un conjunto específico de componentes,
  metadata de un componente, o su configuración.
- **Environment**: desarrollo, integración, despliegue, o runtime.
- **Response**: los cambios quedan completados/integrados/probados/
  desplegados; los componentes intercambian información correcta (sintáctica
  y semánticamente); los componentes colaboran correctamente; no se
  violan límites de recursos.
- **Response measure**: costo en términos de cantidad de componentes
  modificados, porcentaje o líneas de código cambiadas, esfuerzo, dinero,
  tiempo calendario; y el efecto sobre otras medidas de calidad (para
  capturar trade-offs permitidos).
- **Ejemplo del libro (parafraseado)**: aparece un nuevo componente de
  filtrado de datos en el marketplace; se integra y despliega en un mes,
  con no más de un persona-mes de esfuerzo.

## 3. Escalabilidad (Modifiability) — Cap. 8, Tabla 8.1

- **Source**: usuario final, desarrollador, administrador del sistema,
  dueño de la línea de producto, o el propio sistema (si se auto-modifica).
- **Stimulus**: una directiva de agregar/eliminar/modificar funcionalidad;
  cambiar un atributo de calidad, capacidad, plataforma o tecnología;
  agregar un producto nuevo a una línea de productos; o cambiar la
  ubicación de un servicio.
- **Artifact**: código, datos, interfaces, componentes, recursos, casos
  de prueba, configuraciones, documentación.
- **Environment**: runtime, tiempo de compilación, tiempo de build,
  tiempo de inicialización, o tiempo de diseño.
- **Response**: hacer la modificación, probarla, desplegarla, o
  auto-modificarse.
- **Response measure**: costo en términos de cantidad/tamaño/complejidad
  de los artefactos afectados, esfuerzo, tiempo transcurrido, dinero,
  hasta qué punto afecta otras funciones o atributos de calidad, nuevos
  defectos introducidos, cuánto tardó el sistema en adaptarse.
- **Ejemplo del libro (parafraseado)**: un desarrollador quiere cambiar
  la interfaz de usuario; el cambio se hace en tiempo de diseño, toma
  menos de tres horas hacerlo y probarlo, sin efectos secundarios.

## 4. Performance — Cap. 9, Tabla 9.1

- **Source**: externo (pedido de un usuario, pedido de un sistema externo,
  datos llegando de un sensor u otro sistema) o interno (un componente
  pide algo a otro, un timer genera una notificación).
- **Stimulus**: llegada de un evento — periódico (intervalo predecible),
  estocástico (según una distribución de probabilidad), o esporádico (ni
  periódico ni estocástico).
- **Artifact**: el sistema completo o un componente específico.
- **Environment**: en runtime, el sistema/componente puede estar en modo
  normal, modo de emergencia, modo de corrección de errores, carga pico,
  sobrecarga, operación degradada, u otro modo definido.
- **Response**: el sistema devuelve una respuesta, devuelve un error, no
  genera respuesta, ignora el pedido si está sobrecargado, cambia de modo
  o nivel de servicio, atiende un evento de mayor prioridad, o consume
  recursos.
- **Response measure**: latencia (tiempo máximo/mínimo/promedio/mediana
  de respuesta); throughput (cantidad o % de pedidos satisfechos en un
  intervalo); cantidad o % de pedidos no satisfechos; jitter (variación
  del tiempo de respuesta); nivel de uso de un recurso de cómputo.
- **Ejemplo del libro (parafraseado)**: 500 usuarios inician 2000 pedidos
  en 30 segundos bajo operación normal; el sistema procesa todos los
  pedidos con una latencia promedio de 2 segundos.

## 5. Seguridad (Security) — Cap. 11, Tabla 11.1

- **Source**: humano u otro sistema; interno o externo a la organización;
  previamente identificado o desconocido.
- **Stimulus**: un intento no autorizado de mostrar datos, capturar datos,
  cambiar o borrar datos, acceder a servicios del sistema, cambiar su
  comportamiento, o reducir su disponibilidad.
- **Artifact**: servicios del sistema, datos dentro del sistema, un
  componente o recurso, o datos producidos/consumidos por el sistema.
- **Environment**: el sistema está online u offline; conectado o
  desconectado de la red; detrás de un firewall o abierto a la red;
  totalmente, parcialmente, o no operacional.
- **Response**: proteger datos/servicios de acceso no autorizado; evitar
  que se manipulen sin autorización; identificar con confianza a las
  partes de una transacción (no repudio); mantener datos/recursos/
  servicios disponibles para uso legítimo; registrar accesos o intentos
  de acceso; notificar a las entidades correspondientes cuando se detecta
  un aparente ataque.
- **Response measure**: cuánto de un recurso quedó comprometido o quedó
  asegurado; precisión de la detección del ataque; tiempo transcurrido
  hasta detectarlo; cantidad de ataques resistidos; tiempo de recuperación
  tras un ataque exitoso; cantidad de datos vulnerables a un ataque dado.
- **Ejemplo del libro (parafraseado)**: un empleado descontento intenta
  modificar indebidamente la tabla de sueldos en operación normal; el
  acceso no autorizado se detecta, el sistema mantiene un registro de
  auditoría, y el dato correcto se restaura en menos de un día.

## 6. Usabilidad (Usability) — Cap. 13, Tabla 13.1

- **Source**: el usuario final (posiblemente en un rol especializado,
  como administrador), o un evento externo al que el usuario reacciona.
- **Stimulus**: el usuario quiere usar el sistema eficientemente,
  aprender a usarlo, minimizar el impacto de errores, adaptarlo, o
  configurarlo.
- **Artifact**: una interfaz gráfica, una línea de comandos, una interfaz
  de voz, o una pantalla táctil.
- **Environment**: en runtime o en tiempo de configuración del sistema.
- **Response**: el sistema debe dar al usuario las funciones que necesita,
  anticipar sus necesidades, y darle feedback apropiado.
- **Response measure**: tiempo de tarea; cantidad de errores; tiempo de
  aprendizaje; relación entre tiempo de aprendizaje y tiempo de tarea;
  cantidad de tareas completadas; satisfacción del usuario; conocimiento
  ganado; relación entre operaciones exitosas y totales; tiempo o datos
  perdidos cuando ocurre un error.
- **Ejemplo del libro (parafraseado)**: un usuario descarga una
  aplicación nueva y ya la está usando productivamente tras 2 minutos de
  experimentación.

---

## Categorías fuera de alcance (marcar como PENDIENTE)

Si un RNF no encaja claramente en ninguna de las 6 categorías de arriba
(por ejemplo, si describe deployability, eficiencia energética, safety
física, u otro atributo no cubierto), la skill debe:

1. No forzarlo dentro de una de las 6 categorías.
2. Marcarlo explícitamente como **PENDIENTE — atributo fuera de alcance**.
3. Indicar brevemente por qué no encaja, sin intentar construir el
   escenario de 6 partes para él.

---

## Cómo usar este recurso en la skill de QA

Para un requerimiento no funcional (RNF) en lenguaje natural:

1. **Clasificar**: ¿a cuál de las 6 categorías pertenece? Si no encaja
   en ninguna → PENDIENTE.
2. **Instanciar el escenario concreto**: completar Source, Stimulus,
   Artifact, Environment, Response y Response Measure con el contenido
   específico del RNF, usando como guía los valores posibles de la
   categoría correspondiente de arriba.
3. **Construir la tabla de 6 columnas** con esos valores como fila del
   escenario de QA.
