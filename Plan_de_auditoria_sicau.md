# Plan de Auditoría: Disponibilidad del Sistema SICAU

## 1. Identificación del equipo y del caso
**Equipo:** Manuel Gomez Bastidas
**Presentación del caso:** El SICAU es uno de los sistemas informáticos de nuestra institución educativa, encargado de administrar el ciclo de vida académico de los estudiantes y la gestión de los docentes por medio del modelo SIS. La preocupación central de la presente auditoría es la continuidad de la plataforma durante los periodos de mayor tránsito, específicamente durante el periodo de matrículas. Todo ello a través del marco ITIL.

## 2. Contexto y riesgo seleccionado.
El riesgo abordado corresponde al identificador **R-01** de la matriz de riesgos.

| Atributo | Descripción |
| :--- | :--- |
| **ID en Matriz** | R-01 |
| **Activo** | Disponibilidad del servicio SICAU durante el periodo de matrículas. |
| **Amenaza** | Saturación de conexiones concurrentes por inicio de matrículas simultáneas. |
| **Vulnerabilidad** | Ausencia de la infraestructura física necesaria para tolerar la demanda. |
| **Control actual identificado** | La universidad gestiona mediante horarios escalonados quiénes acceden a la parte de matrículas de la plataforma para no colapsar el servidor. |
| **Consecuencia posible** | Estudiantes viendo afectada su calidad académica al terminar con malos horarios, matriculando en un periodo posterior o no logrando matricular todas las materias. En el peor de los casos, varios estudiantes tendrían que pedir ayuda presencial a la universidad por fallas de la plataforma. |
| **Probabilidad** | Media (4) |
| **Impacto** | Alto (5) |
| **Nivel de Riesgo** | Crítico (29) |

## 3. Justificación y objetivo de auditoría
**Justificación:** Las deficiencias en el sistema pueden provocar graves afecciones en los alumnos. Si el sistema no les permite matricularse en los horarios previstos o con todas las materias que desean, terminarán atrasándose o, en el peor de los casos, no podrán garantizar su continuidad académica durante ese semestre. El problema empeora para aquellos que estudian y trabajan; un mal horario por culpa de la plataforma les priva de su continuidad académica o implica mayores sacrificios a nivel personal. ITIL prioriza la gestión de la disponibilidad y de la capacidad; este es el riesgo de servicio más crítico para la operación académica.

**Objetivo de la auditoría:** 
Determinar si el mecanismo de programación y restricción de accesos por horarios implementado en la plataforma SICAU está adecuadamente diseñado y operando de manera efectiva para mitigar la saturación de conexiones y garantizar la disponibilidad del servicio durante los periodos de matrícula.

## 4. Alcance funcional y exclusiones
1. **Proceso o función:** Gestión de la demanda (planificación y asignación de horarios) y Gestión de la disponibilidad/capacidad (monitoreo de carga y conexiones) durante la ejecución de las matrículas estudiantiles.
2. **Sistema o componente:** El Sistema de Información, Control y Apoyo Único (SICAU), abarcando específicamente el módulo web de matrículas, su base de datos de sesiones y el servidor de aplicaciones que procesa las conexiones.
3. **Población revisable:**
   * Configuraciones de las franjas horarias en el sistema SICAU.
   * Logs de control de concurrencia y sesiones activas del servidor durante el periodo de matrícula.
   * Tiquetes de soporte o incidentes reportados en la mesa de ayuda categorizados por lentitud, caída o fallas de inicio de sesión en el SICAU.
4. **Periodo:** El último periodo de matrículas oficial completado (semestre 2026-2), incluyendo una semana previa correspondiente a la fase de planificación y configuración.
5. **Inclusiones:** Se revisará cómo están diseñados los bloques de horarios, la capacidad matemática de sesiones en cada uno, los controles de acceso en el sistema basados en dichos horarios, y los errores más habituales reportados como incidentes.
6. **Exclusiones:** Dado que la auditoría busca únicamente garantizar la continuidad del servicio durante las matrículas, los demás apartados, módulos (ej. pagos, notas) y controles de la plataforma serán ignorados. *Nota: Esta exclusión no limita la conclusión sobre el objetivo, ya que aísla el entorno de estrés de la matrícula.*

## 5. Criterios aplicables o por confirmar
Basado en las prácticas del marco ITIL:

*   **Criterio 1 (Congruencia de Capacidad):** «El volumen máximo de estudiantes habilitados para acceder en una misma franja horaria no debe superar el límite seguro de conexiones concurrentes establecido en el análisis de capacidad técnica del servidor SICAU». *(Fuente: Criterio por confirmar mediante solicitud de la política de diseño de capacidad o arquitectura vigente en TI).*
*   **Criterio 2 (Configuración de Restricciones):** «El módulo de acceso del SICAU debe restringir el inicio de sesión a los estudiantes únicamente durante la franja horaria que les fue asignada y publicada oficialmente». *(Fuente: Política de control de acceso al aplicativo durante matrículas - Confirmada).*

## 6. Programa de trabajo: controles, procedimientos, población/muestra y evidencia esperada

### Procedimiento 1: Comprender o verificar el diseño del control
*   **Control evaluado:** La asignación de horarios escalonados de matrícula (diseñada por Secretaría Académica) reduce la vulnerabilidad al evitar que todos los estudiantes intenten acceder al mismo tiempo.
*   **Procedimiento paso a paso:**
    1. Solicitar al área de TI el documento formal de arquitectura o dimensionamiento que certifique la capacidad máxima del servidor.
    2. Solicitar a Admisiones la matriz oficial de horarios programados para el periodo evaluado.
    3. Comparar matemáticamente el volumen de estudiantes de las franjas más densas contra el límite de capacidad técnica del servidor.
