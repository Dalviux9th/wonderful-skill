# Atributos de calidad y escenarios generales

> Síntesis propia basada en las tablas de escenario general de Bass, Clements
> y Kazman, "Software Architecture in Practice" (4ta ed.), Caps. 3–13.
> Contenido parafraseado, no una transcripción del libro.
---

## Disponibilidad (Availability)
La disponibilidad se refiere a una propiedad del software, concretamente, que esté presente y listo para llevar a cabo su tarea cuando se necesite. La disponibilidad se basa en el concepto de fiabilidad y le añade la noción de recuperación; es decir, que cuando el sistema falla, se repara por sí mismo. La disponibilidad también abarca la capacidad de un sistema para enmascarar o reparar fallos de tal forma que no se conviertan en averías, garantizando así que el período acumulado de interrupción del servicio no supere un valor requerido durante un intervalo de tiempo especificado
### Escenario General
1. Fuente del estimulo: Esto indica de dónde proviene el fallo (Interno/externo: personas, hardware, software, infraestructura física, entorno físico)
2. Estimulo: El estímulo para un escenario de disponibilidad es un fallo (omisión, bloqueo, sincronización incorrecta, respuesta incorrecta)
3. Artefacto: Esto especifica qué partes del sistema son responsables de la avería y cuáles se ven afectadas por ella (procesadores, canales de comunicación, almacenamiento, procesos y artefactos afectados en el entorno del sistema.)
4. Ambiente: Puede que nos interese no solo cómo se comporta un sistema en su entorno «normal», sino también cómo se comporta en situaciones como, por ejemplo, cuando ya se está recuperando de un fallo. (Funcionamiento normal, arranque, apagado, modo de reparación, funcionamiento degradado, funcionamiento con sobrecarga)
5. Respuesta: La respuesta más habitual es evitar que la avería se convierta en un fallo, pero también pueden ser importantes otras respuestas, como notificar a las personas afectadas o registrar la avería para su posterior análisis. En esta sección se especifica la respuesta deseada del sistema (Evitar que la avería se convierta en un fallo; Detectar la avería; Loggear la avería; Notificar a las entidades pertinentes (personas o sistemas); Recuperarse de la avería.)
6. Medida de respuesta:  Podemos centrarnos en una serie de indicadores de disponibilidad, en función de la importancia del servicio que se preste. (Desactivar la fuente de los eventos que provocan el fallo, Quedar temporalmente fuera de servicio mientras se lleva a cabo una reparación, Corregir o enmascarar el fallo o avería, o contener el daño que provoca, Funcionar en modo degradado mientras se lleva a cabo una reparación, Momento o intervalo de tiempo en el que el sistema debe estar disponible, Porcentaje de disponibilidad)

- **Ejemplo del libro**: un servidor de un server farm
  falla en operación normal; el sistema avisa al operador y sigue
  funcionando sin downtime.

## Deployability
Llega un día en el que el software, debe salir de una computadora invididual y aventurarse al mundo para experimentar la vida real. A diferencia de nosotros, el software suele hacer ese viaje muchas veces, a medida que se van realizando cambios y actualizaciones.
Consiste en hacer que esa transición sea lo más ordenada, eficaz y —sobre todo— lo más rápida posible. Ese es el ámbito de la implementación continua (continuous deployment), que se ve facilitada en gran medida por el atributo de calidad de la capacidad de implementación.
### Escenario General
1. Fuente del estimulo: El desencadenante de la implementación. (Usuario final, desarrollador, administrador de sistemas, personal de operaciones, mercado de componentes, responsable de producto.)
2. Estimulo: Lo que provoca el desencadenante. Hay un nuevo elemento disponible para su implementación. Normalmente se trata de una solicitud para sustituir un elemento de software por una nueva versión (corregir un defecto, aplicar un parche de seguridad, actualizar a la última versión de un componente o marco de trabajo, actualizar a la última versión de un elemento producido internamente, se aprueba la incorporación de un nuevo elemento. Es necesario revertir un elemento o conjunto de elementos existentes)
3. Artefacto: lo que se va a modificar. (Componentes o módulos específicos, la plataforma del sistema, su interfaz de usuario, su entorno u otro sistema con el que interactúar, el sistema completo)
4. Ambiente: Entorno de pruebas, producción (o un subconjunto específico de cualquiera de ellos)(Implementación completa. Implementación parcial en un grupo específico de usuarios, máquinas virtuales, contenedores, servidores o plataformas.)
5. Respuesta: Lo que debería ocurrir. (Incorporar los nuevos componentes. Implementar los nuevos componentes. Supervisar los nuevos componentes. Reversar una implementación anterior.)
6. Medida de respuesta: Una medida del coste, el tiempo o la eficacia del proceso para una implementación, o para una serie de implementaciones a lo largo del tiempo. (Coste en términos de: Número, tamaño y complejidad de los artefactos afectados. Esfuerzo medio o en el peor de los casos. Tiempo transcurrido en horas o días. Dinero (gasto directo o coste de oportunidad). Nuevos defectos introducidos. Grado en que esta implementación o reversión afecta a otras funciones o atributos de calidad. Número de implementaciones fallidas. Repetibilidad del proceso. Trazabilidad del proceso. Tiempo de ciclo del proceso.)

