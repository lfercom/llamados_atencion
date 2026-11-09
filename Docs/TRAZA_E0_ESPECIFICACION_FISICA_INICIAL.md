# TRAZA — Especificación física inicial: identidad, fichas e importación

**Versión:** 0.4 — para revisión técnica. **Fecha:** 06-11-2026.
**Estado:** propuesta técnica; no es una migración aprobada ni ejecutada.
**Tarea:** T-E0-03; preparación de contratos de E1/E2.
**Responsable de producto y operación inicial:** Luis Fernando Corredor Mora.

## 1. Alcance y autoridad de las decisiones

Este documento propone tablas, contratos y verificaciones; no contiene SQL ejecutable. No se han creado recursos, cuentas o asociaciones en Supabase. La aprobación para preparar esta especificación no aprueba automáticamente sus propuestas técnicas.

Fuentes: PRD v1.0 RF-01/02, RNT-01/02/08/10/11 y RNF-02/03/06; USER_FLOW v1.0 §7.1/7.2, §10/11/13/17; TRD v1.0 §5, §6.1/6.6, §8 y resoluciones §14.1; PLAN v1.0 T-E0-03/04 y E1/E2; DECISIONES_POR_ENTREGA_TRAZA.md DC-01–06. Registro complementario confirmado: DC-07/DC-08, incorporado el 04-11-2026 por instrucción de Luis Fernando Corredor Mora.

**Confirmado DC-07:** identificación textual; retirar espacios exteriores antes de validar; después admitir exclusivamente caracteres ASCII 0–9 y al menos un dígito. Preservar ceros iniciales, rechazar espacios internos, letras, puntos, guiones y otros caracteres. No convertir a número ni eliminar caracteres inválidos. Error asociado a su fila. Aplicar la misma regla al autorregistro para comparar con la identidad importada.

**Confirmado DC-08:** Luis Fernando Corredor Mora habilita inicialmente instructores y asigna fichas. Es responsabilidad operativa, sin nuevo rol funcional ni pantalla administrativa.

**Confirmado previamente:** dos roles, aprendiz importado independiente de cuenta, acceso por ficha, importación autorizada por fila y éxito parcial, UTC/UTF-8, idempotencia transaccional. Las decisiones físicas de los apartados siguientes son propuestas, salvo reglas identificadas como confirmadas.

**Resolución vigente 06-11-2026:** P-01 y P-06 confirmadas; P-04 aprobada con conflicto de grupo; P-08 aprobada con mensajes exactos de §6.4; P-05 confirma condición institucional de depuración, no plazo. El alcance de primera migración es solo base técnica privada, según [propuesta separada](TRAZA_E0_PRIMERA_MIGRACION_PROPUESTA.md). Las tablas de dominio siguientes corresponden al incremento posterior; no se aprueban automáticamente sus detalles físicos. §12/13 conservan el historial de v0.2/0.3 y sus antiguos estados, actualizados por esta resolución y §14.

## 2. Convenciones físicas propuestas

- Esquema `traza` para datos de dominio y `traza_privado` para staging, idempotencia y auditoría, fuera de acceso directo de la API. Consultas de dominio mediante contratos protegidos; sin publicación automática de esquemas.
- PK de tipo `uuid`, generadas en servidor con estrategia aleatoria compatible con la versión instalada. No usar identificación como PK: evita propagar datos personales a las relaciones. Versión PostgreSQL y generador concreto por verificar antes de migración.
- `text` para identificadores de negocio, nombres y códigos; `timestamptz` para instantes, generados por servidor y serializados con zona UTC. `bigint` para revisión optimista, `integer` para filas y contadores, `jsonb` solo para resultados estructurados acotados.
- En las tablas, NN significa obligatorio; N significa admite nulo. Ningún valor obligatorio se obtiene de un actor declarado libremente por el cliente.
- FKs con eliminación restringida, sin cascadas de borrado. No hay borrado ordinario de aprendices, cuentas, lotes confirmados ni eventos. Limpieza de temporales requiere política separada; no se fija retención productiva aquí.
- Revisión aumenta en cada modificación autorizada. UUID no concede permiso. No guardar contraseñas ni duplicar correo de Auth en tablas de dominio.

## 3. Tablas y diccionario de datos propuestos

### 3.1. `traza.cuentas`

| Campo | Tipo / nulo | Regla |
|---|---|---|
| cuenta_id | uuid NN | PK, servidor |
| auth_user_id | uuid NN | Único; FK a la PK `auth.users.id`, sin borrado en cascada |
| rol | text NN | Solo `instructor` o `aprendiz`; no modificable por cliente |
| habilitada | boolean NN | Por defecto falso; al completar autorregistro válido se fija verdadero en la transacción de vínculo y auditoría (§5.1); ninguna identidad sin cuenta habilitada accede al dominio |
| aprendiz_id | uuid N | FK aprendices; único cuando existe |
| creada_en, actualizada_en | timestamptz NN | Servidor |
| revision | bigint NN | Inicial 1; positivo |

Restricción conjunta: aprendiz exige aprendiz_id; instructor exige aprendiz_id nulo. Un aprendiz tiene cero o una cuenta y cada cuenta aprendiz corresponde a exactamente un aprendiz. La cuenta instructor no puede convertirse en cuenta aprendiz mediante actualización ordinaria. El caso de una misma persona con ambos roles no está habilitado por esta especificación.

### 3.2. `traza.fichas`

| Campo | Tipo / nulo | Regla |
|---|---|---|
| ficha_id | uuid NN | PK |
| numero_ficha | text NN | Único; uno o más dígitos ASCII 0–9; texto con ceros preservados; retirar solo U+0020 exterior (P-01/P-06 confirmadas) |
| creada_en | timestamptz NN | Servidor |
| creada_por_operacion_id | uuid NN | FK operaciones_idempotentes; provisión operativa |

No crear fichas desde un archivo importado. El catálogo se prepara antes de asignarlo; la representación final de numero_ficha es una dependencia localizada, no afecta las FKs uuid.

### 3.3. `traza.instructor_ficha`

| Campo | Tipo / nulo | Regla |
|---|---|---|
| instructor_id, ficha_id | uuid NN | PK compuesta; FKs cuentas y fichas |
| activa | boolean NN | Acceso solo con asociación activa y cuenta habilitada |
| asignada_en, actualizada_en | timestamptz NN | Servidor |
| operacion_id | uuid NN | FK última operación autorizada; historial completo en auditoría |
| revision | bigint NN | Positivo; control de concurrencia |

Una cuenta instructor tiene cero o muchas fichas y una ficha cero o muchos instructores. Operación protegida y validación en persistencia comprueban que instructor_id tiene rol instructor; una FK sola no garantiza el rol. No cambiar rol de cuenta asociada. Desactivar asociación es un control operativo propuesto: no transfiere aprendices ni concede acceso histórico. Los efectos históricos de cambios de responsabilidad siguen pendientes; no habilitar cambios operativos que requieran resolverlos.

### 3.4. `traza.aprendices`

| Campo | Tipo / nulo | Regla |
|---|---|---|
| aprendiz_id | uuid NN | PK |
| documento_identidad | text NN | Único; solo ASCII 0–9, longitud mayor a cero; nunca numérico |
| nombre_completo | text NN | No vacío; límite propuesto P-03 |
| ficha_id | uuid NN | FK fichas; exactamente una ficha inicial |
| importacion_id, fila_origen | uuid NN / integer NN | FK compuesta al resultado de fila; origen obligatorio |
| creado_en | timestamptz NN | Servidor |

Única pareja (importacion_id, fila_origen). La importación únicamente inserta; no actualiza nombre, identificación o ficha existentes. Cambios de ficha quedan fuera de los permisos iniciales, no se implementan como actualización libre. Staging y aprendiz se enlazan al insertar en una transacción. El resultado guarda el id de recurso dentro de la operación durable; no es necesaria una FK circular adicional.

### 3.5. `traza_privado.importaciones`

| Campo | Tipo / nulo | Regla |
|---|---|---|
| importacion_id | uuid NN | PK |
| autor_id | uuid NN | FK cuenta instructor; propietario del lote |
| formato | text NN | `csv` o `json` |
| huella_archivo | text NN | SHA-256 de bytes recibidos; diagnóstico, no clave de deduplicación global |
| contrato_version | text NN | Incluye política de ficha aprobada, parser y normalización utilizados |
| estado | text NN | recibido, validado, procesando, completado, fallido, cancelado |
| revision | bigint NN | Confirma la revisión mostrada, inicial 1 |
| total_filas | integer NN | No negativo; conteos de resultados se calculan desde filas |
| creado_en, actualizado_en | timestamptz NN | Servidor |
| validado_en, confirmado_en, finalizado_en | timestamptz N | Según fase; confirmado_en implica acción expresa |
| operacion_confirmacion_id | uuid N | FK operación de confirmación, única |
| codigo_error | text N | Error técnico seguro, no texto del proveedor |

