# TRAZA — Revisión cruzada documental

**Fecha:** 4 de noviembre de 2026  
**Alcance:** coherencia PRD → USER_FLOW → TRD; alcance, permisos, reglas, datos, integraciones, verificabilidad y preparación del PLAN.  
**Estado:** revisión documental completada con los tres documentos suministrados; ajustes documentales incorporados; decisiones funcionales y validaciones técnicas pendientes identificadas por entrega.  
**Intervención:** ajustes incorporados en PRD, USER_FLOW y TRD por solicitud del responsable. Resoluciones de diseño registradas en TRD §14.1; propuestas funcionales pendientes en el registro por entrega. No se ejecutaron pruebas de la aplicación.

## 1. Fuentes verificadas

| Documento | Archivo examinado | Identificación declarada | Procedencia y observación |
|---|---|---|---|
| PRD | `TRAZA_PRD(5).md` | v1.0; aprobado; 21-10-2026 | PRD vigente adjuntado por el responsable para completar la revisión. Se comprobó igualdad byte a byte con la copia utilizada provisionalmente; no hay diferencias de contenido. |
| USER_FLOW | `TRAZA_USER_FLOW(5).md` | Cabecera v1.0; aprobado; 22-10-2026 | Adjunto actual. El historial y el cierre indican v1.1. Se aplica v1.0 conforme a la indicación expresa del responsable. |
| TRD | `TRAZA_TRD.md` | v1.0 consolidada para revisión; actualización 30-10-2026 | Adjunto actual; estado en revisión, sin aprobación técnica final. |
| Segundo TRD | `TRAZA_TRD(1).md` | Igual al anterior | Adjunto actual. Comparación SHA-256: contenido idéntico; no constituye un tercer documento distinto. |

La incorporación del PRD vigente resuelve la limitación de fuentes del informe anterior. La comparación íntegra del archivo y la revisión de los apartados afectados ratifican los hallazgos H-RC-02 a H-RC-08. USER_FLOW y TRD conservan las mismas huellas de contenido verificadas inicialmente. La revisión documental no constituye aprobación del producto ni ejecución de pruebas.

## 2. Dictamen

Existe **cobertura documental de las nueve funcionalidades del MVP**: cada RF-01 a RF-09 tiene flujo funcional, requisitos técnicos y pruebas previstas. Se conservan las reglas centrales de acceso por rol y ficha, generación manual, firma por versión, integridad documental y reintentos seguros.

Esta cobertura es de **especificación**, no de ejecución ni de aceptación del producto. Las tablas agrupan varios criterios en escenarios generales: aún requieren desgloses y enlaces más precisos para convertirse en casos de prueba ejecutables.

Se puede preparar un **PLAN inicial con dependencias y decisiones explícitas**. Para fijar una línea base de implementación deben corregirse las inconsistencias documentales y resolverse las decisiones que afecten a cada entrega. No es necesario resolver parámetros operativos de todas las entregas antes de comenzar a planificar.

## 3. Hallazgos y acciones propuestas

Las prioridades indican el orden recomendado de atención. «Alta» bloquea el cierre de la revisión o la definición del comportamiento afectado; no implica detener todo el proyecto. Este apartado conserva el diagnóstico original. Las correcciones incorporadas y su cierre se registran en §12.

### H-RC-01. Falta del PRD en la entrega inicial — Resuelto

**Tipo / estado:** limitación de fuentes / Resuelta el 04-11-2026.  
**Antecedente:** la entrega inicial contenía dos TRD idénticos y un USER_FLOW. La revisión inicial usó un PRD anterior como referencia provisional.  
**Resolución:** el responsable suministró `TRAZA_PRD(5).md` como PRD vigente. Se verificó igualdad byte a byte con el PRD examinado provisionalmente, además de revisar la matriz §5.8, los criterios de corrección y el indicador IND-09.  
**Resultado:** se ratifica el contraste documental previo; permanecen abiertos H-RC-02 a H-RC-08. Se conserva este ID para mantener el historial de la revisión.

### H-RC-02. Identificación de versión inconsistente en USER_FLOW

