# Matriz inicial de riesgos

**Institución:** SICAU  
**Marcos de referencia:** ITIL (prioridad) e ISO/IEC 27001

## Caso y contexto actualizado

El SICAU administra el ciclo de vida académico de estudiantes y docentes mediante el modelo SIS, incluyendo el registro histórico de calificaciones y datos personales sensibles. 
El objetivo principal de esta entrega es analizar el como se gestiona y garantiza la disponibilidad del servicio durante la matricula.
La prioridad se otorga a ITIL porque al consultar al personal académico para esta auditoria se evidencia que la seguridad es la prioridad, ya bastante revisada la plataforma en aquel parametro.
ISO/IEC 27001 se integra de forma complementaria para proteger la confidencialidad e integridad de los datos.

## Aclaraciones

- No se dispone de acceso a la documentación interna real ni a los registros de auditoría del SICAU, si bien se puede consultar al personal relacionado incluso con ello la información es limitada y esta sujeta a correcciones en caso de que surja una duda.
- Se asume que no existe un proceso automatizado y documentado de desactivación de cuentas al terminar contratos o cambios de rol.
- Se asume que los logs de cambios de calificaciones existen, pero no se ha verificado su retención mínima de un año ni su revisión periódica.
- Durante el periodo de matricula la plataforma ha presentado irregularidades, esto basado en la experiencia personal del equipo, dado que se carece de la documentación que lo respalde.
- Los valores de probabilidad e impacto se asignan a partir del contexto descrito en la propuesta y en la experiencia en seguridad informatica del equipo, no de mediciones reales.

## Activos o procesos concretos identificados

1. Disponibilidad del servicio SICAU durante el periodo de matrículas.
2. Gestión de incidentes y soporte.
3. Módulo de registro y modificación de calificaciones históricas.
4. Proceso de asignación y retiro de roles de docentes y personal administrativo (RBAC).
5. Registro de auditoría (logs) de accesos y cambios.

## Matriz de riesgos