Estados exclusivos de procesamiento: no son borradores recuperables del formulario. Cancelar antes de confirmar no crea aprendices. Lote completado significa que todas las filas tienen resultado terminal, incluso si ninguna fue incorporada; no significa éxito de todas. Fallido se reserva para imposibilidad técnica de continuar, mostrando si existen filas ya incorporadas. Reanudar recupera el mismo lote.

### 3.6. `traza_privado.resultados_fila`

| Campo | Tipo / nulo | Regla |
|---|---|---|
| importacion_id, numero_fila | uuid NN / integer NN | PK compuesta; FK lote; fila positiva |
| ficha_id_contexto | uuid N | FK ficha de la fila si pudo resolverse y fue autorizada; contexto durable para filtrar reportes, no ficha del registro ajeno existente |
| estado_validacion | text NN | valida, invalida, duplicada_archivo, conflicto_archivo, existente, no_autorizada |
| estado_confirmacion | text NN | no_solicitada, pendiente, incorporada, rechazada |
| errores | jsonb NN | Lista acotada {campo,codigo}; vacía si no hay errores |
| filas_conflicto | integer[] N | Números de filas válidas autorizadas del grupo P-04; sin referencias a filas ajenas; filtrar proyección con permisos actuales |
| proyeccion_restringida | boolean NN | Falso por defecto; antecedente interno propuesto P-08, nunca permiso congelado ni indicador público; recalcular proyección en cada consulta (§6.4) |
| aprendiz_existente_id | uuid N | FK restringida a aprendices, solo para causa interna EXISTENTE; referencia durable privada para comprobar acceso actual al registro que produjo el duplicado, según P-08 (§6.4) |
| validada_en, procesada_en | timestamptz N | Servidor |
| datos_depurados_en | timestamptz N | Servidor; identifica eliminación del payload temporal, no de este resultado |

Una fila solo tiene un resultado final de confirmación. Rechazada exige razón; pendiente únicamente después de confirmación. Incorporada exige procesada_en y un aprendiz vinculado a esta fila por su FK de origen. La obligación de payload válido se comprueba en la transacción de inserción; no obliga a conservar el payload para siempre. Campo y código pueden registrar varias validaciones sin revelar datos existentes ajenos. Los códigos internos y su proyección visible se separan en §6.4; el cliente nunca recibe automáticamente errores completos de esta tabla.

### 3.6.1. `traza_privado.datos_temporales_fila`

Separación propuesta en v0.2: una fila de resultado tiene cero o un payload temporal. El payload tiene exactamente un resultado padre. Esto sustituye los campos originales/validados temporales de §3.6 de v0.1, sin eliminar resultados ni referencias de origen.

| Campo | Tipo / nulo | Regla |
|---|---|---|
| importacion_id, numero_fila | uuid NN / integer NN | PK y FK compuesta a resultados_fila, eliminación restringida |
| documento_original, nombre_original, ficha_original | text N | Datos recibidos, solo mientras se prepara/procesa el lote |
| documento_validado, nombre_validado | text N | Payload validado para incorporación; documento sin espacios exteriores |
| ficha_id_validada | uuid N | FK ficha autorizada para confirmar; nunca ficha ajena descubierta por duplicado |
| creada_en | timestamptz NN | Servidor |

No convertir objetos JSON arbitrarios a texto: indicar tipo inválido. No conservar archivos ni payload en idempotencia o auditoría. Borrar este payload es una operación excepcional protegida descrita en §6.5, no un borrado de evidencia. Aprendices continúa referenciando resultados_fila, nunca esta tabla temporal. La PK compuesta también sirve al acceso por fila; no necesita otro índice idéntico.

### 3.7. `traza_privado.operaciones_idempotentes`

| Campo | Tipo / nulo | Regla |
|---|---|---|
| operacion_id | uuid NN | PK |
| actor_tipo | text NN | cuenta, identidad_auth u operador |
| actor_cuenta_id | uuid N | FK cuentas, obligatorio para tipo cuenta |
| actor_auth_id | uuid N | FK auth.users.id con eliminación restringida; obligatorio exclusivamente para identidad_auth, sin exigir cuenta de dominio |
| actor_operativo | text N | Identificador estable del principal operativo, obligatorio para operador |
| tipo_operacion, clave_intencion | text NN | Tipo permitido y clave opaca |
| huella_entrada | text NN | SHA-256 de entrada canónica versionada |
| estado | text NN | pendiente, procesando, completada, fallida |
| recurso_tipo, recurso_id | text N / uuid N | Referencia de resultado autorizable; tipo permitido, validada por contrato |
| resultado | jsonb N | Resumen mínimo; no copias de PII ni credenciales |
| creada_en, actualizada_en | timestamptz NN | Servidor |
| concesion_hasta | timestamptz N | Recuperación de trabajo; no expiración de la garantía idempotente |
| generacion_ejecucion | bigint NN | Inicial 0; aumenta al reclamar/reemplazar ejecución; no se reutiliza |
| ejecutor_id | uuid N | Identificador del trabajador servidor con concesión, no identidad elegida por cliente |

Exactamente uno de actor_cuenta_id, actor_auth_id y actor_operativo, correspondiente a actor_tipo. Índices únicos parciales por cada identificador/tipo_operacion/clave_intencion: cuenta, identidad Auth y operador. No usar nullable actor en una única clave que admita duplicados. No cambiar el actor de una operación al crearse la cuenta: se mantiene actor_auth_id para consultar/reintentar la misma intención después del vínculo. Las referencias de resultados no son vínculos documentales polimórficos: cada contrato verifica recurso y acceso; los recursos de negocio mantienen FKs reales. No borrar claves por vencimiento de una concesión. Retención pendiente P-05. La FK Auth restringida impide eliminar una identidad con operación/evidencia referenciada sin procedimiento futuro aprobado; nunca se borra como compensación automática.

### 3.8. `traza_privado.eventos_auditoria`

| Campo | Tipo / nulo | Regla |
|---|---|---|
| evento_id | uuid NN | PK |
| operacion_id | uuid NN | FK operación |
| secuencia | integer NN | Positiva; única por operación |
| actor_tipo, actor_cuenta_id, actor_auth_id, actor_operativo | text NN / uuid N / uuid N / text N | Misma exclusión de tres actores; FK cuenta/Auth según corresponda; admite evidencia antes de crear cuenta |
| accion, resultado, recurso_tipo | text NN | Catálogo técnico versionado |
| recurso_id | uuid N | Puede no existir en un rechazo |
| ocurrido_en | timestamptz NN | Servidor |
| detalle | jsonb NN | Lista permitida: código, cantidades, referencias y campos cambiados |

Append-only para las credenciales ordinarias y de ejecución; no se promete inviolabilidad frente al propietario de infraestructura. Registrar habilitación y asignación, comienzo/confirmación/final de lote, rechazos de autorización, fallos y recuperación de vínculo Auth. No guardar contraseñas, tokens, identificación completa, correos ni payload íntegro. Para cambio de asociación se conservan ids y valor anterior/nuevo de activa; actor autenticado, motivo y referencia de solicitud operativa dentro de detalle.

## 4. Índices y restricciones transversales

| Índice propuesto | Justificación |
|---|---|
| Únicos de cuentas.auth_user_id y cuentas.aprendiz_id no nulo | Impedir duplicación de identidad y reclamación concurrente |
| Único aprendices.documento_identidad | Duplicados entre lotes concurrentes; comparación textual exacta |
| Único fichas.numero_ficha | Resolver inequívocamente catálogo, pendiente normalización |
| PK instructor_ficha; adicional (ficha_id, instructor_id) filtrado por activa | Autorización por instructor y búsqueda de responsables por ficha |
| aprendices(ficha_id, aprendiz_id) | Listado paginado y filtro de acceso |
| resultados_fila(importacion_id, estado_confirmacion, numero_fila) | Recuperar pendientes sin reprocesar filas terminales |
| importaciones(autor_id, creado_en, importacion_id) | Historial propio paginado |
| Índices únicos de idempotencia por cuenta, identidad Auth u operador; (estado, concesion_hasta) | Recuperar también autorregistro sin cuenta y trabajos abandonados |
| auditoría(operacion_id, secuencia) único; (ocurrido_en, evento_id) | Orden de operación y consulta operativa |

Agregar índices en FKs usadas para validaciones/búsquedas que no estén cubiertas por prefijos anteriores: aprendices(importacion_id,fila_origen), fichas(creada_por_operacion_id), instructor_ficha(operacion_id), importaciones(operacion_confirmacion_id). No indexar masivamente JSON ni nombres sin evidencia de consulta. Verificar planes con datos sintéticos; esta lista no demuestra rendimiento. Auditoría/filas no se actualizan o eliminan desde clientes; invariantes de rol, origen y estados se verifican en persistencia además del contrato servidor.

## 5. Supabase Auth y autorización

