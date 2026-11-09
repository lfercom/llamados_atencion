# TRAZA — Preparación de E0
**Versión:** 1.0  
**Fecha:** 04-11-2026  
**Estado:** Preparación documental completada; ejecución técnica pendiente.  
**Referencia:** TRAZA_PLAN v1.0, §4 (T-E0-01–07), y línea base allí identificada.

## 1. Resultado esperado
E0 establecerá una base reproducible y demostrará la viabilidad de los componentes críticos antes de desarrollar el MVP completo. Este documento convierte las siete tareas de E0 en instrucciones de trabajo, entregables y pruebas. Es un anexo operativo del PLAN; no agrega requisitos ni sustituye PRD, USER_FLOW o TRD.

En esta preparación se define qué construir, cómo comprobarlo y qué recursos hacen falta. No se ha creado un repositorio de aplicación, configurado servicios, instalado herramientas ni ejecutado las pruebas descritas. Tampoco se declara resuelta la incidencia táctil previa.

## 2. Paquetes de trabajo
Los perfiles de responsable son propuestas de asignación. Una persona puede asumir varios perfiles; los nombres, disponibilidad y fechas deben registrarse antes de ejecutar.

| Tarea del PLAN | Trabajo preparado para ejecución | Entregable previsto | Responsable propuesto | Condición de finalización |
|---|---|---|---|---|
| T-E0-01 | Incorporar fuentes vigentes, registrar revisión y desglosar CA en casos concretos con PF/TEST. | Índice de fuentes y matriz de trazabilidad completa. | Técnico + calidad | Los 101 CA referenciados por el PLAN están identificados sin omisiones; cada uno tiene casos o un bloqueo explícito. |
| T-E0-02 | Crear repositorio, estructura por capas y configuración de ejemplo; seleccionar versiones compatibles. | Proyecto base, README, instrucciones para agentes y registro de herramientas. | Desarrollo + técnico | Un entorno limpio puede obtener dependencias y compilar siguiendo el README. |
| T-E0-03 | Concretar autorización, errores, versiones, idempotencia, auditoría y coordinación de objetos. | Contratos revisados, esquema y primera migración de prueba. | Técnico + datos/seguridad | Contratos sin decisiones funcionales inferidas; migración reproducible en entorno aislado. |
| T-E0-04 | Preparar identidades sintéticas y probar operación protegida y archivos privados. | Configuración de prueba y evidencia de permisos. | Desarrollo + seguridad | Acceso autorizado permitido; acceso ajeno y anónimo denegado en servidor y objetos. |
| T-E0-05 | Reproducir incidencia táctil y comprobar recorrido completo con fallos y concurrencia. | Prototipo vertical de firma e informe por dispositivo. | Desarrollo + calidad | Firma real persistida y consultable sobre la versión exacta; conflictos y fallos no producen aceptación falsa. |
| T-E0-06 | Contrastar documentos renderizados con formatos institucionales vigentes. | Ejemplos, lista de campos y validación de fidelidad. | Producto/institución + desarrollo | Tres tipos documentales revisados, incluidos casos extensos y varias páginas. |
| T-E0-07 | Configurar análisis, compilación, pruebas y revisión de límites entre capas. | Pipeline y registro de revisión. | Técnico + calidad | Ejecución reproducible, fallos visibles y separación de responsabilidades comprobada. |

Todas estas tareas siguen pendientes de ejecución. La preparación de sus fichas no equivale a terminarlas.

## 3. Orden de ejecución
1. Registrar la línea base (T-E0-01) y concretar ambiente, herramientas y repositorio (T-E0-02).
2. Definir los contratos y el esquema inicial (T-E0-03); preparar los casos de prueba antes de implementar el prototipo.
3. Crear el entorno aislado y verificar autorización y almacenamiento (T-E0-04).
4. Validar firma y documentos (T-E0-05/06). La recopilación de formatos y dispositivos puede comenzar desde el primer paso.
5. Incorporar verificaciones al pipeline desde que exista la base compilable (T-E0-07).
6. Revisar evidencias y decidir si se cumple H0 o si quedan tareas bloqueadas.

