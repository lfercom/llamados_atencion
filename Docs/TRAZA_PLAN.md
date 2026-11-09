# TRAZA

## PLAN — Plan de implementación y verificación

**Producto:** Sistema Integral de Gestión de Llamados de Atención y Seguimiento Académico  
**Nombre corto:** TRAZA  
**Versión del documento:** 1.0  
**Estado:** Aprobado        
**Fecha de elaboración:** 04-11-2026  
**Método de trabajo:** Spec Driven AI Development  
**Responsables de ejecución:** Por asignar. Las responsabilidades de este documento corresponden a perfiles, no a personas confirmadas.

## 1. Propósito y referencias

Este PLAN organiza la implementación del MVP en entregas verificables. Relaciona las tareas con los requisitos, los flujos, las decisiones técnicas y las pruebas; establece dependencias y condiciones de inicio y cierre. No sustituye las especificaciones ni autoriza comportamientos pendientes.

El PRD define el alcance y las reglas del producto; el USER_FLOW desarrolla la navegación e interacción; el TRD especifica su implementación; este PLAN organiza la construcción y la obtención de evidencia. Las discrepancias deben resolverse antes de implementar el comportamiento afectado.

### 1.1. Línea base documental

| Documento | Versión y referencia | Uso en el PLAN |
|---|---|---|
| PRD TRAZA — archivo `TRAZA_PRD.md` | v1.0, 21-10-2026; ajustes confirmados el 04-11-2026 | RF-01–09, RNF-01–07, alcance, reglas y criterios CA. |
| USER_FLOW TRAZA — archivo `TRAZA_USER_FLOW.md` | v1.0, 22-10-2026; ajustes confirmados el 04-11-2026 | Pantallas UI, navegación, interacciones y escenarios PF. |
| TRD TRAZA — archivo `TRAZA_TRD.md` | v1.0, elaborada el 28-10-2026 y consolidada el 29-10-2026; actualización y resoluciones del 04-11-2026; estado: Aprobado | RT-001–022, RNFT-001–012, arquitectura, contratos, pruebas TEST y decisiones DT/DP. |
| `DECISIONES_POR_ENTREGA_TRAZA.md` | Registro del 04-11-2026 | Resoluciones DC-01–03 y dependencias pendientes por entrega. |
| `REVISION_CRUZADA_TRAZA_2026-11-04.md` | Informe actualizado el 04-11-2026 | Antecedentes de revisión y cierre documental de hallazgos. |

El TRD v1.0 está aprobado como referencia técnica. Esta aprobación documental mantiene los pendientes DT/DP y sus condiciones de resolución; no acredita su cierre ni la aceptación técnica del producto. Las resoluciones expresas del TRD §14.1 actualizan los estados históricos de propuesta únicamente para los elementos allí resueltos. La selección de una tecnología para diseño no equivale a implementación ni aceptación técnica. Los números entre paréntesis de los nombres de archivo no constituyen versiones del producto.

### 1.2. Estado real al elaborar el plan

Los documentos permiten organizar e iniciar trabajo sobre requisitos definidos. No se acredita aquí que el MVP esté implementado ni que las pruebas del TRD estén ejecutadas. La matriz del TRD §13.3 vincula 101 criterios CA con familias de prueba: esa trazabilidad documental debe convertirse en casos ejecutables y evidencia.

La prueba de concepto previa no valida la integración productiva con Supabase ni la firma en dispositivos reales. La incidencia de captura táctil continúa abierta. Este PLAN no fija fechas, duración, presupuesto, versiones de herramientas o personas sin información suficiente; esas asignaciones se realizarán al preparar cada entrega.

## 2. Alcance y decisiones que deben preservarse

### 2.1. Base técnica seleccionada

| Componente | Selección para diseño | Trabajo pendiente |
|---|---|---|
| Frontend | Flutter Web + Dart, adaptable a escritorio y celular | Versiones reproducibles, navegación, gestión de estado y verificación táctil/accesibilidad. |
| Backend | Supabase Edge Functions con TypeScript y funciones SQL de PostgreSQL | Contratos físicos, autorización, coordinación de servicios y pruebas transaccionales. |
| BaaS | Supabase Auth y almacenamiento privado, además de servicios de backend | Proyectos, permisos, configuración, límites y operación. |
| SGBD | PostgreSQL | Migraciones, restricciones, índices, políticas y restauración. |
| Alojamiento web | Firebase Hosting | Publicación de archivos compilados, HTTPS, configuración por ambiente y reversión. |
| Arquitectura y patrones | Arquitectura modular por capas; MVVM en presentación; Repository, Adapter e inyección de dependencias | Verificar separación y SOLID; no incorporar patrones sin una necesidad concreta. |

Firebase Hosting sirve los recursos públicos de la aplicación; los documentos de los aprendices permanecen en almacenamiento privado. No se incorpora una segunda autenticación. El backend debe autorizar cada operación; los privilegios de servicio no sustituyen esa comprobación.

### 2.2. Reglas confirmadas y límites