Propuesta: Auth conserva credenciales/correo; cuentas conserva identidad de dominio y habilitación. auth.users 1 → 0..1 cuentas. Un aprendiz importado existe sin identidad Auth; crear identidad no concede acceso ni crea rol desde user_metadata. Las decisiones de sesión siguen en DT-004/DP-07; no se fijan tiempos aquí.

Autorregistro: aplicar DC-07, comprobar registro importado y no vinculado en servidor; crear identidad mediante flujo Auth permitido; finalizar cuenta/vínculo/habilitación en transacción con unicidad y auditoría según §5.1. No confiar en un id Auth recibido del cliente sin comprobar que corresponde a la identidad autenticada. La política de verificación de correo permanece pendiente: esta propuesta no añade una condición funcional nueva. No borrar automáticamente identidades preexistentes. La API distingue las causas funcionales CA-01.7/8 sin exponer datos de terceros. No ofrecer una búsqueda pública libre del padrón.

Propuesta de seguridad: habilitar RLS y denegar acceso anónimo a datos de dominio; conceder lectura mínima a cuenta habilitada según relación vigente. Escrituras solo mediante funciones protegidas con permisos explícitos, rutas Edge con autenticación y contexto de actor verificado. El cliente nunca inserta cuentas/asociaciones ni altera rol/habilitación. RLS no sustituye GRANT/revocación de ejecución; revisar ambas capas. Funciones privilegiadas, si se necesitan, usan search_path fijo y objetos cualificados; sin ejecución pública indiscriminada. La credencial de servicio elude RLS: no debe servir como autorización del actor; el backend realiza controles equivalentes en cada operación. Preferir funciones con contexto de usuario para operaciones ordinarias.

| Recurso | Instructor habilitado | Aprendiz habilitado | Operador autorizado |
|---|---|---|---|
| Cuenta | Solo proyección propia, sin escritura | Solo proyección propia | Habilitación/provisión conforme al procedimiento |
| Ficha/asociaciones | Solo asociaciones propias activas y fichas correspondientes | Sin listado de fichas ajenas | Alta de catálogo y asignación controlada |
| Aprendiz | Solo fichas activamente asociadas | Solo su registro, proyección mínima | Sin consulta masiva por defecto |
| Lote/reporte | Solo autor y contenido todavía autorizado | Ninguno | Diagnóstico mínimo justificado |
| Idempotencia | Resultado de operación propia y recurso aún autorizado | Solo operación propia autorizada | Operaciones propias y recuperación autorizada |
| Auditoría completa | Ninguno directo | Ninguno | Lectura restringida con propósito registrado |

Los reportes históricos se vuelven a filtrar: ser autor del lote no permite leer filas de una ficha fuera del ámbito actual. Un lote mixto devuelve resumen y códigos seguros; no revela identificación/nombre/ficha de registros existentes ajenos. El control de bajas de asociación se coordina con importación: confirmar cada fila bajo bloqueo compartido de cuenta/asociación, y modificar habilitación/asociación bajo bloqueo incompatible. El orden es cuenta, asociación, fila; así no se importa después de una revocación ya confirmada y se reducen interbloqueos. Reintentar conflictos transitorios sobre la misma intención.

### 5.1. Autorregistro recuperable y habilitación

Propuesta técnica: después de crear la identidad Auth, el servidor verifica esa identidad con el mecanismo Auth seleccionado; deriva actor_auth_id de la credencial verificada y crea la intención de finalización con actor_tipo=identidad_auth. No requiere cuentas.habilitada ni existencia de cuenta para invocar exclusivamente finalizar/consultar autorregistro propio. Esta excepción no permite consultar el padrón, otros recursos, habilitar instructores ni modificar roles. El estado devuelto es mínimo: pendiente, completado propio o error funcional seguro.

Si ocurre caída antes de registrar la intención, la siguiente autenticación de esa misma identidad permite registrarla y finalizar; si cayó después, consulta/reintenta la clave existente. Perder la clave no obliga a crear otra identidad: una consulta protegida por actor_auth_id y tipo de operación localiza la finalización propia; una segunda clave se reconcilia con el vínculo exclusivo ya existente. Nunca usar correo o identificación enviados como prueba de identidad. Si todavía no hay identidad Auth, repetir el recorrido Auth/recuperación de acceso del proveedor; esta especificación no inventa una identidad anónima ni persiste contraseñas. La recuperación debe ser compatible con la futura política de correo/sesión; no se omite verificación del proveedor para desbloquearla.

En una transacción, verificar id importado, bloquear aprendiz, comprobar vínculo y ausencia de inhabilitación previa, crear cuenta rol aprendiz con aprendiz_id, fijar habilitada=true, registrar evento con actor_auth_id y completar operación. El valor falso por defecto no debe impedir el autorregistro válido. Esta habilitación no exige intervención de Luis: su provisión manual confirmada corresponde a instructores. Confirmar éxito solo tras commit; si falla vínculo, auditoría o resultado, revertir la transacción y mantener identidad sin acceso a dominio. Dos reclamaciones concurrentes: una gana y otra recibe error funcional de vinculación sin datos ajenos. Si ya existe el vínculo propio habilitado, recuperar el resultado sin duplicar cuenta; si cuenta propia fue deshabilitada posteriormente, NO reactivarla por reintento y devolver acceso restringido. Consultar estado técnico de finalización no restaura permisos de dominio.

La recuperación no cambia actor_auth_id por cuenta_id. Auditoría puede referenciar ese actor y el id de cuenta creado en detalle permitido. Antes del punto Auth verificado, rechazos de autenticación se registran como diagnóstico técnico mínimo, sin inventar una FK a cuenta inexistente. La transacción de dominio no se afirma atómica con la creación externa de identidad Auth.

## 6. Contrato de importación propuesto

### 6.1. Preparar y revisar

Entradas: archivo, formato explícito y clave de intención; actor derivado de sesión. CSV con encabezados exactos id,nombre_completo,numero_ficha; JSON como arreglo de objetos con esos campos como cadenas. Campos extra y encabezados repetidos se rechazan como estructura inválida (propuesta P-02). Nada se convierte automáticamente desde JSON numérico. Un error de estructura impide preparar el lote; un error de dato afecta solo su fila. CSV correctamente entrecomillado preserva ceros.

P-01/P-06 confirmadas el 06-11-2026: para identificación y ficha retirar exclusivamente espacios comunes U+0020 exteriores; después exigir uno o más dígitos ASCII 0–9, conservar texto y ceros iniciales. Rechazar vacío, espacios internos, tabuladores y otros caracteres, incluidos espacios Unicode. Aplicar la misma normalización al alta de ficha en catálogo y a su búsqueda en importación; también a la identificación en autorregistro. Nunca convertir a número ni limpiar caracteres internos. Un BOM de archivo permitido por P-02 no autoriza BOM dentro de un campo. Registrar versión del contrato.

Validar tipos y obligatoriedad por fila; resolver ficha y permiso antes de consultar existencia global de identificación. Si no hay permiso o la ficha no existe: código seguro FICHA_NO_AUTORIZADA, sin confirmar existencia del catálogo y sin consultar duplicados globales para esa fila. Para ficha de entrada autorizada, aplicar P-08 aprobada de §6.4: EXISTENTE solo se expone cuando el registro existente está dentro del ámbito vigente; el conflicto fuera de ámbito recibe proyección restringida. No moverlo aunque la fila traiga otra ficha. Duplicados internos P-04 aprobada con ajuste: completar validación y autorización del archivo antes de elegir candidatas. Agrupar solo filas válidas y autorizadas por identificación normalizada. Si coinciden nombre y ficha según comparación versionada, primera fila del grupo candidata y restantes duplicadas internas. Si difiere nombre o ficha, rechazar TODAS las filas válidas autorizadas de ese grupo e indicar sus números para corrección; ninguna prevalece por orden. Filas inválidas/no autorizadas se resuelven aparte y no bloquean una válida autorizada del mismo id; no exponer números/datos de filas ajenas dentro del grupo. Las demás identificaciones continúan. Distinguir esta clasificación interna de P-08 contra registros persistidos.

Propuesta técnica de comparación de nombre pendiente de revisión dentro de P-03/P-04: retirar solo U+0020 exterior y comparar texto exacto, sensible a mayúsculas/acentos y espacios internos; no plegar Unicode ni fusionar silenciosamente nombres. Ficha se compara por valor normalizado P-01/P-06 (o ficha_id resuelto equivalente). No considerar `001` igual a `1`. Registrar reglas en contrato y probar archivos representativos antes de habilitar importación. La aprobación de P-04 no aprueba automáticamente esta precisión de nombre.

Respuesta: lote_id, revisión, versión de contrato, total, contadores por validación, filas numeradas con códigos y valores presentables autorizados. Campos originales solo del archivo del propio usuario y cuando la ficha esté autorizada; para filas ajenas únicamente número/código. No devolver datos recuperados de registros ajenos. Numeración: CSV fila lógica 1 es primer registro después del encabezado; reportar también línea física de inicio como diagnóstico calculado cuando haya saltos dentro de comillas. JSON fila 1 es primer elemento.