*   **Población o muestra:** Revisar el 100% de las franjas horarias planificadas en la matriz para el último periodo de matrículas cerrado (2026-2).
*   **Evidencia esperada:** Documento de diseño o informe técnico de capacidad del servidor y el archivo original (Excel/PDF) con la programación de las franjas horarias.
*   **Posibles excepciones:** Que el límite de capacidad solo se conozca verbalmente sin respaldo documental, o que el diseño de los horarios asigne más estudiantes en una misma franja de los que el servidor es capaz de soportar.

### Procedimiento 2: Verificar la operación del control
*   **Control evaluado:** La restricción automatizada en el sistema SICAU que bloquea el ingreso de usuarios fuera de su horario asignado, administrada por TI, junto con el monitoreo del uso de recursos.
*   **Procedimiento paso a paso:**
    1. Revisar directamente en el sistema o mediante sesión remota cómo está parametrizada la regla de bloqueo por horarios.
    2. Solicitar un extracto de los logs de sesiones del servidor y la sábana de tiquetes de la mesa de ayuda.
    3. Cruzar los logs para confirmar que no hubo inicios de sesión exitosos de perfiles fuera de su horario, y revisar si hubo tiquetes por lentitud o caída.
*   **Población o muestra:**
    *   *Para la configuración:* Una muestra propuesta y aleatoria de 5 perfiles de estudiantes de distintas carreras.
    *   *Para logs/tiquetes:* Una muestra dirigida abarcando exclusivamente los 3 días de mayor tráfico del periodo de matrículas.
*   **Evidencia esperada:** Capturas de pantalla (*screenshots* con fecha y hora) de la configuración de reglas de acceso en el aplicativo, exporte en formato CSV de los logs de sesiones del servidor y reporte de incidentes extraído de la mesa de ayuda.
*   **Posibles excepciones:** Evidencia en logs de estudiantes ingresando en franjas no autorizadas (indicando que la restricción del sistema no operó), o la existencia de tiquetes de soporte por caídas de disponibilidad a pesar del escalonamiento.

## 7. Responsables, cronograma, supuestos y limitaciones

### Responsables dentro del equipo de auditoría
*   **Auditor Líder:** Encargado de las fases de preparación y cierre, interlocución con la gerencia y validación de los criterios de ITIL.
*   **Auditor de TI:** Responsable de la revisión técnica (Fase 3): análisis de logs de servidores, verificación de la configuración de bloqueos en el sistema y revisión del diseño de capacidad.
*   **Auditor de Procesos:** Encargado de evaluar la matriz de horarios de Admisiones y cruzar la planeación operativa contra las alertas de la mesa de ayuda.

### Cronograma de ejecución (Duración estimada: 4 semanas)
*   **Fase 1: Preparación (Semana 1):** Reunión de inicio con los auditados, confirmación del alcance y formalización del requerimiento.
*   **Fase 2: Solicitud de información (Semana 2):** Recepción de documentos normativos, diseño de capacidad, matrices de horarios, extracción de logs y accesos.
*   **Fase 3: Revisión y pruebas (Semana 3):** Ejecución de los procedimientos 1 y 2. Cruce de datos.
*   **Fase 4: Cierre (Semana 4):** Consolidación de resultados, discusión de hallazgos preliminares con TI y Admisiones, y emisión del informe final.

### Dependencias de la organización
*   Disponibilidad y tiempos de respuesta de la Dirección de TI y la Oficina de Admisiones y Registro para atender entrevistas y entregar evidencia.
*   Autorización oportuna para accesos temporales (de solo lectura) a las configuraciones del SICAU y a la mesa de ayuda.

### Hechos comprobados vs. Supuestos
*   **Hecho comprobado:** La principal vulnerabilidad es la ausencia de infraestructura física necesaria. El control actual consiste en gestionar mediante horarios escalonados quiénes acceden. El marco base es ITIL.
*   **Supuesto 1:** Se asume que la organización cuenta con un estudio técnico previo o dimensionamiento de arquitectura que establece matemáticamente la concurrencia soportada.
*   **Supuesto 2:** Se asume que los ingresos al SICAU a módulos distintos al de matrícula no afectan de manera crítica la estabilidad de la misma (o están limitados).

### Limitantes de ejecución
*   **Qué se puede realizar realmente:** Las fases de Preparación (diseño del plan, estructuración de los procedimientos y definición de criterios).
*   **Qué queda como planificación por falta de acceso:** Las fases de Solicitud de información, Revisión y Cierre. Al tratarse de un ejercicio académico o simulación, el equipo auditor no posee credenciales reales para el SICAU ni interactúa con personal de TI real, por lo que no se ejecutarán las pruebas ni se inventarán resultados.

## 8. Fuentes y referencia a la matriz completa
*   **Matriz de Riesgos de TI Institucional:** [Enlace a Google Sheets - Matriz de Riesgos](https://docs.google.com/spreadsheets/d/1bUfc8OOl4p5q25l73-oh9_8TzC5qr_04tAKcQTcUHFY/edit?usp=sharing) (Referencia directa al ID R-01).
*   **Marco de Referencia:** ITIL (Gestión de la Capacidad y Gestión de la Disponibilidad).
