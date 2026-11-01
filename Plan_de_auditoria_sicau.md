# Plan de Auditoría

## 1. Identificación del equipo y del caso

**Equipo:** Manuel Gomez Bastidas **Presentación del caso:**
EI SICAU es uno de los sistemas informáticos de nuestra institución educativa, encargado de administrar el ciclo de vida académico de los estudiantes y la gestión de los docentes por medio del modelo SIS. La preocupación central de la presente auditoría es la continuidad de la plataforma durante los periodos de mayor tránsito, o al menos en este caso particular, durante el periodo de matrículas. Todo ello a través del marco ITIL.

## 2. Contexto y riesgo seleccionado, con referencia a la matriz

**Riesgo seleccionado (Ref. ID R-01):**

| Atributo | Descripción | 
| ----- | ----- | 
| **Activo** | Disponibilidad del servicio SICAU durante el periodo de matrículas. | 
| **Amenaza** | Saturación de conexiones concurrentes por inicio de matrículas simultáneas. | 
| **Vulnerabilidad** | Ausencia de la infraestructura física necesaria para tolerar la demanda. | 
| **Consecuencia posible** | Algunos estudiantes verían afectada su calidad académica terminado con malos horarios al matricular en un periodo posterior al seleccionado o no pudiendo matricular todas las materias. En el peor de los casos varios estudiantes tendrian que acudir a pedir ayuda a la universidad ya que la plataforma no permitió matricularlos. | 
| **Probabilidad** | Media. | 
| **Impacto** | Alto. | 
| **Nivel** | Crítico. | 
| **Control identificado** | La universidad gestiona mediante los horarios quienes acceden a la parte de matriculas de la plataforma para no colapsar el servidor. | 

## 3. Justificación y objetivo de auditoría

**Justificación (Razón):**
Las deficiencias en el sistema pueden provocar graves afecciones en los alumnos, si el mismo no les permite matricularse en los horarios que tienen previstos o con todas las materias que desean terminarán atrasandose o en el peor de los casos no podrán garantizar su continuidad académica durante ese semestre. El problema empeora en el caso de aquellos que estudian y trabajan, un mal horario por culpa de la plataforma les priva de su continuidad académica o implica mayores sacrificios a nivel personal.

**Objetivo de auditoría (Alcance de la auditoría):**
Determinar si el mecanismo de programación y restricción de accesos por horarios implementado en la plataforma SICAU realmente mitiga la saturación de conexiones y garantizar la disponibilidad del servicio durante los periodos de matrícula.

## 4. Alcance funcional y exclusiones

**Delimitar el alcance funcional:**

1. **Proceso o función:** Gestión de la demanda (planificación y asignación de horarios) y Gestión de la disponibilidad (monitoreo de carga y conexiones) durante la ejecución de las matrículas estudiantiles.

2. **Sistema o componente:** El Sistema de Información, Control y Apoyo y Unico (SICAU), abarcando específicamente el módulo web de matrículas, su base de datos de sesiones y el servidor de aplicaciones que procesa las conexiones.

3. **Población:**

   * Configuraciones de las franjas horarias en el sistema SICAU.

   * Logs de control de concurrencia/sesiones activas del servidor durante el periodo de matrícula.

   * Tiquetes de soporte o incidentes reportados en la mesa de ayuda categorizados por lentitud, caída o fallas de inicio de sesión en el SICAU.

4. **Periodo:** El último periodo de matrículas oficial completado (semestre 2026-2) incluyendo una semana previa por la fase de planificación y configuración.

5. **Áreas o responsables:**

   * Dirección de Tecnologías de la Información (custodios de los logs, capacidad técnica y mesa de ayuda).

   * Secretaría Académica (responsables de definir la distribución de la población estudiantil en los horarios).