La matriz completa de CA se desarrolla progresivamente en T-E0-01; los escenarios de este anexo cubren riesgos tempranos y no sustituyen esa matriz.

## 4. Organización propuesta del repositorio
La siguiente distribución es una propuesta operativa de carpetas, no una modificación de la arquitectura. Los nombres pueden ajustarse al preparar el repositorio, conservando responsabilidades.

| Ruta propuesta | Contenido |
|---|---|
| `README.md` | Requisitos del entorno, ejecución, compilación y pruebas. |
| `AGENTS.md` | Fuentes, reglas de trabajo asistido por IA y comprobaciones antes de entregar. |
| `docs/specs/` | Copias identificadas de PRD, USER_FLOW, TRD y PLAN. |
| `docs/decisions/` | Decisiones, estado, responsable y referencias DT/DC/DP. |
| `docs/verification/` | Casos, matriz CA/PF/TEST y evidencia depurada. |
| `apps/web/lib/` | Flutter: presentación MVVM y módulos con límites explícitos. |
| `supabase/functions/` | Edge Functions, autorización de solicitudes y adaptadores. |
| `supabase/migrations/` | Esquema, restricciones, funciones SQL y permisos versionados. |
| `tests/` | Pruebas de integración y recorridos que atraviesan componentes. |
| `config/` | Ejemplos sin secretos y descripción de configuración por ambiente. |

El lugar definitivo de pruebas unitarias y configuración seguirá las convenciones de las herramientas seleccionadas. No se fija aquí una biblioteca de gestión de estado ni una plataforma de integración continua.

### Reglas mínimas para el futuro AGENTS.md
- Consultar los requisitos y flujos aplicables antes de implementar cada tarea.
- Mantener trazabilidad desde tarea a CA/RT/PF y prueba.
- No transformar propuestas o pendientes en reglas de producto.
- Respetar Flutter Web/Dart, Supabase, PostgreSQL y Firebase Hosting seleccionados.
- Separar widgets, estado de presentación, reglas y adaptadores; aplicar SOLID donde corresponda.
- Autorizar en servidor; nunca depender únicamente de controles visuales.
- No almacenar secretos, datos personales reales ni firmas en repositorio o telemetría.
- Conservar originales y firma por versión; probar idempotencia y concurrencia.
- Guardado explícito, sin incorporar autoguardado ni borradores persistentes.
- Informar pruebas ejecutadas, resultados y bloqueos, sin afirmar éxito no comprobado.

## 5. Contratos que deben concretarse en T-E0-03
Estos puntos son una lista de comprobación para redactar los contratos físicos, no endpoints ni esquemas ya aprobados.

| Contrato | Contenido mínimo | Verificación temprana |
|---|---|---|
| Autorización | Actor autenticado, rol, ficha/propiedad, recurso y operación permitida; denegación segura. | Dos instructores con ámbitos diferentes y dos aprendices; solicitudes directas. |
| Datos de identidad | Identificación y ficha textuales; vínculo exclusivo con registro importado. | Preservar ceros iniciales y evitar vínculo concurrente duplicado. |
| Versión documental | Identidad de actuación y versión, referencia al original, versión esperada y aceptación vinculada. | Corregir mientras otro cliente firma: detectar conflicto, preservar original. |
| Idempotencia | Actor, operación, clave de intención, huella de entrada y consulta de resultado. | Repetir misma intención produce un resultado; misma clave con datos distintos se rechaza. |
| Archivos privados | Preparación de objeto, verificación, referencia durable y conciliación de temporales. | Fallo antes/después de transacción no confirma documento inexistente ni elimina objeto vinculado. |
| Errores | Diferenciar validación, acceso, conflicto, fallo e incertidumbre; mensajes sin datos ajenos. | Respuesta perdida no conduce a guardar nuevamente sin consultar resultado. |
| Auditoría | Actor, instante, referencia, operación y resultado; acceso y datos excluidos. | Reconstruir la operación sin exponer contenido sensible. |
| Firma | Evidencia de trazo, confirmación explícita, versión revisada y aceptación única por aprendiz/versión. | No trasladar firma ni registrar éxito antes de persistir. |

