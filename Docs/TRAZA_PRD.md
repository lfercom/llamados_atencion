# TRAZA
## Product Requirements Document (PRD)

**Producto:** Sistema Integral de Gestión de Llamados de Atención y Seguimiento Académico
**Nombre corto:** TRAZA
**Versión:** 1.0
**Estado:** Aprobado
**Fecha:** 21 de octubre de 2026  
**Actualización documental:** 04-11-2026 — ajustes de revisión cruzada; se conserva v1.0 y el alcance funcional aprobado.
**Fuente:** Instructor: Luis Fernando Corredor Mora

---

## 1. Propósito del documento
Este PRD define el problema, los objetivos, los usuarios, el alcance funcional, las reglas de negocio, las restricciones y las condiciones de cumplimiento de TRAZA. Constituye la referencia funcional para orientar el diseño técnico, la planificación, el desarrollo, las pruebas y la aceptación del producto.

Este documento define **qué debe resolver y hacer el producto**. Las decisiones de implementación se detallarán en el TRD y la secuencia de construcción en el PLAN.

## 2. Resumen ejecutivo

TRAZA es una aplicación web orientada a centralizar la gestión de los llamados de atención y el seguimiento académico de los aprendices del SENA. Permitirá a los instructores registrar y consultar actuaciones, generar —por decisión expresa— los planes de mejoramiento y el Formato de comunicación al aprendiz, documentar compromisos y conservar la trazabilidad de los documentos, firmas, observaciones y comunicaciones.

El MVP incluirá dos roles: Instructor y Aprendiz. Los aprendices podrán autorregistrarse mediante la coincidencia de su número de identificación con un registro previamente importado, consultar únicamente sus propios documentos y firmar llamados de atención y planes de mejoramiento mediante una firma manuscrita capturada en pantalla táctil. El acceso de los instructores estará limitado a las fichas previamente asociadas a su responsabilidad.

La disponibilidad documental dependerá del conteo acumulado de llamados por aprendiz: dos llamados habilitan la opción de generar el Plan de mejoramiento 1; tres, la opción de generar el Plan de mejoramiento 2; y cuatro, la opción de generar el Formato de comunicación. Ningún documento se generará automáticamente por alcanzar el umbral. Cuando se genere el Formato de comunicación, TRAZA iniciará su envío por correo electrónico a Coordinación Académica y registrará el resultado y los posibles fallos.

TRAZA conservará la integridad y el historial de las actuaciones, sin determinar automáticamente faltas o sanciones ni sustituir las decisiones del instructor o de las instancias competentes. Las capacidades de inteligencia artificial, las integraciones externas no aprobadas y los comportamientos adicionales para llamados posteriores al cuarto quedan fuera del MVP.

## 3. Problema y oportunidad

### 3.1 Problema

Actualmente, los instructores del Servicio Nacional de Aprendizaje (SENA) gestionan los llamados de atención a los aprendices mediante formatos físicos y hojas de cálculo, lo que dificulta centralizar la información, conservar los registros y realizar un seguimiento oportuno de cada caso.

El procedimiento requiere controlar la acumulación de llamados de atención de cada aprendiz: al acumular dos llamados, el instructor podrá generar el primer plan de mejoramiento; al acumular tres, podrá generar el segundo plan; y al acumular cuatro, podrá generar el Formato de comunicación al aprendiz. La generación de estos documentos será una decisión del instructor y no se realizará automáticamente. El Formato de comunicación podrá incluir los motivos correspondientes y las normas presuntamente infringidas del Reglamento del SENA, de acuerdo con el formato institucional.

Esta gestión manual genera los siguientes problemas:

- **Dispersión y pérdida de información:** los registros se encuentran en diferentes soportes y pueden extraviarse.

- **Seguimiento manual:** el conteo de llamados de atención y la identificación de las actuaciones correspondientes dependen de verificaciones realizadas por los instructores.

- **Carga administrativa:** el registro, la búsqueda y la elaboración de documentos requieren tiempo adicional.

- **Dificultad de trazabilidad:** no siempre resulta sencillo reconstruir cronológicamente el historial de actuaciones de cada aprendiz.

- **Elaboración manual de comunicaciones:** preparar los documentos de convocatoria requiere consultar antecedentes e identificar las disposiciones reglamentarias pertinentes.

### 3.2 Oportunidad

Esta situación representa una oportunidad para desarrollar una aplicación que centralice y facilite la gestión de los llamados de atención, los planes de mejoramiento y las comunicaciones asociadas. La solución podrá incorporar inteligencia artificial para apoyar la consulta del Reglamento del SENA, la preparación de documentos y el análisis de antecedentes, manteniendo la validación y las decisiones correspondientes bajo supervisión humana.

### 3.3 Propuesta de valor

Desarrollar una aplicación web que centralice y facilite la gestión de los llamados de atención a los aprendices del SENA, permitiendo registrar y consultar su historial, realizar seguimiento a los planes de mejoramiento y preparar las comunicaciones asociadas al proceso.

La aplicación incorporará mecanismos de apoyo al control de las reglas de negocio y facilitará al instructor la generación de documentos cuando corresponda. Las capacidades de inteligencia artificial para consultar el Reglamento del SENA o apoyar la elaboración de documentos se evaluarán en futuras iteraciones y no forman parte del MVP.

Con ello, se busca reducir la carga administrativa de los instructores, disminuir los riesgos de pérdida e inconsistencia de la información y mejorar la trazabilidad, la oportunidad y la confiabilidad del proceso de seguimiento de los aprendices.

### 3.4 Visión del producto

Desarrollar TRAZA como una aplicación web para apoyar a los instructores del SENA en la gestión y el seguimiento de los llamados de atención a los aprendices, centralizando la información y facilitando el control de las actuaciones asociadas, desde el registro inicial hasta las comunicaciones derivadas del proceso.

La solución facilitará el registro, la consulta y el seguimiento de las actuaciones, así como la generación de documentos por decisión del instructor. Mantendrá la trazabilidad documental y la protección de la información. Las capacidades de inteligencia artificial se consideran una posible evolución posterior y no se incluyen en el MVP.

## 4. Objetivos

### 4.1 Objetivo general

Desarrollar TRAZA, un sistema integral que permita gestionar y centralizar los llamados de atención, realizar el seguimiento de los planes de mejoramiento y mantener la trazabilidad de las actuaciones relacionadas con los aprendices del SENA, facilitando el control de antecedentes, la aplicación de los procedimientos establecidos en el Reglamento del Aprendiz y la generación oportuna de comunicaciones para las instancias institucionales competentes.

### 4.2 Objetivos específicos

1. **Centralizar la información:** Registrar y organizar los llamados de atención y las actuaciones relacionadas con los aprendices, facilitando su consulta y administración desde una plataforma unificada.

2. **Gestionar los planes de mejoramiento:** Registrar los compromisos establecidos con los aprendices, realizar seguimiento a su cumplimiento y documentar los resultados obtenidos.

3. **Garantizar la trazabilidad de las actuaciones:** Mantener el historial de los llamados de atención, los planes de mejoramiento y las actuaciones asociadas a cada aprendiz, permitiendo consultar sus antecedentes y la secuencia de los eventos registrados.

4. **Facilitar el seguimiento de los casos:** Identificar la acumulación de llamados de atención, los incumplimientos de los planes de mejoramiento y las situaciones que requieran atención o seguimiento institucional.

5. **Apoyar los procedimientos institucionales:** Facilitar la preparación y generación de comunicaciones relacionadas con los llamados de atención y las solicitudes dirigidas a las instancias competentes, conforme a los procedimientos establecidos en el Reglamento del Aprendiz del SENA.

6. **Controlar el acceso y proteger la información:** Gestionar los permisos de acceso según los roles autorizados y preservar la confidencialidad, integridad y disponibilidad de la información registrada.

## 5. Alcance del producto y funcionalidades del MVP

Este apartado delimita las capacidades que se implementarán en la primera versión de TRAZA, denominada **Producto Mínimo Viable (MVP)**. Define las funcionalidades incluidas, las reglas de negocio que condicionan su comportamiento, las capacidades transversales, las exclusiones y las condiciones generales para verificar el cumplimiento del alcance.

El detalle verificable del comportamiento de cada funcionalidad se desarrolla en el apartado 7, mediante los requisitos funcionales y sus criterios de aceptación. Este apartado establece el alcance funcional y no sustituye dichos requisitos.

### 5.1. Alcance del producto

TRAZA —Sistema Integral de Gestión de Llamados de Atención y Seguimiento Académico— permitirá centralizar el registro y la consulta de los llamados de atención de los aprendices del SENA, gestionar los planes de mejoramiento, registrar el seguimiento de sus compromisos, generar el Formato de comunicación al aprendiz y conservar la trazabilidad de las actuaciones y los documentos relacionados.

El MVP contará con dos roles:

- **Instructor:** responsable de registrar y consultar las actuaciones académicas de los aprendices bajo su ámbito de responsabilidad; diligenciar y generar los documentos institucionales; registrar compromisos, observaciones y evidencias de seguimiento; configurar el correo institucional de Coordinación Académica; y consultar y atender los resultados de los envíos.
- **Aprendiz:** podrá autorregistrarse, consultar exclusivamente sus propios llamados de atención y documentos relacionados, y firmar los llamados de atención y los planes de mejoramiento mediante una firma manuscrita capturada en la pantalla táctil de su dispositivo.

Para habilitar el autorregistro, TRAZA permitirá importar los datos básicos de los aprendices mediante archivos CSV o JSON. El registro incluirá el número del documento de identidad, el nombre completo y el número de ficha de formación. La cuenta del aprendiz se vinculará con el registro importado cuando coincida el número de identificación ingresado; no se exigirá un mecanismo adicional de verificación de identidad en el MVP.

El acceso del instructor estará restringido a los aprendices cuyas fichas estén previamente asociadas a su ámbito de responsabilidad. Esta asociación deberá configurarse antes de habilitar el acceso; la administración de dichas asociaciones mediante una interfaz no forma parte del MVP.

El sistema ofrecerá al instructor opciones para generar el Plan de mejoramiento 1 cuando se acumulen dos llamados de atención, el Plan de mejoramiento 2 cuando se acumulen tres y el Formato de comunicación al aprendiz cuando se acumulen cuatro. La generación de estos documentos será manual y potestativa del instructor; alcanzar un umbral no producirá la generación automática del documento.

Después de generar el Formato de comunicación, TRAZA iniciará su envío automático como archivo adjunto al correo institucional de Coordinación Académica seleccionado por el instructor para esa comunicación. El sistema conservará el documento y registrará los intentos y resultados de envío, incluidos los fallos y los reintentos.

TRAZA facilitará la gestión documental y el seguimiento, pero no determinará automáticamente la existencia o calificación definitiva de una falta, ni impondrá sanciones ni sustituirá las decisiones del instructor o de las instancias institucionales competentes.

### 5.2. Funcionalidades incluidas en el MVP

El MVP comprende las siguientes nueve funcionalidades principales. Cada funcionalidad agrupa capacidades relacionadas y se vincula con los requisitos funcionales detallados en el apartado 7.

#### MVP-01. Autenticación, autorregistro y control de acceso

**Descripción:** Permitir el acceso a TRAZA mediante cuentas individuales y aplicar permisos diferenciados según el rol del usuario.

**Funcionalidades incluidas:**

- Inicio y cierre de sesión mediante credenciales individuales.
- Autorregistro de aprendices mediante correo electrónico, contraseña y número de identificación.
- Recuperación de contraseña.
- Vinculación de la cuenta del aprendiz con el registro previamente importado cuando coincida el número de identificación.
- Aplicación de permisos diferenciados para los roles Instructor y Aprendiz.
- Restricción del acceso a las operaciones y los datos según el rol, la propiedad del registro y el ámbito de responsabilidad autorizado.
- Manejo de errores de autenticación, registro y recuperación de contraseña.

**Resultado esperado:** Los usuarios pueden ingresar de manera controlada y acceder únicamente a las funcionalidades y los datos autorizados para su rol.

**Trazabilidad:** RF-01.

#### MVP-02. Importación y consulta de aprendices

**Descripción:** Permitir la carga masiva de los datos básicos de los aprendices mediante archivos CSV o JSON, validarlos y consultar los registros incorporados.

**Funcionalidades incluidas:**

- Carga de archivos CSV y JSON desde la interfaz del sistema.
- Validación de la estructura del archivo y de los campos obligatorios.
- Identificación de registros incompletos, inválidos o duplicados.
- Presentación del resultado de la validación antes de confirmar la importación.
- Inserción de registros válidos que no existan previamente.
- Prevención de duplicados por número de documento de identidad.
- Presentación de un reporte de registros procesados, insertados y rechazados, indicando la razón de cada rechazo.
- Consulta de los aprendices importados.
- Uso del número de ficha para aplicar las restricciones de acceso del instructor.

**Estructura mínima del archivo:**

| Campo | Descripción | Condición |
|---|---|---|
| `id` | Número del documento de identidad del aprendiz. | Obligatorio y único. |
| `nombre_completo` | Nombres y apellidos del aprendiz. | Obligatorio. |
| `numero_ficha` | Número de la ficha de formación a la que pertenece el aprendiz. | Obligatorio para aplicar el control de acceso por ficha. |

El campo `id` se almacenará como texto para preservar su representación original. Podrá corresponder a una tarjeta de identidad, cédula de ciudadanía, cédula de extranjería u otro documento admitido por el sistema. El campo `numero_ficha` se utilizará para determinar si el instructor está autorizado para consultar y gestionar la información del aprendiz.

La relación entre instructores y fichas deberá quedar configurada previamente por un responsable autorizado como parámetro operativo fuera de la interfaz funcional del MVP. Si una ficha no tiene una asociación configurada, el instructor no podrá acceder a sus aprendices hasta que se regularice la configuración. La importación no creará cuentas de usuario ni concederá acceso automáticamente.

**Resultado esperado:** TRAZA dispone de un registro centralizado de aprendices que permite validar el autorregistro y aplicar las restricciones de acceso por ficha.

**Trazabilidad:** RF-01 y RF-02, según el desglose funcional vigente.

#### MVP-03. Registro y consulta de llamados de atención

**Descripción:** Permitir que el instructor diligencie el formato institucional de llamado de atención, registre la actuación y la consulte posteriormente.

**Funcionalidades incluidas:**

- Registro de la información requerida por el formato institucional, incluidos fecha, grupo, número de orden, lugar, identificación del aprendiz, motivo e instructor responsable.
- Registro de las observaciones del aprendiz cuando correspondan al formato.
- Generación y conservación del documento diligenciado.
- Asociación del llamado con el aprendiz y con los antecedentes y documentos relacionados.
- Consulta de los llamados de atención por parte del instructor autorizado.
- Consulta por parte del aprendiz autenticado exclusivamente de sus propios llamados.
- Visualización del documento completo antes de firmarlo.
- Edición del llamado antes de la firma conforme a las reglas de autorización y trazabilidad definidas en el apartado 7.

**Resultado esperado:** Cada llamado queda registrado y asociado al aprendiz y al instructor responsable, y puede consultarse conforme a los permisos establecidos.

**Trazabilidad:** RF-03 y RF-09.

#### MVP-04. Gestión de planes de mejoramiento

**Descripción:** Permitir que el instructor decida y ejecute la generación del Plan de mejoramiento 1 o del Plan de mejoramiento 2, de acuerdo con la acumulación de llamados y utilizando los formatos institucionales aplicables.

**Funcionalidades incluidas:**