6. **Inclusiones y exclusiones:**

   * **Inclusiones:** Como están diseñados los bloques de horarios, cuántas sesiones hay en cada uno y durante cuales son los errores más habituales enviados como queja o reporte.

   * **Exclusiones:** dado que la auditoría busca únicamente garantizar la continuidad del servicio durante las matrículas los demás apartados de la plataforma serán ignorados, solo centrándose en aquellos que tengan algo que ver con la matrícula.

## 5. Criterios aplicables o por confirmar

**Establecer criterios de evaluación (Basado en las prácticas del marco ITIL):**

* **Criterio 1 (Congruencia de Capacidad):** «El volumen máximo de estudiantes habilitados para acceder en una misma franja horaria no debe superar el límite seguro de conexiones concurrentes establecido en el análisis de capacidad técnica del servidor SICAU». (Fuente: criterio por confirmar mediante solicitud de la política de diseño de capacidad vigente).

* **Criterio 2 (Configuración de Restricciones):** «El módulo de acceso del SICAU debe restringir el inicio de sesión a los estudiantes únicamente durante la franja horaria que les fue asignada y publicada oficialmente». (Fuente: Política de control de acceso al aplicativo durante matrículas).

## 6. Programa de trabajo: controles, procedimientos, población/muestra y evidencia esperada

**Procedimiento 1: Comprender o verificar el diseño del control**

* **Control:** La asignación de horarios escalonados de matrícula, Secretaría Académica, reduce la vulnerabilidad al evitar que todos los estudiantes intenten acceder al mismo tiempo.

* **Criterio:** La cantidad máxima de estudiantes citados por cada franja horaria no debe superar el límite que puede tolerar el servidor.

* **Procedimiento:**

  1. Solicitar al área de Tl el documento formal de arquitectura o dimensionamiento que certifique la capacidad máxima del servidor.

  2. Solicitar a Admisiones la matriz oficial de horarios programados para el periodo evaluado.

  3. Comparar el volumen de estudiantes de las franjas más densas contra el límite de capacidad técnica.

* **Población o muestra:** Revisar todas las franjas horarias planificadas en la matriz para el último periodo de matrículas cerrado (2026-2).

* **Evidencia esperada:** Documento de diseño o informe técnico de capacidad del servidor y el archivo original con la programación de las franjas horarias, además del registro de cuantas sesiones activas hubieron.

* **Posibles excepciones:** Que el límite de capacidad solo se conozca verbalmente sin respaldo documental, o que el diseño de los horarios asigne más estudiantes en una misma franja de los que el servidor es capaz de soportar.

**Procedimiento 2: Verificar la operación del control**

* **Control:** La restricción automatizada en el sistema SICAU que bloquea el ingreso de usuarios fuera de su horario asignado, administrada por TI, junto con el monitoreo del uso de recursos durante las matrículas.

* **Criterio:** El sistema SICAU debe impedir el acceso de estudiantes en horarios no autorizados, manteniendo los niveles de concurrencia por debajo del umbral de saturación.

* **Procedimiento:**

  * Revisar directamente en el sistema o mediante sesión remota cómo está parametrizada la regla de bloqueo por horarios.

  * Solicitar un extracto de los logs de sesiones del servidor y la sábana de tiquetes de la mesa de ayuda.

  * Cruzar los logs para confirmar que no hubo inicios de sesión exitosos de perfiles fuera de su horario, y revisar si hubo tiquetes por lentitud o caída.

* **Población o muestra:**

  * Para la configuración: Una muestra propuesta y aleatoria de 5 perfiles de estudiantes de distintas carreras.

  * Para logs/tiquetes: Una muestra dirigida abarcando exclusivamente los 3 días de mayor tráfico del periodo de matrículas.

* **Evidencia esperada:** Capturas de pantalla (screenshots con fecha y hora) de la configuración de reglas de acceso en el aplicativo, exporte en formato CSV de los logs de sesiones del servidor y reporte de incidentes extraído del sistema de mesa de ayuda.

* **Posibles excepciones:** Evidencia en logs de estudiantes ingresando en franjas no autorizadas (indicando que la restricción del sistema no operó), o la existencia de tiquetes de soporte por caídas de disponibilidad a pesar del escalonamiento.