**Tipo / prioridad:** inconsistencia documental / Media.  
**Ubicación:** USER_FLOW cabecera, §18.4 y cierre; TRD observaciones iniciales.  
**Evidencia:** la cabecera declara v1.0, pero el registro de actualización y el cierre declaran v1.1. El TRD ya advierte esta diferencia.  
**Acción:** unificar en v1.0, conforme a la decisión del responsable, conservando la descripción de los ajustes del historial. Actualizar la advertencia del TRD una vez corregida la fuente.  
**Cierre verificable:** cabecera, historial, cierre y referencias cruzadas identifican la misma versión.

### H-RC-03. Matriz del PRD con columnas desalineadas

**Tipo / prioridad:** defecto estructural de trazabilidad / Media.  
**Ubicación:** PRD §5.8; líneas 440, 441, 442 y 444 de la copia examinada.  
**Evidencia:** la cabecera tiene dos columnas; las filas MVP-02, MVP-03 y MVP-06 tienen tres, y MVP-04 tiene cuatro.  
**Consecuencia:** el nombre de la funcionalidad puede ocupar la celda destinada a los RF, dificultando la lectura y el procesamiento automático.  
**Acción:** mantener dos columnas: «Funcionalidad del MVP» y «Requisitos funcionales relacionados». Unir código y nombre en la primera; ubicar todos los RF relacionados en la segunda. Reubicar la explicación adicional de MVP-04 fuera de la tabla o en una columna aplicada a todas las filas. Conservar las relaciones transversales con firma e historial.  
**Cierre verificable:** todas las filas tienen dos celdas y los RF corresponden al contenido de §§5.2 y 7. No basta con eliminar celdas sobrantes.

### H-RC-04. El diagrama de correo no representa todas las alternativas aprobadas

**Tipo / prioridad:** discrepancia entre diagrama y reglas escritas / Alta para RF-07.  
**Ubicación:** USER_FLOW §7.7, diagrama; contrastar con PRD CA-06.8 y CA-07.10, alternativas del propio USER_FLOW §7.7 y TRD §§4.3, 6.2 y 7.5.  
**Evidencia:** el único recorrido del diagrama hacia «Generar Formato de comunicación» pasa por «Dirección válida» y «Guardar configuración». El texto permite generar y conservar el documento sin destinatario válido, registrando el envío no completado. Además, la decisión binaria «¿Envío confirmado por el servicio?» dirige todo «No» a fallo, aunque un resultado incierto requiere verificación antes de reenviar.  
**Acción:** representar la generación y conservación documental como antecedente del despacho. Después, distinguir destinatario ausente/inválido, intento confirmado, fallo confirmado y resultado incierto. Mantener inicio automático sin confirmación adicional. Incorporar expresamente que, tras corregir la dirección, el reintento usa la vigente y conserva el destinatario de cada intento, como exige CA-07.11.  
**Cierre verificable:** el recorrido permite conservar el documento cuando falta configuración; la incertidumbre conduce a conciliación, y el reintento utiliza el mismo documento y la dirección vigente.

### H-RC-05. Fórmula de disponibilidad con agrupación ambigua

**Tipo / prioridad:** defecto de especificación de indicador / Media.  
**Ubicación:** PRD §9, IND-09.  
**Evidencia:** la expresión escrita permite interpretar que solo el tiempo de indisponibilidad se divide entre el tiempo programado, en lugar de dividir toda la diferencia.  
**Acción propuesta:**

`Disponibilidad (%) = ((Tiempo programado de operación − Tiempo de indisponibilidad atribuible al sistema) / Tiempo programado de operación) × 100`

**Comprobación ilustrativa:** para 100 horas programadas y 1 hora de indisponibilidad, el resultado debe ser 99 %. Si el denominador es cero, aplicar la regla «no calculable» de §9.2.  
**Límite:** corregir la fórmula no aprueba la meta propuesta de 99 % ni resuelve la ventana y atribución de incidentes; RNFT-006 y DT-010 continúan pendientes.

### H-RC-06. Trazabilidad de pruebas todavía incompleta a nivel de escenario