- Opción para generar manualmente el Plan de mejoramiento 1 cuando se acumulen dos llamados de atención.
- Opción para generar manualmente el Plan de mejoramiento 2 cuando se acumulen tres llamados de atención.
- Diligenciamiento de la información requerida por el formato institucional, incluida la información de reunión, agenda, objetivos y desarrollo cuando corresponda.
- Registro de varios compromisos o actividades en un mismo plan.
- Registro de fechas, responsables y demás información requerida por el formato.
- Conservación y consulta del documento generado.
- Asociación del plan con el aprendiz y las actuaciones que lo originaron.
- Firma manuscrita del aprendiz capturada en pantalla táctil, vinculada a la versión exacta del documento.
- Registro por parte del instructor de una observación por ausencia de firma cuando haya verificado que el aprendiz fue informado del documento y no encuentre la firma.

La disponibilidad de una opción de generación no implica que el documento se cree automáticamente. La decisión corresponde al instructor.

**Resultado esperado:** Los planes quedan asociados a sus actuaciones de origen, contienen los compromisos definidos y conservan la evidencia de aceptación cuando el aprendiz firma.

**Trazabilidad:** RF-04 y RF-08.

#### MVP-05. Seguimiento de compromisos de los planes de mejoramiento

**Descripción:** Permitir que el instructor registre y consulte el seguimiento realizado a los compromisos establecidos en los planes de mejoramiento.

**Funcionalidades incluidas:**

- Consulta de los compromisos registrados en cada plan.
- Registro de observaciones y evidencias de seguimiento.
- Registro del resultado de las verificaciones realizadas por el instructor.
- Asociación de cada seguimiento con el plan, el compromiso y el instructor responsable.
- Consulta del historial de seguimiento.
- Conservación de las actuaciones previas y trazabilidad de las correcciones o anulaciones autorizadas.

El sistema facilitará el registro y la consulta del seguimiento, pero no decidirá automáticamente si un compromiso se ha incumplido ni sustituirá el criterio del instructor.

**Resultado esperado:** El instructor puede documentar el seguimiento de cada compromiso y reconstruir su historial.

**Trazabilidad:** RF-05 y RF-09.

#### MVP-06. Generación del Formato de comunicación al aprendiz

**Descripción:** Permitir que el instructor genere manualmente el Formato de comunicación al aprendiz cuando se acumulen cuatro llamados de atención.

**Funcionalidades incluidas:**

- Disponibilidad de la opción de generación al alcanzar cuatro llamados acumulados.
- Diligenciamiento de los campos requeridos por el formato institucional GD-F-011.
- Incorporación de los datos del aprendiz y de los antecedentes que correspondan.
- Registro de los motivos de la comunicación y de las normas presuntamente infringidas cuando corresponda según el formato institucional.
- Conservación y consulta del documento generado.
- Asociación del documento con el aprendiz, los llamados y las actuaciones que lo originaron.
- Inicio del envío automático del documento una vez generado, conforme a MVP-07.

TRAZA no determinará automáticamente la existencia de una falta, su calificación definitiva ni la imposición de una sanción.

**Resultado esperado:** El instructor puede generar el documento institucional correspondiente, asociado a los antecedentes pertinentes y listo para su envío.

**Trazabilidad:** RF-06 y RF-07.

#### MVP-07. Configuración y envío automático del Formato de comunicación

**Descripción:** Enviar por correo electrónico el Formato de comunicación generado a la dirección institucional de Coordinación Académica configurada por el instructor y permitir consultar el resultado del envío.

**Funcionalidades incluidas:**

- Registro y actualización de la dirección institucional destinataria.
- Validación del formato de la dirección de correo.
- Inicio inmediato del envío automático después de generar el Formato de comunicación, sin una confirmación adicional para enviarlo.
- Inclusión del documento generado como archivo adjunto; este será el mecanismo de entrega documental del MVP.
- Registro del documento, destinatario, fecha y hora de cada intento y resultado informado por el servicio de correo.
- Registro de errores e información al instructor cuando el envío no se complete.
- Consulta de los intentos y resultados disponibles.
- Reintento del envío fallido utilizando el mismo documento, sin generar nuevamente el Formato de comunicación ni duplicar la actuación documental.
- Si no hay un destinatario válido o el servicio no está disponible, conservación del documento y registro del envío como no completado. Una vez corregida la configuración o restablecido el servicio, el instructor podrá reintentar el envío del mismo documento.

El resultado satisfactorio informado por el servicio de correo no se interpretará como prueba de que el destinatario recibió, abrió o leyó el mensaje.

**Resultado esperado:** El instructor puede consultar el estado conocido de los envíos, identificar los fallos y reintentar sin duplicar actuaciones.

**Trazabilidad:** RF-07 y RF-09.

#### MVP-08. Firma manuscrita y registro de aceptación del aprendiz

**Descripción:** Permitir que el aprendiz manifieste formalmente su aceptación de los llamados de atención y de los planes de mejoramiento mediante una firma manuscrita capturada en la pantalla táctil de su dispositivo.

**Funcionalidades incluidas:**

- Presentación del documento completo antes de firmar.
- Presentación de una indicación explícita sobre el significado de la acción de firmar.
- Captura de la firma manuscrita en pantalla táctil.
- Posibilidad de borrar y repetir el trazo antes de confirmar.
- Confirmación expresa del aprendiz antes de guardar la firma.
- Asociación de la firma con el aprendiz, el documento y la versión exacta mostrada para su aceptación.
- Conservación de la fecha y hora de la firma y de las evidencias técnicas definidas para la auditoría.
- Confirmación de éxito únicamente después de comprobar que la firma fue almacenada correctamente.
- Consulta posterior del documento firmado.
- Protección del documento firmado contra modificaciones o eliminaciones silenciosas.
- Registro por parte del instructor de una observación por ausencia de firma, siempre que haya verificado que el aprendiz fue informado y no encuentre la firma.

El sistema no ofrecerá al aprendiz una opción de autoservicio para registrar su negativa a firmar. La observación del instructor deberá conservar el texto registrado, la identificación del instructor, la fecha y hora y la referencia al documento. La ausencia de firma no equivale a aceptación.

**Resultado esperado:** La aceptación queda respaldada por una firma asociada a la versión exacta del documento, o el instructor puede dejar constancia de la ausencia de firma bajo las condiciones definidas.

**Trazabilidad:** RF-08 y RF-09.

#### MVP-09. Consulta del historial y trazabilidad documental

**Descripción:** Permitir consultar las actuaciones registradas para cada aprendiz y las relaciones entre llamados de atención, planes, compromisos, seguimientos, comunicaciones, firmas, observaciones y resultados de envío disponibles.

**Funcionalidades incluidas:**

- Consulta cronológica de los llamados de atención.
- Consulta de los planes de mejoramiento y sus compromisos.
- Consulta de las observaciones, evidencias y resultados de seguimiento.
- Consulta del Formato de comunicación y de las actuaciones que originaron su generación.
- Consulta de firmas y observaciones por ausencia de firma asociadas a cada documento.
- Consulta de los resultados e intentos de envío disponibles.
- Conservación del historial de actuaciones y de las correcciones o anulaciones autorizadas.
- Acceso del instructor únicamente al historial de aprendices cuyas fichas estén asociadas a su ámbito de responsabilidad.
- Consulta del aprendiz, en modo de solo lectura, exclusivamente de sus propios llamados y documentos relacionados autorizados.

Los llamados posteriores al cuarto también formarán parte del historial acumulado. Mientras no se definan y aprueben reglas adicionales, no se habilitarán opciones documentales nuevas por esos llamados.

**Resultado esperado:** El instructor dispone de un historial centralizado y trazable; el aprendiz puede consultar exclusivamente su propia información autorizada.

**Trazabilidad:** RF-09 y los requisitos funcionales que producen los documentos y eventos consultados.

### 5.3. Reglas de negocio del proceso

El MVP deberá respetar las siguientes reglas aprobadas:

- **RN-01. Registro del llamado:** el llamado se diligencia mediante el formato institucional y se registra en la base de datos. Los llamados no tendrán estados de ciclo de vida.
- **Criterio de acumulación:** los llamados se acumulan por aprendiz de manera continua, sin límite temporal y sin importar el tiempo transcurrido entre ellos.
- **RN-02. Segundo llamado acumulado:** al acumular dos llamados, el sistema ofrecerá al instructor la opción de generar el Plan de mejoramiento 1. La generación será manual.
- **RN-03. Tercer llamado acumulado:** al acumular tres llamados, el sistema ofrecerá al instructor la opción de generar el Plan de mejoramiento 2. La generación será manual.
- **RN-04. Cuarto llamado acumulado:** al acumular cuatro llamados, el sistema ofrecerá al instructor la opción de generar el Formato de comunicación al aprendiz. La generación será manual.
- **RN-05. Correspondencia documental:** cada documento conservará su relación con el aprendiz y con las actuaciones que lo originaron.
- **RN-06. Seguimiento:** el instructor controla el seguimiento y la verificación del cumplimiento de los compromisos.
- **RN-07. Aceptación:** la generación o consulta de un documento no constituye evidencia de aceptación del aprendiz.
- **RN-08. Responsabilidad institucional:** el sistema apoya la gestión documental y el seguimiento, pero no sustituye las decisiones del instructor ni de las instancias competentes.
- **RN-09. Trazabilidad:** las actuaciones, los documentos, las firmas, las observaciones, los intentos de envío y las correcciones o anulaciones autorizadas conservarán un historial verificable.
- **RN-10. Llamados posteriores al cuarto:** estos llamados se acumularán en el historial sin límite temporal. No generarán documentos automáticamente. Las actuaciones u opciones documentales adicionales permanecen pendientes de definición y aprobación.
- **RN-11. Envío automático:** después de generar el Formato de comunicación, el sistema iniciará su envío al correo institucional seleccionado para esa comunicación, registrará los intentos y resultados, informará los fallos y permitirá reintentos sin duplicar la actuación documental.
- **RN-12. Autorregistro:** cada aprendiz podrá crear su cuenta individual ingresando número de identificación, correo electrónico y contraseña. El número de identificación deberá coincidir con un registro previamente importado.
- **RN-13. Firma manuscrita:** el aprendiz podrá manifestar formalmente su aceptación de un llamado de atención o plan de mejoramiento mediante firma manuscrita capturada en pantalla táctil. La firma quedará vinculada al documento y a su versión exacta.
- **RN-14. Ausencia de firma:** el sistema no ofrecerá al aprendiz una opción para registrar su negativa. Si el instructor verifica que el aprendiz fue informado y no encuentra la firma, podrá registrar una observación asociada al documento que incluya el texto, la identificación del instructor, la fecha y hora y la referencia al documento. La ausencia de firma no equivale a aceptación.
- **RN-15. Integridad documental:** los documentos firmados no podrán modificarse ni eliminarse silenciosamente. Las correcciones autorizadas deberán conservar la evidencia original y su historial.
- **RN-16. Importación:** TRAZA permitirá importar datos básicos mediante archivos CSV o JSON.
- **RN-17. Identificación y ficha:** `id` corresponderá al número del documento de identidad y se almacenará como texto único. `numero_ficha` identificará la ficha de formación y será obligatorio para aplicar el control de acceso por ficha.
- **RN-18. Validación de importaciones:** los archivos se validarán antes de incorporar los registros. El sistema informará los registros insertados y rechazados, indicando la razón del rechazo.
- **RN-19. Vinculación de cuentas:** durante el autorregistro, la cuenta se vinculará con el registro importado cuando coincida el número de identificación ingresado.

**Decisiones funcionales confirmadas el 04-11-2026.** La importación admite únicamente aprendices de fichas previamente asociadas al instructor; se verifica el permiso por fila tanto al validar como al confirmar. Las filas no autorizadas se rechazan sin exponer datos de ámbitos ajenos y se conserva el procesamiento de filas válidas autorizadas.

Los correos destinatarios pertenecen a un conjunto limitado de direcciones institucionales disponibles, sin asociación a fichas. El instructor selecciona una dirección para la comunicación al preparar su envío. Para conservar el envío automático aprobado, la selección se presenta antes de confirmar la generación; tras generar y conservar el documento, el sistema inicia el envío sin una segunda confirmación. Si falta una selección válida, conserva el documento, registra envío no completado y permite seleccionar un destinatario y reintentar. Cada intento conserva una copia de la dirección efectivamente utilizada; no se deduce un destinatario a partir de la ficha ni de cambios posteriores del catálogo.

Las opciones documentales no generadas permanecen disponibles después de superar su umbral: Plan 1 desde dos llamados, Plan 2 desde tres y comunicación desde cuatro. La generación sigue siendo manual y potestativa. Con tres llamados pueden coexistir Plan 1 y Plan 2 pendientes; con cuatro o más se conservan las opciones pendientes de los tres tipos. Esto no crea tipos documentales nuevos para el quinto llamado. La cantidad de documentos independientes permitidos del mismo tipo sigue pendiente; no se aprueba una restricción de uno por aprendiz. Las correcciones mantienen versiones y trazabilidad.

### 5.4. Capacidades transversales del MVP

Las siguientes condiciones aplican a las funcionalidades del MVP donde corresponda. No constituyen módulos independientes ni sustituyen los requisitos funcionales y no funcionales que las desarrollan.

#### 5.4.1. Control de acceso y privacidad

- Las operaciones y consultas deberán respetar el rol autenticado, la propiedad del registro y el ámbito de responsabilidad autorizado.
- Cada aprendiz podrá acceder exclusivamente a su propia información y a las funciones autorizadas.
- Cada instructor podrá acceder únicamente a los aprendices cuyas fichas estén previamente asociadas a su responsabilidad.
- La importación de datos no creará cuentas ni concederá acceso automáticamente.
- El tratamiento de datos personales deberá respetar las políticas institucionales y las disposiciones aplicables.

#### 5.4.2. Integridad y trazabilidad documental

- Cada documento deberá conservar la relación con el aprendiz y las actuaciones que lo originaron.
- La firma deberá asociarse a la versión exacta del documento.
- Los documentos firmados no podrán modificarse ni eliminarse silenciosamente.
- Las correcciones o anulaciones autorizadas deberán preservar el original, la evidencia de firma y el historial de cambios.
- Los registros de seguimiento, las observaciones por ausencia de firma y los intentos de envío deberán conservar su trazabilidad.

#### 5.4.3. Manejo de errores y prevención de duplicados

- El sistema comunicará de forma comprensible los errores de validación, los fallos de almacenamiento, los problemas de conexión y las operaciones que no se hayan completado.
- No mostrará una operación como exitosa hasta que se haya confirmado su resultado.
- Los reintentos de envío utilizarán el documento ya generado y no crearán llamados, documentos ni actuaciones duplicados.
- Los resultados de importación deberán permitir identificar los registros aceptados y rechazados y las razones correspondientes.

#### 5.4.4. Confirmación de firma y envío

- La firma solo se considerará registrada cuando el almacenamiento haya sido confirmado.
- El sistema distinguirá entre un intento de envío, el resultado informado por el servicio de correo y la evidencia de recepción o lectura, si esta última llegara a estar disponible.
- La falta de firma no se interpretará como aceptación del documento.

#### 5.4.5. Usabilidad y estados de interfaz

- La interfaz deberá comunicar los estados de carga, validación, éxito, error y operación pendiente de forma comprensible.
- Las operaciones sensibles deberán presentar las confirmaciones que correspondan.
- No deberá mostrarse un mensaje de éxito cuando la operación no haya sido completada.
- Las capacidades técnicas de accesibilidad, compatibilidad, rendimiento, disponibilidad, respaldo y recuperación se especificarán en los requisitos no funcionales y en el TRD, según corresponda.

### 5.5. Funcionalidades excluidas del MVP

