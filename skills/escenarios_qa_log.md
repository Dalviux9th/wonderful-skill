# Escenarios QA — Log

> **Nota:** este `.md` es una exportación puntual (una sola vez, a pedido)
> del mismo contenido que `escenarios_qa_log.xlsx`. La skill sigue
> generando por defecto solo tabla en el chat + archivo xlsx acumulativo;
> este archivo no forma parte del flujo estándar.

---

## 1

**RNF:** Bajo condiciones normales de operación, el sistema debe procesar las transacciones de los usuarios con una latencia promedio de 2 segundos.

**Categoría:** Performance

| Fuente | Estímulo | Artefacto | Entorno | Respuesta | Medida de respuesta |
|---|---|---|---|---|---|
| Usuarios del sistema | Llegada de transacciones de los usuarios | El sistema (componente de procesamiento de transacciones) | Condiciones normales de operación | El sistema procesa la transacción y devuelve una respuesta | Latencia promedio de 2 segundos |

---

## 2

**RNF:** El sistema debe mantener información de auditoría sobre los datos que modifique cualquier individuo correctamente identificado. En caso de un ataque, la imagen correcta de los datos modificados por el usuario debe restaurarse en menos de 1 día.

**Categoría:** Seguridad

| Fuente | Estímulo | Artefacto | Entorno | Respuesta | Medida de respuesta |
|---|---|---|---|---|---|
| Individuo autenticado en el sistema | Intento no autorizado (ataque) de modificar datos | Datos del sistema modificados por el usuario | Operación normal | El sistema mantiene un registro de auditoría de las modificaciones y restaura la imagen correcta de los datos | Restauración de los datos correctos en menos de 1 día |

---

## 3

**RNF:** El sistema debe ser capaz de gestionar despliegues de hasta 1000 dispositivos, que pueden generar un gran volumen de eventos, sin degradar sus tiempos de procesamiento.

**Categoría:** Escalabilidad (refinamiento propio, base Modifiability)

| Fuente | Estímulo | Artefacto | Entorno | Respuesta | Medida de respuesta |
|---|---|---|---|---|---|
| Crecimiento del despliegue (incorporación de dispositivos externos) | Aumento del número de dispositivos desplegados (hasta 1000), generando mayor volumen de eventos | El sistema / los recursos de procesamiento de eventos | Operación bajo carga creciente | El sistema gestiona los despliegues y procesa el volumen de eventos generado | Capacidad: hasta 1.000 dispositivos externos soportados. Tiempo de respuesta bajo escala: tiempo de procesamiento por evento, medido en milisegundos, sin degradación respecto al valor base *(genérico, no explicitado en el RNF)* |

---

## 4

**RNF:** Los usuarios deben poder minimizar el impacto de los errores cancelando la operación en curso, siendo el tiempo de cancelación menor a 1 segundo.

**Categoría:** Usabilidad

| Fuente | Estímulo | Artefacto | Entorno | Respuesta | Medida de respuesta |
|---|---|---|---|---|---|
| Usuario final | El usuario quiere minimizar el impacto de un error cancelando la operación en curso | La interfaz / el componente que ejecuta la operación | Runtime, durante una operación en curso | El sistema cancela la operación en curso | Tiempo de cancelación menor a 1 segundo |

---

## 5

**RNF:** Si el controlador detecta una falla en el procesador principal durante la operación normal, pasará el control al procesador de backup.

**Categoría:** Disponibilidad

| Fuente | Estímulo | Artefacto | Entorno | Respuesta | Medida de respuesta |
|---|---|---|---|---|---|
| Procesador principal (hardware) | Falla detectada en el procesador principal | El controlador / procesador principal | Operación normal | El controlador transfiere el control al procesador de backup | Tiempo de conmutación (failover) al procesador de backup, medido en milisegundos *(genérico, no explicitado en el RNF)* |