**Tipo / prioridad:** brecha de verificabilidad documental / Media.  
**Ubicación:** USER_FLOW §§14–15; TRD §§12.3, 12.6 y 13.  
**Evidencia:** existen 39 PF y 21 TEST, pero no una correspondencia explícita y completa PF → TEST. En la matriz del USER_FLOW no aparecen PF-05/PF-06 —acceso por ficha—, PF-26 —abandono— ni PF-28 —historial vacío—, aunque sí están definidos en §14. Las matrices RF → pruebas principales no permiten por sí solas comprobar cada CA.  
**Acción:** agregar los vínculos omitidos en USER_FLOW y completar un registro RF/CA → PF → RT/RNFT → TEST. Desglosar recuperación de contraseña, identificación ya vinculada, cambio de destinatario, firma ajena y falta de asociación a ficha como variantes comprobables.  
**Cierre verificable:** todos los PF tienen destino de verificación, y cada CA obligatorio tiene resultado esperado identificable o bloqueo justificado. La propuesta de §5 facilita este cierre; no acredita pruebas ejecutadas.

### H-RC-07. Resumen de pendientes tecnológicos sin sincronización completa

**Tipo / prioridad:** deuda editorial del TRD / Baja.  
**Ubicación:** TRD §2.3 frente a §4.4 y DT-001/002/003/004/010.  
**Evidencia:** §2.3 sigue listando tecnologías, proveedor de autenticación, servicios de almacenamiento y alojamiento como pendientes genéricos. §4 ya concreta la propuesta Flutter Web/Dart, Supabase, PostgreSQL y Firebase Hosting.  
**Acción:** remitir §2.3 a la base propuesta en §4 y conservar como pendientes versiones, configuración, políticas, límites, validaciones y aprobación que correspondan.  
**Cierre verificable:** los apartados distinguen de forma uniforme propuesta tecnológica, decisión de selección y aceptación mediante pruebas. No se elimina un pendiente real por actualizar la redacción.

### H-RC-08. Conviene precisar en el PRD la corrección de documentos guardados sin firma

**Tipo / prioridad:** precisión entre documentos / Media para correcciones.  
**Ubicación:** PRD §6.3, CA-03.11, CA-04.9 y RNT-05; USER_FLOW §§7.3, 8.1 y 9.4; TRD RT-019 y §6.4.  
**Evidencia:** el PRD permite corregir antes de firma y exige trazabilidad, pero no expresa en esos puntos con la misma precisión que todo documento ya guardado se corrige mediante versión o correctivo. USER_FLOW y TRD sí lo exigen incluso cuando aún no tiene firma.  
**Evaluación:** no es una contradicción demostrada: versionar satisface la trazabilidad del PRD. Es una precisión importante para evitar que una IA implemente un UPDATE destructivo antes de firma.  
**Acción:** explicitar en el PRD la distinción «antes de guardar: edición/cancelación; después de guardar: versión o correctivo vinculado», conservando la identidad del llamado y su conteo.  
**Cierre verificable:** original, corrección y eventual firma se pueden relacionar sin sobrescritura ni incremento del conteo por corrección.

## 4. Cobertura de los requisitos funcionales

«Cubierto» significa que se encontraron especificaciones y pruebas previstas. No significa implementación terminada, aceptación o resolución de todas sus dependencias.

| PRD | USER_FLOW | TRD | Pruebas técnicas previstas | Evaluación |
|---|---|---|---|---|
| RF-01: autenticación y acceso | §7.1; UI-01–04; §§6.1, 11 y 13 | RT-001–005; §§7.2 y 8 | TEST-001–003 | Cubierto; concretar sesiones, provisión operativa y recuperación. |
| RF-02: importación y consulta | §7.2; UI-05–07 | RT-006/007 y RT-005; §§5–7 | TEST-003/004 | Cubierto; falta cerrar ámbito de importación y contrato CSV/JSON. |
| RF-03: llamados y conteo | §7.3; UI-08–10; §8.1 | RT-008–010/019/020 | TEST-005/006/010/012 | Cubierto; explicitar correcciones y decisiones de anulación. |
| RF-04: planes | §7.4; UI-11/12; §8.2 | RT-010/011/019; §§5 y 10.5 | TEST-006/007/010 | Cubierto; formatos y escenarios de generación omitida/repetida pendientes. |
| RF-05: seguimiento | §7.5; UI-12; §8.4 | RT-012; §§5.1, 5.6 y 8.2 | TEST-003/007 | Cubierto; mantiene seguimiento interno y compromisos sin estados formales. |
| RF-06: comunicación | §7.6; UI-15 | RT-013; §§4.3, 6.2 y 10.5 | TEST-006/008/021 | Cubierto; requiere plantilla/renderizado y coordinación con correo. |
| RF-07: correo | §7.7; UI-16/17; §8.5 | RT-014/015/020; §§6.6 y 7.4–7.5 | TEST-008/012/021 | Cubierto con corrección gráfica H-RC-04; proveedor y ámbito pendientes. |
| RF-08: firma y observación | §7.8; UI-13/14; §§8.3 y 9 | RT-016–018; §§5.4 y 10.6 | TEST-009–011 | Cubierto; validación táctil e integración reales pendientes. |
| RF-09: historial | §7.9; UI-08 y detalles | RT-019/022; §§5 y 10 | TEST-010/014/019/020 | Cubierto; incluye llamados posteriores al cuarto y límites por rol. |