## Eficiencia energetica (Energy Efficiency)
La eficiencia energética se refiere a la forma en que un sistema gestiona la energía que consume, ya se trate de un dispositivo móvil que funciona con batería, un sensor del Internet de las cosas (IoT) o un centro de datos. Se ha convertido en una preocupación de primer orden a medida que la informática se ha ido trasladando a infraestructuras móviles y a escala de la nube, y, inevitablemente, supone un compromiso con el rendimiento, la disponibilidad y el tiempo de comercialización.

### Escenario General
1. Fuente del estimulo: especifica quién o qué solicita o inicia una solicitud para ahorrar o gestionar energía. (Usuario final, responsable, administrador del sistema, agente automatizado)
2. Estimulo: una solicitud para ahorrar energía. (Consumo total, consumo instantáneo máximo, consumo medio, etc.)What it is: Integrability is about how cheaply and safely new or changed components can be combined with an existing system. The book frames integration difficulty as a function of the size (how many potential dependencies exist between the new component and the system) and the distance between them — syntactic, data-semantic, behavioral-semantic, temporal, or resource-related mismatches that have to be bridged.
3. Artefacto: especifica qué es lo que se va a gestionar. (Dispositivos específicos, servidores, máquinas virtuales, clústeres, etc.)
4. Ambiente: la energía se gestiona normalmente en tiempo de ejecución, pero existen muchos casos especiales interesantes, en función de las características del sistema. (Tiempo de ejecución, conectado, alimentado por batería, modo de batería baja, modo de ahorro de energía)
5. Respuesta: Acciones que lleva a cabo el sistema para ahorrar o gestionar el consumo energético. (Desactivar servicios, desasignar servicios en tiempo de ejecución, cambiar la asignación de servicios a los servidores, ejecutar servicios en un modo de menor consumo, asignar/desasignar servidores, cambiar los niveles de servicio, modificar la programación)
6. Medida de respuesta:Medida de respuesta: Las medidas giran en torno a la cantidad de energía ahorrada o consumida y a los efectos sobre otras funciones o atributos de calidad. (Carga máxima/media en kilovatios del sistema, cantidad media/total de energía ahorrada, total de kilovatios-hora consumidos, periodo de tiempo durante el cual debe mantenerse encendido)


## Integrabilidad (Integrity)
Se refiere a la facilidad y seguridad con la que se pueden combinar componentes nuevos o modificados con un sistema ya existente. El libro plantea la dificultad de la integración como una función del tamaño (el número de posibles dependencias que existen entre el nuevo componente y el sistema) y de la distancia entre ambos: discrepancias sintácticas, semánticas en cuanto a los datos, semánticas en cuanto al comportamiento, temporales o relacionadas con los recursos que es necesario salvar.
### Escenario General
1. Fuente del estimulo: ¿De dónde procede el estímulo? (Parte interesada de la misión o del sistema, mercado de componentes, proveedor de componentes)
2. Estimulo:¿Cuál es el estímulo? Es decir, ¿qué tipo de integración se describe? (Añadir un nuevo componente, integrar una nueva versión de un componente existente, integrar componentes existentes entre sí de una nueva forma)
3. Artefacto: ¿Qué partes del sistema intervienen en la integración? (Todo el sistema, un conjunto específico de componentes, metadatos de los componentes, configuración de los componentes)
4. Ambiente: ¿En qué estado se encuentra el sistema cuando se produce el estímulo? (Desarrollo, integración, implementación, tiempo de ejecución)
5. Respuesta: ¿Cómo responderá un sistema «integrable» al estímulo? (Los cambios se {completan, integran, prueban, implementan}; los componentes de la nueva configuración intercambian información de forma correcta y satisfactoria (tanto sintáctica como semánticamente); los componentes de la nueva configuración colaboran con éxito; los componentes de la nueva configuración no superan ningún límite de recursos)
6. Medida de respuesta: ¿Cómo se mide la respuesta? (Coste, en términos de uno o varios de los siguientes aspectos: número de componentes modificados, porcentaje de código modificado)