1. Solo existen los roles de producto Instructor y Aprendiz. La provisión operativa no agrega un rol administrativo ni una pantalla de administración al MVP.
2. Solo se importan aprendices de fichas previamente asociadas al Instructor. Se valida cada fila en revisión y confirmación; se aceptan filas válidas autorizadas y se rechazan las demás sin revelar información ajena. La importación no crea cuentas ni permisos.
3. Las direcciones institucionales disponibles no están vinculadas a fichas. El Instructor selecciona el destinatario antes de confirmar la generación de la comunicación; el documento conservado inicia automáticamente el envío, sin otra confirmación. La falta de destinatario válido no elimina el documento. Cada intento conserva la dirección utilizada.
4. El conteo por aprendiz es continuo, sin reinicio temporal. Plan 1 queda disponible desde dos llamados, Plan 2 desde tres y comunicación desde cuatro; las opciones omitidas permanecen disponibles. La generación es manual y voluntaria. Un quinto llamado se registra y consulta sin originar un nuevo tipo documental.
5. La cantidad de documentos independientes permitidos de un mismo tipo sigue pendiente. No se impone unicidad por aprendiz/tipo ni se autoriza repetición por inferencia. Esto es distinto de evitar duplicados de una misma operación mediante idempotencia.
6. Todo documento guardado conserva su original; las correcciones generan versiones vinculadas, incluso antes de la firma. Una corrección no agrega un llamado. La firma pertenece a la versión exacta revisada y no se traslada.
7. Los planes admiten varios compromisos. Su seguimiento interno corresponde al Instructor; no existen estados formales de compromiso ni determinación automática de incumplimiento.
8. El guardado es explícito, con advertencia de cambios sin guardar y consulta de resultados inciertos. No se incorporan autoguardado, borradores persistentes ni recuperación garantizada de información no guardada.
9. Quedan fuera las funciones excluidas por el PRD, incluidas IA, biometría, aplicaciones nativas, integraciones institucionales no aprobadas, mensajería adicional y decisiones disciplinarias automáticas.

## 3. Organización del trabajo y dependencias

### 3.1. Responsabilidades propuestas

| Perfil | Responsabilidad |
|---|---|
| Responsable del producto / institución | Aclarar reglas pendientes, aportar formatos oficiales, aprobar criterios operativos y aceptar entregas. |
| Responsable técnico | Mantener arquitectura, contratos, decisiones, seguridad de diseño y revisión de código. |
| Desarrollo | Implementar interfaz, servicios, datos y automatización conforme a especificaciones. |
| Calidad | Preparar y ejecutar casos por CA/PF, registrar evidencia y comprobar regresiones. |
| Seguridad y operación | Revisar permisos, secretos, privacidad, ambientes, respaldos, monitoreo y recuperación. |

Una persona puede asumir varios perfiles. Antes de ejecutar una entrega se registrarán los nombres y su disponibilidad. La generación de código asistida por IA no reemplaza la revisión y aceptación responsables.

### 3.2. Secuencia de entregas

| Entrega | Resultado verificable | Dependencia de integración | Hito |
|---|---|---|---|
| E0 | Base reproducible y viabilidad de firma/documentos/servicios | Línea base disponible; acceso autorizado a ambiente de prueba para las validaciones reales | H0: base y evidencias tempranas revisadas. |
| E1 | Identidad y acceso aislado por rol y ámbito | Contratos, entorno y decisiones aplicables de E0 | H1: identidad y aislamiento verificados. |
| E2 | Importación y consulta autorizadas | E1 y contratos de datos | H2: importación verificada. |
| E3 | Llamados, correcciones e historial | E1/E2 y contrato de versión documental de E0 | H3: actuaciones conservadas sin duplicados ni sobrescritura. |
| E4 | Planes y seguimiento interno | E3, formato oficial y reglas aplicables resueltas | H4: planes y seguimiento verificados. |
| E5 | Aceptación mediante firma exacta | Viabilidad de E0; integración incremental con documentos E3/E4 | H5: firma y ausencia de firma verificadas. |
| E6 | Comunicación conservada y envío recuperable | E3; infraestructura documental; proveedor y decisiones aplicables; integración final con E4/E5 | H6: comunicación y correo verificados. |
| E7 | Operación y piloto con evidencia integral | E1–E6 aceptadas y pendientes del alcance resueltos | H7: aceptación del MVP y habilitación operativa. |

Las entregas no equivalen a semanas ni sprints. Los contratos de firma, versiones, seguridad e idempotencia empiezan en E0; no se posponen hasta E5. Se pueden preparar en paralelo los adaptadores de correo, los casos de prueba, las guías y los formatos, siempre que sus contratos estén definidos. RF-06 no exige que se hayan generado o firmado planes anteriores: la dependencia de integración no crea un prerrequisito funcional.

E1 puede probar el autorregistro con registros sintéticos importados mediante preparación controlada del ambiente; E2 verifica después el recorrido completo de importación real. Esa preparación no se incorpora como un camino alternativo de acceso para usuarios.

### 3.3. Estados del trabajo

Las tareas se registran como **Por iniciar**, **Lista para iniciar**, **En curso**, **Bloqueada**, **En verificación** o **Terminada**. Son estados de gestión del desarrollo, no estados de llamados o compromisos en la aplicación. Inicialmente todas las tareas están **Por iniciar**, con las dependencias indicadas; las decisiones pendientes no se consideran aprobadas por la creación de este PLAN.

## 4. E0 — Base técnica y validaciones tempranas

**Objetivo:** reducir las incertidumbres que pueden invalidar la implementación y establecer contratos comunes.  
**Origen:** TRD §§4–5, 7–12, 14; DT-001–003, DT-006–008, DT-012–013 y DT-015.

| Tarea | Trabajo y resultado | Dependencia específica |
|---|---|---|
| T-E0-01 | Registrar la línea base y los cambios confirmados; desglosar los 101 CA en una matriz de casos con PF/TEST, entrega, resultado y evidencia. | Documentos vigentes. |
| T-E0-02 | Crear repositorio y estructura por capas para Flutter, funciones y migraciones; fijar herramientas y versiones compatibles, instrucciones de ejecución y configuración de ejemplo sin secretos. | DT-002/012: selección técnica documentada. |
| T-E0-03 | Definir contratos de autorización, errores, versión esperada, idempotencia, auditoría y archivos privados; diseñar esquema y migraciones iniciales sin restricciones funcionales pendientes. | TRD §§5–8; DT-003/007/008/013. |
| T-E0-04 | Preparar entorno aislado y datos sintéticos; comprobar Auth, operación protegida y acceso privado a objetos. Registrar permisos y limpiar recursos de prueba según procedimiento. | Accesos y configuración autorizados. |
| T-E0-05 | Reproducir la incidencia táctil y verificar documento completo → trazo → limpiar/redibujar → confirmar → persistir → volver a consultar en dispositivos reales. Probar también fallo de red y cambio de versión. | Dispositivos y matriz inicial acordados; T-E0-03/04. |
| T-E0-06 | Obtener copias institucionales vigentes; evaluar representación/renderizado de llamado, GOR-F-084 V02 y GD-F-011 con campos extensos y varias páginas. Documentar biblioteca y lugar de ejecución elegido. | DT-006; copias aportadas por institución. |
| T-E0-07 | Configurar análisis, compilación y pruebas mínimas en integración continua; documentar SOLID, límites entre capas y revisión de dependencias. | T-E0-02; DT-012. |