Quedan por decidir detalles físicos: límites de archivos/evidencia, retención de claves, códigos definitivos, normalización y zona institucional de presentación. Su elección debe quedar registrada y verificada. No se agrega una restricción de un documento independiente por aprendiz/tipo.

## 6. Datos sintéticos de prueba
Preparar únicamente para un entorno aislado. Las cuentas de prueba usarán direcciones controladas por el equipo; los alias siguientes no son correos ni credenciales.

| Alias | Preparación | Uso |
|---|---|---|
| Instructor-A | Asociado a Ficha-A | Acceso permitido a ámbito A. |
| Instructor-B | Asociado a Ficha-B | Comprobar aislamiento entre instructores. |
| Aprendiz-A | Registro importado de Ficha-A y cuenta vinculada | Consulta y firma propias. |
| Aprendiz-B | Registro importado de Ficha-B y cuenta vinculada | Intento de acceso cruzado. |
| Aprendiz-SinCuenta | Registro importado sin vínculo | Pruebas posteriores de autorregistro. |
| Documento-A-v1 | Documento de Aprendiz-A, sin aceptación | Firma, consulta y reintentos. |
| Documento-A-v2 | Corrección vinculada que conserva v1 | Conflictos y firma de versión exacta. |

Los contenidos deben identificarse como ficticios. La preparación controlada del entorno no crea una función de administración del MVP. No utilizar los datos para envíos externos salvo un ensayo deliberado a destinatarios de prueba.

## 7. Escenarios tempranos de verificación
Los identificadores E0-Pxx pertenecen a este anexo; no reemplazan los TEST del TRD. **Todos están no ejecutados.**

| Caso | Preparación y acción | Resultado esperado | Evidencia / relación |
|---|---|---|---|
| E0-P01 | Obtener proyecto en ambiente limpio y seguir README. | Dependencias y compilación reproducibles; versiones registradas. | Log depurado; TEST-018. |
| E0-P02 | Aplicar migración inicial sobre base de prueba vacía. | Esquema y permisos creados sin intervención manual no documentada. | Registro de migración; T-E0-03. |
| E0-P03 | Instructor-A consulta recurso A; repetir como Instructor-B y anónimo mediante solicitud directa. | Solo acceso autorizado; rechazo sin contenido ajeno. | Respuestas depuradas; TEST-003. |
| E0-P04 | Solicitar objeto privado como propietario y como tercero, usando referencia conocida. | Permiso verificado; no acceso público ni acceso ajeno. | Prueba de descarga; TEST-003/019. |
| E0-P05 | En celular real: abrir documento completo, dibujar, limpiar, redibujar y confirmar. Volver a consultar. | Trazo utilizable, aceptación explícita y evidencia persistida en versión correcta. | Dispositivo, SO, navegador y resultado; TEST-009/017. |
| E0-P06 | Interrumpir red antes/durante confirmación de firma. | Sin éxito falso; resultado incierto consultable; reintento no duplica aceptación. | Secuencia y registros; TEST-009/012. |
| E0-P07 | Presentar v1 para firma y crear v2 antes de confirmar. | Conflicto comunicado; nueva revisión necesaria; trazo no trasladado. | Identificadores de versión y resultado; TEST-010. |
| E0-P08 | Repetir la misma intención de escritura; luego reutilizar clave con contenido distinto. | Un resultado para intención repetida; conflicto para contenido diferente. | Conteo y respuesta; TEST-012. |
| E0-P09 | Simular fallo entre almacenamiento de objeto y transacción; ejecutar conciliación. | Referencias confirmadas válidas; temporales identificables; objetos vinculados preservados. | Estado antes/después; TEST-012/019. |
| E0-P10 | Renderizar cada formato con campos largos, varios compromisos y varias páginas. | Campos íntegros y legibles, estructura institucional conservada, sin recortes. | Comparación con copias oficiales; T-E0-06. |
| E0-P11 | Recorrer interfaz de prueba con teclado y tecnología de apoyo acordada. | Documentación de barreras; cumplimiento evaluado contra criterio aprobado. | Procedimiento y matriz; TEST-017. |
| E0-P12 | Ejecutar pipeline con caso válido y con fallo deliberado. | Compilación/pruebas informan resultado y el fallo impide considerar verificada la revisión. | Ejecuciones y revisión de capas; TEST-018. |