### 6.2. Confirmar y recuperar

Entrada: lote_id, revisión revisada y clave de confirmación. Comprobar autor, habilitación y versión; congelar contenido revisado. Si cambió la revisión, conflicto y nueva revisión explícita. La confirmación crea la operación durable y marca filas candidatas pendientes; filas inválidas pasan a rechazadas sin crear aprendices.

**Inicio y recuperación autónoma propuestos (P-07 ampliada):** la Edge Function de confirmación autentica al instructor y registra en la misma transacción lote confirmado, operación pendiente y filas pendientes. Ese registro durable es la solicitud de procesamiento; no depende de una tarea en memoria, del navegador ni de un token de sesión conservado. Tras commit, la función puede invocar un trabajador Edge de importación como activación inmediata de mejor esfuerzo. Si esa invocación falla o la respuesta se pierde, la solicitud sigue disponible. No se necesita una nueva confirmación. La invocación inicial no es la garantía de recuperación.

Se propone un despachador periódico de servidor mediante Supabase Cron (`pg_cron`), que invoque una Edge Function de despacho con credencial técnica protegida. El despachador busca operaciones de importación confirmadas pendientes sin ejecutor y operaciones procesando cuya concesion_hasta venció, siempre con filas pendientes o cierre de lote por completar. El vencimiento sin renovación es el indicio de ejecución interrumpida; no se requiere detectar el cierre del navegador. El despachador activa/reclama un trabajador por la operación existente, incrementa generacion_ejecucion y asigna ejecutor_id y vigencia con los bloqueos descritos abajo. Una ejecución activa no se reclama por una segunda señal; dos señales concurrentes compiten por la misma reclamación atómica. También se recupera el cierre cuando todas las filas son terminales pero faltó completar la operación/lote.

El trabajador procesa unidades cortas, cada fila con su transacción, y renueva la concesión únicamente si sigue vigente y es su generación. Al aproximarse al presupuesto de ejecución cede el trabajo de forma controlada para otra activación, sin cambiar resultados terminales. Caídas y límites de ejecución dejan trabajo detectable por vencimiento. Errores transitorios se recuperan por este recorrido; un error técnico no recuperable requiere diagnóstico operativo y no un bucle ilimitado de reintentos ni una nueva confirmación del instructor. Proponer frecuencia inicial de despacho de un minuto, tamaño de tanda y retroceso limitado por validar en desarrollo; no son tiempos de recuperación garantizados ni parámetros aprobados. P-07 conserva su estado de propuesta, incluida la concesión inicial de 60 s.

La identidad técnica permite ejecutar el trabajo ya confirmado, no asumir permisos ilimitados del instructor. Para cada fila pendiente, el servidor relee habilitación, rol y asociación vigente del autor original con la ficha; no usa una copia de permisos de la confirmación ni exige reabrir sesión de navegador. Cerrar el navegador o vencer su token no cancela por sí solo una intención durable; una deshabilitación o pérdida de asociación sí impide incorporar filas afectadas, que terminan rechazadas por autorización sin exponer datos ajenos. Se mantiene la revalidación bajo bloqueo; no procesar bajo privilegios de servicio omitiendo esos controles. Credencial del despachador aislada, endpoint no público de ejecución arbitraria y secretos fuera de cliente/registro. La consulta posterior del resultado exige sesión y autorización actuales.

**Definible ahora:** intención durable transaccional, responsable de activación servidor, búsqueda por estado/concesión, reclamación atómica, procesamiento independiente del navegador, conservación de resultados y revalidación por fila. **Por comprobar en desarrollo:** disponibilidad/configuración de Cron y activación autenticada de Edge en el entorno elegido, permisos técnicos mínimos, almacenamiento/rotación de secretos, índices de búsqueda, frecuencia, tandas, renovación, límites reales de CPU/duración y recuperación tras fallos del cron/despachador/red. Las tareas en segundo plano de Edge tienen límites y no sustituyen el registro y barrido durables. Si la infraestructura está caída no se promete progreso durante la caída: el barrido al restablecerse debe encontrar pendientes. Antes de aceptar este contrato debe demostrarse FI-15 con navegador cerrado, incluidos activación inicial fallida y despacho interrumpido. Esta propuesta no configura Cron ni despliega funciones en esta tarea.

Procesar cada fila en transacción: reclamar pendiente, revalidar ficha/rol/habilitación, intentar inserción bajo unicidad global, guardar resultado, auditoría y resultado de intención por fila atómicamente. Derivar intención de fila de operación de confirmación y número de fila; no inventar otra tras pérdida de respuesta. Si dos lotes compiten por identificación, uno incorpora y el otro conserva causa interna EXISTENTE con proyección según §6.4. Nada actualiza el registro anterior. Fallo de infraestructura revierte esa fila, permanece pendiente y se recupera; no se denomina rechazo de datos ni se ocultan las filas incorporadas anteriormente.

Finalizar lote solo cuando no quedan pendientes; resumen calculado desde resultados: total = incorporadas + rechazadas al completar. Mientras procesa: total = incorporadas + rechazadas + pendientes. Retomar tras caída usando concesión y reclamación exclusiva; token de ejecución impide que un trabajador vencido finalice trabajo reclamado por otro. La unicidad y el estado de fila protegen incluso si vence una concesión durante una transacción.

**Contrato propuesto de concesión:** generacion_ejecucion es un número de exclusión de ejecución, distinto de la clave idempotente. Reclamar exige estado recuperable y concesión libre/vencida; incrementa generación y fija ejecutor_id y concesion_hasta con reloj de servidor. Cada escritura de resultado de fila, resultado de operación, renovación o cierre de lote exige coincidencia de operación, generación y ejecutor y concesión todavía vigente. Comprobar al aplicar la mutación, bajo bloqueo del registro de operación, y volver a comprobar antes de finalizar la unidad transaccional; sin mantener llamadas externas dentro de ella. Un proceso vencido no puede autorrenovar ni aceptar un resultado calculado antes del vencimiento: debe reclamar nueva generación y recalcular/revalidar estado. La sustitución aumenta generación incluso si usa el mismo ejecutor_id.

Rechazar EJECUCION_OBSOLETA si generación/ejecutor no coinciden o venció concesión, aunque nadie la haya sustituido. No escribir resultado, aprendiz, auditoría de éxito ni estado terminal de ese proceso; revertir su unidad. Un diagnóstico de rechazo independiente puede registrarse sin confundirlo con resultado de negocio. La comprobación usa tiempo efectivo de servidor al finalizar escrituras, no el instante fijo de inicio de transacción. Si la concesión vence después de la última comprobación pero antes de que el commit termine de responder, el orden se define por esa comprobación y exclusión transaccional: no se promete un plazo físico de red. La nueva reclamación espera la unidad bloqueada y relee resultados comprometidos; nunca sobrescribe uno terminal. Orden de bloqueos ampliado: operación, cuenta, asociación, fila; todas las rutas respetan el mismo orden.

La misma clave, actor y entrada devuelve operación existente sin duplicar. Misma clave con otra huella: CONFLICTO_IDEMPOTENCIA. Hash de archivo no reemplaza clave: un archivo puede volverse a revisar intencionalmente y sus ids existentes se reportan. Canonicidad incluye versión, bytes/hash de archivo al preparar, lote/revisión al confirmar y actor autorizado; no incluye contraseña. Dos claves para el mismo lote no permiten confirmar dos veces: operacion_confirmacion_id se fija una sola vez mediante control atómico, y devuelve el resultado original.

Consulta de operación/lote exige autorización vigente. Un resultado perdido se consulta antes de repetir. Nunca devolver detalles protegidos desde el caché de idempotencia sin volver a autorizar.

### 6.3. Decisiones y parámetros: estado vigente 06-11-2026