Se verificaron referencias literales CA del TRD contra los identificadores presentes en el PRD examinado: no se encontraron identificadores CA literales inexistentes. Esta comprobación no demuestra por sí sola que cada rango o criterio esté completamente cubierto por una prueba detallada.

## 5. Correspondencia propuesta PF → TEST

Este registro completa el enlace de diseño pendiente. Las pruebas agrupadas deberán desglosarse antes de ejecutarse. Los enlaces se proponen por equivalencia de escenario, no se encontraron todos escritos en las fuentes.

| PF del USER_FLOW | TEST del TRD propuesto | Precisión requerida |
|---|---|---|
| PF-01, PF-02 | TEST-001 | Cuenta habilitada/no habilitada y credenciales. |
| PF-03, PF-04 | TEST-002 | Agregar identificación/cuenta ya vinculada y concurrencia. |
| PF-05, PF-06 | TEST-003 | Incluir ficha ajena y ausencia total de asociación. Vincular a RF-01 en USER_FLOW §15. |
| PF-07, PF-08 | TEST-004 | CSV y JSON, prevalidación, éxito parcial, duplicados y ausencia de creación de cuentas. |
| PF-09, PF-10, PF-11 | TEST-005; TEST-010 para versión/firma concurrentes | Corrección guardada sin firma y conteo continuo. |
| PF-12, PF-13 | TEST-006 | Umbrales y cancelación; escenarios omitidos/repetidos dependen de DT-014. |
| PF-14 | TEST-006/007 | Formato institucional, varios compromisos y asociaciones. |
| PF-15, PF-38 | TEST-007 | Actuaciones acumuladas sin estados formales. |
| PF-16 | TEST-003/007 | Probar también solicitudes directas y archivos internos. |
| PF-17, PF-18 | TEST-009 | Firma táctil, rehacer trazo, confirmación, almacenamiento y versión exacta. |
| PF-19 | TEST-010 | Intentos de alterar o eliminar la versión firmada. |
| PF-20 | TEST-011 | Condición de aprendiz informado, datos mínimos y ausencia distinta de aceptación. |
| PF-21 | TEST-006/008/021 | Generación manual, conservación y primer intento automático. |
| PF-22, PF-23, PF-24 | TEST-008/021 | Adjuntar documento exacto, no afirmar lectura, conservar intentos y usar dirección vigente. |
| PF-25 | TEST-012/021; TEST-009 para fallo de firma | Distinguir fallo de incertidumbre y consultar antes de repetir. |
| PF-26, PF-36 | TEST-013 | Regresar o descartar, sin borrador persistente. PF-26 requiere vínculo en USER_FLOW §15. |
| PF-27 | TEST-001/003 | Cierre, navegación atrás y solicitud directa. |
| PF-28 | TEST-014, ampliar expresamente | Historial vacío distinto de error; agregar vínculo a RF-09 en USER_FLOW §15. |
| PF-29 | TEST-003 | Rutas y recursos protegidos, sin exposición de datos. |
| PF-30 | TEST-014 | Quinto y posteriores se conservan; sin nuevas opciones inferidas. |
| PF-31 | TEST-013 | Cancelar antes de guardar no crea llamado ni documento. |
| PF-32 | TEST-005/010 | Conservar original y vínculo; no aumentar conteo. |
| PF-33 | TEST-020 | Bloqueada por DP-05 hasta definir autorización y efecto. |
| PF-34 | TEST-010 | Firma permanece en original; nueva aceptación explícita según decisión aplicable. |
| PF-35 | TEST-012/020 | Corrección incierta verificable; variante de anulación bloqueada por DP-05. |
| PF-37 | TEST-014 | Consulta por historial sin depender del formulario original. |
| PF-39 | TEST-012 | Reintento de intención ya confirmada y control de entrada diferente. |