Las siguientes capacidades no forman parte del alcance inicial de TRAZA y no deberán interpretarse como compromisos de implementación:

- Firma biométrica mediante huella dactilar u otros mecanismos biométricos.
- Funcionalidades de inteligencia artificial para consultar el Reglamento del SENA, analizar antecedentes o apoyar la elaboración de documentos.
- Aplicación móvil nativa independiente; el acceso desde dispositivos móviles se realizará mediante la aplicación web.
- Envío de comunicaciones por WhatsApp, SMS u otros canales diferentes del correo electrónico definido.
- Integraciones con sistemas institucionales externos que no hayan sido aprobadas expresamente.
- Analítica predictiva y decisiones disciplinarias automatizadas.
- Determinación automática de la existencia de una falta, su calificación definitiva o la imposición de sanciones.
- Funciones para que el aprendiz registre, modifique o elimine llamados de atención, gestione planes de mejoramiento o administre otros usuarios.
- Interfaz para administrar cuentas de instructores, roles, permisos o asociaciones entre instructores y fichas.
- Comportamientos automáticos u opciones documentales adicionales para llamados posteriores al cuarto, hasta que se definan y aprueben las reglas correspondientes.

La exclusión de mecanismos biométricos no elimina la firma manuscrita capturada en pantalla táctil, que sí forma parte del MVP para los llamados de atención y los planes de mejoramiento.

### 5.6. Restricciones y consideraciones

- **Formatos institucionales:** el Plan de mejoramiento utilizará el formato **GOR-F-084, versión 02 (V02)** y el Formato de comunicación al aprendiz utilizará el formato **GD-F-011**. El llamado de atención deberá ajustarse al formato institucional vigente, que deberá incorporarse como anexo funcional antes de iniciar su implementación. Los formatos deberán conservar sus campos y estructura institucionales; cualquier cambio deberá reflejarse en la referencia documental del PRD.
- **Relación instructor-ficha:** la asociación entre cada instructor y las fichas bajo su responsabilidad deberá configurarse previamente por un responsable autorizado. La interfaz para administrar esta asociación no forma parte del MVP. Si la asociación no existe, el acceso a los aprendices de esa ficha deberá denegarse.
- **Importación:** el archivo de importación deberá incluir `id`, `nombre_completo` y `numero_ficha`. El identificador se almacenará como texto. Los registros duplicados no se insertarán nuevamente y deberán reportarse.
- **Autorregistro:** la coincidencia del número de identificación con un registro importado habilitará la vinculación de la cuenta. El MVP no exigirá un mecanismo adicional de verificación de identidad.
- **Acumulación y generación documental:** los llamados se acumularán por aprendiz sin límite temporal. Las opciones de generación se habilitarán al alcanzar dos, tres y cuatro llamados, según corresponda; la generación será manual y potestativa del instructor.
- **Firma y aceptación:** la firma manuscrita representa la manifestación formal de aceptación prevista en el MVP. Deberá quedar asociada al aprendiz y a la versión exacta del documento. Su implementación deberá ajustarse al procedimiento institucional aplicable.
- **Negativa o ausencia de firma:** solo el instructor podrá registrar la observación cuando haya verificado que el aprendiz fue informado y no encuentre la firma. La observación deberá incluir el texto, la identificación del instructor, la fecha y hora y la referencia al documento.
- **Correcciones documentales:** antes de la firma, las correcciones autorizadas deberán conservar la trazabilidad sin crear una nueva actuación cuando se trate de corregir el mismo documento. Después de la firma, el documento original y su firma deberán preservarse; la corrección deberá generar una nueva versión o documento relacionado, según el procedimiento autorizado.
- **Correo electrónico:** el envío se intentará inmediatamente después de generar el Formato de comunicación. Si no hay destinatario válido o el servicio no está disponible, el documento se conservará y el intento se registrará como no completado. Una vez corregida la configuración o restablecido el servicio, el instructor podrá reintentar el envío del mismo documento.
- **Responsabilidad institucional:** TRAZA facilitará el registro y el seguimiento documental, pero no reemplazará los procedimientos ni las decisiones de las instancias competentes.
- **Requisitos no funcionales:** los valores y criterios concretos de rendimiento, seguridad, disponibilidad, respaldo y recuperación, compatibilidad, mantenibilidad, auditoría y accesibilidad se definirán en el apartado correspondiente y en el TRD. Su mención en este apartado no sustituye la especificación de criterios verificables.

### 5.7. Criterios generales de aceptación del MVP

El alcance funcional del MVP se considerará cubierto cuando se verifique que:

1. Los usuarios pueden autenticarse y acceder únicamente a las funciones y los datos autorizados para su rol.
2. Los aprendices pueden autorregistrarse mediante la coincidencia de su número de identificación con un registro previamente importado.
3. El sistema permite importar archivos CSV o JSON con los campos requeridos, validar los datos, evitar duplicados y reportar los resultados.
4. El control de acceso del instructor restringe la consulta y gestión a los aprendices cuyas fichas estén previamente asociadas a su responsabilidad.
5. El instructor puede diligenciar, registrar y consultar los llamados de atención.
6. El sistema acumula los llamados por aprendiz y ofrece las opciones de generación documental al alcanzar dos, tres y cuatro llamados, sin generar documentos automáticamente.
7. El instructor puede generar planes de mejoramiento, registrar varios compromisos por plan y documentar su seguimiento.
8. El instructor puede generar el Formato de comunicación al aprendiz y el sistema inicia su envío automático como archivo adjunto al correo institucional seleccionado para esa comunicación.
9. El instructor puede consultar los intentos y resultados de envío, identificar los fallos y reintentar sin duplicar la actuación documental.
10. El aprendiz puede consultar exclusivamente sus propios llamados y documentos relacionados, y firmar llamados y planes mediante una firma manuscrita capturada en pantalla táctil.
11. La firma queda vinculada a la versión exacta del documento y el sistema confirma su almacenamiento antes de informar que la operación se completó.
12. El instructor puede registrar una observación por ausencia de firma bajo las condiciones establecidas, sin que dicha ausencia se interprete como aceptación.
13. Los documentos firmados conservan su integridad; las correcciones o anulaciones autorizadas preservan la evidencia original y el historial.
14. El instructor puede consultar el historial de llamados, planes, compromisos, seguimientos, observaciones, firmas y comunicaciones dentro de su ámbito de responsabilidad.
15. Los errores y las operaciones no completadas se comunican de manera comprensible y no se presentan como exitosas.
16. Las funcionalidades excluidas no se incorporan sin una decisión formal de cambio de alcance.
17. Las decisiones funcionales pendientes que condicionen un comportamiento se resuelven antes de implementar dicho comportamiento.

La verificación detallada se realizará mediante los requisitos funcionales y sus criterios de aceptación del apartado 7, los flujos de usuario y los casos de prueba que se definan en las siguientes etapas.

### 5.8. Matriz de trazabilidad entre funcionalidades del MVP y requisitos funcionales

La siguiente matriz establece la correspondencia principal entre las funcionalidades del MVP y los requisitos funcionales del apartado 7. La trazabilidad detallada se verificará contra los criterios de aceptación de cada requisito.

| Funcionalidad del MVP | Requisitos funcionales relacionados |
|---|---|
| MVP-01. Autenticación, autorregistro y control de acceso | RF-01 |
| MVP-02. Importación y consulta de aprendices | RF-01 y RF-02 |
| MVP-03. Registro y consulta de llamados de atención | RF-03, RF-08 y RF-09 |
| MVP-04. Planes de mejoramiento | RF-04, RF-08 y RF-09 |
| MVP-05. Seguimiento de compromisos de los planes de mejoramiento | RF-05 y RF-09 |
| MVP-06. Generación del Formato de comunicación al aprendiz | RF-06, RF-07 y RF-09 |
| MVP-07. Configuración y envío automático del Formato de comunicación | RF-07 y RF-09 |
| MVP-08. Firma manuscrita y registro de aceptación del aprendiz | RF-08 y RF-09 |
| MVP-09. Consulta del historial y trazabilidad documental | RF-09 |

Esta matriz expresa la relación principal, pero no reemplaza los requisitos funcionales, sus criterios de aceptación ni las reglas de negocio transversales. Si durante la auditoría del apartado 7 se modifica la numeración o se redistribuyen requisitos, la matriz deberá actualizarse para reflejar la correspondencia definitiva.

## 6. Usuarios, roles y permisos

### 6.1 Usuarios finales

Los usuarios finales de **TRAZA** son las personas que interactúan directamente con la plataforma para registrar, consultar y gestionar los llamados de atención de los aprendices, realizar el seguimiento correspondiente y formalizar las actuaciones previstas en el proceso académico.

Se identifican los siguientes perfiles de usuario:

| Usuario | Descripción | Necesidades principales |
|---|---|---|
| **Instructor** | Responsable de registrar los llamados de atención y gestionar las actuaciones de seguimiento académico asociadas a los aprendices bajo su responsabilidad. | Registrar llamados de atención, consultar el historial de cada aprendiz únicamente cuando su ficha esté asociada al instructor, gestionar las observaciones relacionadas con la firma, generar los documentos correspondientes y realizar el seguimiento de los planes de mejoramiento y demás actuaciones previstas. |
| **Aprendiz** | Persona vinculada al proceso de formación que puede consultar sus propios llamados de atención y realizar la firma correspondiente desde un dispositivo móvil. | Acceder de forma segura a sus llamados de atención, consultar su historial y firmar los registros que requieran esta formalización. |

**Consideraciones funcionales:**

- Cada aprendiz dispondrá de una cuenta de acceso mediante correo electrónico y contraseña.
- El instructor podrá gestionar las actuaciones correspondientes a los aprendices cuyas fichas estén asociadas a su ámbito de responsabilidad, de acuerdo con los permisos establecidos.
- Cada aprendiz únicamente podrá consultar sus propios llamados de atención y realizar las operaciones expresamente autorizadas para su perfil.
- La firma del aprendiz constituye la aceptación formal del llamado de atención y deberá quedar asociada al registro correspondiente.
- Si el instructor verifica que el aprendiz fue informado del documento y no encuentra la firma, podrá registrar una observación asociada al documento. La observación deberá incluir el texto registrado por el instructor, su identificación, la fecha y hora y la referencia al documento. La ausencia de firma no equivale a aceptación. La ausencia de firma no se interpretará como aceptación del registro.
- Una vez firmado un llamado de atención, el registro quedará disponible únicamente para consulta, sin posibilidad de modificarlo o eliminarlo.
- Cuando sea necesario corregir un documento firmado, deberá generarse una nueva versión o documento relacionado, conservando el registro original y su trazabilidad.
- La plataforma deberá aplicar las reglas de seguimiento académico a partir del historial de llamados de atención del aprendiz, facilitando la generación de los documentos y las comunicaciones correspondientes.
- El acceso a la información estará restringido según el rol del usuario y las responsabilidades que tenga asignadas.

La definición de estos perfiles constituye la base para establecer la matriz de permisos, los requisitos funcionales, los flujos de usuario y las políticas de autorización de la plataforma.

### 6.2. Matriz RBAC

TRAZA implementará un modelo de control de acceso basado en roles (*Role-Based Access Control*, RBAC), mediante el cual las operaciones disponibles estarán determinadas por el rol del usuario y las restricciones aplicables a cada registro.

La autorización deberá considerar tanto el rol del usuario como la propiedad del registro, las condiciones funcionales del documento y las reglas de negocio aplicables. La matriz define los permisos funcionales del MVP; las medidas técnicas para hacerlos cumplir se especificarán en el TRD.

| Funcionalidad / Permiso | Instructor | Aprendiz |
|---|:---:|:---:|
| Acceder a la plataforma | ✓ | ✓ |
| Iniciar y cerrar sesión | ✓ | ✓ |
| Recuperar contraseña propia | ✓ | ✓ |
| Autorregistrar una cuenta de aprendiz | ✗ | ✓ |
| Consultar los datos básicos de aprendices importados | ✓* | ✗ |
| Importar aprendices mediante CSV o JSON | ✓ | ✗ |
| Consultar el resultado de una importación | ✓ | ✗ |
| Registrar llamados de atención | ✓ | ✗ |
| Consultar llamados de atención | ✓* | ✓* |
| Consultar el detalle y documento completo de un llamado | ✓* | ✓* |
| Modificar un llamado de atención antes de su firma | ✓* | ✗ |
| Modificar o eliminar un llamado de atención firmado | ✗ | ✗ |
| Consultar el conteo acumulado de llamados de un aprendiz | ✓* | ✗ |
| Consultar las opciones de generación documental disponibles | ✓* | ✗ |
| Generar el Plan de mejoramiento 1 | ✓* | ✗ |
| Generar el Plan de mejoramiento 2 | ✓* | ✗ |
| Consultar planes de mejoramiento | ✓* | ✓* |
| Registrar y gestionar compromisos de los planes | ✓* | ✗ |
| Registrar observaciones, evidencias y resultados de seguimiento | ✓* | ✗ |
| Consultar el historial de seguimiento de compromisos | ✓* | ✗ |
| Generar el Formato de comunicación al aprendiz | ✓* | ✗ |
| Configurar o actualizar el correo institucional de Coordinación Académica | ✓ | ✗ |
| Consultar los intentos y resultados del envío del Formato de comunicación | ✓* | ✗ |
| Reintentar el envío fallido del Formato de comunicación | ✓* | ✗ |
| Firmar un llamado de atención propio | ✗ | ✓* |
| Firmar un plan de mejoramiento propio | ✗ | ✓* |
| Consultar la firma asociada a un documento propio | ✓* | ✓* |
| Registrar una observación por ausencia de firma | ✓* | ✗ |
| Consultar observaciones por ausencia de firma | ✓* | ✓* |
| Consultar el historial documental de un aprendiz | ✓* | ✓* |
| Consultar documentos y actuaciones relacionados con otros aprendices | ✓* | ✗ |
| Modificar o eliminar documentos firmados | ✗ | ✗ |
| Corregir o anular actuaciones mediante el procedimiento autorizado | ✓* | ✗ |
| Administrar cuentas, roles o permisos de otros usuarios | No definido en el MVP | ✗ |

**Convenciones:**

- **✓ Permitido:** operación autorizada dentro del alcance del rol.
- **✓\*** Condicionado: operación permitida únicamente cuando se cumplen las restricciones de propiedad, responsabilidad, firma, acumulación de llamados o demás reglas de negocio aplicables.
- **✗ No permitido:** operación no autorizada para el rol.
- **No definido en el MVP:** el alcance funcional actual no establece un permiso para esta operación; no deberá implementarse como capacidad adicional sin una decisión formal.

**Restricciones aplicables a la matriz:**