| ID | Decisión / propuesta | Estado y dependencia |
|---|---|---|
| P-01 | Ficha textual, uno o más dígitos ASCII; conservar ceros, retirar solo U+0020 exterior; misma normalización en catálogo e importación | Confirmada 06-11-2026; rechazar vacío, espacios internos, tabs y otros caracteres. No fija longitud máxima |
| P-02 | CSV coma, comillas dobles con escape doble, LF/CRLF, UTF-8 con BOM opcional; JSON arreglo; rechazar extras | Contrato determinista; revisar archivos representativos. Sin autodetección de delimitador ni coerción. |
| P-03 | Archivo 5 MiB, 5.000 filas, id/ficha hasta 64 caracteres, nombre hasta 250, fila hasta 4 KiB; nombre con trim exterior y no vacío | Límites técnicos candidatos; no longitud institucional confirmada. Validar memoria/tiempo en entorno elegido. Exceso de archivo/filas rechaza lote antes de insertar; exceso de campo rechaza fila. |
| P-04 | Agrupar filas válidas autorizadas por id normalizado: idénticas en nombre/ficha, primera candidata; conflicto de nombre/ficha, rechazo de todas con números de fila | Aprobada con ajuste 06-11-2026; precisión técnica de comparación de nombre pendiente en §6.1; no bloquear por filas inválidas/ajenas |
| P-05 | Depuración productiva condicionada a política institucional de conservación/eliminación; desarrollo con datos sintéticos y plazos de ensayo identificados | Condición confirmada 06-11-2026; plazo productivo pendiente. Las 24 h anteriores no son política aprobada ni default productivo |
| P-06 | Retirar exclusivamente U+0020 exterior en identificación y ficha; luego validar dígitos ASCII no vacíos | Confirmada 06-11-2026; no trim Unicode general |
| P-07 | Trabajo por fila con concesión inicial de 60 s, activación Edge tras confirmación y barrido autónomo mediante Supabase Cron; frecuencia inicial propuesta de un minuto (§6.2) | Mecanismo y parámetros por validar en desarrollo, sin depender del navegador ni garantizar tiempo de finalización; no es política de sesión. |
| P-08 | Causa exacta interna protegida y mensajes según autorización vigente, en validación/confirmación/consultas y contadores (§6.4) | Aprobada expresamente 06-11-2026; detalles físicos aún para revisión |

### 6.4. P-08 aprobada — 06-11-2026

Decisión expresa de Luis Fernando Corredor Mora: impedir duplicación y conservar causa exacta interna con acceso restringido. No mostrar causa o registro ajeno por conocer la identificación. Misma regla en validación previa, confirmación y consultas posteriores, incluidas pantalla, descargas, contadores y caché; revalidar permisos, nunca congelarlos al importar.

| Situación | Evidencia interna | Respuesta visible exacta, con número de fila |
|---|---|---|
| Ficha de entrada inexistente o no autorizada | Causa exacta restringida si puede determinarse; no buscar duplicados globales de esta fila | «No se pudo validar la ficha para esta fila»; no distinguir inexistencia de falta de permiso |
| Ficha autorizada y acceso vigente verificable al aprendiz existente | EXISTENTE; no insertar ni actualizar | «Identificación ya registrada» |
| Ficha autorizada y duplicidad con aprendiz ajeno o permiso actual no acreditable | Causa exacta protegida, sin datos del registro en la respuesta | «No fue posible incorporar esta fila»; sin nombre, ficha, id interno ni motivo de duplicidad |

No hay medio ni responsable documentados para revisar registros ajenos; por eso no se remite a un canal inexistente. DC-08 no concede a Luis acceso a otras fichas. El mensaje genérico puede permitir sospechar duplicidad o recordar información antes conocida, pero no revela directamente su causa ni elimina toda inferencia. No se promete no inferencia absoluta. CA-02.5/6 se actualizan por esta aprobación; CA-02.7 se conserva.

Los campos propuestos de resultados_fila son `proyeccion_restringida` (antecedente, no autorización durable) y `aprendiz_existente_id` (§3.6). Cuando se detecta EXISTENTE, conservar internamente la referencia al aprendiz que produjo el conflicto, también si entonces estaba dentro del ámbito. Tras conflicto de unicidad concurrente, resolver esa referencia en servidor protegido; no devolver el UUID al instructor. Su conservación permite comprobar permisos actuales después de depurar identificación/nombre/ficha del payload. No requiere copiar esos datos a auditoría ni conservar el archivo. FK con borrado restringido, acceso exclusivamente servidor y retención ligada al resultado durable, sujeta a DT-011/DP-08. No crear índice inverso innecesario: la consulta parte del lote/fila y accede por la PK del aprendiz. Esta relación de verificación no cambia su ficha ni aprueba traslados o acceso histórico.

**Proyección en el momento de cada consulta, pantalla o descarga (P-08 aprobada):** comprobar primero sesión, habilitación y autoría del lote; aplicar el filtro vigente sobre ficha_id_contexto de la fila. Para mostrar EXISTENTE y contabilizarlo como duplicado visible, además exigir aprendiz_existente_id resoluble y acceso actual a la ficha del aprendiz referenciado según las asociaciones vigentes. No basta acceder a la ficha de entrada ni haber accedido al registro al importar. Si falta referencia, no se resuelve, o no se puede acreditar acceso actual, usar la respuesta restringida; un fallo de comprobación no autoriza divulgar. El caso no se reevalúa buscando por la identificación temporal, ya depurada. La marca histórica proyeccion_restringida=false no permite saltar estas comprobaciones; true tampoco decide por sí sola permisos actuales.

**Ejemplo A/B:** al importar para A, el instructor accede a A y B y el conflicto corresponde a aprendiz de B: se guarda causa interna EXISTENTE y su referencia privada. Tras perder acceso a B pero conservar A, el servidor puede mostrar número y resultado restringido de la fila de A, pero no EXISTENTE, datos de B ni el antiguo desglose de duplicados. Si ya se depuró el payload, no se muestran sus valores ni se reconstruyen desde B. Si no existe referencia verificable, aplicar exactamente la misma respuesta restringida. Si se pierde también A, ocultar los valores y aplicar la proyección mínima de fila fuera de ámbito, sin detalles de B. No se restauran datos que ya vio o descargó legítimamente antes; el contrato protege las nuevas respuestas.

El reporte interno sigue contabilizando causas EXISTENTE; el público recalcula contadores sobre la proyección vigente: los conflictos restringidos se agrupan entre rechazadas de revisión restringida, nunca en un contador de duplicados externos. Mantener totales de procesamiento coherentes (incorporadas, rechazadas, pendientes), sin reutilizar desglose histórico que revele causas ahora protegidas. Pantalla, descarga, API y resultado de idempotencia usan el mismo proyector de servidor y momento de autorización de la respuesta; controles y consultas coherentes en una unidad de lectura, sin prometer revocar bytes ya entregados.

No servir reportes públicos preconstruidos ni respuestas renderizadas de caché sin nueva autorización. La caché interna puede conservar resultados durables mínimos o referencias, pero cada recuperación debe volver a comprobar acceso tanto a A como al aprendiz existente y recalcular campos y contadores. Propuesta: respuestas y descargas sensibles no cacheables en cliente/intermediarios; invalidar vistas abiertas al volver a consultar y no ofrecer enlaces durables a exportaciones sin control de acceso. Un export generado anteriormente se regenera con permisos actuales para una nueva descarga; no basta firmar otra vez el archivo antiguo. El proyector no usa el booleano histórico como caché de autorización.

No incluir en errores del proveedor, descargas, auditoría accesible al instructor o mensajes de conflicto de índice información que evite esta proyección. Restringir el canal de diagnóstico a operación autorizada, motivo registrado y respuesta mínima; Luis no recibe acceso masivo a PII por su sola responsabilidad de habilitación/asignación. El acceso excepcional de diagnóstico debe autorizarse expresamente. Proponer límites de frecuencia y control de abuso de importación sin fijar valores aún.

**Límite y trazabilidad:** la causa EXISTENTE interna no se altera cuando una consulta posterior pierde autorización. Cambia su proyección visible y el desglose de contadores, no el resultado persistido. No servir información histórica de caché sin nueva autorización. La aprobación funcional no aprueba por sí sola cada campo, índice o mecanismo físico propuesto.

### 6.5. Depuración: condición institucional confirmada y mecanismo propuesto

Separar payload temporal (§3.6.1) de resultados durables (§3.6) permite eliminar datos originales/validados y cualquier objeto temporal del archivo sin romper aprendices(importacion_id,fila_origen). Conservar lote, resultado por fila, contexto autorizado de ficha, causa interna mínima, referencia privada aprendiz_existente_id cuando exista según P-08, instantes, versión de contrato, huella de archivo, operación y eventos requeridos. La referencia de duplicado no se depura junto con el payload; si por una política futura ya no está disponible, §6.4 exige proyección restringida, no reconstrucción por datos eliminados. Huella no sustituye archivo como prueba del contenido original ni demuestra por sí sola fidelidad de importación; esta es evidencia de procesamiento, no reproducción completa del archivo. Retención de esa evidencia y eventual minimización de contexto se decidirán con DT-011/DP-08.

La limpieza productiva requiere política institucional de conservación/eliminación aprobada, cuyo plazo sigue pendiente. Desarrollo admite datos sintéticos y plazos de ensayo explícitos; las 24 h anteriores no son un plazo productivo confirmado. Mecanismo propuesto: actor técnico autorizado, intención idempotente, registro de qué se depuró y comprobación de referencias. No eliminar resultados_fila ni lotes con referencias; no eliminar claves de idempotencia necesarias. No usar cascadas ni poner nulos en las FKs de origen. No depurar payload de lote en proceso, filas pendientes o recuperación activa. Tomar bloqueo de operación/lote compatible con el procesamiento para evitar carrera con confirmación, comprobar estados y ausencia de concesión activa, y borrar payload y fijar datos_depurados_en con auditoría atómicamente. Ausencia de payload en una fila pendiente es inconsistencia: detener recuperación, no crear un resultado ficticio.