PF-26 y PF-36 se solapan; PF-10/PF-32 y PF-25/PF-35/PF-39 también comparten comportamientos. Mantener sus IDs y diferenciar el alcance evita perder referencias históricas. No es necesario renumerarlos para cerrar esta revisión.

## 6. Requisitos no funcionales y principios

| PRD | TRD | Evidencia prevista | Resultado documental |
|---|---|---|---|
| RNF-01 | RNFT-001/002; DT-009 | TEST-015 | Alineado: 2 s/95 % permanece propuesto; carga y operaciones especiales pendientes. |
| RNF-02 | RNFT-003/004; DT-004/011/013 | TEST-001/003/019 | Alineado: autorización por recurso, privacidad y secretos; sesiones/conservación por concretar. |
| RNF-03 | RNFT-005 | TEST-009/010/019 | Alineado: original, versiones, firma y auditoría. |
| RNF-04 | RNFT-006/007; DT-010/011 | TEST-016 | Alineado: respaldo debe recuperar datos y objetos, no solo base de datos. |
| RNF-05 | RNFT-008/009; DT-015 | TEST-017 | Alineado: dispositivos, navegadores y criterios pendientes. |
| RNF-06 | RNFT-010; DT-005/008 | TEST-008/012/021 | Alineado: resultado incierto, idempotencia y documento conservado ante fallo de correo. |
| RNF-07 | RNFT-011; DT-012 | TEST-018 | Alineado: versiones, documentación, revisión y pruebas reproducibles. |
| Necesidades transversales RNF-03/04/06 | RNFT-012; DT-016 | TEST-019 | Observabilidad derivada e identificada; no incorpora reportes funcionales nuevos. |

SOLID se especifica como principio en TRD §2.4 y con aplicación de diseño en §4.1. La arquitectura propuesta es modular por capas sobre servicios administrados; MVVM se limita a presentación Flutter. Repository, Adapter, inyección de dependencias y outbox están identificados como propuestas. No se encontró que MVC se exija como arquitectura global.

## 7. Pendientes existentes que debe recoger el PLAN

Estos puntos ya figuran en el TRD o en el USER_FLOW. **No se presentan como nuevos defectos ni se consideran resueltos por esta revisión.**

| Tema | Referencia | Definición o evidencia requerida | Momento de resolución |
|---|---|---|---|
| Importación por ámbito | H-TRD-01 / DT-014 | Precisar si un instructor puede incorporar filas de fichas no asociadas y qué información recibe ante duplicados ajenos. | Antes del contrato definitivo de importación por ficha. |
| Configuración de correo | H-TRD-02 / DT-014 | Determinar si es global, por ficha o por responsable y cómo resolver cambios concurrentes. | Antes del modelo y envío productivo de comunicaciones. |
| Cambios de ficha | H-TRD-03 / DT-014 | Definir acceso a antecedentes y conteo al cambiar ficha o responsabilidad. | Antes de implementar traslados; no bloquea una importación inicial sin cambios. |
| Opciones omitidas y generaciones repetidas | H-TRD-04 / DT-014 | Determinar si Plan 1 continúa disponible tras el tercer llamado y si se admite más de un documento del mismo nivel. No imponer prerrequisitos entre planes por inferencia. | Antes de cerrar disponibilidad y restricciones de generación. |
| Anulaciones | DP-05; TEST-020 | Autoridad, efecto sobre conteo/disponibilidad y documentos ya emitidos. | Antes de habilitar anulación y pruebas dependientes. |
| Identidad y sesiones | DP-07 / DT-004 | Provisión de Instructor, asociación operativa, recuperación, expiración, almacenamiento y revocación; fallo parcial cuenta/vínculo. | Antes de aceptar RF-01 y controles de sesión. |
| Plantillas y firmas | DT-006/007 | Copias institucionales vigentes, campos, renderizador, evidencia de firma y tratamiento de compromisos corregidos. | Antes de aceptar documentos, firmas y correcciones. |
| Firma táctil y accesibilidad | DP-06 / DT-002/007/015 | Cerrar incidencia táctil indicada en TRD §4.4 con dispositivos objetivo; verificar lectura, captura, persistencia y servicios de prueba reales. | Prueba técnica temprana; aceptación antes de liberar el componente. |
| Correo durable | DT-005/008 | Proveedor, límites, despacho/recuperación, conciliación de resultado incierto y retención idempotente. | Antes de aceptar RF-07. |
| Capacidad y continuidad | DT-009/010/011 | Carga, tiempos, disponibilidad, entornos, respaldo completo, RPO/RTO y conservación. | Según dependencia de diseño y antes de la aceptación operativa afectada. |
| Pruebas y observabilidad | DT-012/013/016 | Herramientas, contratos físicos, límites, catálogo de eventos y alertas. | Antes de la entrega que requiera esas verificaciones. |

