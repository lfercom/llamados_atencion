# TRAZA — Primera migración: base técnica privada

**Versión:** 0.1 — para revisión. **Fecha:** 06-11-2026.
**Estado:** alcance y secuencia confirmados por Luis Fernando Corredor Mora; diseño concreto propuesto, sin SQL generado ni ejecutado.
**Referencias:** PLAN T-E0-03; TRD §6.6, §8, §11.5, DT-003/008/012/016; especificación física v0.4 §10/14. No equivale a aceptación de E0, RF-01 o RF-02.

## 1. Alcance confirmado y límite

Primero se prepara y revisa una base PostgreSQL privada de idempotencia y auditoría técnica. Identidad, fichas, asociaciones instructor–ficha e importación de aprendices quedan para un incremento posterior. No se crean cuentas Auth, tablas de dominio, archivos, funciones Edge, Cron, colas externas ni recursos Supabase en este paso documental.

Esta propuesta NO es todavía una migración autorizada para generar o ejecutar. Los nombres, permisos y contratos siguientes deben revisarse antes de esa instrucción. La primera migración futura no cambiará objetos gestionados por Supabase ni creará roles de producto.

## 2. Inventario propuesto de objetos y dependencias

| Objeto futuro | Contenido y función | Dependencias |
|---|---|---|
| Esquema `traza_privado` | Espacio de nombres privado; fuera de esquemas expuestos a Data API | PostgreSQL y principal de despliegue con CREATE; comprobar configuración de API aparte |
| Tabla `operaciones_idempotentes` | Intención durable de actor técnico; estado y exclusión de ejecución | Solo esquema y tipos nativos; UUID provisto por invocador técnico, sin extensión/generador adicional |
| Tabla `eventos_auditoria` | Eventos técnicos append-only asociados a operación | FK restringida operaciones_idempotentes; sin identidad de aplicación |
| Restricciones e índices | PK uuid en ambas; unicidad de intención; secuencia de evento; validaciones y búsqueda de recuperables | Tablas anteriores; sin índices o claves hacia cuentas/Auth |
| Función `iniciar_operacion_tecnica` | Crear intención o devolver estado existente; rechazar misma clave con huella distinta | Tabla operaciones y evento de inicio coordinados en transacción |
| Función `reclamar_operacion_tecnica` | Reclamar ejecución libre/vencida; incrementar generación y asignar ejecutor/vigencia | Tabla operaciones, reloj servidor, bloqueos y evento de reclamación |
| Función `finalizar_operacion_tecnica` | Validar generación/ejecutor/vigencia y guardar resultado terminal/evento atómicamente | Ambas tablas; reloj efectivo al validar; no acepta sobrescribir terminal |
| Función `consultar_operacion_tecnica` | Consulta mínima por actor técnico autenticado y referencia propia | Tabla operaciones; contexto del principal de base de datos, no actor libre recibido |
| Privilegios y RLS | Denegación por defecto, políticas mínimas para ejecución técnica y ACL explícitas | Roles existentes verificados; no suponer valores por defecto seguros |

No se incluyen vistas, secuencias, tipos ENUM propios, disparadores, tarea de depuración, políticas públicas ni funciones de negocio. Los estados se restringen mediante CHECK; UUIDs explícitos permiten pruebas sin instalar extensiones. No crear esquema `traza` vacío anticipadamente. Catálogo permitido de operaciones técnicas: inicialmente solo `ensayo_base`; ampliarlo exige revisión de contrato, no aceptar operaciones arbitrarias del cliente.

### 2.1. Campos e invariantes de esta primera versión

**operaciones_idempotentes:** operacion_id uuid PK; actor_tipo text fijo `operador`; actor_operativo text no vacío derivado del principal técnico conectado; tipo_operacion text; clave_intencion text no vacía; huella_entrada text SHA-256 hexadecimal validada, calculada por el futuro invocador técnico sobre entrada canónica; estado text en pendiente/procesando/completada/fallida; resultado jsonb nullable y acotado a códigos/contadores sintéticos; creada_en y actualizada_en timestamptz de servidor; generacion_ejecucion bigint no negativa, inicial cero; ejecutor_id uuid nullable; concesion_hasta timestamptz nullable. Excepto campos marcados nullable, todos obligatorios. Estado procesando exige generación positiva, ejecutor y concesión; pendiente no tiene ejecutor/concesión. Estado terminal exige resultado y no permite nueva reclamación ni cambio de resultado. Conservar generación/ejecutor del cierre como evidencia.

Unicidad (actor_operativo,tipo_operacion,clave_intencion). Índice (estado,concesion_hasta) para candidatos recuperables. Repetir intención con misma huella devuelve operación existente; distinta huella rechaza sin mutarla. La huella verifica coherencia del reintento, no prueba integridad del contenido que no se conserva.