**Entrada:** acceso a la línea base y responsables técnicos identificados para las decisiones iniciales. Se puede diseñar con datos sintéticos mientras llegan los recursos externos; una simulación no cierra las validaciones de servicios reales.

**Salida y evidencia:** compilación reproducible, contrato inicial revisado, migración reproducible en ambiente aislado, acceso privado comprobado, acta de validación de formatos y resultado de firma táctil real. Si falla la firma, registrar reproducción, diagnóstico y corrección; una alternativa de frontend requiere evaluar impacto y actualizar el TRD antes de adoptarla. E0 no se declara totalmente cerrada mientras esa validación o la fidelidad documental necesaria permanezcan sin evidencia.

## 5. E1 — Identidad, sesión y autorización

**Origen:** RF-01; RT-001–005; TEST-001–003; DT-004 y DP-07.

| Tarea | Trabajo y resultado | Dependencia específica |
|---|---|---|
| T-E1-01 | Documentar provisión operativa de Instructores y asociaciones instructor-ficha, responsables y revocación; preparar fixtures de dos instructores, dos fichas y varios aprendices. | Responsable institucional y E0. |
| T-E1-02 | Implementar ingreso, cierre, recuperación y manejo de expiración/renovación; depurar datos de sesión visibles tras cierre. | Política de sesión acordada. |
| T-E1-03 | Implementar autorregistro y vínculo exclusivo con aprendiz importado; probar identificación inexistente, duplicada, vínculo concurrente y fallos entre Auth y datos de dominio. | Contrato de identidad y compensación/reconciliación. |
| T-E1-04 | Aplicar autorización en servidor, consultas, operaciones y archivos; configurar políticas/grants; probar solicitudes directas y privilegios internos. | T-E1-01–03 y contratos E0. |
| T-E1-05 | Integrar navegación por rol, errores de acceso y recuperación de sesión; ejecutar TEST-001–003 y documentar el riesgo residual de reclamo de cuenta con identificación conocida. | T-E1-02–04. |

**Entrada:** contratos de E0, entorno aislado y política de sesión definida antes de implementar el comportamiento correspondiente.  
**Salida:** cada rol accede únicamente a sus datos y operaciones; no se concede acceso sin ficha asociada ni vínculo válido. Las pruebas negativas deben incluir objetos privados y seguimiento interno. Queda documentado quién provisiona y revoca acceso. No se incorpora verificación adicional de identidad por inferencia.

## 6. E2 — Importación y consulta de aprendices

**Origen:** RF-02; RT-005–007; TEST-003/004; DC-01 confirmado; DT-013/014.

| Tarea | Trabajo y resultado | Dependencia específica |
|---|---|---|
| T-E2-01 | Fijar estructura CSV/JSON, delimitador, límites, normalización y mensajes con archivos representativos; preservar `id` y `numero_ficha` como texto, incluidos ceros iniciales. | DT-013; UTF-8 ya adoptado. |
| T-E2-02 | Implementar análisis y revisión previa por fila: campos `id`, `nombre_completo`, `numero_ficha`, duplicados, estructura inválida y ámbito autorizado. | T-E2-01; E1. |
| T-E2-03 | Implementar confirmación explícita con revalidación de ámbito, inserción de filas válidas nuevas y reporte de incorporados/rechazados; proteger concurrencia y reintentos. | T-E2-02; contrato idempotente. |
| T-E2-04 | Implementar consulta autorizada y estados vacíos; probar que importar no crea cuentas, cambia fichas existentes ni habilita acceso por sí mismo. | T-E2-03. |
| T-E2-05 | Ejecutar TEST-003/004 con mezcla de filas válidas, inválidas y ajenas, cambios de permiso entre revisión/confirmación, duplicados concurrentes y fallos de red. | T-E2-02–04. |

**Entrada:** acceso E1 verificado y contratos de importación acordados.  
**Salida:** archivos CSV y JSON reproducibles, resultado por fila consistente y ausencia de filtración de datos ajenos. El éxito parcial autorizado no oculta rechazos. Los traslados entre fichas siguen pendientes y no se implementan mediante actualización automática de duplicados.

## 7. E3 — Llamados, versiones e historial

**Origen:** RF-03/09; RT-008/009/019–022; TEST-005/010/012–014 y TEST-020 condicionado a DP-05.

| Tarea | Trabajo y resultado | Dependencia específica |
|---|---|---|
| T-E3-01 | Implementar formulario del llamado según formato vigente, validación, cancelar y aviso de cambios sin guardar. | Formato E0; E1/E2. |
| T-E3-02 | Persistir actuación, versión, auditoría y resultado idempotente; coordinar objeto privado verificado y transacción relacional, con conciliación de temporales. | Contratos E0; almacenamiento validado. |
| T-E3-03 | Implementar conteo continuo y corrección mediante versión vinculada, sin sobrescritura ni incremento por corrección; controlar edición concurrente. | T-E3-02. |
| T-E3-04 | Implementar historial autorizado y consulta completa con relaciones de versiones; incluir estado vacío y llamados posteriores al cuarto. | T-E3-02/03. |
| T-E3-05 | Ejecutar pruebas de guardado, doble envío, respuesta perdida, conflicto de versión, permisos e historial; registrar evidencia antes/después de fallos. | T-E3-01–04. |
| T-E3-06 | Resolver DP-05 con producto; solo después especificar e implementar las anulaciones aplicables y ejecutar TEST-020. | Autoridad, efectos sobre conteo y documentos derivados aprobados. |