La selección tecnológica se distingue de la aceptación de su implementación. Se puede fijar Flutter/Supabase/PostgreSQL/Firebase como base de diseño por decisión del responsable y mantener pendientes versiones, políticas y pruebas. No se debe exigir que el producto esté construido para documentar una selección tecnológica; tampoco presentarla como prueba de funcionamiento.

DP-01, DP-03, DP-04 y el comportamiento de DP-10 permanecen resueltos según las fuentes: sin estados formales de compromisos, sin autoguardado/borradores, advertencia de abandono y comprobación antes de repetir operaciones inciertas. DP-02 y DP-09 no bloquean el MVP actual: un flujo nuevo de negativa y nuevas actuaciones posteriores al cuarto requieren cambio aprobado.

## 8. Reglas que deben conservarse al corregir

- Solo dos roles funcionales del MVP: Instructor y Aprendiz. La operación de infraestructura no crea un tercer rol de interfaz.
- Cuenta del aprendiz vinculada a identificación importada; identificación textual, sin pérdida de ceros; importación no crea cuentas.
- Acceso Instructor por ficha asociada; Aprendiz solo a documentos propios autorizados. Seguimientos internos y sus evidencias no se exponen al Aprendiz.
- Conteo continuo por identidad de llamado, sin límite temporal; una versión correctiva no es otro llamado.
- Los umbrales 2/3/4 habilitan decisiones manuales. Generar comunicación inicia correo automáticamente; no agregar una confirmación de envío.
- Falta de destinatario o fallo del correo no elimina la comunicación. Reintentos conservan documento e historial; aceptación del proveedor no prueba recepción o lectura.
- Firma manuscrita con lectura previa, repetición del trazo y confirmación expresa; vínculo exacto y guardado confirmado. Ausencia de firma no equivale a aceptación.
- Guardado explícito, sin autoguardado ni borradores persistentes; comprobación de operaciones inciertas.
- Llamados posteriores al cuarto se conservan y consultan. No inferir nuevas opciones ni generación automática.
- IA, biometría, app nativa independiente e integraciones no aprobadas permanecen fuera del MVP.

## 9. Secuencia recomendada hacia el PLAN

1. Con el PRD vigente ya incorporado, corregir H-RC-02 a H-RC-05. Sincronizar los apartados editoriales y la precisión de correcciones.
2. Incorporar la correspondencia de pruebas de §5 y desglosar los CA de la primera entrega. Mantener identificadores existentes.
3. Resolver las reglas funcionales que cambian contratos o permisos: DT-014 y las dependencias de la entrega elegida. Mantener anulación bloqueada si DP-05 sigue abierto.
4. Registrar selección de base técnica y separar decisiones, validaciones y aceptación. Programar al inicio las pruebas de mayor incertidumbre: firma táctil, documento institucional y correo durable.
5. Estructurar entregas por capacidades: base técnica/acceso; importación; llamados/historial; planes/seguimiento; firma/correcciones; comunicación/correo; verificación operativa y piloto. Dependencias compartidas, como integridad e idempotencia, se implementan desde las primeras escrituras.
6. Para cada entrega, consignar RF/CA, RT/RNFT, PF/TEST, tareas, dependencias, evidencia esperada y criterio de finalización. Los pendientes llevan responsable e hito; no se convierten en supuestos aprobados.

## 10. Evidencia de identificación

| Archivo | SHA-256 |
|---|---|
| `TRAZA_PRD(5).md` | `228f4a39092d4b6ad2eaa23f59604cd33834a8c7efd93bb056d486703d16596d` |
| `TRAZA_USER_FLOW(5).md` | `2ad0a00e000d114046817dd690fc7587d58854a6d190573e63db13875992eeed` |
| `TRAZA_TRD.md` y `TRAZA_TRD(1).md` | `500af562ba7f64130b220c3a3219c482ed4c04852807bce3af5ea590b4af3b43` |