**eventos_auditoria:** evento_id uuid PK; operacion_id uuid FK restringida; secuencia integer positiva; accion text de catálogo inicio/reclamacion/finalizacion; ocurrido_en timestamptz servidor; resultado text y detalle jsonb de campos permitidos, sin PII, secretos o payload de negocio. Todos obligatorios. Actor se obtiene mediante la operación padre, no se duplica identidad humana ni se acepta nombre libre como autenticación. Índice único (operacion_id,secuencia); índice temporal (ocurrido_en,evento_id). La secuencia se asigna bajo bloqueo de la operación; inserción de evento y cambio de operación son atómicos.

La unidad final de escritura rechaza generación/ejecutor distintos o concesión vencida, incluso sin sustituto. Misma operación con respuesta perdida se consulta antes de repetir; una llamada tardía no renueva autoridad. Prueba de límite: el orden se define por comprobación final bajo bloqueo y reloj efectivo, no por el instante en que responde la red. Presupuesto/duración de ensayo explícitos; no adoptar 60 s de P-07 como regla productiva.

### 2.2. División respecto del modelo completo

En esta fase no existen actor_cuenta_id, actor_auth_id ni sus FKs; tampoco referencias a aprendiz, ficha, lote o fila. Las funciones no crean usuarios ni asignan permisos de negocio. La futura migración de identidad añadirá los tipos de actor y sus restricciones/FKs antes de habilitarlos, preservando intenciones históricas y sin usar UUIDs ficticios para satisfacer dependencias. No es correcto copiar literalmente §3.7–3.8 del modelo completo con referencias a tablas inexistentes.

## 3. Permisos propuestos y límites de confianza

Propuesta inicial deliberadamente cerrada: ningún runtime de aplicación recibe acceso a esta base todavía. Las pruebas positivas usan un principal técnico de base de datos autorizado; los roles de cliente se prueban de forma negativa. No se necesita implementar identidad TRAZA para verificar permisos PostgreSQL.

| Principal | Permisos propuestos sobre objetos de TRAZA |
|---|---|
| `PUBLIC` | Sin CREATE/USAGE del esquema; sin privilegios de tabla ni EXECUTE de funciones |
| `anon` | Sin acceso directo a esquema, tablas o funciones, tampoco mediante permisos heredados de PUBLIC |
| `authenticated` ordinario | Igual denegación; estar autenticado en Supabase no concede acceso a objetos privados ni rol operativo |
| `service_role` | Sin GRANT explícito, ni acceso heredado por PUBLIC; no se elige como runtime de esta fase. Comprobar ACL efectivas: su capacidad de eludir RLS no elimina la necesidad de privilegios de objeto |
| Principal técnico de despliegue/pruebas (nombre real por inventariar) | Propietario de objetos o acceso propietario equivalente verificado; puede aplicar migración, inspeccionar y ejecutar pruebas. No distribuir credencial a clientes ni a la aplicación |
| Futuro runtime limitado | Fuera de esta migración. Definir rol técnico, pertenencias y permisos específicos antes de habilitarlo; nunca conceder acceso por seleccionar rol en la UI |

Funciones propuestas SECURITY INVOKER, nombres cualificados y search_path fijo; sin puente SECURITY DEFINER público. Por ahora solo el propietario técnico puede ejecutarlas y modificar tablas; no es un contrato de acceso de aplicación. Revocar EXECUTE automático de PUBLIC en cada función. Revocar todos los privilegios de objetos existentes de este esquema que pudieran haber sido heredados por clientes y fijar privilegios por defecto del creador real para futuras tablas/funciones/secuencias del esquema. No cambiar globalmente objetos ajenos al esquema. Verificar membresías heredadas y cualquier grant previo a service_role.

RLS habilitada en ambas tablas sin políticas de cliente; defensa adicional, no sustituto de ACL. El propietario/privilegiados pueden eludirla: auditoría no es inviolable frente a infraestructura. No se concede UPDATE/DELETE/TRUNCATE de auditoría a clientes; las funciones nunca los ejecutan. Una prueba directa con `anon` o `authenticated` debe fallar por privilegios, no solo retornar cero filas. No hace falta otorgarles login SQL: un arnés privilegiado puede asumir esos roles para probar permisos. Una eventual prueba de API usa credenciales de ensayo, sin agregar cuentas de dominio.

La migración puede establecer ACL/RLS; la lista de esquemas expuestos es una comprobación de configuración del entorno que puede requerir un paso operativo separado. No confundir exclusión de API con denegación SQL: exigir ambas. No exponer el esquema ni instalar endpoints para facilitar pruebas.

## 4. Qué se puede demostrar antes de identidad