**Entrada:** datos y autorización disponibles; formato y contrato documental revisados.  
**Salida:** persistencia comprobada antes de confirmar éxito; originales preservados; consulta de resultado incierto; conteo correcto. La ausencia de firma no habilita edición destructiva. Si DP-05 permanece abierta, solo cabe aceptar explícitamente una entrega parcial con esa limitación; no marcar E3 ni el MVP completos por omisión del caso.

## 8. E4 — Planes y seguimiento de compromisos

**Origen:** RF-04/05; RT-010–012/019; TEST-003/006/007/010; DC-03 parcialmente resuelto y DC-06 pendiente.

| Tarea | Trabajo y resultado | Dependencia específica |
|---|---|---|
| T-E4-01 | Implementar elegibilidad manual de Plan 1 desde dos llamados y Plan 2 desde tres; conservar opciones omitidas al aumentar conteo. | E3; disponibilidad DC-03 confirmada. |
| T-E4-02 | Implementar GOR-F-084 V02 con varios compromisos, fechas y responsables, vínculos con antecedentes y conservación del documento. | Plantilla validada; política de generaciones independientes por resolver antes de habilitar repeticiones. |
| T-E4-03 | Implementar notas, evidencias y resultados de seguimiento exclusivos del Instructor; negar acceso al Aprendiz incluso mediante solicitudes directas. | T-E4-02; contrato de evidencia. |
| T-E4-04 | Implementar correcciones y vínculo de compromisos/seguimientos según decisión funcional aprobada; preservar originales y firma de cada versión. | DC-06/DT-007 resueltos para el caso afectado. |
| T-E4-05 | Ejecutar escenarios con 1, 2, 3, 4 y 5 llamados, omisión de Plan 1, cancelación, múltiples compromisos, acceso indebido y corrección concurrente. | T-E4-01–04; política de repetición resuelta para cobertura completa. |

**Entrada:** contratos de versiones E3, formato oficial y decisiones aplicables.  
**Salida:** opciones tardías disponibles, generación voluntaria y seguimiento privado verificables, sin estados formales ni incumplimiento automático. No se exige generar Plan 1 antes de Plan 2. La aceptación completa queda condicionada a resolver repeticiones y tratamiento del seguimiento al corregir compromisos; se puede desarrollar el resto sin convertir una propuesta en regla.

## 9. E5 — Firma manuscrita y aceptación

**Origen:** RF-08; RT-016–019; TEST-009–011/017; DT-007/015.

| Tarea | Trabajo y resultado | Dependencia específica |
|---|---|---|
| T-E5-01 | Integrar visualización completa, explicación de aceptación, captura táctil, limpieza/redibujo y confirmación explícita por el Aprendiz. | Viabilidad E0; documentos E3/E4. |
| T-E5-02 | Conservar evidencia privada y aceptación única por aprendiz/versión; comprobar versión esperada y persistencia antes de confirmar; impedir traslado de trazo ante conflicto. | Contrato E0; límites/formato de evidencia acordados. |
| T-E5-03 | Implementar observación de ausencia de firma cuando el Instructor compruebe que el Aprendiz fue informado; registrar actor, fecha, texto y documento. | Reglas RF-08; permisos E1. |
| T-E5-04 | Ejecutar firma real en matriz aprobada, cambio de orientación/tamaño, red interrumpida, sesión vencida, doble confirmación y corrección simultánea; comprobar accesibilidad del recorrido. | T-E5-01–03; DT-015. |

**Entrada:** evidencia táctil temprana y contratos de versión disponibles.  
**Salida:** firma consultable sobre la versión exacta presentada; una corrección no hereda aceptación. La observación no constituye firma ni aceptación. No existe un botón de rechazo agregado ni firma del Instructor en nombre del Aprendiz. TEST-017 requiere dispositivos/navegadores reales de la matriz; una emulación aislada no acredita compatibilidad final.

## 10. E6 — Comunicación y correo

**Origen:** RF-06/07; RT-010/013–015/019/020/022; TEST-006/008/012/014/021; DC-02 confirmado; DT-005/006/014.

| Tarea | Trabajo y resultado | Dependencia específica |
|---|---|---|
| T-E6-01 | Implementar generación manual del formato GD-F-011 desde cuatro llamados, conservando la opción omitida con conteos superiores; vincular antecedentes y versión. | E3; formato validado; política de repeticiones pendiente para cierre completo. |
| T-E6-02 | Implementar direcciones institucionales disponibles bajo permisos ya definidos, sin vínculo con fichas; selección previa a generación y captura del destinatario por intento. | DC-02; E1. |
| T-E6-03 | Implementar conservación documental y solicitud durable de correo en transacción relacional; verificar archivo antes de confirmar; iniciar primer intento automático sin segunda confirmación. | T-E6-01/02; infraestructura documental. |
| T-E6-04 | Seleccionar y configurar adaptador de correo, remitente y despacho recuperable; adjuntar el documento conservado; fijar reintentos, límites y conciliación según capacidades verificadas. | DT-005 y acceso autorizado al servicio de prueba. |
| T-E6-05 | Implementar historial de intentos y recuperación: conservar documento sin destinatario válido, permitir selección/reintento, conciliar respuesta incierta y no modificar destinatarios históricos por cambios del catálogo. | T-E6-03/04. |
| T-E6-06 | Ejecutar TEST-008/021: caída antes/después de envío, trabajo recuperado, respuesta perdida, rechazo del proveedor, cambio de destinatario y adjunto íntegro; integrar recorrido final con E4/E5. | T-E6-01–05. |