| ID | Activo | Amenaza | Vulnerabilidad | Riesgo | Prob. | Impacto | Nivel | Control actual o evidencia | Control propuesto | Justificación |
|---|---|---|---|---|---:|---:|---:|---|---|---|
| R-01 | Disponibilidad del servicio SICAU durante el periodo de matrículas | Mal funcionamiento de la plataforma durante este periodo | Alta demanda dado el volumen de accesos en un momento en especifico, saturando los sistemas | El sistema podría quedar inaccesible durante la matrícula impidiendo a los estudiantes garantizar su continuidad academica en los horarios deseados | 4 | 5 | 20 | Se supone que no existen reportes formales de uptime ni SLA definidos y medidos para periodos de matrícula | Definir e implementar SLA de disponibilidad específicos para periodos de matrícula, con monitoreo continuo de uptime y planes de capacidad previos a cada ciclo | ITIL prioriza la gestión de la disponibilidad y de la capacidad; este es el riesgo de servicio más crítico para la operación académica |
| R-02 | Gestión de incidentes y soporte (Service Desk) | Fallas recurrentes o demoras en la resolución de caídas y problemas de acceso | Ausencia de un proceso estandarizado de gestión de incidentes (clasificación, priorización, escalamiento y post-mortem) | Los incidentes de disponibilidad o acceso podrían resolverse de forma inconsistente y lenta, prolongando el tiempo de indisponibilidad y afectando a múltiples usuarios | 4 | 4 | 16 | Se asume que no existe una ticketera con clasificación formal, tiempos de respuesta definidos ni análisis post-incidente documentados | Implementar un proceso formal de gestión de incidentes alineado a ITIL (registro, categorización, priorización, resolución y post-mortem) con una ticketera centralizada y reportes de cumplimiento de tiempos de respuesta | ITIL exige una gestión de incidentes robusta; sin ella no se puede asegurar la restauración rápida del servicio en momentos críticos |
| R-03 | Módulo de registro y modificación de calificaciones históricas | Un docente o administrativo retirado (o con rol cambiado) intenta modificar notas | No existe un proceso formal y automatizado de baja de cuentas o revisión periódica de roles al terminar contratos | Un excolaborador podría consultar o alterar calificaciones históricas porque su cuenta permanece activa, afectando la integridad de los registros académicos y la confianza en el servicio | 4 | 5 | 20 | Se supone que la baja de cuentas depende de gestión manual y no se encontró evidencia de revisión mensual de roles administrativos | Desactivar automáticamente la cuenta al finalizar el contrato o cambio de rol y realizar revisión mensual documentada de todas las cuentas con permisos de modificación de calificaciones | Aunque prioritario es ITIL, la integridad de los datos que el servicio entrega es esencial; un acceso residual compromete tanto la seguridad como la confiabilidad del servicio |
| R-04 | Proceso de asignación y retiro de roles (RBAC) | Uso indebido de privilegios elevados por un usuario con rol excesivo | Segregación de roles incompleta o ausencia de matriz de control de acceso actualizada | Un usuario podría modificar calificaciones o datos de estudiantes fuera de su competencia porque los permisos no están correctamente segregados, generando alteraciones no autorizadas que afectan la calidad del servicio | 3 | 5 | 15 | Se asume que no existe una matriz RBAC formal y verificable | Elaborar y mantener una matriz de control de acceso (RBAC) actualizada, con revisión trimestral y aprobación formal de cambios de privilegios | Complementa ITIL con controles de ISO/IEC 27001; la correcta segregación de roles reduce incidentes de seguridad que impactan la continuidad del servicio |
| R-05 | Registro de auditoría (logs) de accesos y cambios | Alteración o eliminación de registros de quién modificó calificaciones o provocó incidentes | Ausencia de política formal de retención de logs (mínimo 1 año) y de revisión periódica | Podría no detectarse ni investigarse una modificación no autorizada o la causa raíz de un incidente porque los logs se eliminan prematuramente o no se revisan, impidiendo la mejora continua del servicio | 4 | 4 | 16 | Se asume que no existe evidencia de política documentada de retención de logs ni de pruebas de revisión de los últimos periodos | Implementar retención de logs de auditoría por al menos 12 meses, con protección contra modificación/eliminación y revisión semanal de cambios e incidentes relevantes | Los logs son clave tanto para la gestión de problemas (ITIL) como para la trazabilidad exigida por ISO/IEC 27001; sin ellos no se pueden prevenir recurrencias |

## Orden de prioridad por nivel de riesgo (enfoque ITIL)

1. **R-01** (Nivel 20) – Disponibilidad del servicio durante matrículas (gestión de la disponibilidad y capacidad).  
2. **R-03** (Nivel 20) – Integridad de calificaciones por cuentas residuales (impacto directo en la confiabilidad del servicio).  
3. **R-02** y **R-05** (Nivel 16) – Gestión de incidentes y trazabilidad mediante logs (procesos centrales de ITIL).  
4. **R-04** (Nivel 15) – Segregación de roles (control de acceso que reduce incidentes de seguridad).

Los valores de probabilidad e impacto se justifican por el contexto de la propuesta, ahora priorizando ITIL: los periodos de matrícula concentran la demanda del sistema y cualquier indisponibilidad tiene alto impacto operativo. Los controles propuestos son verificables (SLA documentados, ticketera, post-mortems, automatización de bajas, matriz RBAC y retención de logs) y responden directamente a las vulnerabilidades identificadas. ITIL guía la gestión del servicio y de los incidentes; ISO/IEC 27001 aporta los controles de seguridad de la información necesarios para que el servicio sea confiable y protegido.

*nota: en cuanto se tenga la oportunidad los puntos descritos serán validados con el personal del sicau, dado que se desea conocer e informar apropiadamente sobre la plataforma* 