1. El instructor solo podrá gestionar o consultar información de los aprendices cuyas fichas estén asociadas previamente a su responsabilidad. La asociación instructor-ficha se configurará como parámetro operativo antes de habilitar el acceso; no se incluye en el MVP una interfaz para administrar usuarios, roles ni permisos. El sistema deberá denegar el acceso si la asociación no existe.
2. El aprendiz solo podrá consultar sus propios llamados de atención, planes de mejoramiento, documentos relacionados, firmas y observaciones autorizadas. No podrá acceder a información de otros aprendices.
3. El aprendiz podrá firmar únicamente sus propios llamados de atención y planes de mejoramiento cuando el documento esté disponible para firma.
4. La consulta de un documento por parte del aprendiz no le concederá permisos para modificarlo, eliminarlo ni alterar las actuaciones registradas.
5. Los documentos firmados no podrán modificarse ni eliminarse silenciosamente. Las correcciones o anulaciones autorizadas deberán conservar la evidencia original y su historial.
6. El instructor podrá registrar una observación por ausencia de firma únicamente cuando haya verificado que el aprendiz fue informado del documento y no encuentre la firma correspondiente. El registro deberá conservar el texto de la observación, la identificación del instructor, la fecha y hora y la referencia al documento. La ausencia de firma no equivale a aceptación.
7. La generación de planes de mejoramiento y del Formato de comunicación al aprendiz estará condicionada a las reglas de acumulación de llamados. La generación será manual y potestativa del instructor.
8. El acceso a observaciones de seguimiento y evidencias de los compromisos por parte del aprendiz no queda autorizado por esta matriz: se limita a la consulta de sus documentos y de las observaciones por ausencia de firma que estén asociadas a ellos. La consulta de los registros internos de seguimiento permanece restringida al instructor.
9. El permiso para corregir o anular actuaciones no autoriza a sobrescribir documentos firmados ni a eliminar su historial. El procedimiento específico deberá respetar las reglas de integridad documental.
10. La matriz no concede permisos para administrar cuentas de instructor, cambiar roles ni delegar autorizaciones, ya que estas capacidades no están definidas en el alcance aprobado del MVP.

La implementación técnica deberá aplicar estas restricciones en las operaciones del sistema y en el acceso a los registros, independientemente de la interfaz o del dispositivo utilizado.

### 6.3 Reglas de autorización

Las siguientes reglas determinan las condiciones que deberá cumplir la plataforma para permitir o impedir las operaciones relacionadas con los llamados de atención.

**Autenticación y acceso**

- Todo usuario deberá autenticarse antes de acceder a las funcionalidades protegidas de la plataforma.
- Cada usuario tendrá asociado un rol que determinará las operaciones que puede realizar.
- La plataforma deberá verificar tanto los permisos del rol como las restricciones aplicables al registro solicitado.
- Los permisos se aplicarán independientemente de la interfaz o del dispositivo utilizado para acceder al sistema.

**Gestión de llamados de atención**

- El instructor será responsable de registrar y gestionar los llamados de atención de los aprendices cuyas fichas estén asociadas a su ámbito de responsabilidad.
- El sistema deberá permitir consultar el historial de llamados de atención de cada aprendiz y determinar la secuencia necesaria para aplicar las reglas de seguimiento académico.
- El instructor podrá corregir un llamado de atención mientras no haya sido firmado. Cada corrección deberá dejar constancia en el historial de auditoría y no se contabilizará como un nuevo llamado. La firma se asociará a la versión exacta que el aprendiz haya revisado.
- Una vez firmado el llamado de atención, el sistema deberá impedir su modificación y eliminación, independientemente del rol del usuario.
- La corrección de un llamado de atención firmado deberá realizarse mediante una nueva versión o documento corregido vinculado al original, sin sobrescribirlo ni eliminar su historial. El documento original y su firma permanecerán consultables.

**Firma y ausencia de firma**

- El aprendiz podrá consultar y firmar únicamente los llamados de atención que le pertenezcan y estén habilitados para esta operación.
- La firma deberá quedar asociada al llamado de atención correspondiente y permitir identificar el registro formalizado.
- Una vez registrada la firma, el llamado de atención quedará bloqueado para modificaciones y eliminación.
- Si el instructor verifica que el aprendiz fue informado del llamado de atención y no encuentra la firma, podrá registrar una observación asociada al documento. La observación deberá incluir el texto registrado, la identificación del instructor, la fecha y hora y la referencia al documento. La ausencia de firma no equivale a aceptación.
- La plataforma deberá distinguir entre un llamado firmado y uno sin firma con observación registrada. La ausencia de firma no podrá interpretarse como aceptación.
- El instructor no podrá registrar una firma en nombre del aprendiz ni alterar una firma previamente registrada.

**Reglas de seguimiento académico**

- Cuando un aprendiz acumule dos llamados de atención, el sistema deberá ofrecer al instructor la opción de generar el Plan de mejoramiento 1.
- Cuando un aprendiz acumule tres llamados de atención, el sistema deberá ofrecer al instructor la opción de generar el Plan de mejoramiento 2.
- Cuando un aprendiz acumule cuatro llamados de atención, el sistema deberá ofrecer al instructor la opción de generar el Formato de comunicación al aprendiz.
- La generación del Plan de mejoramiento 1, del Plan de mejoramiento 2 y del Formato de comunicación al aprendiz será potestativa del instructor. El cumplimiento de las condiciones de seguimiento no deberá generar estos documentos automáticamente.
- Cuando el instructor genere el Formato de comunicación al aprendiz, el sistema deberá iniciar inmediatamente el envío del documento como archivo adjunto al correo institucional de Coordinación Académica seleccionado por el instructor para esa comunicación. Si no existe una dirección válida o el servicio no está disponible, deberá registrar el fallo, conservar el documento y permitir el reintento del mismo envío una vez resuelta la causa.
- Los documentos generados deberán conservar su relación con el aprendiz y con los llamados de atención que originaron la actuación correspondiente.

**Privacidad y trazabilidad**

- Cada aprendiz tendrá acceso exclusivamente a su propia información y a las funcionalidades autorizadas para su rol.
- El instructor solo podrá acceder a la información de los aprendices cuyas fichas estén previamente asociadas a su ámbito de responsabilidad.
- La plataforma deberá conservar la trazabilidad de las firmas, las observaciones por ausencia de firma, las correcciones documentales y las actuaciones que generen documentos de seguimiento.
- Los intentos de ejecutar operaciones no autorizadas deberán ser rechazados, sin permitir que la operación se complete parcialmente.
- La plataforma deberá proteger la información personal y académica mediante controles de acceso y medidas de seguridad acordes con las disposiciones aplicables.

Las reglas técnicas para implementar la autenticación, la autorización, el control de acceso a los registros y la protección de la integridad de los documentos se especificarán en el Documento de Requisitos Técnicos (TRD).

# 7. Requisitos funcionales y criterios de aceptación

Este apartado especifica el comportamiento funcional verificable del MVP de TRAZA. Cada requisito define la necesidad que debe resolver el sistema y los criterios que permitirán comprobar su cumplimiento.

Los requisitos se relacionan con las funcionalidades MVP descritas en el apartado 5. Las reglas de negocio transversales de este apartado complementan las reglas de negocio del punto 5; no deben interpretarse como funcionalidades adicionales ni contradecir el alcance aprobado.

## RF-01. Autenticación, autorregistro y control de acceso

**Historia de usuario**

Como usuario de TRAZA, quiero acceder al sistema mediante una cuenta individual para utilizar las funcionalidades autorizadas según mi rol y consultar únicamente la información que me corresponde.

**Criterios de aceptación**

- **CA-01.1. Inicio de sesión exitoso:** Dado que el usuario tiene una cuenta habilitada y credenciales válidas, cuando las ingresa, el sistema debe permitirle iniciar sesión y habilitar las funcionalidades correspondientes a su rol.
- **CA-01.2. Credenciales inválidas:** Cuando se ingresen credenciales incorrectas, el sistema debe rechazar el acceso e informar que no fue posible iniciar sesión, sin exponer información sensible.
- **CA-01.3. Cuenta no habilitada:** El sistema debe impedir el acceso cuando la cuenta no esté habilitada para iniciar sesión.
- **CA-01.4. Cierre de sesión:** Cuando el usuario cierre sesión, el sistema debe finalizarla e impedir el acceso posterior a funcionalidades protegidas sin una nueva autenticación.
- **CA-01.5. Autorregistro:** El sistema debe permitir que un aprendiz cree su cuenta ingresando número de identificación, correo electrónico y contraseña.
- **CA-01.6. Vinculación con registro importado:** El autorregistro solo podrá completarse cuando el número de identificación ingresado coincida con el de un registro de aprendiz previamente importado.
- **CA-01.7. Identificación no encontrada:** Si el número de identificación no corresponde a un registro importado, el sistema debe impedir la creación de la cuenta e informar que no se encontró un registro que permita realizar la vinculación.
- **CA-01.8. Cuenta o identificación ya vinculada:** Si el número de identificación o la cuenta ya están vinculados a una cuenta existente, el sistema debe impedir la creación de una cuenta duplicada e informar el resultado.
- **CA-01.9. Recuperación de contraseña:** El sistema debe ofrecer el mecanismo de recuperación de contraseña disponible para las cuentas y comunicar el resultado sin revelar credenciales.
- **CA-01.10. Permisos por rol:** El sistema debe restringir las operaciones y los datos de acuerdo con el rol autenticado. El aprendiz no podrá registrar ni gestionar actuaciones académicas ni acceder a información de otros aprendices.
- **CA-01.11. Autorización por ámbito de responsabilidad:** El instructor solo podrá consultar o gestionar información de aprendices cuyas fichas estén previamente asociadas a su responsabilidad. Si la asociación no existe, el acceso deberá denegarse.
- **CA-01.12. Aplicación de controles:** Las restricciones de autorización deberán aplicarse a las operaciones y a los datos, independientemente de la interfaz o del dispositivo utilizado.

## RF-02. Importación y consulta de aprendices

**Historia de usuario**

Como instructor, quiero importar y consultar los datos básicos de los aprendices para disponer de un registro centralizado que permita vincular sus cuentas y asociar correctamente las actuaciones académicas.

**Criterios de aceptación**

- **CA-02.1. Formatos admitidos:** El sistema debe permitir importar archivos CSV o JSON.
- **CA-02.2. Campos obligatorios:** Cada registro debe contener `id`, `nombre_completo` y `numero_ficha`. El sistema debe validar la presencia y estructura de estos campos antes de procesar la importación.
- **CA-02.3. Validación de estructura y registros:** El sistema debe identificar archivos con estructura inválida y registros incompletos, inválidos o duplicados, e informar los errores encontrados.
- **CA-02.4. Identificación única:** El campo `id` debe corresponder al número del documento de identidad del aprendiz y almacenarse como texto, conservando ceros iniciales. Decisión confirmada 04-11-2026 (DC-07): retirar exclusivamente espacios comunes U+0020 al inicio y al final antes de validar (P-06 confirmada 06-11-2026); admitir únicamente dígitos ASCII del `0` al `9` y rechazar valores vacíos, espacios internos, letras, puntos, guiones y cualquier otro carácter. No convertir a número ni eliminar silenciosamente caracteres inválidos. Informar el error en su fila de importación. Esta regla no aprueba caracteres ni normalización de `numero_ficha`.
- **CA-02.5. Prevención de duplicados:** Si el número de identificación ya existe en TRAZA, no insertar un segundo registro y conservar internamente la causa exacta EXISTENTE con acceso restringido. Con ficha de entrada autorizada, mostrar el número de fila y «Identificación ya registrada» solo si se acredita permiso vigente sobre el aprendiz existente; en los demás casos de duplicidad mostrar el número de fila y «No fue posible incorporar esta fila», sin revelar nombre, ficha, identificador interno ni motivo de duplicidad. Aplicar P-08 en validación, confirmación y consultas posteriores. Los duplicados dentro del archivo se resuelven por P-04: comparar filas válidas autorizadas por identificación normalizada; si nombre y ficha coinciden según contrato, primera candidata y siguientes duplicadas; si difieren, rechazar todas las filas en conflicto e indicar sus números. Una fila inválida o no autorizada no bloquea otra válida autorizada; las demás identificaciones continúan.
- **CA-02.6. Resultado de importación:** Antes de confirmar la incorporación, permitir revisar el resultado de validación. Al finalizar, presentar resumen de registros procesados, incorporados y rechazados, conservando internamente la causa exacta y mostrando por fila solo el detalle autorizado vigente conforme a P-08. Ficha inexistente o no autorizada: mostrar «No se pudo validar la ficha para esta fila» sin distinguir ambas ni buscar duplicados globales. Duplicado accesible: «Identificación ya registrada»; duplicado ajeno o permiso no acreditado: «No fue posible incorporar esta fila». Aplicar idéntica protección en pantalla, confirmación, consultas posteriores, descargas, contadores y caché; recalcular con permisos actuales sin desglose de duplicados restringidos.
- **CA-02.7. Inserción de registros válidos:** El sistema debe incorporar únicamente registros válidos nuevos cuya ficha esté previamente asociada al instructor, sin crear cuentas. Revalidar el ámbito al confirmar; rechazar por fila las fichas no autorizadas sin revelar información de registros ajenos.
- **CA-02.8. Consulta de aprendices:** El instructor debe poder consultar los datos básicos de los aprendices importados únicamente cuando sus fichas estén asociadas a su ámbito de responsabilidad.
- **CA-02.9. Control por ficha:** El sistema debe utilizar `numero_ficha` para determinar el ámbito de acceso del instructor. La relación instructor-ficha debe estar configurada previamente; si no existe, el sistema debe denegar el acceso.
- **CA-02.10. Separación entre importación y acceso:** La importación de un aprendiz no debe crear una cuenta, habilitar una sesión ni conceder por sí misma acceso a los documentos.
- **CA-02.11. Reporte de errores:** Los errores de estructura y de datos deben presentarse de manera comprensible para que el responsable pueda corregir el archivo y volver a intentarlo.

## RF-03. Registro y consulta de llamados de atención

**Historia de usuario**

Como instructor, quiero diligenciar, registrar y consultar los llamados de atención de cada aprendiz para documentar las actuaciones académicas y mantener organizados sus antecedentes.

**Criterios de aceptación**

- **CA-03.1. Diligenciamiento:** El sistema debe permitir al instructor diligenciar los campos definidos en el formato institucional vigente del llamado de atención, incluidos los datos de identificación del aprendiz, fecha, grupo, número de orden, lugar, motivo y demás campos aplicables.
- **CA-03.2. Asociación y responsable:** Cada llamado debe quedar asociado al aprendiz correspondiente y al instructor que registra la actuación.
- **CA-03.3. Validación:** Antes de guardar, el sistema debe validar la presencia y el formato de los campos obligatorios definidos para el documento.
- **CA-03.4. Registro y conservación:** Cuando el instructor complete los datos requeridos y confirme el registro, el sistema debe guardar la actuación y conservar su relación con el aprendiz.
- **CA-03.5. Consulta por instructor:** El instructor debe poder consultar los llamados y sus documentos únicamente de los aprendices cuyas fichas estén asociadas a su responsabilidad.
- **CA-03.6. Consulta por aprendiz:** El aprendiz autenticado debe poder consultar exclusivamente sus propios llamados y visualizar el documento completo.
- **CA-03.7. Conteo acumulado:** El sistema debe contabilizar los llamados registrados para cada aprendiz, sin importar el tiempo transcurrido entre ellos, para determinar la disponibilidad de las opciones documentales definidas en el punto 5.
- **CA-03.8. Sin ciclo de vida:** El registro del llamado no debe requerir transiciones entre estados operativos. El conteo acumulado y la disponibilidad de opciones documentales no constituyen estados del llamado.
- **CA-03.9. Prevención de duplicados por reintento:** Si una operación de registro se reintenta debido a un problema de comunicación, el sistema debe evitar que el mismo envío de la operación cree llamados duplicados.
- **CA-03.10. Relación documental:** El llamado debe conservar su relación con el aprendiz y con los documentos posteriores que se generen a partir de los antecedentes correspondientes.
- **CA-03.11. Corrección antes de la firma:** Antes de que el aprendiz firme, el instructor autorizado debe poder corregir el llamado. El sistema debe registrar la corrección en el historial y no contabilizarla como un nuevo llamado. Antes de guardar, podrá editarse o cancelarse el formulario. Después de guardar, la corrección creará una nueva versión o documento correctivo vinculado, conservando el original y su historial; no creará una nueva actuación ni incrementará el conteo de llamados.
- **CA-03.12. Bloqueo de la versión firmada:** Una vez firmada una versión, esta no podrá editarse ni sobrescribirse. Cualquier corrección posterior deberá producir una nueva versión o documento vinculado al original, preservando el contenido y la firma originales.
- **CA-03.13. Versión presentada para firma:** La firma deberá vincularse a la versión exacta del llamado que el aprendiz visualizó antes de firmar.

