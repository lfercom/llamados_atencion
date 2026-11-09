# TRAZA — Decisiones y dependencias por entrega

**Fecha:** 04-11-2026. **Estado:** resoluciones técnicas de diseño y recomendaciones funcionales para validación. Este registro prepara el PLAN; no fija fechas, presupuesto ni aceptación del producto.

## 1. Decisiones técnicas resueltas para el diseño

Se seleccionan Flutter Web/Dart; Edge Functions/TypeScript y SQL; Supabase Auth/Storage; PostgreSQL y Firebase Hosting. Arquitectura modular por capas y MVVM para presentación; Repository, Adapter e inyección de dependencias. No se requiere seleccionar una biblioteca de estado para aprobar esta organización.

Se adoptan versiones documentales inmutables, firma asociada a versión, control de concurrencia con versión esperada, una aceptación por aprendiz/versión y operaciones idempotentes con resultado transaccional. El envío documental usa outbox durable, primer intento automático y conciliación de incertidumbre. Los archivos privados se verifican antes de confirmar sus referencias; la limpieza de temporales debe respetar objetos vinculados.

La implementación y las pruebas demostrarán estas garantías. No se da por superada la incidencia táctil previa. Versiones de SDK, bibliotecas, proveedor de correo y ejecución del renderizador se seleccionarán al comprobar compatibilidad en el ambiente de implementación; faltan las copias institucionales para comprobar fidelidad documental.

## 2. Recomendaciones funcionales concretas para confirmar

DC-01, DC-02 y la disponibilidad de DC-03 fueron confirmadas e incorporadas en los tres documentos. Las demás propuestas mantienen su estado pendiente.

| ID de trabajo | Tema / origen | Recomendación | Consecuencia |
|---|---|---|---|
| DC-01 | Importación por ficha; DT-014/H-TRD-01 | **Confirmada:** solo fichas asociadas al instructor; validar por fila al revisar y confirmar; rechazo seguro y éxito parcial autorizado. | Implementar y probar. |
| DC-02 | Correo; DT-014/H-TRD-02 | **Confirmada con cambio:** correos disponibles sin vínculo con fichas. El Instructor selecciona al preparar la comunicación; generación conservada inicia automáticamente envío. Revisa selección antes de reintento. | Descartada la propuesta de correo por ficha. Conservar destinatario por intento. |
| DC-03 | Umbrales; DT-014/H-TRD-04 | **Confirmada parcialmente:** mantener opciones no generadas al superar 2/3/4. | No se confirmó uno por tipo/aprendiz; generaciones independientes repetidas pendientes. |
| DC-04 | Cambios de ficha; DT-014/H-TRD-03 | Mantener traslados fuera de la interfaz MVP. Antes de permitir un cambio operativo, acordar el acceso al historial anterior y la responsabilidad sobre este. Conservar siempre el conteo continuo por aprendiz. | La primera importación puede avanzar; un traslado no se implementa por actualizar libremente numero_ficha. |
| DC-05 | Anulaciones; DP-05 | Mantener la acción deshabilitada hasta definir autoridad institucional y efectos. Propuesta para discusión: autorización institucional registrada, original conservado y exclusión del llamado anulado del conteo efectivo, sin borrar documentos ya emitidos; su revisión sería una actuación explícita. | No está resuelto quién autoriza ni cómo se atienden planes/comunicaciones previos. No se acepta como regla ni se retira del alcance sin decisión del responsable. |
| DC-06 | Compromisos corregidos; DT-007 | Conservar seguimiento en la versión de compromiso original. Si una corrección crea un compromiso sustancialmente distinto, iniciar seguimiento separado en el nuevo compromiso y mantener vínculo con el anterior. | Evita trasladar evidencias a obligaciones diferentes; requiere validación funcional antes de habilitar este caso. |

DC identifica propuestas de este registro, no sustituye los identificadores DP/DT del TRD. DC-01 y DC-02 están confirmadas; DC-03 está resuelta en disponibilidad y pendiente en cantidad de generaciones. DC-06 requiere confirmación. DC-04/DC-05 requieren aclarar responsabilidades institucionales antes de habilitar los casos afectados.

## 3. Entregas y condiciones de entrada/salida