## Modificabilidad (Modifiability)
La modificabilidad se refiere, fundamentalmente, al coste y al riesgo que conlleva realizar un cambio. Qué puede cambiar, qué probabilidad hay de que se produzca ese cambio, en qué momento del ciclo de vida se lleva a cabo el cambio y quién lo realiza, y cuánto cuesta dicho cambio. Entre los conceptos especializados relacionados se incluyen la escalabilidad (adaptarse a una mayor cantidad de algo), la variabilidad (admitir variantes planificadas del producto), la portabilidad (trasladarse a una nueva plataforma) y la independencia de la ubicación.
### Escenario General
1. Fuente del estimulo: El agente que provoca que se produzca un cambio. La mayoría son personas, pero el sistema podría ser uno que aprende o se modifica por sí mismo, en cuyo caso la fuente es el propio sistema. (Usuario final, desarrollador, sistema, administrador, línea de productos, propietario, el propio sistema)
2. Estimulo: El cambio al que el sistema debe adaptarse. (Una orden para añadir, eliminar o modificar una funcionalidad, o para cambiar un atributo de calidad, una capacidad, una plataforma o una tecnología; una orden para añadir un nuevo producto a una línea de productos; una orden para trasladar un servicio a otra ubicación)
3. Artefacto: Los artefactos que se modifican. Componentes o módulos específicos, la plataforma del sistema, su interfaz de usuario, su entorno u otro sistema con el que interactúa. (Código, datos, interfaces, componentes, recursos, casos de prueba, configuraciones, documentación)
4. Ambiente: El momento o la fase en la que se realiza el cambio. (Tiempo de ejecución, tiempo de compilación, tiempo de construcción, tiempo de inicio, tiempo de diseño)
5. Respuesta: Realizar el cambio e incorporarlo al sistema. (Una o más de las siguientes acciones: realizar la modificación, probar la modificación, implementar la modificación, auto-modificarse)
6. Medida de respuesta: Los recursos que se han empleado para realizar el cambio. (Coste en términos de: número, tamaño y complejidad de los artefactos afectados; esfuerzo; tiempo transcurrido)

- **Ejemplo del libro**: un desarrollador quiere cambiar
  la interfaz de usuario; el cambio se hace en tiempo de diseño, toma
  menos de tres horas hacerlo y probarlo, sin efectos secundarios.