E0-P11 no prueba accesibilidad completa del producto. La emulación de un teléfono no sustituye E0-P05 en hardware real. Las pruebas de contrato simuladas no acreditan integración real con Supabase.

### Registro por ejecución
- Caso y tarea: pendiente.
- Commit/versión, migraciones y ambiente: pendiente.
- Dispositivo, sistema operativo y navegador/versiones, cuando aplique: pendiente.
- Precondiciones, pasos y resultado esperado: según caso, detallados al ejecutarlo.
- Resultado observado: pendiente.
- Estado: no ejecutada / aprobada / fallida / bloqueada.
- Evidencia depurada, defecto o decisión relacionada: pendiente.
- Fecha, ejecutor y revisor: pendientes.

## 8. Recursos y decisiones para comenzar
“No confirmado” significa que no se ha comprobado su disponibilidad para esta ejecución; no significa que el recurso no exista.

| Recurso o decisión | Información necesaria | Estado | Qué permite avanzar |
|---|---|---|---|
| Lugar de trabajo | Carpeta/repositorio y equipo donde se ejecutará Flutter; si ya existe código, identificarlo antes de crear otro. | No confirmado | T-E0-02 y ejecución reproducible. |
| Herramientas | Versiones instaladas de Flutter/Dart, Git y herramientas backend; seleccionar las compatibles y registrar evidencia. | Pendiente de inventario | T-E0-02/07. |
| Entorno Supabase | Proyecto de desarrollo o entorno local elegido, acceso autorizado y responsable. | No confirmado | T-E0-04 y persistencia real de firma. |
| Firebase Hosting | Proyecto de prueba y mecanismo de publicación cuando se valide acceso web desde dispositivos. | No confirmado | Ensayo web alojado; el trabajo local puede iniciar antes. |
| Formatos institucionales | Copias vigentes del llamado, GOR-F-084 V02 y GD-F-011, con instrucciones de diligenciamiento. | Pendientes de incorporación a E0 | T-E0-06 y aceptación de fidelidad. |
| Dispositivos | Celular(es) y computador disponibles, SO y navegador; necesidades de accesibilidad. | No confirmado | Matriz y pruebas T-E0-05. |
| Responsables | Persona de producto, ejecución técnica, revisión y operación; pueden coincidir. | Por asignar | Decisiones y aceptación verificables. |
| Política de secretos | Configuración por mecanismos seguros del entorno, sin incluir credenciales en documentos ni chat. | Por concretar | Uso seguro de servicios. |
| Copias de evidencia | Ubicación de informes depurados y responsable de revisión. | Por concretar | Revisión de H0. |

Para pruebas táctiles, preparar inicialmente un escritorio y al menos un celular real disponible; esa selección es una propuesta de ensayo, no la matriz definitiva de soporte. Si la población utiliza Android e iOS, la matriz final deberá considerar ambos antes de afirmar compatibilidad con ellos.

### Decisiones que no es necesario resolver para preparar E0
Las generaciones repetidas, anulaciones, traslados de ficha y seguimiento de compromisos corregidos permanecen pendientes según el PLAN. E0 puede preparar contratos y pruebas sin implementar esos comportamientos ni imponer restricciones que los resuelvan indirectamente.