| Entrega propuesta | Contenido y referencia | Puede avanzarse ahora | Condición para cerrar la entrega |
|---|---|---|---|
| E0. Base técnica y validaciones tempranas | §4 TRD; DT-001/002/003/006/007/012/015 | Estructura modular, contratos, datos sintéticos y prototipos de documento/firma. | Fijar versiones reproducibles y herramientas; obtener formatos institucionales; demostrar captura táctil completa y acceso privado con servicios de prueba. |
| E1. Identidad y acceso | RF-01; RT-001–005; TEST-001–003 | Diseño de provisión operativa y vínculo de aprendiz; pruebas de aislamiento y fallos parciales. | Definir sesiones, renovación/expiración, cierre y recuperación; responsable de altas Instructor/fichas. Verificar acceso directo y ausencia de exposición tras cierre. |
| E2. Importación y consulta | RF-02; TEST-003/004 | Parser, validación, duplicados, reporte y confirmación explícita. | DC-01 confirmada; fijar delimitador, límites y normalización con archivos representativos; probar CSV/JSON y fallos parciales. |
| E3. Llamados e historial | RF-03/09; TEST-005/010/012/014 | Guardado, historial, versión correctiva, conteo continuo y estado vacío. | Disponer del formato oficial; probar idempotencia, integridad y permisos. Anulación queda bloqueada por DP-05; registrar esa limitación al aceptar una entrega parcial. |
| E4. Planes y seguimiento | RF-04/05; TEST-006/007/010 | Representación institucional, varios compromisos y actuaciones internas. | DC-03 confirmada en disponibilidad; resolver generaciones repetidas y DC-06; validar plantilla y relaciones de versiones/seguimientos. |
| E5. Firma y aceptación | RF-08; TEST-009–011/017 | Pruebas tempranas desde E0; consulta, trazo, confirmación y vínculo exacto. | Aprobar matriz de dispositivos y criterios de accesibilidad; ejecutar firma táctil real, fallos, concurrencia y persistencia. La prueba de laboratorio previa no cierra esta entrega. |
| E6. Comunicaciones y correo | RF-06/07; TEST-008/021 | Contratos, outbox y adaptador simulado; conservación del documento sin destinatario. | DC-02 y disponibilidad DC-03 confirmadas; resolver generaciones repetidas; elegir proveedor con evidencia de adjunto y tratamiento de incertidumbre, validar remitente institucional y mecanismo de despacho recuperable. |
| E7. Operación y piloto | RNF-01–07; TEST-015–019 | Preparar procedimientos de restauración y guías de operación. | Aprobar carga, objetivos de rendimiento/disponibilidad, RPO/RTO, conservación, región, presupuesto y responsables. Probar restauración coherente de datos y objetos y revisar pendientes funcionales antes de declarar MVP completo. |

La firma y la integridad son transversales: E5 no justifica posponer sus contratos hasta después de implementar documentos. E0 debe comprobar sus incertidumbres; E3/E4 respetan desde el inicio las versiones y referencias que usará E5.

## 4. Información necesaria que no puede inferirse

- Copias vigentes de los formatos institucionales de llamado, GOR-F-084 V02 y GD-F-011, incluidas instrucciones de diligenciamiento.
- Autoridad para anular y responsable de provisión de instructores/asociaciones.
- Dispositivos/navegadores reales de los usuarios y necesidades de accesibilidad.
- Usuarios concurrentes, volumen esperado, presupuesto y condiciones institucionales de alojamiento/correo.
- Políticas de sesión y conservación, pérdida tolerable de datos y tiempo de recuperación aceptable.

Cada elemento se solicita antes de la entrega que dependa de él. No bloquea redactar el PLAN ni preparar pruebas con datos sintéticos. El cierre de una decisión técnica debe diferenciar «seleccionada para diseño», «implementada» y «verificada».

## 5. Confirmación del responsable

El 04-11-2026 el responsable confirmó DC-01, sustituyó el correo por ficha por selección de destinatario sin asociación a fichas (DC-02) y confirmó únicamente la conservación de opciones omitidas de DC-03. La propuesta de un documento independiente de cada tipo por aprendiz no fue confirmada y permanece pendiente. La selección previa a generación conserva el envío automático sin confirmación adicional ya aprobado.


## Registro complementario confirmado — 04-11-2026 (DC-07/DC-08)

**Fuente:** instrucción expresa de Luis Fernando Corredor Mora en la revisión de E0. Se conserva la versión documental existente; este registro actualiza únicamente las decisiones indicadas y no aprueba las propuestas físicas del nuevo anexo.

- **DC-07, confirmada:** identificación del aprendiz como texto, con ceros iniciales; retirar espacios exteriores antes de validar; exigir uno o más dígitos ASCII 0–9. Rechazar vacío, espacios internos, letras, puntos, guiones y otros caracteres; no convertir a número ni limpiar caracteres inválidos silenciosamente. Error localizado por fila. ` 00123456 ` se acepta como `00123456`; `0012 3456`, `1.234.567` y solo espacios se rechazan. Aplicar la misma regla al dato de identificación utilizado en autorregistro. El conjunto exacto de espacios exteriores se precisa como propuesta P-06 del anexo, sin ampliarlo silenciosamente.
- **DC-08, confirmada:** Luis Fernando Corredor Mora asume inicialmente la habilitación de instructores y asignación de fichas. No se crea rol administrador ni interfaz administrativa del MVP. El mecanismo técnico y sus controles son propuestas para revisión.
- **Ficha pendiente:** no se han aprobado caracteres ni normalización de numero_ficha. P-01 del anexo propone una política explícita; no se aplica automáticamente DC-07 a ese campo ni se bloquean relaciones independientes.
- **Alcance autorizado:** especificación física inicial de identidad, fichas e importación, autorización, auditoría, idempotencia, procedimiento operativo y casos de prueba. Entregar para revisión antes de convertir en migración; sin ejecutar cambios ni crear recursos Supabase.
- **Pendientes conservados:** generaciones independientes repetidas, acceso histórico ante traslados/cambios de responsabilidad, autoridad y efectos de anulaciones y continuidad del seguimiento de compromisos corregidos. No se resuelven mediante restricciones implícitas.
- **Formatos:** se identificaron ejemplos diligenciados GOR-F-084 V02 y GD-F-011; no está confirmada su incorporación a Docs ni su vigencia institucional. Se requieren copias/instrucciones validadas para fidelidad documental, sin bloquear el núcleo independiente. No se inventan campos definitivos.