## Rendimiento (Performance)
Tiene que ver con el tiempo: cómo responde el sistema a los eventos (interrupciones, solicitudes, mensajes o impulsos del reloj) dentro de unos límites aceptables de tiempo o de rendimiento. Todo sistema tiene requisitos de rendimiento.
### Escenario General
1. Fuente del estimulo: El estímulo puede provenir de un usuario (o de varios usuarios), de un sistema externo o de alguna parte del sistema en cuestión. (Externo: solicitud de un usuario, solicitud de un sistema externo, datos procedentes de un sensor u otro sistema; interno: un componente puede realizar una solicitud a otro componente, un temporizador puede generar una notificación.)
2. Estimulo: El estímulo es la llegada de un evento. El evento puede ser una solicitud de servicio o una notificación de algún estado, ya sea del sistema en cuestión o de un sistema externo. (Llegada de un evento periódico, esporádico o estocástico: un evento periódico llega a intervalos predecibles; un evento estocástico llega según una distribución de probabilidad; un evento esporádico llega siguiendo un patrón que no es ni periódico ni estocástico.)
3. Artefacto: El artefacto estimulado puede ser todo el sistema o solo una parte del mismo. Por ejemplo, un evento de encendido puede estimular todo el sistema. Una solicitud de usuario puede llegar a (estimular) la interfaz de usuario. (Sistema completo, componente dentro del sistema)
4. Ambiente: El estado del sistema o del componente cuando llega el estímulo. Los modos inusuales —modo de error, modo de sobrecarga— afectarán a la respuesta. Por ejemplo, se permiten tres intentos fallidos de inicio de sesión antes de que se bloquee el dispositivo. (Tiempo de ejecución. El sistema o componente puede estar funcionando en: modo normal, modo de emergencia, modo de corrección de errores, carga máxima, modo de sobrecarga, modo de funcionamiento degradado, algún otro modo definido del sistema)
5. Respuesta: El sistema procesará el estímulo. El procesamiento del estímulo llevará tiempo. Este tiempo puede ser necesario para el cálculo, o bien puede deberse a que el procesamiento se ve bloqueado por la contienda por los recursos compartidos. Las solicitudes pueden no satisfacerse debido a que el sistema está sobrecargado o a un fallo en algún punto de la cadena de procesamiento. (El sistema devuelve una respuesta, el sistema devuelve un error, el sistema no genera ninguna respuesta, el sistema ignora la solicitud si está sobrecargado, el sistema cambia el modo o el nivel de servicio, el sistema atiende un evento de mayor prioridad, el sistema consume recursos)
6. Medida de respuesta: Las medidas de tiempo pueden incluir la latencia o el rendimiento. Los sistemas con plazos de tiempo también pueden medir la fluctuación de la respuesta y la capacidad para cumplir dichos plazos. Medir cuántas de las solicitudes quedan sin atender también es un tipo de medida, al igual que la cantidad de recursos informáticos (por ejemplo, CPU, memoria, grupo de subprocesos, búfer) que se utiliza. (El tiempo (máximo, mínimo, medio, mediana) que tarda la respuesta (latencia); el número o porcentaje de solicitudes atendidas durante un intervalo de tiempo determinado (rendimiento) o un conjunto de eventos recibidos; el número o porcentaje de solicitudes que quedan sin atender; la variación en el tiempo de respuesta (fluctuación); el nivel de uso de un recurso informático)

- **Ejemplo del libro**: 500 usuarios inician 2000 pedidos
  en 30 segundos bajo operación normal; el sistema procesa todos los
  pedidos con una latencia promedio de 2 segundos.

## Proteccion (Safety)
La proteccion se refiere a la capacidad de un sistema para evitar entrar en estados que puedan provocar lesiones, la muerte o daños, así como para detectarlos y recuperarse en caso de que se produzcan. Los estados inseguros pueden surgir de omisiones, eventos espurios («de comisión»), eventos inoportunos, valores incorrectos (obviamente erróneos o sutilmente erróneos) y eventos que faltan o están fuera de secuencia.
### Escenario General
1. Fuente del estimulo: Una fuente de datos (un sensor, un componente de software que calcula un valor, un canal de comunicación), una fuente de tiempo (reloj) o una acción del usuario (instancias específicas de: sensor, componente de software, canal de comunicación, dispositivo (como un reloj))
2. Estimulo: Una omisión, una acción indebida o la aparición de datos o sincronizaciones incorrectos (Un ejemplo concreto de omisión: un valor nunca llega. Una funciónnunca se ejecuta. Un ejemplo concreto de acción indebida: Una función se ejecuta de forma incorrecta. Un dispositivo genera un evento espurio. Un dispositivo genera datos incorrectos. Un caso concreto de datos incorrectos: Un sensor transmite datos incorrectos. Un componente de software produce resultados incorrectos. Un fallo de sincronización: Los datos llegan demasiado tarde o demasiado pronto. Un evento generado se produce demasiado tarde o demasiado pronto, o a una frecuencia incorrecta. Los eventos se producen en un orden incorrecto.)
3. Artefacto: The artifact is some part of the system. (Safety-critical portions of the system)
4. Ambiente: System operating mode (Normal operation, Degraded operation, Manual operation, Recovery mode)
5. Respuesta: El sistema no sale del espacio de estados seguros, o bien vuelve a él, o bien continúa funcionando en modo degradado para evitar (más) lesiones o daños, o para minimizarlos. Se avisa a los usuarios del estado inseguro o (Reconocer el estado inseguro y una o varias de las siguientes acciones: Evitar el estado inseguro. Recuperarse. Continuar en modo degradado o modo seguro. Apagar. Cambiar a funcionamiento manual. Cambiar a un sistema de respaldo. Notificar a las entidades competentes)
6. Medida de respuesta: tiempo necesario para volver al estado seguro; daños o lesiones causados (uno o varios de los siguientes: número o porcentaje de entradas en estados inseguros que se evitan; número o porcentajes de estados inseguros a partir de los cuales el sistema puede recuperar (automáticamente), Variación de la exposición al riesgo, Porcentaje de tiempo durante el cual el sistema puede recuperarse, Tiempo que el sistema permanece en modo degradado o seguro, Tiempo o porcentaje de tiempo que el sistema permanece apagado, Tiempo transcurrido hasta el inicio y la recuperación (desde el funcionamiento manual, desde un modo seguro o degradado))