Idempotencia técnica por principal PostgreSQL, exclusión de ejecución y persistencia atómica son invariantes independientes del padrón de aprendices. Puede ensayarse el mismo principal/intención dos veces, competir desde dos conexiones y rechazar generación vencida. Auditoría aquí prueba trazabilidad de esas operaciones sintéticas y reversión conjunta; no prueba actor humano autenticado, permisos por ficha, autorregistro o auditoría académica. El principal conectado se registra desde contexto fiable, no desde un argumento libre. Herramientas de despliegue compartidas no acreditan autoría personal: el registro externo debe identificar ejecutor nominativo y solicitud; DC-08 no convierte a Luis en una cuenta técnica automáticamente.

## 5. Criterios de aceptación previstos, no ejecutados

| Caso | Comprobación y resultado exigido |
|---|---|
| M1-01 Base limpia | En base de desarrollo aislada con plataforma PostgreSQL/Supabase inicial pero sin objetos TRAZA, aplicar futura migración una vez sin intervención manual no documentada; obtener inventario exacto de §2 y permisos §3 |
| M1-02 Reproducibilidad | Repetir en otra base limpia de igual versión; mismo inventario/ACL. Una segunda aplicación en la misma base debe ser controlada por el historial de migraciones, no ignorar divergencias con IF NOT EXISTS |
| M1-03 Anónimo | Bajo anon intentar lectura, inserción, actualización, borrado, truncado, creación de objetos y ejecución de cada función privada: denegado; ningún dato o cambio, aunque conozca nombres/UUID |
| M1-04 Autenticado ordinario | Repetir matriz anterior bajo authenticated, también con identidad Auth de prueba si el entorno la ofrece: denegado sin crear cuenta TRAZA; no debe confundirse con ejecutar como propietario |
| M1-05 API/ACL | Esquema no expuesto por Data API; revisar ACL, PUBLIC, herencias, defaults y RLS. Ausencia de ruta API sola no satisface M1-03/04 |
| M1-06 Positivo técnico | Principal autorizado inicia, reclama, finaliza y consulta operación sintética; eventos correlacionados y horas servidor; ninguna PII ni credencial en resultado |
| M1-07 Reintento/conflicto | Misma intención/huella produce una operación; otra huella se rechaza sin sobrescritura; consulta tras respuesta perdida recupera resultado |
| M1-08 Concurrencia | Dos conexiones compiten por intención/reclamación: una operación, generación ganadora única, secuencias sin duplicación; trabajador sustituido o vencido sin sustituto no finaliza |
| M1-09 Atomicidad | Provocar fallo de evento durante finalización: operación no queda terminal parcialmente. Sin eventos de éxito sin estado correspondiente |
| M1-10 Integridad | FK huérfana, secuencia duplicada, estado incompatible y borrado de operación referenciada se rechazan. No cascadas de borrado |
| M1-11 Alcance | Sin tablas de dominio, Auth, Cron, triggers de identidad, archivos ni políticas de negocio; sin tarea de depuración productiva |
| M1-12 Registro | Evidencia depurada con versión motor, migración/checksum, ambiente, principal efectivo por prueba, esperado/observado y ejecutor/revisor. No declarar aceptación si falla denegación o reproducibilidad |

Un arnés futuro podrá usar fixtures dentro de transacciones revertidas; no incluir seeds de personas o credenciales en la migración. Para demostrar denegación con tablas no vacías, insertar datos sintéticos como técnico y repetir pruebas negativas. Los tiempos de ensayo y eventual eliminación de bases efímeras se registran como desarrollo, no política productiva P-05. Esta tarea no crea el arnés ni ejecuta comandos SQL.

## 6. Dependencias y siguiente punto de revisión

Antes de redactar SQL: revisar este inventario y contratos; identificar versión PostgreSQL, herramienta de migración, principal creador y roles reales disponibles, sin asumir propietario/grants de fábrica. Equipo técnico concreta tipos, catálogo y contratos de funciones sin ampliar alcance. Antes de ejecutar: instrucción posterior, base aislada autorizada y plan de pruebas/reversión del entorno de ensayo. Sin identidad de producto, no se otorgan permisos a una app real.

P-01/04/06/08 aprobadas afectan el incremento posterior; no son bloqueos para esta base. P-02/03/07 siguen por validar para importación; P-05 permite ensayos sintéticos y condiciona depuración productiva a política institucional con plazo pendiente. No se necesita decidir generaciones, traslados, anulaciones o compromisos corregidos para revisar esta propuesta; permanecen abiertos.

Referencias técnicas consultadas 06-11-2026: [Supabase, seguridad de API](https://supabase.com/docs/guides/api/securing-your-api) distingue grants y RLS y recomienda superficie explícita; [Supabase, RLS](https://supabase.com/docs/guides/database/postgres/row-level-security) describe los controles por fila. La configuración real de TRAZA no se ha inspeccionado ni validado.