## RF-04. Generación y gestión de planes de mejoramiento

**Historia de usuario**

Como instructor, quiero generar manualmente los planes de mejoramiento que correspondan a la acumulación de llamados de atención para establecer compromisos con el aprendiz y documentar las actuaciones acordadas.

**Criterios de aceptación**

- **CA-04.1. Disponibilidad del Plan de mejoramiento 1:** Desde dos llamados acumulados, ofrecer generar el Plan 1 si aún no se ha generado; conservar esta opción cuando el conteo alcance tres o más. La política de generaciones independientes adicionales permanece pendiente.
- **CA-04.2. Disponibilidad del Plan de mejoramiento 2:** Desde tres llamados acumulados, ofrecer generar el Plan 2 si aún no se ha generado; conservar esta opción al superar el umbral, junto con Plan 1 si sigue pendiente. La política de generaciones independientes adicionales permanece pendiente.
- **CA-04.3. Generación manual:** El sistema no debe generar automáticamente ninguno de los planes por alcanzar el número de llamados correspondiente. La generación requiere la decisión expresa del instructor.
- **CA-04.4. Formato institucional:** El sistema debe permitir diligenciar los campos aplicables del formato GOR-F-084 V02, incluidos los datos de reunión, agenda, objetivos, desarrollo y demás información prevista.
- **CA-04.5. Varios compromisos:** El instructor debe poder registrar varios compromisos o actividades dentro de un mismo plan, con sus fechas, responsables y demás datos previstos en el formato.
- **CA-04.6. Conservación y asociación:** Una vez generado, el plan debe conservarse y quedar asociado al aprendiz y a los llamados o actuaciones que lo originaron.
- **CA-04.7. Consulta:** El instructor debe poder consultar los planes generados y el aprendiz debe poder consultar sus propios planes conforme a los permisos establecidos.
- **CA-04.8. No implica aceptación:** La generación o consulta del plan no debe interpretarse como aceptación del aprendiz. La aceptación formal requiere la firma correspondiente.
- **CA-04.9. Corrección antes de la firma:** Un plan generado pero aún no firmado podrá corregirse por el instructor autorizado. El sistema deberá conservar la trazabilidad de las correcciones y mantener la relación con el documento correspondiente. Antes de guardar, podrá editarse o cancelarse el formulario. Después de guardar, la corrección creará una nueva versión o documento correctivo vinculado, conservando el original y su historial; no creará una nueva actuación ni incrementará el conteo de llamados.
- **CA-04.10. Corrección después de la firma:** Una vez firmado un plan, no podrá modificarse ni sobrescribirse. La corrección deberá generar una nueva versión o documento vinculado al original y preservar el contenido y la firma originales.
- **CA-04.11. Versión presentada para firma:** La firma del aprendiz deberá vincularse a la versión exacta del plan que se le presentó para su aceptación.
- **CA-04.12. Ausencia de firma:** Si el instructor comprueba que el aprendiz fue informado del plan y no encuentra la firma, podrá registrar la observación definida en RF-08.

## RF-05. Seguimiento de compromisos de los planes de mejoramiento

**Historia de usuario**

Como instructor, quiero registrar y consultar el seguimiento de los compromisos de cada plan de mejoramiento para documentar las verificaciones realizadas, sus resultados y las actuaciones posteriores que correspondan.

**Criterios de aceptación**

- **CA-05.1. Consulta de compromisos:** El sistema debe permitir al instructor consultar los compromisos registrados en cada plan.
- **CA-05.2. Registro de seguimiento:** El instructor debe poder registrar observaciones, evidencias y resultados de las verificaciones realizadas sobre cada compromiso.
- **CA-05.3. Asociación del registro:** Cada registro de seguimiento debe quedar asociado al plan, al compromiso correspondiente y al instructor que lo registra.
- **CA-05.4. Historial cronológico:** El sistema debe conservar los registros de seguimiento y permitir reconstruir cronológicamente las actuaciones realizadas.
- **CA-05.5. Conservación de antecedentes:** Un nuevo registro de seguimiento no debe eliminar ni sobrescribir los registros anteriores.
- **CA-05.6. Consulta restringida:** Los registros internos de seguimiento serán consultables por el instructor autorizado. El aprendiz podrá consultar sus documentos propios, pero el MVP no le concede acceso a las observaciones y evidencias internas de seguimiento.
- **CA-05.7. Valoración del instructor:** El sistema debe facilitar el registro y la consulta, pero no debe determinar automáticamente si un compromiso constituye incumplimiento ni sustituir la valoración del instructor.
- **CA-05.8. Correcciones autorizadas:** Las correcciones o anulaciones autorizadas deben conservar la actuación original y la trazabilidad de la modificación.

## RF-06. Generación del Formato de comunicación al aprendiz

**Historia de usuario**

Como instructor, quiero generar el Formato de comunicación cuando el aprendiz acumule cuatro llamados de atención para documentar la comunicación correspondiente y relacionarla con sus antecedentes.

**Criterios de aceptación**

- **CA-06.1. Disponibilidad:** Desde cuatro llamados acumulados, ofrecer generar el Formato de comunicación si aún no se ha generado; conservar la opción al superar cuatro. La política de generaciones independientes adicionales permanece pendiente.
- **CA-06.2. Generación manual:** El formato no debe generarse automáticamente al alcanzar el cuarto llamado. Su generación requiere la decisión expresa del instructor.
- **CA-06.3. Formato institucional:** El sistema debe permitir completar los campos establecidos en el formato GD-F-011, utilizando la información disponible y los antecedentes que correspondan.
- **CA-06.4. Motivos y normas:** El formato debe permitir registrar los motivos de la comunicación y las normas presuntamente infringidas del Reglamento del Aprendiz del SENA cuando corresponda según el formato institucional. El sistema no debe determinar automáticamente la existencia de una falta ni su calificación definitiva.
- **CA-06.5. Asociación con antecedentes:** El documento generado debe quedar asociado al aprendiz y a los llamados y actuaciones que originaron su generación.
- **CA-06.6. Conservación:** El sistema debe conservar el documento generado para su consulta y trazabilidad posterior.
- **CA-06.7. Inicio del envío:** Una vez generado el Formato de comunicación, el sistema debe iniciar inmediatamente su envío automático al correo institucional de Coordinación Académica seleccionado por el instructor para esa comunicación, conforme a RF-07.
- **CA-06.8. Fallo de envío:** La falta de destinatario válido o la indisponibilidad del servicio de correo no deberá impedir que el documento generado se conserve. El fallo se registrará y se atenderá conforme a RF-07.

## RF-07. Configuración y envío automático del Formato de comunicación

**Historia de usuario**

Como instructor, quiero configurar el correo institucional de Coordinación Académica y consultar los resultados de envío del Formato de comunicación para remitir el documento al destinatario institucional y atender los fallos.

**Criterios de aceptación**

- **CA-07.1. Configuración del destinatario:** El instructor debe poder registrar y actualizar las direcciones institucionales disponibles conforme a los permisos del MVP, sin asociarlas a fichas, y seleccionar una de ellas para cada comunicación antes de confirmar su generación y envío automático. El catálogo contiene el conjunto limitado de correos disponibles; no se fija una cantidad por inferencia.
- **CA-07.2. Validación de dirección:** El sistema debe validar que la dirección tenga un formato admisible antes de utilizarla como destinatario.
- **CA-07.3. Envío automático inmediato:** Después de generar y conservar la comunicación, iniciar automáticamente el envío a la dirección seleccionada por el instructor para esa comunicación, sin una segunda confirmación. Si falta selección válida, conservar el documento y registrar envío no completado.
- **CA-07.4. Mecanismo de entrega:** El mensaje debe incluir el Formato de comunicación generado como archivo adjunto. Este es el mecanismo de entrega documental definido para el MVP.
- **CA-07.5. Registro del intento:** El sistema debe conservar el documento relacionado con el envío, el destinatario, la fecha y hora del intento y el resultado informado por el servicio de correo.
- **CA-07.6. Notificación del fallo:** Si el envío no puede completarse, el sistema debe registrar el error e informar al instructor.
- **CA-07.7. Reintento sin duplicación:** El sistema debe permitir reintentar un envío fallido utilizando el mismo documento, sin duplicar el llamado, generar de nuevo el Formato de comunicación ni crear otra actuación documental por causa del reintento. Cada intento debe quedar registrado por separado.
- **CA-07.8. Consulta de resultados:** El instructor debe poder consultar los intentos de envío y los resultados disponibles.
- **CA-07.9. Alcance de la confirmación:** El sistema debe distinguir entre el resultado satisfactorio informado por el servicio de correo y la confirmación de recepción o lectura del mensaje. No debe afirmar que el mensaje fue recibido o leído si no dispone de evidencia para ello.
- **CA-07.10. Destinatario no configurado o servicio no disponible:** Si no existe una dirección válida o el servicio de correo no está disponible, el sistema debe conservar el documento, registrar el envío como no completado e informar al instructor. Una vez corregida la configuración o restablecido el servicio, el instructor podrá reintentar el envío del mismo documento, conservando los intentos anteriores y sin duplicar la actuación.
- **CA-07.11. Reintento tras cambio de destinatario:** Después de un fallo, permitir al instructor revisar, cambiar o conservar su selección de destinatario antes de reintentar. Usar la dirección seleccionada para ese intento, conservar los destinatarios anteriores y reutilizar el mismo documento. Un cambio del catálogo no redirige por sí solo un intento ya registrado.

## RF-08. Firma manuscrita y registro de aceptación del aprendiz

**Historia de usuario**

Como aprendiz, quiero revisar y firmar los llamados de atención y los planes de mejoramiento desde mi dispositivo móvil para dejar constancia de mi aceptación del documento correspondiente.

**Criterios de aceptación**

- **CA-08.1. Visualización previa:** Antes de firmar, el sistema debe mostrar al aprendiz el documento completo que se propone aceptar.
- **CA-08.2. Información sobre la acción:** El sistema debe presentar una indicación explícita sobre el significado de la acción de firmar.
- **CA-08.3. Captura de firma:** El sistema debe permitir capturar una firma manuscrita mediante la pantalla táctil del dispositivo.
- **CA-08.4. Repetición del trazo:** Antes de confirmar el registro, el aprendiz debe poder borrar la firma capturada y realizarla nuevamente.
- **CA-08.5. Confirmación expresa:** El sistema debe solicitar confirmación expresa antes de registrar la firma como evidencia de aceptación.
- **CA-08.6. Asociación con documento y versión:** La firma debe quedar vinculada al aprendiz, al documento firmado y a la versión exacta que se mostró para su aceptación.
- **CA-08.7. Registro temporal:** El sistema debe conservar la fecha y hora de la firma y las evidencias técnicas definidas para permitir la verificación posterior de la actuación.
- **CA-08.8. Almacenamiento confirmado:** El sistema solo debe informar que la firma se registró correctamente después de confirmar que la evidencia se almacenó satisfactoriamente.
- **CA-08.9. Fallo de almacenamiento:** Si la firma no puede guardarse, el sistema debe informar que la operación no se completó y no presentar el documento como firmado.
- **CA-08.10. Consulta posterior:** El aprendiz debe poder consultar posteriormente el documento firmado desde su cuenta, sin modificarlo ni eliminarlo.
- **CA-08.11. Aplicación a documentos:** El mecanismo debe aplicarse tanto a los llamados de atención como a los planes de mejoramiento incluidos en el MVP.
- **CA-08.12. Observación por ausencia de firma:** El sistema no debe ofrecer al aprendiz una opción para registrar su negativa. Cuando el instructor compruebe que el aprendiz fue informado del documento y no encuentre la firma, podrá registrar una observación asociada al documento.
- **CA-08.13. Datos mínimos de la observación:** La observación debe conservar el texto registrado, la identificación del instructor, la fecha y hora y la referencia al documento.
- **CA-08.14. Ausencia de aceptación:** La falta de firma no debe interpretarse como aceptación del documento.
- **CA-08.15. Integridad documental:** Una vez firmado, el documento no podrá modificarse ni eliminarse silenciosamente. Las correcciones autorizadas deberán conservar la evidencia original y su historial.
- **CA-08.16. No suplantación:** El instructor no podrá registrar una firma en nombre del aprendiz ni alterar una firma previamente almacenada.

## RF-09. Consulta del historial y trazabilidad documental

**Historia de usuario**

Como instructor, quiero consultar el historial de actuaciones y los documentos asociados a cada aprendiz para reconstruir los antecedentes, verificar la secuencia de los eventos y facilitar el seguimiento académico.

**Criterios de aceptación**

- **CA-09.1. Historial de llamados:** El sistema debe permitir consultar los llamados de atención registrados para un aprendiz y su secuencia cronológica.
- **CA-09.2. Historial de planes:** El sistema debe permitir consultar los planes de mejoramiento, sus compromisos y los registros de seguimiento relacionados.
- **CA-09.3. Historial de comunicaciones:** El sistema debe permitir consultar el Formato de comunicación generado y las actuaciones que dieron origen a su generación.
- **CA-09.4. Evidencias asociadas:** El historial debe permitir identificar las firmas, observaciones por ausencia de firma y evidencias de envío disponibles asociadas a cada actuación.
- **CA-09.5. Consulta del instructor:** El instructor debe poder consultar únicamente las actuaciones e historiales que esté autorizado a gestionar según la asociación entre su responsabilidad y la ficha del aprendiz.
- **CA-09.6. Consulta del aprendiz:** El aprendiz autenticado debe poder consultar exclusivamente sus propios llamados y documentos relacionados autorizados.
- **CA-09.7. Conservación del historial:** Las correcciones y anulaciones autorizadas deben registrarse sin eliminar silenciosamente la evidencia original ni los antecedentes necesarios para reconstruir la actuación.
- **CA-09.8. Identificación de actuaciones:** El historial debe permitir identificar la actuación, el documento relacionado y el responsable de las operaciones registradas, según la información disponible para cada evento.
- **CA-09.9. Consulta de solo lectura:** La consulta del historial por parte del aprendiz debe ser de solo lectura y no permitirle modificar registros ni documentos.
- **CA-09.10. Llamados posteriores al cuarto:** El sistema debe permitir consultar los llamados acumulados posteriores al cuarto, sin habilitar automáticamente opciones documentales adicionales mientras las reglas correspondientes permanezcan pendientes de definición y aprobación.

## 7.1. Reglas de negocio transversales

Estas reglas se aplican a varios requisitos funcionales. Complementan las reglas de negocio del apartado 5 y deben respetarse durante el diseño, desarrollo y pruebas del MVP.

### RNT-01. Control de acceso por rol y ámbito de responsabilidad

Las operaciones deben estar restringidas según el rol autenticado, la propiedad del registro y el ámbito de responsabilidad autorizado. El instructor solo podrá gestionar información de aprendices cuyas fichas estén asociadas a su responsabilidad. El aprendiz podrá consultar y firmar sus propios documentos, pero no registrar ni gestionar actuaciones académicas ni acceder a información de otros aprendices. Los controles deberán aplicarse tanto a la interfaz como a las operaciones y datos.

### RNT-02. Identificación y vinculación de aprendices