**Entrada:** contratos documentales y de autorización disponibles; proveedor y mecanismo real de despacho definidos antes de validar envíos.  
**Salida:** generación manual y primer envío automático; fallo de correo no borra documento; intentos trazables y recuperables. El estado debe distinguir solicitud pendiente, resultado conocido e incertidumbre según el contrato aprobado, sin confundir aceptación por proveedor con entrega o lectura. No se promete envío externo exactamente una vez. Los estados técnicos de despacho no crean estados de llamados o compromisos.

## 11. E7 — Operación, verificación integral y piloto

**Origen:** RNF-01–07; RNFT-001–012; TRD §§8–13; TEST-015–019; DT-009–012/015/016.

| Tarea | Trabajo y resultado | Dependencia específica |
|---|---|---|
| T-E7-01 | Acordar perfiles de carga, métricas, disponibilidad, RPO/RTO, conservación, región, costos y responsables; registrar valores y criterios verificables en TRD. | Decisiones institucionales y mediciones preliminares. |
| T-E7-02 | Preparar despliegue versionado, migraciones, secretos, aislamiento de ambientes, verificaciones de salud y reversión compatible con datos. | E0; configuración aprobada; DT-010/012. |
| T-E7-03 | Implementar y probar respaldo/restauración coherente de base de datos y objetos privados, incluidos documentos y firmas; medir pérdida y tiempo frente a objetivos acordados. | DT-011 resuelto; conjunto de prueba representativo. |
| T-E7-04 | Ejecutar rendimiento, compatibilidad, accesibilidad, revisión SOLID y seguridad; revisar políticas, permisos privilegiados y ausencia de datos sensibles en telemetría. | E1–E6 integradas; umbrales y matriz aprobados. |
| T-E7-05 | Completar métricas, alertas y procedimientos de incidentes, conciliación de archivos/correo y gestión de acceso; preparar guías para Instructor y Aprendiz. | DT-016; operación real definida. |
| T-E7-06 | Ejecutar recorrido integral importación → autorregistro → llamados → planes/seguimiento → firma → comunicación → correo → historial; adjuntar resultados por CA/PF y resolver defectos. | E1–E6; datos de prueba controlados. |
| T-E7-07 | Realizar piloto con alcance y participantes autorizados; obtener aceptación de producto y autorización de paso a operación, registrar versión desplegada y contingencia. | Evidencia integral, pendientes resueltos y responsables asignados. |

**Entrada:** entregas funcionales verificadas y umbrales aprobados para las pruebas correspondientes. La preparación operativa puede comenzar antes.  
**Salida:** restauración demostrada, requisitos funcionales y no funcionales aceptados, guías y responsables disponibles y decisión explícita de puesta en operación. Ninguna tarea de este PLAN constituye por sí misma autorización para contratar servicios, publicar producción o utilizar datos personales reales en pruebas.

## 12. Matriz de trazabilidad de la ejecución

### 12.1. Requisitos funcionales

| Origen PRD | Requisitos técnicos principales | Entregas | Familias de prueba |
|---|---|---|---|
| RF-01: identidad y acceso | RT-001–005 | E1; regresión transversal | TEST-001–003 |
| RF-02: importación y consulta | RT-005–007 | E2 | TEST-003/004 |
| RF-03: llamados | RT-008/009/019/020/022 | E3, integración E5 | TEST-005/010/012/014; TEST-020 condicionado |
| RF-04: planes | RT-010/011/019 | E4, integración E5 | TEST-006/007/010 |
| RF-05: seguimiento | RT-005/012/019 | E4 | TEST-003/007/010 |
| RF-06: comunicación | RT-010/013/019/020/022 | E6 | TEST-006/008/012/014 |
| RF-07: correo | RT-013–015/020/022 | E6 | TEST-008/021 |
| RF-08: aceptación y ausencia de firma | RT-016–019 | E0/E5; integración E3/E4 | TEST-009–011/017 |
| RF-09: historial | RT-005/019/022 | E3–E6 | TEST-003/010/014 |
| Guardado y errores transversales | RT-020/021 | E0–E6 | TEST-012/013 |

Esta tabla resume la asignación; no sustituye las correspondencias detalladas CA/PF/TEST del TRD §13.3. T-E0-01 debe conservar todos los CA y asociar cada caso concreto con los PF y pantallas UI que intervienen, sin inventar identificadores de origen. Una familia TEST puede contener varios casos y ejecutarse en distintas entregas.

### 12.2. Calidad y operación

| Requisito TRD | Preparación / verificación | Evidencia y dependencia |
|---|---|---|
| RNFT-001/002: rendimiento | E0/E7; TEST-015 | Carga y percentiles medidos. La propuesta de 2 s/95 % no se considera aprobada; cerrar DT-009. |
| RNFT-003: autorización | E1 y cada entrega | Pruebas de acceso permitido/denegado por recurso, incluidas llamadas directas. |
| RNFT-004/005: privacidad e integridad | E0–E7; TEST-010/012/019 | Controles de datos sensibles, auditoría e invariantes ante fallos. |
| RNFT-006/007: disponibilidad y recuperación | E7; TEST-016 | Objetivos acordados y ensayo de restauración DB + objetos; DT-010/011. |
| RNFT-008/009: compatibilidad y accesibilidad | E0/E5/E7; TEST-017 | Matriz real aprobada y criterios de accesibilidad; DT-015. |
| RNFT-010: confiabilidad | E3–E7; TEST-012/021 | Reintentos y concurrencia sin duplicación de la operación; incertidumbre de correo visible. |
| RNFT-011: mantenibilidad | E0 y revisiones; TEST-018 | Compilación reproducible, reglas separadas de UI/proveedores y revisión SOLID. |
| RNFT-012: observabilidad | Todas; cierre E7; TEST-019 | Eventos y alertas operables, sin secretos, firmas ni contenido sensible; DT-016. |