Control de identificadores: 9 RF y 7 RNF del PRD; 17 UI y 39 PF del USER_FLOW; 22 RT, 12 RNFT, 21 TEST y 16 DT del TRD. Son conteos de identificación, no porcentajes de cumplimiento. Los defectos estructurales de tabla detectados corresponden al PRD §5.8; no se detectaron diferencias de cantidad de columnas en las tablas de USER_FLOW y TRD con el control aplicado.

## 11. Actualización de la revisión

El 04-11-2026 se recibió el PRD vigente, se comprobó su coincidencia íntegra con la referencia provisional y se cerró H-RC-01. Se mantienen siete hallazgos abiertos, la matriz de cobertura y los pendientes funcionales/técnicos. Se actualizó exclusivamente este informe; las correcciones propuestas siguen pendientes de incorporación en los documentos fuente.

## 12. Incorporación de ajustes — 04-11-2026

Se incorporaron H-RC-02 a H-RC-08 en PRD, USER_FLOW y TRD: versión unificada, tabla §5.8, flujo de correo con incertidumbre, fórmula IND-09, enlaces PF/TEST y registro de 101 CA, sincronización del resumen tecnológico y precisión de correcciones posteriores al guardado. Se cierran estos hallazgos en su alcance documental; el detalle de ejecución y las evidencias de pruebas se desarrollarán por entrega.

Se agregó `DECISIONES_POR_ENTREGA_TRAZA.md`: contiene resoluciones técnicas acotadas y propuestas DC-01 a DC-06 para decisiones funcionales pendientes. Las propuestas no equivalen a aprobación institucional. Las descripciones anteriores se conservan como historial del hallazgo, no como estado posterior a este cierre. Las huellas de §10 identifican las fuentes anteriores a los ajustes.


## Registro complementario confirmado — 04-11-2026 (DC-07/DC-08)

**Fuente:** instrucción expresa de Luis Fernando Corredor Mora en la revisión de E0. Se conserva la versión documental existente; este registro actualiza únicamente las decisiones indicadas y no aprueba las propuestas físicas del nuevo anexo.

- **DC-07, confirmada:** identificación del aprendiz como texto, con ceros iniciales; retirar espacios exteriores antes de validar; exigir uno o más dígitos ASCII 0–9. Rechazar vacío, espacios internos, letras, puntos, guiones y otros caracteres; no convertir a número ni limpiar caracteres inválidos silenciosamente. Error localizado por fila. ` 00123456 ` se acepta como `00123456`; `0012 3456`, `1.234.567` y solo espacios se rechazan. Aplicar la misma regla al dato de identificación utilizado en autorregistro. El conjunto exacto de espacios exteriores se precisa como propuesta P-06 del anexo, sin ampliarlo silenciosamente.
- **DC-08, confirmada:** Luis Fernando Corredor Mora asume inicialmente la habilitación de instructores y asignación de fichas. No se crea rol administrador ni interfaz administrativa del MVP. El mecanismo técnico y sus controles son propuestas para revisión.
- **Ficha pendiente:** no se han aprobado caracteres ni normalización de numero_ficha. P-01 del anexo propone una política explícita; no se aplica automáticamente DC-07 a ese campo ni se bloquean relaciones independientes.
- **Alcance autorizado:** especificación física inicial de identidad, fichas e importación, autorización, auditoría, idempotencia, procedimiento operativo y casos de prueba. Entregar para revisión antes de convertir en migración; sin ejecutar cambios ni crear recursos Supabase.
- **Pendientes conservados:** generaciones independientes repetidas, acceso histórico ante traslados/cambios de responsabilidad, autoridad y efectos de anulaciones y continuidad del seguimiento de compromisos corregidos. No se resuelven mediante restricciones implícitas.
- **Formatos:** se identificaron ejemplos diligenciados GOR-F-084 V02 y GD-F-011; no está confirmada su incorporación a Docs ni su vigencia institucional. Se requieren copias/instrucciones validadas para fidelidad documental, sin bloquear el núcleo independiente. No se inventan campos definitivos.

**Entregable vigente:** [TRAZA_E0_ESPECIFICACION_FISICA_INICIAL.md](TRAZA_E0_ESPECIFICACION_FISICA_INICIAL.md), v0.4 para revisión técnica, 06-11-2026; decisiones funcionales actualizadas en el registro final de esta fecha. FI-01–39 previstos, no ejecutados. Primera migración: [propuesta v0.1](TRAZA_E0_PRIMERA_MIGRACION_PROPUESTA.md), sin SQL.