Cada aprendiz se identificará mediante el número de su documento de identidad, almacenado como texto y único en el registro importado. El autorregistro vinculará la cuenta con el registro previamente importado cuando coincida el número de identificación. La importación no creará cuentas ni concederá acceso automáticamente.

### RNT-03. Acumulación de llamados y disponibilidad documental

Los llamados de atención se acumularán por aprendiz sin límite temporal, conforme a la secuencia aprobada:

- Dos llamados acumulados: opción para generar el Plan de mejoramiento 1.
- Tres llamados acumulados: opción para generar el Plan de mejoramiento 2.
- Cuatro llamados acumulados: opción para generar el Formato de comunicación al aprendiz.

La disponibilidad de estas opciones no implica la generación automática de documentos. El instructor conserva la decisión de generarlos. El comportamiento para llamados posteriores al cuarto permanece pendiente de definición y aprobación.

### RNT-04. Responsabilidad del instructor e instancias competentes

TRAZA facilitará el registro, la consulta, la generación documental y el seguimiento. No determinará automáticamente la existencia de una falta, su calificación definitiva ni la imposición de una sanción. Las decisiones correspondientes permanecerán bajo la responsabilidad de las personas e instancias competentes.

### RNT-05. Correspondencia e integridad documental

Cada documento deberá permanecer asociado al aprendiz y a las actuaciones que lo originaron. Los documentos firmados no podrán modificarse ni eliminarse silenciosamente. Antes de la firma, las correcciones autorizadas deberán quedar registradas sin crear una nueva actuación cuando se trate de corregir el mismo documento. Después de la firma, la corrección deberá generar una nueva versión o documento vinculado al original, preservando el contenido, la firma y el historial originales.

### RNT-06. Aceptación y ausencia de firma

La generación o consulta de un documento no constituye evidencia de aceptación. La aceptación formal de un llamado de atención o de un plan de mejoramiento se registrará mediante la firma manuscrita contemplada en el MVP. Si el instructor verifica que el aprendiz fue informado y no encuentra la firma, podrá registrar una observación asociada al documento. La ausencia de firma no equivale a aceptación.

### RNT-07. Seguimiento de compromisos

El instructor será responsable de registrar y verificar el cumplimiento de los compromisos de los planes de mejoramiento. El sistema conservará las observaciones, evidencias y resultados de seguimiento, sin sustituir el criterio del instructor mediante decisiones automáticas.

### RNT-08. Trazabilidad de las actuaciones

El sistema conservará la información necesaria para reconstruir la secuencia de las actuaciones, identificar los documentos relacionados y consultar las firmas, observaciones, correcciones autorizadas y resultados de envío disponibles. Cada documento deberá poder relacionarse con el aprendiz y los antecedentes que motivaron su generación.

### RNT-09. Envío automático y control de reintentos

Después de generar el Formato de comunicación, el sistema iniciará inmediatamente el envío automático al correo institucional seleccionado para esa comunicación. Los intentos y resultados deberán quedar registrados. Los fallos serán visibles para el instructor y los reintentos no duplicarán el llamado ni la actuación documental. El resultado informado por el servicio de correo no deberá interpretarse como evidencia de lectura del mensaje.

### RNT-10. Protección de datos personales

El acceso, la consulta, la conservación y el tratamiento de los datos personales deberán respetar los permisos establecidos, las políticas institucionales y las disposiciones aplicables. El sistema no expondrá información de un aprendiz a otro usuario sin autorización.

### RNT-11. Manejo de errores y confirmación de operaciones

El sistema comunicará de forma comprensible los errores que impidan completar una operación. No presentará como exitosa una importación, un registro, una firma o un envío si el resultado no ha sido confirmado. Cuando una operación admita reintentos, estos deberán evitar duplicaciones y conservar la trazabilidad.

## 7.2. Condiciones para aceptar el MVP

Se considerará que el MVP cumple con los requisitos funcionales cuando se verifique que:

1. Los usuarios pueden autenticarse y acceder únicamente a las funciones y datos autorizados para su rol.
2. Los aprendices pueden autorregistrarse cuando su número de identificación coincide con un registro previamente importado.
3. El sistema permite importar archivos CSV o JSON con los campos requeridos, validar los registros, evitar duplicados y reportar los resultados.
4. El control de acceso restringe a cada instructor a los aprendices cuyas fichas estén asociadas previamente a su responsabilidad.
5. El instructor puede diligenciar, registrar y consultar llamados de atención.
6. El sistema acumula los llamados por aprendiz y ofrece las opciones de generación documental al alcanzar dos, tres y cuatro llamados, sin generar los documentos automáticamente.
7. El instructor puede generar planes de mejoramiento, registrar varios compromisos por plan y documentar su seguimiento.
8. El instructor puede generar el Formato de comunicación y el sistema inicia su envío automático como archivo adjunto al correo institucional seleccionado para esa comunicación.
9. El instructor puede consultar los intentos y resultados de envío, identificar fallos y reintentar sin duplicar la actuación documental.
10. El aprendiz puede consultar exclusivamente sus propios llamados y documentos relacionados y firmar llamados y planes mediante una firma manuscrita capturada en pantalla táctil.
11. La firma queda vinculada a la versión exacta del documento y el sistema confirma su almacenamiento antes de informar que la operación se completó.
12. El instructor puede registrar una observación por ausencia de firma bajo las condiciones establecidas, sin que dicha ausencia se interprete como aceptación.
13. Los documentos firmados conservan su integridad; las correcciones o anulaciones autorizadas preservan la evidencia original y el historial.
14. El instructor puede consultar el historial de llamados, planes, compromisos, seguimientos, observaciones, firmas y comunicaciones dentro de su ámbito de responsabilidad.
15. Los errores y las operaciones no completadas se comunican de forma comprensible y no se presentan como exitosas.
16. Las funcionalidades excluidas no se incorporan sin una decisión formal de cambio de alcance.
17. Los comportamientos que aún no están definidos, incluidos los asociados a llamados posteriores al cuarto, no se implementan sin una decisión funcional aprobada.

La verificación detallada de estas condiciones se realizará mediante los criterios de aceptación de cada requisito, los flujos de usuario y los casos de prueba definidos durante las siguientes etapas.

## 7.3. Matriz de trazabilidad entre requisitos funcionales y funcionalidades del MVP

La siguiente matriz relaciona los requisitos funcionales del apartado 7 con las funcionalidades descritas en el apartado 5. Esta relación permite comprobar la cobertura del alcance; no reemplaza los criterios de aceptación de cada requisito.

| Requisito funcional | Funcionalidad(es) del MVP relacionada(s) |
|---|---|
| RF-01. Autenticación, autorregistro y control de acceso | MVP-01 |
| RF-02. Importación y consulta de aprendices | MVP-02 |
| RF-03. Registro y consulta de llamados de atención | MVP-03 |
| RF-04. Generación y gestión de planes de mejoramiento | MVP-04 |
| RF-05. Seguimiento de compromisos de los planes de mejoramiento | MVP-05 |
| RF-06. Generación del Formato de comunicación al aprendiz | MVP-06 |
| RF-07. Configuración y envío automático del Formato de comunicación | MVP-06 y MVP-07 |
| RF-08. Firma manuscrita y registro de aceptación del aprendiz | MVP-03, MVP-04 y MVP-08 |
| RF-09. Consulta del historial y trazabilidad documental | MVP-03, MVP-04, MVP-05, MVP-06, MVP-07 y MVP-09 |

La matriz deberá mantenerse sincronizada con cualquier cambio posterior en la numeración, el alcance de las funcionalidades o los requisitos funcionales.

# 8. Requisitos no funcionales

Los requisitos no funcionales establecen las condiciones de calidad que deberá satisfacer TRAZA durante la operación del MVP. Sus criterios de aceptación deberán verificarse mediante pruebas o evidencias apropiadas. Los valores que todavía no hayan sido aprobados se identificarán como pendientes y no se considerarán compromisos definitivos hasta su aprobación.

## RNF-01. Rendimiento y tiempos de respuesta

**Descripción:** TRAZA deberá responder oportunamente a las operaciones habituales de sus usuarios, evitando demoras que afecten el registro y la consulta de llamados de atención, la gestión de planes de mejoramiento, el seguimiento de compromisos y la consulta del historial documental.

**Criterios de aceptación:**

- Las operaciones habituales de consulta, registro y actualización deberán responder en un tiempo máximo de 2 segundos para al menos el 95 % de las solicitudes, bajo condiciones de operación previamente definidas y aprobadas.
- Las pruebas deberán incluir, como mínimo, el inicio de sesión, la consulta de aprendices autorizados, el registro de llamados de atención, la consulta del historial y el registro de seguimientos.
- Las operaciones de generación documental, importación de archivos, almacenamiento de firmas y envío de correos deberán evaluarse según su naturaleza y los tiempos objetivo que se definan para cada una.
- Las pruebas deberán ejecutarse con una cantidad de usuarios concurrentes y un volumen de registros representativos del uso previsto para el MVP.
- El tiempo de respuesta deberá medirse mediante un método documentado, distinguiendo, cuando corresponda, el procesamiento de TRAZA y la intervención de servicios externos.
- Los resultados deberán registrar las condiciones de ejecución, los tiempos medidos, el porcentaje de solicitudes que cumplen el umbral y las desviaciones identificadas.

**Parámetros pendientes de aprobación:**

- Umbral definitivo de tiempo de respuesta.
- Número de usuarios concurrentes de referencia.
- Volumen de registros y operaciones para las pruebas.
- Tiempos objetivo para importaciones, generación documental, almacenamiento de firmas y envío de correo.

## RNF-02. Seguridad, autorización y privacidad

**Descripción:** TRAZA deberá proteger la información personal y académica mediante mecanismos de autenticación, autorización y control de acceso que respeten el rol del usuario, la propiedad del registro y el ámbito de responsabilidad del instructor.

**Criterios de aceptación:**

- Todo usuario deberá autenticarse antes de acceder a las funcionalidades protegidas.
- Las operaciones y consultas deberán autorizarse en función del rol autenticado y de las restricciones aplicables al registro solicitado.
- El instructor solo podrá consultar o gestionar información de aprendices cuyas fichas estén previamente asociadas a su ámbito de responsabilidad. Si la asociación no existe, el acceso deberá denegarse.
- El aprendiz solo podrá consultar y firmar sus propios documentos autorizados, sin acceder a información de otros aprendices ni gestionar actuaciones académicas.
- Los controles de autorización deberán aplicarse a las operaciones y a los datos, no únicamente a los elementos visibles en la interfaz.
- La información personal y académica no deberá exponerse a usuarios que carezcan de autorización.
- Las credenciales y los secretos técnicos deberán gestionarse de forma que no queden expuestos en la interfaz, en los registros de auditoría ni en el código fuente.
- Las pruebas deberán comprobar intentos de acceso no autorizado entre aprendices y entre ámbitos de responsabilidad de instructores.

**Parámetros pendientes de definición y aprobación:**

- Reglas específicas de gestión de sesiones y vencimiento de credenciales, según las capacidades de la solución de autenticación seleccionada.
- Plazos y condiciones de conservación de los datos, sujetos a las políticas institucionales y las obligaciones aplicables.

## RNF-03. Integridad y trazabilidad documental

**Descripción:** TRAZA deberá preservar la integridad de los llamados de atención, los planes de mejoramiento, las comunicaciones, las firmas y los registros asociados, permitiendo reconstruir las actuaciones y sus modificaciones autorizadas.

**Criterios de aceptación:**

- Cada documento deberá mantener su asociación con el aprendiz y con las actuaciones que originaron su generación.
- La firma manuscrita deberá vincularse con el aprendiz, el documento y la versión exacta que se le presentó para su aceptación.
- Una vez firmada una versión, esta no podrá modificarse ni eliminarse silenciosamente.
- Las correcciones posteriores a la firma deberán generar una nueva versión o un documento relacionado, preservando el original, la firma y el historial correspondiente.
- Las correcciones autorizadas antes de la firma deberán conservar trazabilidad y no deberán contabilizarse como una nueva actuación cuando correspondan a la corrección del mismo documento.
- Los eventos relevantes deberán permitir identificar, según corresponda, el usuario responsable, la fecha y hora, el documento o registro afectado y la operación realizada.
- Las observaciones por ausencia de firma, los registros de seguimiento y los intentos de envío de correo deberán conservar su relación con la actuación correspondiente.
- Las pruebas deberán comprobar que los documentos firmados, las firmas y los antecedentes no pueden sobrescribirse mediante las operaciones ordinarias del sistema.

**Parámetros pendientes de definición y aprobación:**

- Detalle de los eventos técnicos que deberán auditarse y sus periodos de conservación.
- Mecanismos técnicos de integridad y protección de los registros, que se especificarán en el TRD.

## RNF-04. Disponibilidad, respaldo y recuperación

**Descripción:** TRAZA deberá contar con condiciones de disponibilidad y mecanismos de respaldo y recuperación que permitan proteger la información del MVP y restablecer el servicio ante fallos, de acuerdo con los objetivos que se aprueben.

**Criterios de aceptación:**

- La estrategia técnica deberá identificar los mecanismos de respaldo de la información persistente necesaria para el funcionamiento de TRAZA.
- Deberá existir un procedimiento documentado para restaurar la información a partir de los respaldos disponibles.
- La recuperación deberá comprobarse mediante pruebas documentadas de restauración.
- Los fallos que impidan completar operaciones deberán comunicarse al usuario y no deberán presentarse como operaciones exitosas.
- La indisponibilidad del servicio de correo no deberá provocar la pérdida del Formato de comunicación generado ni de la información de los intentos de envío.
- El diseño técnico deberá identificar las dependencias críticas del servicio y los mecanismos de supervisión de disponibilidad que correspondan.

**Parámetros pendientes de definición y aprobación:**

- Objetivo de disponibilidad del servicio.
- Frecuencia de los respaldos y periodo de conservación.
- Objetivos de punto de recuperación (RPO) y tiempo de recuperación (RTO), según las necesidades institucionales.
- Responsabilidades y procedimiento operativo para ejecutar y verificar las restauraciones.

## RNF-05. Compatibilidad, accesibilidad y usabilidad

**Descripción:** TRAZA deberá ofrecer una interfaz comprensible y utilizable desde los navegadores y dispositivos definidos para el MVP, incluyendo los dispositivos con pantalla táctil requeridos para la firma manuscrita del aprendiz.

**Criterios de aceptación:**

- La interfaz deberá adaptarse a los tamaños de pantalla definidos para el uso previsto en el MVP.
- El aprendiz deberá poder visualizar el documento completo antes de firmarlo y capturar una firma manuscrita mediante una pantalla táctil compatible.
- La interfaz deberá comunicar de forma comprensible los estados de carga, procesamiento, éxito, error y operación no completada.
- Los mensajes de error deberán orientar al usuario sobre el problema y, cuando sea posible, la acción que puede realizar para resolverlo.
- Las operaciones sensibles, como confirmar una firma, deberán presentar las indicaciones y confirmaciones funcionales definidas en los requisitos correspondientes.
- Las pruebas deberán contemplar los navegadores y dispositivos incluidos en la matriz de compatibilidad aprobada.
- Las pruebas de usabilidad deberán verificar que instructores y aprendices pueden completar las tareas principales sin ambigüedades que impidan su ejecución.

**Parámetros pendientes de definición y aprobación:**

- Navegadores y versiones mínimas compatibles.
- Tamaños de pantalla y dispositivos de referencia.
- Criterios específicos de accesibilidad que se adoptarán para el MVP.

## RNF-06. Confiabilidad y manejo de errores