## 13. Decisiones y dependencias pendientes

Los responsables de esta tabla son perfiles propuestos. Cada cierre requiere registrar decisión, fecha, autor, fundamento, documento afectado y evidencia cuando corresponda. Se puede continuar con tareas independientes, pero no habilitar el comportamiento bloqueado.

| Dependencia | Estado al elaborar el PLAN | Responsable propuesto | Hito afectado / resolución necesaria |
|---|---|---|---|
| DC-01: ámbito de importación | Confirmada | Producto / técnico | Implementar E2; no volver a proponer importación de fichas ajenas. |
| DC-02: destinatario sin ficha | Confirmada | Producto / técnico | Implementar E6 con selección por comunicación y trazabilidad por intento. |
| DC-03: opciones omitidas | Confirmada en disponibilidad | Producto / técnico | Implementar E4/E6 a partir de umbrales acumulados. |
| DC-03 / DT-014: generaciones independientes repetidas | Pendiente | Producto | Antes del cierre completo E4/E6: definir cantidad, alcance y condiciones; no confundir con versiones correctivas. |
| DC-04 / DT-014: traslados de ficha | Pendiente | Producto / institución | Antes de cualquier traslado operativo: definir acceso al historial y responsabilidades; mantener conteo continuo. |
| DC-05 / DP-05: anulaciones | Pendiente | Producto / autoridad institucional | Antes de habilitar caso E3: autoridad, conteo y tratamiento de documentos previos; ejecutar TEST-020. |
| DC-06 / DT-007: compromisos corregidos | Pendiente | Producto | Antes de habilitar caso E4: correspondencia de compromisos y conservación del seguimiento. |
| DT-002/003/012: versiones, herramientas y esquema | Selección base resuelta; concreción pendiente | Técnico | E0: fijar versiones, migraciones, pruebas y pipeline reproducibles. |
| DT-004 / DP-07: sesiones y provisión | Pendiente de política operativa | Seguridad / producto | E1: duración, renovación, revocación, recuperación y responsable de altas/asociaciones. |
| DT-005: proveedor y despacho de correo | Outbox adoptado; ejecución pendiente | Técnico / operación | E6: capacidades comprobadas, remitente, adjuntos, límites, conciliación y recuperación. |
| DT-006: formatos y renderizado | Pendiente de copias/validación | Institución / técnico | E0 y entregas documentales: representación fiel, ejecución y biblioteca verificadas. |
| DT-007/008: evidencia e idempotencia | Diseño adoptado; detalles pendientes | Técnico / seguridad | E0/E3/E5: formato/límites de firma y conservación/consulta de claves; probar concurrencia. |
| DT-009/010: carga, alojamiento y costo | Pendiente de valores/configuración | Producto / operación | E7: cargas, objetivos, región, ambientes, planes de servicio y presupuesto. |
| DT-011 / DP-08: continuidad y conservación | Pendiente | Institución / operación | E7: plazos, respaldos, RPO/RTO y restauración íntegra. |
| DT-013: contratos físicos | Tipos textuales, UTF-8 y UTC adoptados; detalles pendientes | Técnico / producto | E0/E2: límites, delimitador, normalización y zona institucional de presentación. |
| DT-015 / DP-06: dispositivos y accesibilidad | Pendiente | Producto / calidad | E0/E5/E7: matriz, estándar/nivel aplicable y pruebas reales. |
| DT-016: observabilidad | Pendiente de detalle | Seguridad / operación | E7: eventos, acceso, conservación, métricas y alertas. |

Las propuestas de excluir llamados anulados del conteo o separar el seguimiento de compromisos sustancialmente corregidos no están aprobadas. El equipo no debe implementarlas hasta que el responsable decida. Una decisión de aplazar o excluir un caso del MVP requiere ajustar las fuentes y registrar aceptación del cambio; no basta con quitar su tarea del PLAN.

## 14. Procedimiento de desarrollo guiado por especificaciones

### 14.1. Condiciones para iniciar una tarea

Una tarea queda lista cuando se identifican sus RF/CA, RT y PF aplicables, se conocen entradas/salidas, permisos y errores, se resolvieron las decisiones que afectan su comportamiento y existe una forma reproducible de verificarla. El contrato y la migración necesarios deben estar revisados. Los ejemplos de datos se preparan sin información personal real.

### 14.2. Ciclo de implementación

1. Seleccionar una tarea o conjunto pequeño coherente; leer los apartados vigentes del PRD, USER_FLOW y TRD que la gobiernan.
2. Preparar una especificación de trabajo con comportamiento, exclusiones, contratos, casos positivos/negativos y dependencias resueltas. No delegar al generador de código decisiones de producto pendientes.
3. Implementar cambios acotados de interfaz, servidor y datos; incluir migraciones y configuración reproducible cuando corresponda. Mantener las reglas de negocio fuera de widgets y adaptadores.
4. Revisar el código generado o escrito, especialmente autorización, SQL, uso de privilegios, concurrencia, manejo de archivos y datos personales.
5. Ejecutar los casos aplicables y regresiones afectadas; incluir fallos e incertidumbre en escrituras críticas. Un adaptador simulado valida contratos, pero no sustituye pruebas del proveedor real.
6. Registrar evidencia, actualizar trazabilidad y documentación operativa; presentar la entrega al responsable correspondiente. Si aparece una regla nueva, tramitar el cambio antes de incorporarla.

### 14.3. Condiciones para terminar una tarea y cerrar una entrega

Una tarea se termina cuando el comportamiento acordado está implementado, revisado, verificable y documentado; sus pruebas aplicables pasan y sus cambios pueden reproducirse. Una prueba bloqueada no equivale a aprobada.