## 7. Responsables, cronograma, supuestos y limitaciones

**Organizar la ejecución propuesta**

**Cronograma breve (Duración estimada: 4 semanas)**

* **Fase 1: Preparación (Semana 1):** Reunión de inicio con los auditados, confirmación del alcance y formalización del requerimiento de auditoría.

* **Fase 2: Solicitud de información (Semana 2):** Recepción de documentos normativos, diseño de capacidad, matrices de horarios, extracción de logs y acceso de lectura al aplicativo SICAU.

* **Fase 3: Revisión y pruebas (Semana 3):** Ejecución de los procedimientos 1 (diseño) y 2 (operación). Cruce de datos entre capacidad técnica, horarios programados y logs de concurrencia.

* **Fase 4: Cierre (Semana 4):** Consolidación de resultados, discusión de hallazgos preliminares con TI y Admisiones, y emisión del informe final.

**Responsables dentro del equipo de auditoría**

* **Auditor Líder:** Encargado de las fases de preparación y cierre, interlocución con la gerencia y validación de los criterios de ITIL.

* **Auditor de TI:** Responsable de la revisión técnica (Fase 3): análisis de logs de servidores, verificación de la configuración de bloqueos en el sistema y revisión del diseño de capacidad.

* **Auditor de Procesos:** Encargado de evaluar la matriz de horarios de Admisiones y cruzar la planeación operativa contra las alertas de la mesa de ayuda.

**Dependencias de la organización**

* Disponibilidad y tiempos de respuesta de la Dirección de TI y la Oficina de Admisiones y Registro para atender entrevistas y entregar la evidencia solicitada.

* Autorización oportuna para accesos temporales (de solo lectura) a las configuraciones del SICAU y a la herramienta de mesa de ayuda.

**Recursos necesarios**

* Herramientas de análisis de datos (ej. Excel o ACL) para procesar altos volúmenes de logs.

**Limitante de ejecución.**

* **Qué se puede realizar realmente:** Las fases de Preparación (diseño del plan, estructuración de los procedimientos y definición de criterios).

* **Qué queda como planificación por falta de acceso:** Las fases de Solicitud de información, Revisión y Cierre. Al tratarse de un ejercicio académico o de simulación sobre un caso propuesto, el equipo auditor no posee credenciales reales para el SICAU, no interactúa con el personal de TI, ni tiene acceso a logs verídicos, por lo que no se ejecutará la prueba.

**Aclaraciones:**
**Hecho comprobado:**

* La principal vulnerabilidad es la ausencia de infraestructura física necesaria para tolerar la demanda libre de todos los estudiantes al mismo tiempo.

* El control actualmente identificado e implementado por la universidad consiste en gestionar mediante horarios escalonados quiénes acceden a la plataforma de matrículas, más este mismo control sigue permitiendo acceder de manera habitual al SICAU.

* El marco de referencia metodológico seleccionado para esta auditoría es ITIL.

**Supuesto:**

* Se asume que la organización cuenta con un estudio técnico previo o dimensionamiento de arquitectura que establece matemáticamente cuántas conexiones simultáneas soporta el servidor antes de degradarse.

* Se asume que los ingresos al SICAU si no son directamente a la parte de matricula no deberían afectar la estabilidad de la misma.

**Información por solicitar:**

* El documento de política o procedimiento interno de Gestión de Capacidad y Disponibilidad.

* La matriz oficial de horarios de matrícula expedida por Admisiones y Registro para el último periodo.

* Los registros de auditoría (logs) del servidor del sistema SICAU y el reporte de incidentes de la mesa de ayuda correspondientes a las fechas críticas de matrículas.

## 8. Fuentes y referencia a la matriz completa

* **Matriz de Riesgos:** [Documento de Google Sheets](https://docs.google.com/spreadsheets/d/1bUfc8OOl4p5q25l73-oh9_8TzC5qr_04tAKcQTcUHFY/edit?usp=sharing)