Para lote no confirmado vencido/cancelado: conservar esqueleto mínimo de lote/filas con causa de expiración, cerrar su posibilidad de confirmación bajo bloqueo y depurar payload según política; nueva importación exige archivo y revisión nuevos. Para lote terminal confirmado: conservar resultado y origen, depurar exclusivamente payload/objeto no referenciado. Si eliminación de objeto externo falla, registrar tarea de conciliación durable sin afirmar que se completó; si se borró objeto pero falló registro final, conciliar por la misma intención. Archivo temporal y datos validados no se presentan como recuperables después de depuración.

Reportes posteriores muestran resultado conservado y «datos temporales depurados»; no reconstruyen valores desde un aprendiz ajeno ni desde logs. Las filas incorporadas se verifican por la FK de origen y estado, no por supervivencia de campos temporales. La evidencia de depuración indica cantidades y referencias, sin copiar el payload eliminado. No se habilita depuración productiva en esta tarea.

## 7. Procedimiento operativo propuesto y autorizado en su propósito

Responsable confirmado: Luis Fernando Corredor Mora. Mecanismo propuesto: herramienta local de operación versionada, ejecutada con principal de infraestructura nominativo autorizado; credenciales en almacén seguro, no en repo/chat/cliente web. No es rol de producto. Antes de implementarla, verificar permisos mínimos reales disponibles en el entorno; no asumir que una clave service-role puede restringirse con RLS. Si se requiere esa clave para Auth Admin, aislarla en componente servidor dedicado, sin exponer ejecución genérica ni SQL arbitrario.

1. Registrar solicitud con motivo, destinatario/identidad del instructor, ambiente, fichas y referencia única; confirmar que Luis la autoriza. Este documento autoriza el procedimiento, no cuentas o fichas concretas aún no identificadas.
2. Ejecutar previsualización de cambios sin mutación: identidad existente, rol, habilitación y asociaciones; confirmar ambiente y diferencias. La ejecución posterior requiere solicitud autorizada, no nueva aprobación del diseño por cada reintento.
3. Resolver identidad Auth por procedimiento controlado; no asumir correo como PK ni vincular una identidad existente sin comprobar titularidad. Si no existe, crear/invitar con API administrativa de servidor, sin asignar contraseñas compartidas. Mantener cuenta no habilitada durante preparación; nunca promover una cuenta aprendiz.
4. En transacción protegida, habilitar cuenta instructor y registrar operación/auditoría con actor operativo nominativo y cuenta objetivo. Repetir misma intención no duplica. Si Auth tuvo éxito y dominio falló, registrar recuperación y conservar acceso denegado hasta completar.
5. Preparar catálogo de fichas con códigos revisados aplicando P-01/P-06 confirmadas; asignar únicamente fichas existentes. Alta/repetición de pareja es idempotente; no crea aprendiz ni cambia ficha de uno existente. Cambios concurrentes exigen revision esperada.
6. Guardar comprobante depurado de resultado con operación, actor, motivo, fecha y diferencias; verificar lectura autorizada y rechazo de ámbito ajeno. Un fallo de auditoría revierte la mutación de dominio; fallos externos quedan en registro operativo seguro para conciliación.
7. Revocación/deshabilitación: mecanismo técnico propuesto para cortar acceso futuro inmediatamente desde cuenta/asociación; no ejecutar traslados ni resolver acceso histórico automáticamente. Cambios de responsabilidad con efectos históricos requieren DC-04 antes de habilitar ese caso.

El principal técnico no puede obtenerse seleccionando `rol=operador` en la aplicación. Inventariar personas con acceso a secretos, registrar uso y rotación. El nombre del responsable no sustituye autenticación. Su identidad técnica concreta y configuración de acceso son dependencias de ejecución, no recursos creados en este paso.

## 8. Casos de prueba previstos, no ejecutados