## 9. Criterios de cierre H0
E0 se presenta para cierre cuando exista evidencia de:

- [ ] Fuentes identificadas y matriz completa de CA con pruebas o bloqueos explícitos.
- [ ] Repositorio y compilación reproducible con herramientas fijadas.
- [ ] Contratos iniciales revisados y migración reproducible.
- [ ] Autorización de servidor y almacenamiento privado comprobados.
- [ ] Recorrido completo de firma probado en dispositivo real, con fallos y concurrencia.
- [ ] Formatos contrastados con copias institucionales vigentes.
- [ ] Análisis, compilación y pruebas mínimas ejecutables de forma repetible.
- [ ] Decisiones y limitaciones registradas; revisión del responsable.

Si falta evidencia de firma real o de fidelidad documental, E0 permanece abierta. Las tareas independientes pueden avanzar; eso no equivale a aceptación integral. El inicio de trabajos de E1 requiere que sus contratos y decisiones concretas estén disponibles, conforme a las dependencias del PLAN.

## 10. Estado de esta preparación y siguiente acción
**Completado:** desglose operativo de T-E0-01–07, propuesta de organización, lista de contratos, conjunto sintético, doce escenarios tempranos, recursos necesarios y lista de cierre.

**Pendiente de ejecución:** repositorio, herramientas, contratos físicos, migraciones, servicios, prototipo, matriz completa de CA y pruebas. No se modificaron los cuatro documentos base.

**Primer paso práctico:** identificar la carpeta/repositorio y el equipo de trabajo; incorporar los formatos y registrar los dispositivos disponibles. Con esos datos se puede iniciar T-E0-01/02 y organizar las validaciones que necesitan recursos externos.



## Registro complementario confirmado — 04-11-2026 (DC-07/DC-08)

**Fuente:** instrucción expresa de Luis Fernando Corredor Mora en la revisión de E0. Se conserva la versión documental existente; este registro actualiza únicamente las decisiones indicadas y no aprueba las propuestas físicas del nuevo anexo.

- **DC-07, confirmada:** identificación del aprendiz como texto, con ceros iniciales; retirar espacios exteriores antes de validar; exigir uno o más dígitos ASCII 0–9. Rechazar vacío, espacios internos, letras, puntos, guiones y otros caracteres; no convertir a número ni limpiar caracteres inválidos silenciosamente. Error localizado por fila. ` 00123456 ` se acepta como `00123456`; `0012 3456`, `1.234.567` y solo espacios se rechazan. Aplicar la misma regla al dato de identificación utilizado en autorregistro. El conjunto exacto de espacios exteriores se precisa como propuesta P-06 del anexo, sin ampliarlo silenciosamente.
- **DC-08, confirmada:** Luis Fernando Corredor Mora asume inicialmente la habilitación de instructores y asignación de fichas. No se crea rol administrador ni interfaz administrativa del MVP. El mecanismo técnico y sus controles son propuestas para revisión.
- **Ficha pendiente:** no se han aprobado caracteres ni normalización de numero_ficha. P-01 del anexo propone una política explícita; no se aplica automáticamente DC-07 a ese campo ni se bloquean relaciones independientes.
- **Alcance autorizado:** especificación física inicial de identidad, fichas e importación, autorización, auditoría, idempotencia, procedimiento operativo y casos de prueba. Entregar para revisión antes de convertir en migración; sin ejecutar cambios ni crear recursos Supabase.
- **Pendientes conservados:** generaciones independientes repetidas, acceso histórico ante traslados/cambios de responsabilidad, autoridad y efectos de anulaciones y continuidad del seguimiento de compromisos corregidos. No se resuelven mediante restricciones implícitas.
- **Formatos:** se identificaron ejemplos diligenciados GOR-F-084 V02 y GD-F-011; no está confirmada su incorporación a Docs ni su vigencia institucional. Se requieren copias/instrucciones validadas para fidelidad documental, sin bloquear el núcleo independiente. No se inventan campos definitivos.