Actualización posterior al cierre de §12: los dos registros complementarios están presentes en Docs; PLAN referencia los nombres actuales y TRD v1.0 aprobado. Las referencias con (5), las huellas y los estados iniciales del informe son antecedentes históricos. La revisión física inicial sigue abierta: falta aceptar contratos y propuestas del anexo; no hay pruebas de aplicación ejecutadas.


### Revisión documental del anexo físico v0.2 — 04-11-2026

Se contrastaron cinco hallazgos con v0.1 antes de modificar; todos aplican, tres parcialmente cubiertos y dos con vacíos explícitos. El detalle consta en §12 del anexo: recuperación sin cuenta, habilitación aprendiz, concesión vencida, depuración y duplicados externos. P-08 queda pendiente de confirmación; no se altera la aceptación del PRD. FI-25–35 amplían la verificación prevista; ninguna prueba funcional se ejecutó. Esta actualización no cierra H0 ni valida una migración.


## Decisiones confirmadas y secuencia E0 — 06-11-2026

**Fuente:** aprobación expresa de Luis Fernando Corredor Mora. Este registro actualiza los pendientes históricos de 04/05-11-2026 solo en lo resuelto aquí; no cambia generaciones repetidas, traslados/acceso histórico, anulaciones ni continuidad de seguimiento de compromisos corregidos. DC-07/DC-08 permanecen confirmadas.

- **P-08 aprobada:** impedir duplicación y conservar causa exacta interna restringida. Ficha inexistente/no autorizada: número de fila y «No se pudo validar la ficha para esta fila», sin distinguir ambas ni buscar duplicados globales. Ficha autorizada y permiso vigente verificable sobre aprendiz existente: número y «Identificación ya registrada». Otros casos de duplicidad: número y «No fue posible incorporar esta fila», sin datos ajenos ni motivo de duplicidad. Aplicar en validación, confirmación, nuevas consultas, descarga, contadores y caché con permisos actuales. La ficha de entrada no acredita acceso al existente. Mensaje genérico reduce exposición, no elimina toda inferencia. Sin canal de revisión inventado; DC-08 no autoriza consultar otras fichas. PRD CA-02.5/6 ajustados; CA-02.7 conservado.
- **P-01/P-06 confirmadas:** identificación y ficha textuales de uno o más dígitos ASCII 0–9, con ceros preservados; retirar exclusivamente U+0020 exterior, rechazar vacío, espacios internos, tabs y otros caracteres. Misma normalización en catálogo y búsqueda de ficha en importación; también en identificación de autorregistro.
- **P-04 aprobada con ajuste:** agrupar filas válidas autorizadas por id normalizado; coincidencia de nombre y ficha según contrato: primera candidata y siguientes duplicadas internas. Diferencia de nombre o ficha: rechazar todas las filas del grupo conflictivo e indicar números de fila para corregir. Filas inválidas/ajenas se tratan aparte, no bloquean válidas ni exponen datos a través de agrupación. Otras identificaciones continúan. Distinto de P-08 frente a datos ya persistidos. La comparación concreta de nombre sigue como precisión técnica propuesta en §6.1 del anexo, no se deduce su aprobación.
- **P-05:** depuración productiva condicionada a política institucional; plazo pendiente. Desarrollo con datos sintéticos y plazos de ensayo explícitos, sin convertirlos en política productiva.
- **Primera migración:** alcance/secuencia confirmados, base técnica privada PostgreSQL; identidad, fichas, asociaciones e importación en incremento posterior. Diseño de objetos y permisos todavía para revisión; no se autoriza generar/ejecutar SQL ni crear recursos.

Referencias vigentes: [especificación física v0.4](TRAZA_E0_ESPECIFICACION_FISICA_INICIAL.md), para revisión técnica, FI-01–39 previstos; [primera migración propuesta v0.1](TRAZA_E0_PRIMERA_MIGRACION_PROPUESTA.md), M1-01–12 previstos. P-02/03/07, precisión de comparación de nombre, plazo productivo de P-05 y validaciones técnicas permanecen pendientes. No hay pruebas funcionales ejecutadas ni H0 cerrado.