## Seguridad
Mide la capacidad de un sistema para proteger los datos y los servicios frente al acceso no autorizado, sin dejar de prestar servicio a los usuarios autorizados. El marco clásico es el de CIA: confidencialidad (sin acceso no autorizado), integridad (sin manipulación no autorizada) y disponibilidad (no se bloquea el uso legítimo, por ejemplo, mediante un ataque de denegación de servicio).
### Escenario General
1. Fuente del estimulo:
2. Estimulo: El estímulo es un ataque. Un intento no autorizado de: (mostrar datos, capturar datos, modificar o eliminar datos, acceder a los servicios del sistema, alterar el comportamiento del sistema, reducir la disponibilidad)
3. Artefacto:  ¿Cuál es el objetivo del ataque? (Servicios del sistema, datos dentro del sistema, un componente o recursos del sistema, datos producidos o consumidos por el sistema)
4. Ambiente: ¿Cuál es el estado del sistema cuando se produce el ataque? El sistema está: (en línea o fuera de línea, conectado o desconectado de una red, protegido por un cortafuegos o abierto a una red, totalmente operativo, parcialmente operativo, no operativo)
5. Respuesta: El sistema garantiza el mantenimiento de la confidencialidad, la integridad y la disponibilidad. Las transacciones se llevan a cabo de tal manera que (los datos o servicios estén protegidos contra el acceso no autorizado; los datos o servicios no sean manipulados sin autorización; las partes de una transacción sean identificadas con certeza; las partes de la transacción no puedan negar su participación; y los datos, recursos y servicios del sistema estén disponibles para su uso legítimo, El sistema realiza un seguimiento de las actividades que tienen lugar en su interior mediante: (el registro de accesos o modificaciones; el registro de intentos de acceso a datos, recursos o servicios; la notificación a las entidades pertinentes —personas o sistemas— cuando se produce un ataque aparente))
6. Medida de respuesta: Las medidas de respuesta de un sistema están relacionadas con la frecuencia de los ataques que tienen éxito, el tiempo y el coste que supone resistir y reparar los ataques, y los daños derivados de dichos ataques. Uno o varios de los siguientes aspectos: (qué parte de un recurso se ve comprometida o garantizada; la precisión en la detección de ataques; cuánto tiempo transcurrió antes de que se detectara un ataque; cuántos ataques se repelieron; cuánto tiempo se tarda en recuperarse de un ataque exitoso; qué cantidad de datos es vulnerable a un ataque concreto)

- **Ejemplo del libro (parafraseado)**: un empleado descontento intenta
  modificar indebidamente la tabla de sueldos en operación normal; el
  acceso no autorizado se detecta, el sistema mantiene un registro de
  auditoría, y el dato correcto se restaura en menos de un día.