**Entregable vigente:** [TRAZA_E0_ESPECIFICACION_FISICA_INICIAL.md](TRAZA_E0_ESPECIFICACION_FISICA_INICIAL.md), v0.4 para revisión técnica, 06-11-2026; decisiones funcionales actualizadas en el registro final de esta fecha. FI-01–39 previstos, no ejecutados. Primera migración: [propuesta v0.1](TRAZA_E0_PRIMERA_MIGRACION_PROPUESTA.md), sin SQL.

Avance documental de T-E0-03: especificación v0.4 preparada para revisión técnica; no se declara tarea terminada ni H0 cerrado. El responsable de habilitación/asociaciones deja de estar por asignar; formatos, entorno, políticas y verificación siguen pendientes según dependencia.


## Decisiones confirmadas y secuencia E0 — 06-11-2026

**Fuente:** aprobación expresa de Luis Fernando Corredor Mora. Este registro actualiza los pendientes históricos de 04/05-11-2026 solo en lo resuelto aquí; no cambia generaciones repetidas, traslados/acceso histórico, anulaciones ni continuidad de seguimiento de compromisos corregidos. DC-07/DC-08 permanecen confirmadas.

- **P-08 aprobada:** impedir duplicación y conservar causa exacta interna restringida. Ficha inexistente/no autorizada: número de fila y «No se pudo validar la ficha para esta fila», sin distinguir ambas ni buscar duplicados globales. Ficha autorizada y permiso vigente verificable sobre aprendiz existente: número y «Identificación ya registrada». Otros casos de duplicidad: número y «No fue posible incorporar esta fila», sin datos ajenos ni motivo de duplicidad. Aplicar en validación, confirmación, nuevas consultas, descarga, contadores y caché con permisos actuales. La ficha de entrada no acredita acceso al existente. Mensaje genérico reduce exposición, no elimina toda inferencia. Sin canal de revisión inventado; DC-08 no autoriza consultar otras fichas. PRD CA-02.5/6 ajustados; CA-02.7 conservado.
- **P-01/P-06 confirmadas:** identificación y ficha textuales de uno o más dígitos ASCII 0–9, con ceros preservados; retirar exclusivamente U+0020 exterior, rechazar vacío, espacios internos, tabs y otros caracteres. Misma normalización en catálogo y búsqueda de ficha en importación; también en identificación de autorregistro.
- **P-04 aprobada con ajuste:** agrupar filas válidas autorizadas por id normalizado; coincidencia de nombre y ficha según contrato: primera candidata y siguientes duplicadas internas. Diferencia de nombre o ficha: rechazar todas las filas del grupo conflictivo e indicar números de fila para corregir. Filas inválidas/ajenas se tratan aparte, no bloquean válidas ni exponen datos a través de agrupación. Otras identificaciones continúan. Distinto de P-08 frente a datos ya persistidos. La comparación concreta de nombre sigue como precisión técnica propuesta en §6.1 del anexo, no se deduce su aprobación.
- **P-05:** depuración productiva condicionada a política institucional; plazo pendiente. Desarrollo con datos sintéticos y plazos de ensayo explícitos, sin convertirlos en política productiva.
- **Primera migración:** alcance/secuencia confirmados, base técnica privada PostgreSQL; identidad, fichas, asociaciones e importación en incremento posterior. Diseño de objetos y permisos todavía para revisión; no se autoriza generar/ejecutar SQL ni crear recursos.

Referencias vigentes: [especificación física v0.4](TRAZA_E0_ESPECIFICACION_FISICA_INICIAL.md), para revisión técnica, FI-01–39 previstos; [primera migración propuesta v0.1](TRAZA_E0_PRIMERA_MIGRACION_PROPUESTA.md), M1-01–12 previstos. P-02/03/07, precisión de comparación de nombre, plazo productivo de P-05 y validaciones técnicas permanecen pendientes. No hay pruebas funcionales ejecutadas ni H0 cerrado.