**Descripción:** TRAZA deberá gestionar de forma controlada los errores de validación, almacenamiento, conectividad e integración, evitando la pérdida de información, las duplicaciones y las confirmaciones incorrectas de operaciones.

**Criterios de aceptación:**

- El sistema no deberá informar que una operación se completó satisfactoriamente hasta contar con evidencia de que el resultado esperado se confirmó.
- Si falla el almacenamiento de una firma, el documento no deberá mostrarse como firmado y el usuario deberá recibir un mensaje que indique que la operación no se completó.
- Los reintentos de registro deberán evitar la creación duplicada de llamados u otras actuaciones como consecuencia de una misma operación reenviada.
- Los reintentos de envío de correo deberán utilizar el mismo documento generado, conservar cada intento y evitar duplicar la actuación documental.
- Si el envío de correo falla o no hay un destinatario válido, el documento deberá conservarse y el instructor deberá poder consultar el resultado y reintentar cuando se haya resuelto la causa.
- Los errores de importación deberán identificar, cuando sea posible, los registros afectados y la causa del rechazo.
- Las operaciones incompletas deberán dejar un estado o resultado coherente con lo que realmente ocurrió, sin presentar como exitosos los procesos fallidos.
- Las pruebas deberán incluir fallos de conectividad, errores de almacenamiento y reintentos de operaciones que puedan generar duplicados.

**Parámetros pendientes de definición y aprobación:**

- Política de reintentos para las operaciones que los admitan.
- Información técnica y funcional que se conservará para diagnosticar los errores, sin exponer datos personales innecesarios.

## RNF-07. Mantenibilidad y verificabilidad

**Descripción:** La solución deberá organizarse de manera que su código, configuración y pruebas puedan comprenderse, verificarse y modificarse de forma controlada, sin comprometer las reglas de negocio ni la integridad de la información.

**Criterios de aceptación:**

- El código fuente y los cambios deberán gestionarse mediante control de versiones.
- Las instrucciones necesarias para configurar, ejecutar, probar y desplegar la solución deberán documentarse.
- Las reglas de negocio críticas deberán contar con pruebas automatizadas o procedimientos de prueba reproducibles, según corresponda.
- Los cambios deberán poder verificarse mediante pruebas antes de incorporarse a una versión destinada a despliegue.
- La configuración sensible deberá mantenerse separada del código fuente y gestionarse conforme a las decisiones técnicas definidas en el TRD.
- Las dependencias técnicas relevantes deberán quedar identificadas y documentadas.
- La verificación del MVP deberá producir evidencias que permitan relacionar los requisitos con las pruebas ejecutadas y sus resultados.

**Parámetros pendientes de definición y aprobación:**

- Estrategia y alcance mínimo de pruebas automatizadas.
- Criterios de revisión de código y validación previa al despliegue.
- Herramientas de integración, despliegue y análisis técnico que se seleccionarán en el TRD.

## 8.1. Validación y verificación de los requisitos no funcionales

Los requisitos no funcionales deberán verificarse mediante pruebas, inspecciones y evidencias apropiadas para cada condición de calidad. La verificación deberá relacionar cada requisito con los escenarios ejecutados, los resultados obtenidos y los defectos identificados.

Como mínimo, la estrategia deberá contemplar:

- **Rendimiento:** pruebas de carga y concurrencia sobre las operaciones habituales, con medición de tiempos de respuesta.
- **Seguridad, autorización y privacidad:** pruebas de autenticación, permisos por rol, restricciones por ficha y prevención del acceso a información no autorizada.
- **Integridad y trazabilidad documental:** pruebas de asociación de firmas con versiones, conservación de documentos originales, correcciones autorizadas y consulta del historial.
- **Disponibilidad y recuperación:** revisión de los mecanismos de supervisión, respaldo y restauración, incluyendo pruebas de recuperación documentadas.
- **Compatibilidad, accesibilidad y usabilidad:** pruebas con los navegadores y dispositivos aprobados, revisión de la interfaz y ejecución de tareas representativas por usuarios de los roles previstos.
- **Confiabilidad y manejo de errores:** pruebas de interrupciones, errores de almacenamiento, reintentos, operaciones incompletas y prevención de duplicados.
- **Mantenibilidad y verificabilidad:** revisión de la documentación técnica, el control de versiones, las pruebas automatizadas y la trazabilidad entre requisitos y pruebas.

Los resultados deberán documentar los escenarios ejecutados, las condiciones y los datos de prueba, los resultados obtenidos, los defectos identificados y las acciones correctivas necesarias. Las pruebas deberán utilizar datos controlados y evitar la exposición innecesaria de información personal real.

## 8.2. Parámetros pendientes de definición y aprobación

Los siguientes parámetros deberán resolverse antes de aprobar las decisiones técnicas que dependan directamente de ellos. Su inclusión en esta lista no implica que los valores estén aprobados.

| Parámetro | Estado | Relación con el TRD |
|---|---|---|
| Tiempo de respuesta y percentil objetivo | Propuesta inicial: máximo de 2 segundos para al menos el 95 % de las solicitudes habituales; pendiente de aprobación | Dimensionamiento y pruebas de rendimiento |
| Número de usuarios concurrentes y volumen de registros de referencia | Pendiente de definir | Capacidad, consultas y pruebas de carga |
| Tiempos objetivo para importación, generación documental, firma y envío de correo | Pendiente de definir | Diseño y pruebas de las operaciones |
| Objetivo de disponibilidad | Pendiente de definir | Arquitectura y supervisión del servicio |
| Frecuencia y retención de respaldos | Pendiente de definir | Configuración de almacenamiento y recuperación |
| Objetivos de punto y tiempo de recuperación (RPO y RTO) | Pendiente de definir | Estrategia de continuidad y recuperación |
| Periodos de conservación de datos y registros de auditoría | Pendiente de validar con las políticas institucionales y las obligaciones aplicables | Modelo de datos, almacenamiento y auditoría |
| Navegadores, versiones y dispositivos compatibles | Pendiente de aprobar | Interfaz y matriz de pruebas |
| Criterios de accesibilidad aplicables al MVP | Pendiente de definir | Diseño de interfaz y verificación |
| Alcance de las pruebas automatizadas y controles previos al despliegue | Pendiente de definir en coordinación con el TRD | Mantenibilidad, calidad e integración y despliegue |

La resolución de estos parámetros deberá registrarse como una decisión aprobada y reflejarse en el TRD y en los artefactos de prueba correspondientes. Los valores que no sean necesarios para una decisión técnica inmediata podrán permanecer pendientes, siempre que no se presenten como compromisos aprobados ni impidan verificar los requisitos afectados.

# 9. Indicadores de éxito del producto

Los indicadores de éxito de **TRAZA** permitirán evaluar el cumplimiento de los objetivos del producto en términos de digitalización, eficiencia del registro, trazabilidad del seguimiento académico, integridad de la información, registro de la manifestación del aprendiz, aplicación de las reglas de seguimiento, generación documental, consulta de antecedentes, disponibilidad y seguridad.

Las metas incluidas en este apartado corresponden a **propuestas iniciales**. Deberán validarse y aprobarse antes de utilizarlas como compromisos definitivos de aceptación del MVP. Cuando se requieran datos operativos que todavía no estén disponibles, se establecerá una línea base durante las pruebas o la fase piloto.

Para cada indicador se especifican su descripción, fórmula de cálculo, fuente de evidencia, periodicidad, responsable de medición, meta inicial y estado de aprobación.

| Código | Indicador | Descripción y fórmula de cálculo | Meta inicial propuesta |
|---|---|---|---|
| IND-01 | Digitalización de los llamados de atención | Mide la proporción de llamados de atención registrados y gestionados mediante TRAZA frente al total de llamados de atención registrados durante el período evaluado. **Fórmula:** (Número de llamados de atención gestionados mediante TRAZA / Total de llamados de atención registrados durante el período) × 100. | ≥ 95 % |
| IND-02 | Eficiencia en el registro | Mide la proporción de registros de llamados de atención completados correctamente y que no requieren correcciones posteriores por errores de diligenciamiento. **Fórmula:** (Número de registros correctos sin correcciones por errores de diligenciamiento / Total de registros de llamados de atención realizados en el período) × 100. | ≥ 95 % |
| IND-03 | Trazabilidad del seguimiento académico | Mide la proporción de aprendices con antecedentes de llamados de atención cuyo historial puede consultarse de forma íntegra, cronológica y asociado a su identificación. **Fórmula:** (Número de aprendices con antecedentes cuyo historial cumple los criterios de trazabilidad / Total de aprendices con antecedentes de llamados de atención evaluados) × 100. | 100 % |
| IND-04 | Integridad de los registros | Mide la proporción de registros firmados que conservan su contenido original y su historial, sin modificaciones no autorizadas ni pérdida de información. **Fórmula:** (Número de registros firmados que cumplen los controles de integridad / Total de registros firmados evaluados) × 100. | 100 % |
| IND-05 | Registro de la manifestación del aprendiz | Mide la proporción de llamados de atención y planes de mejoramiento en los que la manifestación del aprendiz se encuentra documentada conforme a las reglas aprobadas, incluyendo la firma cuando exista o la observación correspondiente cuando se haya verificado una situación de ausencia o negativa a firmar. **Fórmula:** (Número de documentos evaluados con manifestación o situación documentada conforme a las reglas aplicables / Total de documentos evaluados que requieren dicha documentación) × 100. | 100 % |
| IND-06 | Cumplimiento de las reglas de seguimiento | Mide la proporción de casos de prueba en los que TRAZA identifica correctamente el nivel de seguimiento académico correspondiente, según las reglas de negocio aprobadas. **Fórmula:** (Número de casos de prueba con resultado correcto / Total de casos de prueba ejecutados para validar las reglas de seguimiento) × 100. | 100 % |
| IND-07 | Generación de documentos de seguimiento | Mide la proporción de solicitudes de generación documental realizadas por el instructor que concluyen correctamente y respetan las reglas de negocio y los datos registrados. **Fórmula:** (Número de solicitudes de generación documental completadas correctamente / Total de solicitudes de generación documental realizadas durante el período) × 100. | ≥ 98 % |
| IND-08 | Consulta de antecedentes académicos | Mide la proporción de consultas de antecedentes que se completan correctamente y presentan íntegramente la información disponible a la que el usuario está autorizado a acceder. **Fórmula:** (Número de consultas completadas correctamente / Total de consultas de antecedentes realizadas durante el período) × 100. | ≥ 98 % |
| IND-09 | Disponibilidad del sistema | Mide la proporción del tiempo programado de operación durante el cual TRAZA se encuentra disponible para los usuarios autorizados. **Fórmula:** ((Tiempo programado de operación − Tiempo de indisponibilidad atribuible al sistema) / Tiempo programado de operación) × 100. | ≥ 99 % |
| IND-10 | Seguridad y control de acceso | Mide la proporción de pruebas de autorización ejecutadas cuyo resultado coincide con los permisos definidos para cada rol y ámbito de responsabilidad. **Fórmula:** (Número de pruebas de autorización con resultado esperado / Total de pruebas de autorización ejecutadas) × 100. | 100 % |

## 9.1. Fuentes de evidencia, periodicidad y responsables

| Código | Fuente de evidencia | Periodicidad de medición | Responsable de la medición |
|---|---|---|---|
| IND-01 | Registros de llamados de atención en TRAZA y consolidado de los llamados registrados durante el período, cuando exista una fuente institucional de comparación. | Mensual durante la fase piloto y la operación. | Responsable funcional del producto, con validación del responsable institucional designado. |
| IND-02 | Registros de auditoría, historial de correcciones y resultados de revisión de los registros. | Mensual durante la fase piloto y la operación. | Responsable funcional del producto. |
| IND-03 | Historiales de los aprendices, relaciones entre llamados y documentos, y resultados de pruebas de consulta y trazabilidad. | En cada ciclo de pruebas y mensualmente durante la operación. | Responsable funcional del producto, con apoyo del responsable técnico cuando se requiera. |
| IND-04 | Historial de versiones, evidencias de firma, registros de auditoría y pruebas de integridad documental. | En cada ciclo de pruebas y trimestralmente durante la operación. | Responsable técnico del producto, con validación funcional. |
| IND-05 | Documentos generados, evidencias de firma y observaciones registradas por el instructor, según las reglas aprobadas. | Mensual durante la fase piloto y la operación. | Responsable funcional del producto o responsable institucional designado. |
| IND-06 | Casos de prueba, resultados de ejecución y evidencias de validación de las reglas de negocio. | En cada ciclo de pruebas funcionales y antes de aprobar una versión del producto. | Responsable de pruebas, con validación del responsable funcional. |
| IND-07 | Registros de solicitudes, resultados de generación documental y revisión del contenido de los documentos producidos. | En cada ciclo de pruebas y mensualmente durante la operación. | Responsable funcional del producto, con apoyo del responsable técnico cuando se requiera. |
| IND-08 | Registros de consultas, resultados de ejecución y pruebas de integridad y autorización de la información presentada. | En cada ciclo de pruebas y mensualmente durante la operación. | Responsable funcional del producto, con apoyo del responsable técnico cuando se requiera. |
| IND-09 | Métricas de disponibilidad, registros de incidentes y reportes de supervisión de la infraestructura. | Mensual, con seguimiento técnico de los incidentes cuando ocurran. | Responsable técnico de la plataforma o del servicio de alojamiento. |
| IND-10 | Matriz de roles y permisos, casos de prueba de autorización y evidencias de ejecución. | En cada ciclo de pruebas de seguridad y antes de aprobar una versión del producto. | Responsable técnico y responsable de pruebas, con validación funcional de los permisos esperados. |

## 9.2. Reglas para interpretar y validar los indicadores

1. **Estado de las metas:** todas las metas de las tablas anteriores tienen el estado **propuesta inicial**. Solo se considerarán aprobadas cuando exista una decisión documentada por parte de los responsables del producto.

2. **Período de medición:** la periodicidad indicada constituye una propuesta inicial y deberá confirmarse antes de la fase piloto. Los indicadores basados en pruebas se calcularán con los casos efectivamente ejecutados; los indicadores operativos se calcularán con los registros del período correspondiente.

3. **Denominadores válidos:** cuando el total de elementos evaluados sea cero, el indicador no deberá reportarse como 0 % ni como 100 %. Se registrará como **no calculable** y se explicará la causa.

4. **Calidad de la evidencia:** cada medición deberá conservar evidencia suficiente para reproducir o verificar el resultado, incluyendo el período evaluado, los datos utilizados, el cálculo aplicado y las incidencias que puedan afectar su interpretación.

5. **Registro de la manifestación del aprendiz:** el indicador IND-05 no mide la obligación de aceptar ni de firmar. La falta de firma no equivale a aceptación. Las observaciones por ausencia o negativa a firmar deberán cumplir las condiciones establecidas en los requisitos funcionales aprobados.

6. **Indicadores de pruebas y de operación:** los resultados obtenidos en pruebas controladas deberán distinguirse de los resultados observados durante la operación. No se utilizarán pruebas aisladas como sustituto de evidencia operativa cuando el indicador mida el desempeño real del sistema.

7. **Línea base y ajuste de metas:** durante las pruebas o la fase piloto se recopilará la información necesaria para validar la viabilidad de las metas propuestas. Los cambios deberán documentarse y aprobarse antes de considerarse compromisos definitivos.

8. **Coherencia documental:** las fórmulas, fuentes de evidencia y periodicidades que requieran capacidades técnicas específicas deberán ser coherentes con el TRD, el USER_FLOW y el PLAN. Si una medición depende de un registro, una métrica o una función que todavía no esté definida, esta dependencia deberá resolverse antes de utilizar el indicador como criterio de aceptación del MVP.