## Testabilidad (Testability)
Es la facilidad con la que el software revela sus fallos mediante las pruebas; dicho de manera informal, si existe un error, ¿qué probabilidad hay de que salga a la luz en la siguiente ejecución de pruebas? Una buena testabilidad también implica que sea fácil reproducir un error y delimitar su causa.
### Escenario General
1. Fuente del estimulo: Los casos de prueba pueden ser ejecutados por una persona o por una herramienta de pruebas automatizadas. (Probadores unitarios, probadores de integración, probadores de sistema, probadores de aceptación, usuarios finales; pueden ejecutar las pruebas manualmente o utilizar herramientas de pruebas automatizadas)
2. Estimulo: Se inicia una prueba o un conjunto de pruebas. (Validar las funciones del sistema, validar la calidad, detectar amenazas emergentes para la calidad)
3. Artefacto: El artefacto es la parte del sistema que se está probando y cualquier infraestructura de pruebas necesaria. (Una unidad de código (que se corresponde con un módulo de la arquitectura), componentes, servicios, subsistemas, el sistema completo, la infraestructura de pruebas)
4. Ambiente: Las pruebas se llevan a cabo en diversos eventos o hitos del ciclo de vida. (La finalización de un incremento de código, como una clase, una capa o un servicio; la integración completa de un subsistema; la implementación completa de todo el sistema; el despliegue del sistema en un entorno de producción; la entrega del sistema a un cliente; un calendario de pruebas).
5. Respuesta:  El sistema y su infraestructura de pruebas pueden controlarse para realizar las pruebas deseadas, y pueden observarse los resultados de las mismas. (Ejecutar el conjunto de pruebas y capturar los resultados; capturar la actividad que provocó el fallo; controlar y supervisar el estado del sistema)
6. Medida de respuesta: Las medidas de respuesta tienen por objeto representar la facilidad con la que un sistema sometido a prueba «revela» sus fallos o defectos. (Esfuerzo necesario para encontrar un fallo o una clase de fallos; esfuerzo necesario para alcanzar un porcentaje determinado de cobertura del espacio de estados; probabilidad de que un fallo se revele en la siguiente prueba; tiempo necesario para realizar las pruebas; esfuerzo necesario para detectar fallos; tiempo necesario para preparar la infraestructura de pruebas; esfuerzo necesario para llevar el sistema a un estado específico; reducción de la exposición al riesgo)



## Usabilidad (Usability)
Se refiere a la facilidad con la que un usuario puede llevar a cabo lo que se propone, así como al apoyo que le brinda el sistema durante el proceso. Ayudar a los usuarios a familiarizarse con el sistema, permitirles trabajar de forma eficiente, minimizar los efectos negativos de los errores de los usuarios, adaptar el sistema a las necesidades del usuario y fomentar la confianza y la satisfacción del usuario.
### Escenario General
1. Fuente del estimulo: ¿De dónde procede el estímulo? (El usuario final que puede desempeñar una función especializada, como la de administrador de sistemas o de redes es la fuente principal del estímulo en lo que respecta a la usabilidad. Un evento externo que llega al sistema, y al que el usuario puede reaccionar también puede ser una fuente de estímulo.)
2. Estimulo: ¿Qué quiere el usuario final? (Utilizar un sistema de forma eficiente, aprender a utilizar el sistema, minimizar el impacto de los errores, adaptar el sistema, configurar el sistema)
3. Artefacto: ¿Qué parte del sistema está siendo estimulada? (Una interfaz gráfica de usuario, una interfaz de línea de comandos, una interfaz de voz, una pantalla táctil)
4. Ambiente: ¿Cuándo llega el estímulo al sistema? (Las acciones del usuario que afectan a la usabilidad siempre tienen lugar en tiempo de ejecución o en el momento de la configuración del sistema.)
5. Respuesta: ¿Cómo debe responder el sistema? (Proporcionar al usuario las funciones necesarias, anticiparse a las necesidades del usuario, proporcionar una retroalimentación adecuada al usuario)
6. Medida de respuesta: ¿Cómo se mide la respuesta? (Tiempo de realización de la tarea, número de errores, tiempo de aprendizaje, relación entre el tiempo de aprendizaje y el tiempo de realización de la tarea, número de tareas completadas, satisfacción del usuario, aumento de los conocimientos del usuario, relación entre las operaciones correctas y el total de operaciones, cantidad de tiempo o datos perdidos cuando se produce un error)
**Ejemplo del libro (parafraseado)**: un usuario descarga una
  aplicación nueva y ya la está usando productivamente tras 2 minutos de
  experimentación.

---

## Trabajar con categorias no especificadas

Si una descripcion no encaja claramente en ninguna de las categorias de arriba la skill debe:

1. No forzarlo dentro de una de las 10 categorías.
2. Marcarlo explícitamente como **PENDIENTE — atributo fuera de alcance**.
3. Indicar brevemente por qué no encaja, sin intentar construir el escenario de 6 partes para él.

---

## Cómo usar este recurso en la skill de QA

Para un atributo de calidad en lenguaje natural:

1. **Clasificar**: ¿a cuál de las categorías pertenece? Si no encaja
   en ninguna → PENDIENTE.
2. **Instanciar el escenario concreto**: completar Source, Stimulus,
   Artifact, Environment, Response y Response Measure con el contenido
   específico del RNF, usando como guía los valores posibles de la
   categoría correspondiente de arriba.
3. **Construir la tabla de 6 columnas** con esos valores como fila del
   escenario de QA.