**Entregable vigente:** [TRAZA_E0_ESPECIFICACION_FISICA_INICIAL.md](TRAZA_E0_ESPECIFICACION_FISICA_INICIAL.md), v0.4 para revisión técnica, 06-11-2026; decisiones funcionales actualizadas en el registro final de esta fecha. FI-01–39 previstos, no ejecutados. Primera migración: [propuesta v0.1](TRAZA_E0_PRIMERA_MIGRACION_PROPUESTA.md), sin SQL.

DC-07 y DC-08 son resoluciones confirmadas; complementan DC-01–06 sin alterar el estado de sus pendientes. Revisar las propuestas P-01–08 antes de incorporar validadores o parámetros afectados a una migración.


### Propuesta técnica P-08 — revisión v0.2, 04-11-2026

El anexo físico §6.4 propone separar causa interna de duplicado externo y reporte visible restringido. El mensaje genérico no elimina todo riesgo de inferencia de existencia. Requiere confirmación de Luis Fernando Corredor Mora sobre su compatibilidad con CA-02.5/6/7; no se considera resolución DC ni modifica el PRD. Se mantienen las decisiones confirmadas y los pendientes anteriores. §12 del anexo registra contraste y soluciones técnicas todavía para revisión.


## Decisiones confirmadas y secuencia E0 — 06-11-2026

**Fuente:** aprobación expresa de Luis Fernando Corredor Mora. Este registro actualiza los pendientes históricos de 04/05-11-2026 solo en lo resuelto aquí; no cambia generaciones repetidas, traslados/acceso histórico, anulaciones ni continuidad de seguimiento de compromisos corregidos. DC-07/DC-08 permanecen confirmadas.

- **P-08 aprobada:** impedir duplicación y conservar causa exacta interna restringida. Ficha inexistente/no autorizada: número de fila y «No se pudo validar la ficha para esta fila», sin distinguir ambas ni buscar duplicados globales. Ficha autorizada y permiso vigente verificable sobre aprendiz existente: número y «Identificación ya registrada». Otros casos de duplicidad: número y «No fue posible incorporar esta fila», sin datos ajenos ni motivo de duplicidad. Aplicar en validación, confirmación, nuevas consultas, descarga, contadores y caché con permisos actuales. La ficha de entrada no acredita acceso al existente. Mensaje genérico reduce exposición, no elimina toda inferencia. Sin canal de revisión inventado; DC-08 no autoriza consultar otras fichas. PRD CA-02.5/6 ajustados; CA-02.7 conservado.
- **P-01/P-06 confirmadas:** identificación y ficha textuales de uno o más dígitos ASCII 0–9, con ceros preservados; retirar exclusivamente U+0020 exterior, rechazar vacío, espacios internos, tabs y otros caracteres. Misma normalización en catálogo y búsqueda de ficha en importación; también en identificación de autorregistro.
- **P-04 aprobada con ajuste:** agrupar filas válidas autorizadas por id normalizado; coincidencia de nombre y ficha según contrato: primera candidata y siguientes duplicadas internas. Diferencia de nombre o ficha: rechazar todas las filas del grupo conflictivo e indicar números de fila para corregir. Filas inválidas/ajenas se tratan aparte, no bloquean válidas ni exponen datos a través de agrupación. Otras identificaciones continúan. Distinto de P-08 frente a datos ya persistidos. La comparación concreta de nombre sigue como precisión técnica propuesta en §6.1 del anexo, no se deduce su aprobación.
- **P-05:** depuración productiva condicionada a política institucional; plazo pendiente. Desarrollo con datos sintéticos y plazos de ensayo explícitos, sin convertirlos en política productiva.
- **Primera migración:** alcance/secuencia confirmados, base técnica privada PostgreSQL; identidad, fichas, asociaciones e importación en incremento posterior. Diseño de objetos y permisos todavía para revisión; no se autoriza generar/ejecutar SQL ni crear recursos.

Referencias vigentes: [especificación física v0.4](TRAZA_E0_ESPECIFICACION_FISICA_INICIAL.md), para revisión técnica, FI-01–39 previstos; [primera migración propuesta v0.1](TRAZA_E0_PRIMERA_MIGRACION_PROPUESTA.md), M1-01–12 previstos. P-02/03/07, precisión de comparación de nombre, plazo productivo de P-05 y validaciones técnicas permanecen pendientes. No hay pruebas funcionales ejecutadas ni H0 cerrado.