| Caso | Entrada / acción | Resultado verificable | Trazabilidad |
|---|---|---|---|
| FI-01 | ` 00123456 ` | Guarda `00123456`, sin número ni pérdida de ceros | DC-07; CA-02.4; TEST-004 |
| FI-02 | `0012 3456`, `1.234.567`, `12-34`, letras, vacío, solo espacios | Rechazo por fila; no inserta; otras filas válidas continúan | DC-07; CA-02.3/7 |
| FI-03 | JSON id numérico, notación científica y dígitos Unicode | Tipo/carácter inválido; no coerción | DT-013; TEST-004 |
| FI-04 | Tabs, BOM de campo o espacios Unicode exteriores/interiores en id y ficha; U+0020 exterior válido | Rechazar otros caracteres; retirar solo U+0020 exterior; preservar ceros. BOM de archivo se prueba separadamente en parser | DC-07; P-01/P-06 confirmadas |
| FI-05 | CSV con ceros, comillas, salto en nombre, JSON equivalente | Preserva id; fila lógica y diagnóstico correctos | CA-02.1/2; P-02 |
| FI-06 | Encabezado repetido, JSON mal formado, archivo/filas excedidos | Lote rechazado sin aprendices | P-02/03; TEST-004 |
| FI-07 | Dos filas válidas autorizadas con mismo id normalizado, nombre y ficha comparativamente iguales | Primera candidata, siguientes duplicadas internas; números y causa por fila; sin confundir con EXISTENTE persistido | P-04 aprobada; §6.1; CA-02.3/5 |
| FI-08 | Identificación existente en misma u otra ficha | No actualiza ni duplica; no expone datos existentes | CA-02.5/7; TEST-003/004 |
| FI-09 | Lote mixto con ficha autorizada y ajena | Incorpora válidas autorizadas; rechazo seguro por fila | DC-01; PF-05/06; TEST-003/004 |
| FI-10 | Instructor B consulta lote/operación de A; anónimo y aprendiz intentan importar | Acceso denegado sin payload sensible | CA-01.10/12 |
| FI-11 | Revocar ámbito/habilitación entre revisión y confirmación; competir con commit de fila | Orden transaccional verificable; no inserción posterior a revocación confirmada | CA-02.7; TEST-003 |
| FI-12 | Dos instructores/lotes insertan simultáneamente el mismo id | Exactamente un aprendiz; el otro conserva causa interna EXISTENTE y referencia privada al existente. Con P-08 aprobada, cada respuesta usa ámbito vigente: EXISTENTE solo con acceso acreditado al registro; sin él, mensaje restringido y contadores recalculados. P-08 fue aprobada el 06-11-2026 | §6.2/6.4; CA-02.5/6/7; TEST-004/012 |
| FI-13 | Repetir clave con misma entrada; después con otra | Un resultado; conflicto con entrada distinta | DT-008; TEST-012 |
| FI-14 | Dos confirmaciones simultáneas con claves distintas para un lote | Una sola operación de confirmación; sin filas duplicadas | DT-008 |
| FI-15 | Confirmar 100 filas; 40 incorporadas; interrumpir proceso y cerrar navegador. Variantes: activación inicial falla, pérdida de respuesta, caída antes/después de commit y caída antes de cierre del lote | Sin reabrir aplicación, recargar archivo ni reconfirmar, Cron/despachador detecta trabajo pendiente o concesión vencida y activa nueva generación/ejecutor/vigencia; conserva 40 resultados terminales, revalida permisos vigentes de cada una de las 60 pendientes y deja un resultado por fila. Detalle y criterios en §8.1 | §6.2; P-07; RNF-06; TEST-004/012 |
| FI-16 | Dos trabajadores tras vencimiento de concesión | Un resultado final por fila; trabajador antiguo no sobrescribe | P-07; DT-008 |
| FI-17 | Dos autorregistros del mismo aprendiz; Auth creado y vínculo fallido | Solo una cuenta vinculada; identidad sin vínculo no accede | CA-01.6/8; TEST-002 |
| FI-18 | Manipular rol, habilitada, autor o ficha en API/metadatos | Sin elevación; escrituras directas denegadas | CA-01.10/12; TEST-003 |
| FI-19 | Cuenta deshabilitada con token previo; consulta de operación antes autorizada | Acceso denegado con política vigente | CA-01.3; DT-004 |
| FI-20 | Luis habilita/asigna mediante operación autorizada; repetir y competir por revisión | Resultado idempotente y trazable; conflicto con revisión vieja | DC-08; TEST-003/012 |
| FI-21 | Actor ordinario intenta usar canal operativo o modificar auditoría | Denegado; sin ejecución de comandos arbitrarios | RNF-02/03 |
| FI-22 | Fallo al escribir auditoría durante alta/importación | Sin mutación parcial de dominio; recuperación documentada | RNF-03/06 |
| FI-23 | Intentar borrar Auth/cuenta/ficha con referencias o mover aprendiz | Restricción y contrato deniegan; sin cascada ni traslado implícito | DC-04; TRD §5.4 |
| FI-24 | Lote con cero filas válidas; cancelación antes de confirmar | Revisión sin insertados; cancelación no crea aprendiz; terminales coherentes | CA-02.6/7; DP-03/04 |
| FI-25 | Auth creado; caída antes de crear intención y sin cuenta de dominio | Misma identidad verificada registra/recupera finalización propia; no accede al padrón ni requiere cuenta habilitada | §5.1; CA-01.6/8; TEST-002 |
| FI-26 | Intención de autorregistro existe; caída antes/después de vínculo y respuesta perdida | Conserva actor Auth, recupera misma operación aun después de crear cuenta; una cuenta y un resultado, sin contraseña persistida | §3.7/5.1; DT-008; TEST-002/012 |
| FI-27 | Completar autorregistro válido; después repetir tras deshabilitación operativa | Primer commit deja cuenta aprendiz habilitada y acceso propio; fallo de auditoría revierte; reintento no reactiva cuenta luego deshabilitada | §3.1/5.1; CA-01.1/3/6; TEST-001/002 |
| FI-28 | Consultar/finalizar intención usando otra identidad Auth, auth_user_id manipulado o sin credencial verificada | Denegado; no filtra existencia, estado o datos de otra intención; excepción no abre recursos ordinarios | §5.1; CA-01.10/12; TEST-003 |
| FI-29 | Proceso envía resultado tras vencimiento sin sustituto, o con generación anterior tras sustitución | EJECUCION_OBSOLETA; sin aprendiz, resultado terminal ni auditoría de éxito del proceso rechazado; reclamar nueva generación no reutiliza resultado sin revalidar | §6.2; FI-16; DT-008; TEST-012 |
| FI-30 | Depurar payload de lote completado con aprendices vinculados; repetir limpieza y consultar reporte | FKs/origen, filas, conteos y evidencia subsisten; payload eliminado y marcado; sin reconstrucción no autorizada | §6.5; P-05; RNF-03; TEST-004/012 |
| FI-31 | Limpieza compite con confirmación/recuperación; eliminación de objeto falla o se pierde respuesta | No borra datos pendientes/activos; estado bloqueado coherente; tarea durable de conciliación idempotente y sin afirmación falsa de borrado | §6.5; DT-011; TEST-012 |
| FI-32 | Id existente fuera del ámbito con ficha de entrada autorizada; validar, confirmar y descargar reporte | Con P-08 aprobada: no inserta/actualiza, causa interna restringida, fila visible con código genérico y sin datos del existente ni desglose externo; registrar límite de inferencia. Mensajes aprobados en §6.4; mecanismo técnico por verificar | §6.4; CA-02.5/6/7; TEST-003/004 |
| FI-33 | Acceso inicial A/B; importar fila para A con id existente en B; perder B, conservar A y consultar/descargar reporte tras depurar payload; variantes de caché, referencia ausente y ficha de entrada ajena | Con P-08 aprobada, comprobar acceso actual al aprendiz existente por referencia privada; sin acceso a B o sin prueba verificable, respuesta restringida sin EXISTENTE ni datos de B, contadores recalculados en pantalla/descarga/caché. Para entrada ajena no buscar duplicados globales. Detalle en §8.2 | §5/6.4; P-08 aprobada; DC-01; TEST-003/004 |
| FI-34 | Lote no confirmado expira y se depura; intento tardío de confirmar | Confirmación denegada; esqueleto/evidencia conservados y nueva revisión con archivo requerida, sin aprendices creados por expiración | §6.5; P-05; TEST-004/012 |
| FI-35 | Concesión vence durante transacción; sustitución espera bloqueo; mismo ejecutor reclama nueva generación | Comprobación final usa reloj efectivo; generación antigua rechazada; nuevo trabajador relee resultados terminales sin sobrescribirlos | §6.2; P-07; TEST-012 |
| FI-36 | Mismo id normalizado con nombre distinto o ficha distinta entre filas válidas autorizadas; tercer id independiente válido | Rechazar TODAS las filas del grupo conflictivo e indicar sus números; no insertar primera; tercero sigue; probar variantes de comparación de nombre una vez fijado contrato | P-04; §6.1; CA-02.3/6 |
| FI-37 | Fila no autorizada y fila válida autorizada comparten id; también variante de fila inválida | Fila ajena recibe «No se pudo validar la ficha para esta fila», sin búsqueda global; inválida recibe su error seguro; ninguna bloquea a la válida ni revela datos ajenos mediante agrupación | P-04/P-08; DC-01; CA-02.7 |
| FI-38 | Registrar ficha ` 001234 `; buscarla en importación con espacios exteriores; probar vacío, tabs, espacios internos y letras | Catálogo/búsqueda coinciden como texto `001234`; inválidos se rechazan; `001234` no equivale a `1234` | P-01/P-06; DC-07 |
| FI-39 | Ficha inexistente y ficha ajena; duplicado accesible y duplicado ajeno; repetir en validación, confirmación y consulta/descarga/caché | Primeros dos casos comparten mensaje exacto y no buscan duplicados; accesible muestra «Identificación ya registrada»; ajeno muestra «No fue posible incorporar esta fila»; contadores no exponen duplicados restringidos | P-08; CA-02.5/6/7 |

Cada caso requiere ambiente aislado, datos sintéticos, versión de contrato/migración futura, pasos, esperado/observado, ejecutor, fecha y evidencia depurada. Los FI son casos previstos, no reemplazan PF/TEST ni acreditan pruebas ejecutadas. Desglosar las variantes en ejecución. Verificar acceso por API directa además de interfaz y simular fallos reales de transacción; mocks no prueban RLS.

### 8.1. Ampliación FI-15: recuperación sin navegador

Preparar 100 filas válidas con permiso inicial, confirmar una sola vez, observar 40 filas incorporadas y detener abruptamente trabajador/despachador antes de la siguiente unidad. Cerrar navegador sin nueva interacción. Conservar el payload de las 60 pendientes: §6.5 prohíbe depurarlo mientras hay trabajo por recuperar. Observar que el siguiente barrido servidor tras vencer la concesión encuentra la misma operación y activa otra generación con ejecutor/vigencia nuevos, sin archivo reenviado, cookie ni token de usuario persistido.

Comprobar que los 40 resultados, ids de aprendices y auditorías de incorporación no cambian ni vuelven a ejecutarse. Cada una de las 60 pendientes pasa por comprobación actual de rol, habilitación y asociación, no por el resultado de validación inicial. Con permisos conservados y sin conflictos nuevos: 100 incorporadas, 0 rechazadas, 0 pendientes y exactamente 100 resultados. Variante con pérdida de permiso para 10 pendientes: 90 incorporadas, 10 rechazadas por autorización y 0 pendientes, sin deshacer las 40 iniciales ni revelar datos ajenos. Si hay duplicados concurrentes, conservar causa interna y aplicar proyección aprobada P-08. Verificar también recuperación del cierre con 100 filas terminales y lote aún procesando.

Intentar publicar desde la generación antigua: rechazo EJECUCION_OBSOLETA aun si conserva credenciales técnicas; sin alterar resultados ni contadores. Simular barrido duplicado, fallo de activación inicial y caída del scheduler: la solicitud durable no se pierde y se descubre al restablecer el servicio. Registrar tiempos observados sin declararlos SLA. La prueba solo pasa al comprobar activación autónoma real en desarrollo; una llamada manual de prueba al trabajador no demuestra esta condición.

### 8.2. Ampliación FI-33: pérdida de B después de depurar

Caso de P-08 aprobada: instructor asociado a A y B importa para A identificación existente en B. Registrar EXISTENTE interno y aprendiz_existente_id; reporte inicial puede mostrar EXISTENTE por acceso entonces vigente. Completar lote y depurar payload conforme a política aprobada; retirar acceso a B conservando A, sin trasladar al aprendiz. Volver a consultar pantalla, descargar y recuperar operación por idempotencia/caché. Verificar que se comprueba el registro de B por FK privada con permisos actuales; el booleano histórico falso y la ficha A no habilitan EXISTENTE. Se devuelve mensaje restringido de §6.4, sin datos depurados reconstruidos, UUID ajeno ni desglose externo.

Comparar contador de duplicados visibles antes/después: este caso deja de contarse como duplicado visible, sigue rechazado y entra en revisión restringida; total procesado no cambia. Preparar caché con respuesta antigua que contenía EXISTENTE y demostrar que no se sirve directamente ni se exporta un archivo antiguo. Variante sin referencia verificable: misma respuesta restringida, sin buscar por identificación ni consultar logs para reconstruirla. Variante de pérdida también de A: proyección mínima de fila fuera de ámbito. Mantener la variante original de entrada ajena sin consulta global y verificar errores seguros de índice/proveedor. Nada de esto demuestra eliminación del conocimiento de un reporte descargado antes de perder B.

## 9. Pendientes y límites del núcleo