Una entrega se cierra cuando todas sus tareas y criterios aplicables tienen evidencia, las decisiones bloqueantes están resueltas, los defectos que impiden cumplir requisitos están corregidos y la persona responsable registra la aceptación. Se pueden presentar avances parciales identificados, sin declarar cumplimiento de los casos omitidos. Toda excepción que cambie el alcance debe reflejarse en PRD/USER_FLOW/TRD según corresponda.

### 14.4. Registro mínimo de evidencia

| Campo | Contenido obligatorio |
|---|---|
| Identificación | Tarea T-E…, CA, RT/RNFT, PF y TEST aplicables. |
| Versión | Commit o versión de código, migraciones y configuración relevante sin secretos. |
| Ambiente | Entorno, datos de prueba, navegador/dispositivo y versión cuando aplique. |
| Caso | Precondición, pasos, resultado esperado y resultado observado. |
| Resultado | No ejecutada, aprobada, fallida o bloqueada; motivo y defecto/decisión relacionado. |
| Evidencia | Informe, log depurado, captura no sensible o registro de ejecución. |
| Revisión | Fecha, responsable de ejecución y persona que valida. |

## 15. Riesgos y respuesta prevista

| Riesgo | Respuesta y trabajo asociado | Condición que impide aceptar |
|---|---|---|
| Firma táctil no utilizable | Reproducir temprano y probar dispositivos reales; T-E0-05/T-E5-04. | No completar el recorrido de firma en la matriz acordada. |
| Formato no fiel al institucional | Obtener originales y validar ejemplos extensos; T-E0-06. | Campos o estructura sin validación. |
| Acceso a datos o firmas ajenas | Pruebas negativas en servidor y objetos privados; T-E1-04 y regresión. | Cualquier acceso fuera del ámbito aprobado. |
| Pérdida o desalineación de datos y archivos | Preparación privada, verificación, transacción, conciliación y restauración; T-E3-02/T-E7-03. | Documento confirmado sin objeto recuperable o restauración incoherente. |
| Doble actuación o firma de versión incorrecta | Idempotencia y control optimista; T-E3-05/T-E5-02. | Duplicación de intención o transferencia de firma. |
| Correo con resultado incierto | Outbox durable, conciliación e historial; T-E6-03–06. | Pérdida silenciosa de solicitud o afirmación de entrega sin evidencia. |
| Suplantación mediante identificación conocida | Registrar riesgo de autorregistro y decisión institucional; T-E1-03/05. | Riesgo sin responsable ni tratamiento acordado antes de operación. |
| Regla pendiente convertida en comportamiento | Revisión contra §13 y control de cambios. | Restricción o permiso incorporado sin decisión aplicable. |
| Objetivos operativos indefinidos | Acordar carga, costos, continuidad y responsables; T-E7-01. | Rendimiento, recuperación o disponibilidad sin criterio evaluable. |

## 16. Estimación, seguimiento y control de cambios

Antes de programar cada entrega se asignarán responsables, capacidad disponible, estimación por tarea y fecha objetivo. Las estimaciones deben separar implementación, pruebas, correcciones y esperas externas; un pendiente institucional no se estimará como trabajo de programación. Se recalcularán con los resultados de E0 y la experiencia de las primeras entregas.

El seguimiento mostrará tareas terminadas con evidencia, bloqueos y su responsable, decisiones pendientes y defectos por resolver. No se calculará avance únicamente por cantidad de archivos o código generado. La revisión periódica tendrá una frecuencia acordada con el equipo; este PLAN no presupone sprints ni duración fija.

Para cada cambio se registrará: motivo, origen, requisitos y flujos afectados, impacto en datos/seguridad/pruebas, decisión del responsable y documentos actualizados. Se preservarán los identificadores existentes; los nuevos se asignarán sin reutilizar eliminados. El PLAN se actualizará después de aprobar el cambio de especificación, conservando historial.

## 17. Criterios de finalización del MVP

El MVP puede declararse terminado cuando se cumplan simultáneamente las siguientes condiciones:

1. RF-01–09 y todos sus CA aplicables tienen evidencia satisfactoria; la matriz registra PF, TEST y versión verificada. Los casos eliminados o diferidos cuentan con cambio de alcance aprobado.
2. Los recorridos completos de Instructor y Aprendiz funcionan con autorización, versiones, firmas, correo e historial; se comprueban errores, concurrencia y reintentos críticos.
3. Los RNF/RNFT tienen criterios acordados y evidencia, incluidas compatibilidad real, accesibilidad, privacidad y recuperación coherente de base de datos y archivos.
4. No quedan decisiones que impidan el comportamiento incluido ni defectos que incumplan sus criterios de aceptación.
5. Despliegue, reversión, operación, respaldo, conciliación e incidentes tienen procedimientos probados y responsables identificados.
6. El responsable del producto acepta la entrega y se registra la autorización operativa, junto con la versión liberada y sus limitaciones aceptadas.

**Siguiente acción de ejecución:** preparar E0, asignar responsables y reunir formatos institucionales, dispositivos y acceso al entorno de prueba. La elaboración de este PLAN no acredita la ejecución de ninguna de sus tareas.

## 18. Historial del documento

| Versión | Fecha | Cambio |
|---|---|---|
| 1.0 | 04-11-2026 | Elaboración inicial a partir de PRD, USER_FLOW y TRD ajustados; ocho entregas E0–E7, tareas, trazabilidad, condiciones de aceptación y decisiones pendientes. |
| 1.0 — ajuste editorial | 04-11-2026 | Actualización de la línea base al TRD v1.0 aprobado y aclaración del alcance de la aprobación documental; se conservan tareas, pendientes y condiciones de inicio y cierre. |


## Registro complementario confirmado — 04-11-2026 (DC-07/DC-08)

**Fuente:** instrucción expresa de Luis Fernando Corredor Mora en la revisión de E0. Se conserva la versión documental existente; este registro actualiza únicamente las decisiones indicadas y no aprueba las propuestas físicas del nuevo anexo.