## 9.3. Condición de aprobación

Los indicadores y sus metas definitivas deberán validarse antes de establecerlos como criterios formales de aceptación del MVP. La aprobación deberá identificar, como mínimo, la meta acordada, el período de medición, la fuente de evidencia y el responsable de validar el resultado.

El cumplimiento de estos indicadores permitirá evaluar el desempeño funcional y técnico de TRAZA, identificar oportunidades de mejora y disponer de evidencia para decidir sobre la aceptación del MVP y la evolución posterior del producto.

# 10. Supuestos y dependencias

## 10.1. Objetivo

Identificar las condiciones que se consideran ciertas para la planificación, el desarrollo y la operación de **TRAZA**, así como los factores externos, recursos y servicios tecnológicos de los que depende la implementación del producto. Esta identificación permitirá anticipar riesgos, establecer condiciones para la ejecución del proyecto y mantener la coherencia entre el alcance funcional del MVP, los requisitos del producto y las decisiones técnicas.

## 10.2. Supuestos del proyecto

Los siguientes supuestos constituyen condiciones de referencia para la planificación y el desarrollo del MVP. Si alguno deja de cumplirse, será necesario evaluar su impacto sobre el alcance, los requisitos, el cronograma o la viabilidad del producto.

### SUP-01. Alcance funcional del MVP

El MVP de TRAZA se limitará a las funcionalidades expresamente definidas y aprobadas en el PRD. Las funcionalidades adicionales que no formen parte de este alcance deberán evaluarse para futuras iteraciones, sin incorporarse automáticamente al desarrollo del MVP.

### SUP-02. Disponibilidad de los usuarios involucrados

Se contará con la participación de los instructores y demás actores institucionales necesarios para validar los requisitos, los flujos de usuario, las reglas de negocio y los criterios de aceptación del producto.

### SUP-03. Disponibilidad y calidad de los datos de entrada

La información básica de identificación de los aprendices estará disponible para su incorporación al sistema mediante los mecanismos de importación definidos para el MVP. Los archivos deberán cumplir con la estructura y las reglas de validación establecidas por TRAZA para permitir su procesamiento.

### SUP-04. Definición de las reglas de seguimiento académico

Las reglas institucionales que determinan el registro de llamados de atención y los niveles de seguimiento académico serán definidas y validadas antes de implementar las funcionalidades que dependan de ellas. TRAZA deberá aplicar exclusivamente las reglas aprobadas y documentadas en el PRD.

### SUP-05. Participación del instructor en el seguimiento académico

El instructor conservará la responsabilidad de decidir cuándo corresponde generar los documentos de seguimiento académico cuya elaboración sea potestativa, de acuerdo con las reglas definidas para el producto. El sistema facilitará su elaboración y registro, sin sustituir las decisiones que correspondan al instructor.

### SUP-06. Disponibilidad de información institucional

Se contará con la información institucional necesaria para configurar los parámetros del sistema, los perfiles de usuario, los permisos y las demás condiciones operativas requeridas por el MVP.

## 10.3. Dependencias del proyecto

Las siguientes dependencias representan condiciones, recursos o servicios necesarios para desarrollar, desplegar u operar TRAZA. Su disponibilidad deberá verificarse durante las etapas correspondientes del proyecto.

### DEP-01. Infraestructura tecnológica

El desarrollo y la operación del MVP dependerán de la disponibilidad y configuración de la infraestructura tecnológica seleccionada y aprobada en el documento de requisitos técnicos (TRD).

### DEP-02. Servicios externos y plataformas tecnológicas

La implementación dependerá de la disponibilidad y el funcionamiento de los servicios y plataformas tecnológicas definidos en el TRD, así como de la configuración de sus accesos, credenciales, permisos y parámetros de integración.

### DEP-03. Repositorio de código y control de versiones

El desarrollo dependerá de la disponibilidad del repositorio de código fuente y de los mecanismos de control de versiones definidos para el proyecto, necesarios para gestionar los cambios, mantener el historial de desarrollo y facilitar la colaboración.

### DEP-04. Servicios de autenticación y autorización

La operación del sistema dependerá de la disponibilidad y correcta configuración de los mecanismos de autenticación y autorización que permitan identificar a los usuarios y controlar el acceso a las funcionalidades y los datos de acuerdo con los roles y permisos definidos.

### DEP-05. Disponibilidad de los responsables de validación

La validación de los requisitos, las reglas de negocio y los criterios de aceptación dependerá de la participación oportuna de los responsables designados para revisar y aprobar las definiciones funcionales del producto.

### DEP-06. Disponibilidad de los datos de identificación de los aprendices

La funcionalidad de autorregistro dependerá de que los datos de identificación de los aprendices hayan sido incorporados previamente al sistema mediante los mecanismos de importación autorizados. La validación de la identidad deberá realizarse conforme a las reglas definidas en el PRD, sin asumir que la existencia de un registro equivale, por sí sola, a una verificación de identidad.

## 10.4. Gestión de supuestos y dependencias

Los supuestos y las dependencias identificados deberán revisarse durante la evolución del proyecto y cuando se produzcan cambios que puedan afectar el alcance, los requisitos o la viabilidad del MVP.

- **Validación:** los supuestos deberán contrastarse con las condiciones reales del proyecto y las decisiones institucionales confirmadas.
- **Seguimiento:** las dependencias deberán verificarse antes de ejecutar las actividades que requieran su disponibilidad.
- **Gestión de cambios:** si un supuesto deja de cumplirse o una dependencia no está disponible, se deberá evaluar el impacto y determinar las acciones correctivas correspondientes.
- **Trazabilidad:** los elementos que afecten requisitos funcionales, decisiones técnicas o actividades de implementación deberán relacionarse con los apartados pertinentes del PRD, el TRD, el USER_FLOW y el PLAN.
- **Control de versiones:** cualquier modificación relevante deberá documentarse conforme al mecanismo de control de cambios establecido para el proyecto.

# 11. Riesgos funcionales

Los riesgos funcionales de **TRAZA** corresponden a situaciones que podrían afectar el cumplimiento de los requisitos funcionales, la aplicación de las reglas de negocio o la correcta ejecución de los procesos contemplados en el MVP. Su identificación permitirá establecer medidas preventivas y reducir la probabilidad de errores en la gestión de los llamados de atención y el seguimiento académico.

| Código | Riesgo funcional | Medida preventiva |
|---|---|---|
| RFU-01 | Aplicación incorrecta de las reglas de seguimiento académico, lo que podría ocasionar la identificación errónea del nivel de seguimiento correspondiente a un aprendiz. | Definir, documentar y validar las reglas de negocio antes de implementarlas, y verificar su cumplimiento mediante pruebas funcionales. |
| RFU-02 | Registro de llamados de atención asociados a un aprendiz equivocado o cuya identificación no coincida con los datos previamente cargados. | Validar la identificación del aprendiz contra los registros disponibles antes de permitir el registro del llamado de atención. |
| RFU-03 | Generación de documentos de seguimiento académico que no correspondan a las decisiones del instructor o a las reglas definidas en el producto. | Respetar el carácter potestativo de la generación de los documentos y validar las condiciones que habilitan su elaboración. |
| RFU-04 | Pérdida de trazabilidad entre los llamados de atención y los documentos de seguimiento asociados. | Mantener las relaciones entre los registros y permitir la consulta de los antecedentes correspondientes al aprendiz. |
| RFU-05 | Registro incompleto o inconsistente de la aceptación del aprendiz frente a un llamado de atención o documento de seguimiento. | Definir y validar los estados y las reglas aplicables a la aceptación, la no aceptación y los casos pendientes, de acuerdo con los requisitos aprobados. |
| RFU-06 | Incorporación de datos de aprendices con errores o duplicados durante la importación de archivos. | Validar la estructura de los archivos, los campos obligatorios, los formatos y la unicidad de la identificación antes de incorporar los registros. |

Los riesgos identificados deberán considerarse durante la definición de los criterios de aceptación y la elaboración de las pruebas funcionales del MVP. Su tratamiento se limitará a los aspectos relacionados con el comportamiento funcional de TRAZA.

# 12. Estados de interfaz obligatorios

Las interfaces de **TRAZA** deberán contemplar los siguientes estados para informar al usuario sobre el resultado de sus acciones y facilitar la gestión de los procesos del MVP.

| Estado | Comportamiento esperado |
|---|---|
| Cargando | Informar que se está procesando una operación y evitar acciones duplicadas cuando corresponda. |
| Vacío | Indicar que no existen registros para mostrar y, cuando aplique, orientar al usuario sobre la acción que puede realizar. |
| Éxito | Confirmar que la operación solicitada se completó correctamente. |
| Error | Informar que la operación no pudo completarse, explicar la causa cuando sea posible y orientar sobre cómo proceder. |
| Validación | Identificar los campos obligatorios, los formatos incorrectos y las inconsistencias que impidan completar una operación. |
| Sin resultados | Informar que una búsqueda o un filtro no produjo coincidencias. |
| Sin autorización | Informar que el usuario no tiene permisos para acceder a una funcionalidad o ejecutar una operación. |
| Confirmación | Solicitar confirmación antes de ejecutar acciones que requieran autorización explícita del usuario o puedan tener consecuencias relevantes. |

Estos estados deberán implementarse de manera coherente con los roles y permisos, las reglas de negocio y los flujos de usuario definidos para TRAZA. Los mensajes deberán ser claros, comprensibles y consistentes, sin exponer información sensible ni detalles técnicos innecesarios.
**Decisiones de producto 04-11-2026:** importación solo por ficha asociada; destinatario seleccionado sin relación con ficha; conservación de opciones documentales omitidas al superar el umbral. Generaciones independientes repetidas siguen pendientes.


## Registro complementario confirmado — 04-11-2026 (DC-07/DC-08)

**Fuente:** instrucción expresa de Luis Fernando Corredor Mora en la revisión de E0. Se conserva la versión documental existente; este registro actualiza únicamente las decisiones indicadas y no aprueba las propuestas físicas del nuevo anexo.

- **DC-07, confirmada:** identificación del aprendiz como texto, con ceros iniciales; retirar espacios exteriores antes de validar; exigir uno o más dígitos ASCII 0–9. Rechazar vacío, espacios internos, letras, puntos, guiones y otros caracteres; no convertir a número ni limpiar caracteres inválidos silenciosamente. Error localizado por fila. ` 00123456 ` se acepta como `00123456`; `0012 3456`, `1.234.567` y solo espacios se rechazan. Aplicar la misma regla al dato de identificación utilizado en autorregistro. El conjunto exacto de espacios exteriores se precisa como propuesta P-06 del anexo, sin ampliarlo silenciosamente.
- **DC-08, confirmada:** Luis Fernando Corredor Mora asume inicialmente la habilitación de instructores y asignación de fichas. No se crea rol administrador ni interfaz administrativa del MVP. El mecanismo técnico y sus controles son propuestas para revisión.
- **Ficha pendiente:** no se han aprobado caracteres ni normalización de numero_ficha. P-01 del anexo propone una política explícita; no se aplica automáticamente DC-07 a ese campo ni se bloquean relaciones independientes.
- **Alcance autorizado:** especificación física inicial de identidad, fichas e importación, autorización, auditoría, idempotencia, procedimiento operativo y casos de prueba. Entregar para revisión antes de convertir en migración; sin ejecutar cambios ni crear recursos Supabase.
- **Pendientes conservados:** generaciones independientes repetidas, acceso histórico ante traslados/cambios de responsabilidad, autoridad y efectos de anulaciones y continuidad del seguimiento de compromisos corregidos. No se resuelven mediante restricciones implícitas.
- **Formatos:** se identificaron ejemplos diligenciados GOR-F-084 V02 y GD-F-011; no está confirmada su incorporación a Docs ni su vigencia institucional. Se requieren copias/instrucciones validadas para fidelidad documental, sin bloquear el núcleo independiente. No se inventan campos definitivos.

**Entregable vigente:** [TRAZA_E0_ESPECIFICACION_FISICA_INICIAL.md](TRAZA_E0_ESPECIFICACION_FISICA_INICIAL.md), v0.4 para revisión técnica, 06-11-2026; decisiones funcionales actualizadas en el registro final de esta fecha. FI-01–39 previstos, no ejecutados. Primera migración: [propuesta v0.1](TRAZA_E0_PRIMERA_MIGRACION_PROPUESTA.md), sin SQL.

Este registro precisa CA-02.4, CA-01.6 y RNT-02; la responsabilidad operativa no amplía los roles ni permisos de la interfaz.


## Decisiones confirmadas y secuencia E0 — 06-11-2026

**Fuente:** aprobación expresa de Luis Fernando Corredor Mora. Este registro actualiza los pendientes históricos de 04/05-11-2026 solo en lo resuelto aquí; no cambia generaciones repetidas, traslados/acceso histórico, anulaciones ni continuidad de seguimiento de compromisos corregidos. DC-07/DC-08 permanecen confirmadas.

- **P-08 aprobada:** impedir duplicación y conservar causa exacta interna restringida. Ficha inexistente/no autorizada: número de fila y «No se pudo validar la ficha para esta fila», sin distinguir ambas ni buscar duplicados globales. Ficha autorizada y permiso vigente verificable sobre aprendiz existente: número y «Identificación ya registrada». Otros casos de duplicidad: número y «No fue posible incorporar esta fila», sin datos ajenos ni motivo de duplicidad. Aplicar en validación, confirmación, nuevas consultas, descarga, contadores y caché con permisos actuales. La ficha de entrada no acredita acceso al existente. Mensaje genérico reduce exposición, no elimina toda inferencia. Sin canal de revisión inventado; DC-08 no autoriza consultar otras fichas. PRD CA-02.5/6 ajustados; CA-02.7 conservado.
- **P-01/P-06 confirmadas:** identificación y ficha textuales de uno o más dígitos ASCII 0–9, con ceros preservados; retirar exclusivamente U+0020 exterior, rechazar vacío, espacios internos, tabs y otros caracteres. Misma normalización en catálogo y búsqueda de ficha en importación; también en identificación de autorregistro.
- **P-04 aprobada con ajuste:** agrupar filas válidas autorizadas por id normalizado; coincidencia de nombre y ficha según contrato: primera candidata y siguientes duplicadas internas. Diferencia de nombre o ficha: rechazar todas las filas del grupo conflictivo e indicar números de fila para corregir. Filas inválidas/ajenas se tratan aparte, no bloquean válidas ni exponen datos a través de agrupación. Otras identificaciones continúan. Distinto de P-08 frente a datos ya persistidos. La comparación concreta de nombre sigue como precisión técnica propuesta en §6.1 del anexo, no se deduce su aprobación.
- **P-05:** depuración productiva condicionada a política institucional; plazo pendiente. Desarrollo con datos sintéticos y plazos de ensayo explícitos, sin convertirlos en política productiva.
- **Primera migración:** alcance/secuencia confirmados, base técnica privada PostgreSQL; identidad, fichas, asociaciones e importación en incremento posterior. Diseño de objetos y permisos todavía para revisión; no se autoriza generar/ejecutar SQL ni crear recursos.

Referencias vigentes: [especificación física v0.4](TRAZA_E0_ESPECIFICACION_FISICA_INICIAL.md), para revisión técnica, FI-01–39 previstos; [primera migración propuesta v0.1](TRAZA_E0_PRIMERA_MIGRACION_PROPUESTA.md), M1-01–12 previstos. P-02/03/07, precisión de comparación de nombre, plazo productivo de P-05 y validaciones técnicas permanecen pendientes. No hay pruebas funcionales ejecutadas ni H0 cerrado.