| Pendiente conservado | Impacto concreto |
|---|---|
| DC-03 generaciones independientes | No existen tablas de planes/comunicaciones aquí; futura migración no impondrá unicidad aprendiz/tipo por inferencia |
| DC-04 traslados/acceso histórico | aprendices.ficha_id no se actualiza ordinariamente; instructor_ficha no decide permisos históricos. Podría requerir membresías temporales y contexto de ficha en actuaciones futuras |
| DC-05 autoridad/efectos de anulación | Sin bandera de anulación ni contador efectivo; futuro modelo debe registrar actuación sin borrar original y definir efectos antes de implementar |
| DC-06 compromisos corregidos | Sin tablas de compromisos/seguimientos aquí; conservar vínculo con versión original y no aprobar separación de seguimiento automáticamente |
| Formatos institucionales | Se identificaron ejemplos diligenciados GOR-F-084 V02 y GD-F-011; incorporación local y vigencia institucional NO verificadas. No se inventan campos; no bloquea identidad/importación |
| Parámetros técnicos de contrato | P-01/P-06 confirmadas; revisar P-02/03/07 y comparación de nombre antes de incorporar validadores físicos; no bloquean primera base técnica privada |
| DT-004/011/016 | Políticas de sesión, retención y acceso operativo detallado pendientes; no declarar aceptada E1 ni operación productiva |

## 10. Primera migración: alcance y secuencia confirmados

La primera migración se limita a base técnica privada PostgreSQL; identidad, fichas, asociaciones e importación quedan para incremento posterior. Revisar [TRAZA_E0_PRIMERA_MIGRACION_PROPUESTA.md](TRAZA_E0_PRIMERA_MIGRACION_PROPUESTA.md) v0.1: inventario, permisos, dependencias y M1-01–12. Se aprueba secuencia/alcance, NO sus detalles técnicos ni generación/ejecución SQL. Las tablas de dominio de §3 siguen como diseño futuro; no se copiarán FKs a tablas inexistentes. P-01/04/06/08 confirmadas y condición P-05 registrada; P-02/03/07 y comparación técnica de nombre pendientes según dependencia.

## 11. Referencias técnicas consultadas el 04-11-2026

Las propuestas de integración deben validarse contra la versión elegida; estas fuentes no aprueban decisiones de producto:

- [Supabase: gestión de usuarios](https://supabase.com/docs/guides/auth/managing-user-data): identidad administrada y relación con tablas propias.
- [Supabase: Row Level Security](https://supabase.com/docs/guides/database/postgres/row-level-security): control por fila y límites de credenciales privilegiadas.
- [Supabase: Auth Admin createUser](https://supabase.com/docs/reference/javascript/auth-admin-createuser): operación administrativa solo en servidor; no exponer claves privilegiadas.

Consulta complementaria del 05-11-2026 para la propuesta P-07 (no constituye validación de la configuración de TRAZA): [Supabase Cron](https://supabase.com/docs/guides/cron) permite programar activaciones de servidor; [tareas en segundo plano](https://supabase.com/docs/guides/functions/background-tasks) y [límites de Edge Functions](https://supabase.com/docs/guides/functions/limits) justifican trabajar con unidades acotadas y recuperación durable, sin asumir que una invocación permanece activa hasta terminar todo el lote. Compatibilidad efectiva y parámetros pendientes de ensayo en desarrollo.

## 12. Contraste previo de hallazgos y cambios v0.2

El contraste se realizó sobre v0.1 antes de editar; los cinco temas del encargo aplican. Los estados siguientes describen esa versión y no declaran aceptación técnica de la solución propuesta.

| Hallazgo | Evidencia en v0.1 / diagnóstico previo | Resolución documental v0.2 | Pruebas previstas |
|---|---|---|---|
| Recuperar autorregistro sin cuenta | §5 ya exigía recuperación y negaba acceso sin vínculo; §3.7/3.8 solo admitían actor cuenta/operador. Parcial: faltaba actor válido para ese momento | Actor identidad_auth, restricciones e índices, excepción acotada y recorrido de recuperación; §3.7/3.8/4/5.1 | FI-25/26/28 |
| Habilitar aprendiz al completar | §3.1 tenía habilitada=false por defecto y §5 creaba vínculo sin indicar transición. Vacío aplicable | Commit de cuenta/vínculo/habilitada=true/auditoría; reintento no reactiva cuenta deshabilitada; §3.1/5.1 | FI-27 |
| Rechazar ejecución vencida/sustituida | §6.2 y FI-16 ya impedían sobrescritura por trabajador antiguo. Parcial: faltaban campos y condición de rechazo por mero vencimiento | Generación, ejecutor, reloj efectivo, bloqueo y rechazo atómico aun sin sustituto; §3.7/6.2 | FI-29/35 y FI-16 |
| Depuración sin perder referencias | §2 y P-05 prohibían borrados ordinarios, pero §3.4 referenciaba resultados que §3.6 mezclaba con payload temporal. Vacío aplicable | Tabla temporal separada, resultado/origen durables, estados y limpieza coordinada; §3.4/3.6/3.6.1/6.5 | FI-30/31/34 |
| Duplicados ajenos | §5/6.1 ya ocultaban datos del registro, pero EXISTENTE revelaba existencia; FI-08 no distinguía esa inferencia. Parcial | P-08 separa evidencia interna/proyección, explicita riesgo residual y exige confirmación sin modificar PRD; §3.6/6.1/6.2/6.3/6.4 | FI-32/33 y FI-08/12, sujetos a confirmación |

**Comprobación documental:** revisión de referencias, tipos, invariantes, numeración de casos y coherencia de propuestas/pendientes. Ninguna prueba FI/PF/TEST se ejecutó; no se ha demostrado recuperación, RLS, concurrencia ni depuración en un sistema real.

**Decisiones por confirmar:** P-01–07 se conservan; P-08 se añade para reporte restringido de duplicados y tratamiento del riesgo de inferencia. Revisar las soluciones técnicas de identidad Auth, habilitación transaccional, concesión y separación temporal antes de migración; son propuestas, no decisiones funcionales nuevas aprobadas. DC-07/DC-08, DC-01/02 y disponibilidad de DC-03 permanecen confirmadas. DC-03 en generaciones, DC-04/05/06, sesiones, conservación y formatos siguen pendientes en su alcance anterior.

| Versión | Fecha | Cambio |
|---|---|---|
| 0.1 | 04-11-2026 | Primera especificación física propuesta con FI-01–24 y P-01–07 |
| 0.2 — para revisión | 04-11-2026 | Contraste de cinco hallazgos; actor previo a cuenta, habilitación explícita, rechazo de ejecución obsoleta, payload separado, P-08 y FI-25–35. Solo documentación |
| 0.3 — para revisión | 05-11-2026 | Recuperación autónoma servidor en §6.2/P-07 y FI-15/§8.1; referencia privada durable y proyección vigente P-08 en §3.6/6.4/6.5 y FI-33/§8.2; FI-12/32 condicionales. P-08 sigue pendiente; sin cambios en criterios del PRD |

## 13. Alcance histórico de la revisión v0.3 (actualizado por §14)

Solo se completa activación/recuperación de importaciones y autorización actual del reporte de duplicados. P-07 es mecanismo técnico propuesto compatible en diseño con Supabase, no configuración desplegada ni prueba de fiabilidad. P-08 y sus campos privados son propuestas pendientes de decisión; no se aprueban al corregir sus casos. DC-07 y DC-08 siguen confirmadas. P-01–06, los demás pendientes funcionales y las dependencias de formatos, retención y sesiones conservan su estado.

Comprobaciones documentales previstas: coherencia de campos, secciones, casos FI-12/15/32/33, referencias al entregable vigente y ausencia de aprobación implícita de P-08. Pruebas funcionales de Cron/Edge, cierre de navegador, permisos vigentes, caché, concurrencia y depuración: no ejecutadas. No se genera SQL, código de aplicación ni recursos Supabase.


## 14. Resolución vigente 06-11-2026 y control de cambios

Este registro prevalece sobre los estados históricos de §12/13 (v0.2/v0.3). P-08 aprobada con mensajes de §6.4; P-01/P-06 confirmadas; P-04 aprobada con rechazo de grupo conflictivo; P-05 confirma condición institucional de depuración, plazo pendiente y ensayos sintéticos permitidos. Primera migración de base técnica privada antes de identidad/importación; propuesta concreta separada para revisión. DC-07/DC-08 continúan confirmadas. No se aprueban generaciones repetidas, traslados/acceso histórico, anulaciones ni seguimiento de compromisos corregidos; tampoco se valida vigencia de formatos.

Versión 0.4 para revisión técnica, 06-11-2026: decisiones funcionales expresas incorporadas sin declarar aprobada toda la especificación física. FI-01–39 son casos previstos, no ejecutados; M1-01–12 figuran en propuesta separada. Comparación de nombre, P-02/03/07, plazo P-05, sesiones y mecanismos físicos siguen por revisar. Ningún SQL, implementación o recurso creado en esta tarea.
