# Marco-de-Auditoria


**Institución:** SICAU

## Contexto
El SICAU es uno de los sistemas informáticos de nuestra institución educativa, encargado de administrar el ciclo de vida académico de los estudiantes y la gestión de los docentes por medio del modelo SIS. Maneja grandes volúmenes de datos sensibles, incluyendo información personal y el registro histórico de calificaciones. Sus principales riesgos son la vulneración de la confidencialidad, la pérdida de integridad, como la alteración no autorizada de notas y riesgos de servicio, como la caída del sistema durante el periodo de matrícula.

## Marco de Trabajo
* ISO/IEC 27001
* ITIL

## Justificación
Se aplicará primero **ISO/IEC 27001** porque el riesgo más crítico para la institución es la vulneración de datos sensibles. Este marco nos da los lineamientos exactos para implementar un Sistema de Gestión de Seguridad de la Información (SGSI), garantizando la confidencialidad de los datos y la integridad de las calificaciones. 

En segundo lugar, se integrará **ITIL**, ya que los riesgos de servicio (caídas del sistema en matrículas) requieren una gestión robusta. ITIL permitirá estandarizar la gestión de incidentes y asegurar la disponibilidad cuando los estudiantes más lo necesitan, complementando así la seguridad aportada por la ISO.

## Evidencias Requeridas al Equipo de TI

### Para sustentar ISO/IEC 27001:
* **Matriz de Control de Acceso (RBAC):** Documento o registro del sistema que demuestre cómo están segregados los roles.
* **Registro de Auditoría (Logs):** Evidencia de que el sistema registra quién entra y qué modifica, junto con la política documentada y las pruebas de los últimos backups realizados para garantizar la recuperación de datos (ya que los logs no deberían eliminarse en al menos 1 año).

### Para sustentar ITIL:
* **Reportes de Acuerdos de Nivel de Servicio (SLA):** Estadísticas de "uptime" (tiempo de actividad) del SICAU durante el último periodo de matrículas.
* **Registro (Ticketera) de Gestión de Incidentes:** Historial de cómo el equipo de soporte documenta, clasifica y resuelve las caídas del sistema o problemas de acceso de los usuarios.