- **DC-07, confirmada:** identificación del aprendiz como texto, con ceros iniciales; retirar espacios exteriores antes de validar; exigir uno o más dígitos ASCII 0–9. Rechazar vacío, espacios internos, letras, puntos, guiones y otros caracteres; no convertir a número ni limpiar caracteres inválidos silenciosamente. Error localizado por fila. ` 00123456 ` se acepta como `00123456`; `0012 3456`, `1.234.567` y solo espacios se rechazan. Aplicar la misma regla al dato de identificación utilizado en autorregistro. El conjunto exacto de espacios exteriores se precisa como propuesta P-06 del anexo, sin ampliarlo silenciosamente.
- **DC-08, confirmada:** Luis Fernando Corredor Mora asume inicialmente la habilitación de instructores y asignación de fichas. No se crea rol administrador ni interfaz administrativa del MVP. El mecanismo técnico y sus controles son propuestas para revisión.
- **Ficha pendiente:** no se han aprobado caracteres ni normalización de numero_ficha. P-01 del anexo propone una política explícita; no se aplica automáticamente DC-07 a ese campo ni se bloquean relaciones independientes.
- **Alcance autorizado:** especificación física inicial de identidad, fichas e importación, autorización, auditoría, idempotencia, procedimiento operativo y casos de prueba. Entregar para revisión antes de convertir en migración; sin ejecutar cambios ni crear recursos Supabase.
- **Pendientes conservados:** generaciones independientes repetidas, acceso histórico ante traslados/cambios de responsabilidad, autoridad y efectos de anulaciones y continuidad del seguimiento de compromisos corregidos. No se resuelven mediante restricciones implícitas.
- **Formatos:** se identificaron ejemplos diligenciados GOR-F-084 V02 y GD-F-011; no está confirmada su incorporación a Docs ni su vigencia institucional. Se requieren copias/instrucciones validadas para fidelidad documental, sin bloquear el núcleo independiente. No se inventan campos definitivos.

**Entregable vigente:** [TRAZA_E0_ESPECIFICACION_FISICA_INICIAL.md](TRAZA_E0_ESPECIFICACION_FISICA_INICIAL.md), v0.4 para revisión técnica, 06-11-2026; decisiones funcionales actualizadas en el registro final de esta fecha. FI-01–39 previstos, no ejecutados. Primera migración: [propuesta v0.1](TRAZA_E0_PRIMERA_MIGRACION_PROPUESTA.md), sin SQL.

T-E0-03 entrega ahora el anexo para revisión previa a migración. T-E0-04 y las migraciones continúan sin ejecutar. Luis está asignado a habilitación/asociaciones; no se infiere que asuma todos los demás perfiles del PLAN.


## Decisiones confirmadas y secuencia E0 — 06-11-2026

**Fuente:** aprobación expresa de Luis Fernando Corredor Mora. Este registro actualiza los pendientes históricos de 04/05-11-2026 solo en lo resuelto aquí; no cambia generaciones repetidas, traslados/acceso histórico, anulaciones ni continuidad de seguimiento de compromisos corregidos. DC-07/DC-08 permanecen confirmadas.

- **P-08 aprobada:** impedir duplicación y conservar causa exacta interna restringida. Ficha inexistente/no autorizada: número de fila y «No se pudo validar la ficha para esta fila», sin distinguir ambas ni buscar duplicados globales. Ficha autorizada y permiso vigente verificable sobre aprendiz existente: número y «Identificación ya registrada». Otros casos de duplicidad: número y «No fue posible incorporar esta fila», sin datos ajenos ni motivo de duplicidad. Aplicar en validación, confirmación, nuevas consultas, descarga, contadores y caché con permisos actuales. La ficha de entrada no acredita acceso al existente. Mensaje genérico reduce exposición, no elimina toda inferencia. Sin canal de revisión inventado; DC-08 no autoriza consultar otras fichas. PRD CA-02.5/6 ajustados; CA-02.7 conservado.
- **P-01/P-06 confirmadas:** identificación y ficha textuales de uno o más dígitos ASCII 0–9, con ceros preservados; retirar exclusivamente U+0020 exterior, rechazar vacío, espacios internos, tabs y otros caracteres. Misma normalización en catálogo y búsqueda de ficha en importación; también en identificación de autorregistro.
- **P-04 aprobada con ajuste:** agrupar filas válidas autorizadas por id normalizado; coincidencia de nombre y ficha según contrato: primera candidata y siguientes duplicadas internas. Diferencia de nombre o ficha: rechazar todas las filas del grupo conflictivo e indicar números de fila para corregir. Filas inválidas/ajenas se tratan aparte, no bloquean válidas ni exponen datos a través de agrupación. Otras identificaciones continúan. Distinto de P-08 frente a datos ya persistidos. La comparación concreta de nombre sigue como precisión técnica propuesta en §6.1 del anexo, no se deduce su aprobación.
- **P-05:** depuración productiva condicionada a política institucional; plazo pendiente. Desarrollo con datos sintéticos y plazos de ensayo explícitos, sin convertirlos en política productiva.
- **Primera migración:** alcance/secuencia confirmados, base técnica privada PostgreSQL; identidad, fichas, asociaciones e importación en incremento posterior. Diseño de objetos y permisos todavía para revisión; no se autoriza generar/ejecutar SQL ni crear recursos.

Referencias vigentes: [especificación física v0.4](TRAZA_E0_ESPECIFICACION_FISICA_INICIAL.md), para revisión técnica, FI-01–39 previstos; [primera migración propuesta v0.1](TRAZA_E0_PRIMERA_MIGRACION_PROPUESTA.md), M1-01–12 previstos. P-02/03/07, precisión de comparación de nombre, plazo productivo de P-05 y validaciones técnicas permanecen pendientes. No hay pruebas funcionales ejecutadas ni H0 cerrado.
