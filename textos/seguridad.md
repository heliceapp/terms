# MEDIDAS DE SEGURIDAD DE HELICE.APP
**Versión 1.0-3-ge2ad81d**

Este documento describe las **medidas técnicas y organizativas** que Helice.app aplica para garantizar un nivel de seguridad adecuado al riesgo, conforme al **artículo 32 del RGPD**. Forma parte del [Acuerdo de Encargo de Tratamiento (DPA)](/terminos-de-uso#dpa) de los [Términos y Condiciones](/terminos-de-uso). Las medidas se revisan y actualizan periódicamente, sin reducir el nivel de seguridad ofrecido.

## 1. Alojamiento y ubicación de los datos

La infraestructura de Helice.app está alojada en **DigitalOcean**, en su centro de datos de **Frankfurt (Alemania)**, de modo que los datos se tratan dentro del Espacio Económico Europeo. La seguridad física de las instalaciones —control de acceso, energía, climatización y protección contra incendios— corresponde al proveedor, que la acredita mediante sus propias certificaciones (ISO/IEC 27001 y SOC 2), disponibles públicamente en su portal de confianza.

La plataforma se despliega sobre **varios servidores independientes**, cada uno con su propia base de datos y su propio almacenamiento. Los Proyectos de un cliente residen en un servidor concreto, lo que aporta una ventaja de contención: un incidente que afecte a un servidor no alcanza a los Proyectos alojados en los demás.

Además del entorno de producción, Gooveris mantiene una **instalación propia en sus oficinas de Córdoba (España)**, con acceso físico restringido al personal autorizado, que actúa como destino de las copias de seguridad y como entorno de desarrollo y pruebas. Ambas ubicaciones están dentro del Espacio Económico Europeo.

## 2. Cifrado

**En tránsito.** Todo el tráfico de la plataforma —panel, webs de los Proyectos, aplicaciones móviles y API— viaja cifrado mediante **HTTPS con TLS 1.2 y TLS 1.3**; no se admiten versiones anteriores del protocolo. Los certificados se emiten con Let's Encrypt y se renuevan de forma automática antes de su expiración, y las peticiones que llegan por HTTP se redirigen a HTTPS.

**Credenciales del equipo organizador: no existen.** El acceso al panel de gestión se realiza mediante código de un solo uso (OTP) o inicio de sesión corporativo (SSO), de modo que **Helice.app no almacena contraseñas de los usuarios del panel** — la base de datos ni siquiera dispone de un campo donde guardarlas. Esta decisión de diseño elimina de raíz varios de los vectores de ataque más frecuentes:

- **No hay credenciales que robar.** Un acceso indebido a la base de datos no expone contraseñas, ni siquiera cifradas, por lo que no puede alimentar ataques de reutilización de credenciales contra otros servicios del usuario.
- **No hay fuerza bruta ni relleno de credenciales.** Sin contraseña que adivinar, los ataques automatizados de prueba masiva carecen de objetivo.
- **No hay recuperación de contraseña**, que es uno de los mecanismos más explotados para el secuestro de cuentas: no existe enlace de restablecimiento que interceptar ni pregunta de seguridad que suplantar.
- **Cada acceso verifica el canal**, porque el código se envía al correo corporativo del usuario o la identidad la confirma su proveedor de SSO.

**Credenciales de los usuarios finales.** Cuando un Proyecto habilita el acceso de sus inscritos con contraseña —además del acceso por código enviado al correo—, esta se almacena mediante **funciones de hash con sal (bcrypt)**, un procedimiento irreversible: no se guarda en claro ni puede recuperarse, solo restablecerse.

**Datos de pago.** Helice.app **no almacena datos de tarjeta ni credenciales bancarias**. El proceso de pago se delega íntegramente en la pasarela contratada (Redsys, Stripe u otras), que recoge los datos en su propio entorno certificado PCI DSS y devuelve a la plataforma únicamente el resultado de la operación.

**En reposo.** El almacenamiento de la plataforma combina el disco de los propios servidores con volúmenes de bloque del proveedor de infraestructura, que aplica cifrado en reposo sobre estos últimos. Los soportes físicos y su ciclo de vida —incluida la destrucción segura al retirarlos— están bajo el control del proveedor, cubierto por sus certificaciones. Las credenciales de servicios de terceros que el Cliente configura para su Proyecto (pasarela de pago, servidor de correo, SMS) se guardan asociadas exclusivamente a ese Proyecto y se utilizan solo para ejecutar sus propias operaciones.

## 3. Control de accesos

**Acceso del equipo organizador.** El panel de gestión se basa en dos mecanismos, ninguno de los cuales requiere que el usuario mantenga una contraseña:

- **Código de un solo uso (OTP)** enviado al correo del usuario. Verifica en cada acceso la titularidad de la dirección, caduca por sí solo y no deja ningún secreto permanente almacenado en la plataforma.
- **Inicio de sesión corporativo (SSO)** con **Google, Microsoft (Azure AD) o LinkedIn**. La identidad la valida el proveedor corporativo de la organización, que aplica sus propias políticas —doble factor, dispositivos autorizados, expulsión inmediata al dar de baja a un empleado en el directorio—, de modo que la baja de una persona en el sistema del Cliente cierra también su acceso a Helice.app.

Los Proyectos deciden qué mecanismos ofrecen a sus propios usuarios finales, que además pueden acceder con contraseña propia si el Proyecto lo habilita.

**Roles y permisos.** El acceso al panel se organiza por **áreas funcionales** (inscripciones, contenidos, comunicaciones, facturación, accesos, etc.). El administrador del Cliente da de alta a sus colaboradores y les asigna permisos por área y por Proyecto, de forma que cada persona ve únicamente aquello que necesita para su trabajo — principio de mínimo privilegio. Las altas y bajas son inmediatas y las gestiona el propio Cliente, sin intervención de Gooveris: al revocar un acceso, el colaborador deja de tener entrada al Proyecto.

**Usuarios finales.** Cada Proyecto decide cómo se identifican sus asistentes e inscritos, entre cuatro modos: **código de un solo uso** enviado al correo, **usuario y contraseña**, **un campo identificador** del propio registro (número de colegiado, DNI, identificador corporativo) o **autenticación delegada** en un sistema del propio Cliente a través de la API. No necesitan cuenta corporativa ni SSO.

**Políticas de acceso configurables por Proyecto.** Cuando el Proyecto habilita el acceso con contraseña, el Cliente define su propia política de seguridad, que la Plataforma **valida en el servidor** en todos los puntos donde puede crearse o cambiarse una contraseña —alta desde la web pública, alta desde el panel, formularios de inscripción, importaciones y API—, no solo en el navegador:

| Control | Qué permite |
|---|---|
| **Longitud mínima** | Exigir entre 5 y 16 caracteres |
| **Complejidad** | Exigir letras, al menos una mayúscula y al menos un número |
| **Caracteres especiales** | Exigir al menos uno de los símbolos que el propio Cliente define para su Proyecto |
| **Dominios autorizados** | Restringir el registro a los dominios de correo que el Cliente indique, de modo que solo puedan darse de alta las direcciones de su organización |
| **Sesión única** | Limitar cada cuenta a un dispositivo activo, lo que impide compartir credenciales entre varias personas |
| **Recuperación de contraseña** | Habilitarla por correo electrónico o **desactivarla por completo**, eliminando ese vector de ataque en Proyectos que no la necesitan |

Los intentos que no cumplen la política se rechazan indicando el requisito incumplido, y la Plataforma genera contraseñas conformes cuando el alta se realiza de forma automática.

**Acceso interno de Gooveris.** El acceso administrativo a los servidores se realiza exclusivamente mediante **autenticación por clave pública SSH**, sin contraseña, desde equipos autorizados; cualquier otro intento de conexión se rechaza y se bloquea automáticamente. El acceso del personal a los datos de un Proyecto se limita a lo estrictamente necesario para prestar el soporte solicitado.

Los niveles de administración de la plataforma (**superadministrador** y **master**), que son los únicos con visibilidad transversal, están sujetos a un control adicional: **no pueden concederse desde la interfaz ni desde la API**, sino únicamente mediante intervención directa en la base de datos por parte del personal autorizado. Una cuenta comprometida no puede, por tanto, elevar sus propios privilegios a través de la aplicación. El acceso a estos niveles se realiza con código de un solo uso (OTP).

## 4. Registro de actividad y trazabilidad

- **Historial de actividad del Proyecto.** La plataforma registra las acciones relevantes realizadas en el panel, asociándolas al usuario y al momento en que se producen. El Cliente puede consultarlo desde su propio panel. El historial se conserva hasta **doce (12) meses**, con un límite de registros configurable por Proyecto.
- **Registros técnicos.** El servidor web registra cada petición (origen, recurso, resultado y tiempo de respuesta) y la aplicación registra los errores y las incidencias de ejecución. Estos registros permiten detectar patrones de abuso, diagnosticar incidencias y reconstruir lo ocurrido ante un incidente de seguridad.
- **Registro de bloqueos y desbloqueos.** Toda solicitud de desbloqueo de una dirección IP queda registrada con su motivo, fecha y resultado (véase el apartado 6).

Los registros residen en los mismos servidores protegidos que la plataforma, accesibles únicamente por el personal autorizado de Gooveris.

## 5. Copias de seguridad y recuperación

Cada servidor de producción realiza copias de seguridad automáticas de forma programada, que se replican fuera del servidor de origen, en la instalación propia de Gooveris en España.

| Elemento | Frecuencia | Alcance |
|---|---|---|
| **Base de datos** | Diaria | Copia completa |
| **Ficheros de los Proyectos** (documentos, imágenes, adjuntos) | Cada 7 días | Copia completa |

- **Retención:** las copias se conservan **30 días**, transcurridos los cuales se eliminan automáticamente.
- **Transferencia:** la replicación al destino se realiza **cifrada mediante SSH**.
- **Restauración:** el procedimiento permite restaurar tanto un entorno completo como un Proyecto, una tabla o un conjunto de ficheros concretos. Las restauraciones parciales se realizan con regularidad como parte de la operación ordinaria —recuperación de datos borrados por error, reconstrucción de un contenido—, lo que verifica de forma continua que las copias son utilizables.

**Efecto sobre la supresión de datos.** El plazo de retención de las copias es independiente del ciclo de vida del Proyecto. Cuando un Proyecto se elimina, sus datos dejan de estar accesibles de inmediato y desaparecen también de las copias conforme estas rotan, en un plazo máximo de 30 días desde la eliminación (cláusula D5.7 del DPA).

## 6. Seguridad de la aplicación y del desarrollo

**Protección perimetral.** La plataforma aplica varias capas de defensa antes de que una petición llegue a la aplicación:

- **Limitación de peticiones (rate limiting)** por dirección IP y por dominio, que absorbe picos legítimos y frena la automatización abusiva devolviendo un código 429.
- **Bloqueo automático de direcciones IP** ante patrones característicos de ataque —rastreo de rutas inexistentes, exploración de rutas de WordPress y de paneles ajenos a la plataforma, peticiones malformadas, accesos denegados repetidos, intentos de conexión SSH—, con duraciones de bloqueo crecientes según la gravedad.
- **Bloqueo de rastreadores abusivos** y de agentes conocidos por consumo indebido de recursos.
- **Restricción de métodos HTTP** a los estrictamente necesarios y bloqueo de rutas y extensiones sensibles (ficheros de configuración, copias, volcados de base de datos, ficheros ocultos).
- **Ocultación de la versión del servidor** y separación estricta entre el directorio público y el código de la aplicación: solo el punto de entrada de la aplicación es ejecutable.

**Servicio de desbloqueo.** Como el bloqueo automático puede afectar a un usuario legítimo tras una sucesión de errores, Gooveris publica un servicio independiente en **seguridad.helice.app** donde cualquier usuario puede comprobar si su dirección IP está bloqueada y solicitar su desbloqueo inmediato. El desbloqueo automático solo se concede si la dirección está vinculada a una sesión de usuario o cliente real; en los demás casos, la solicitud se remite a soporte. Todas las solicitudes quedan registradas.

**Desarrollo.** El código se gestiona con control de versiones **Git**, con ramas separadas y despliegue controlado a producción. Los entornos de **desarrollo y pruebas están separados del de producción** y residen en la instalación propia de Gooveris. La plataforma está construida sobre un framework que aplica de serie consultas parametrizadas —lo que neutraliza la inyección SQL—, validación de entradas y separación entre lógica de negocio y ficheros públicos.

**Integraciones: API REST.** El acceso programático a un Proyecto se realiza mediante **claves de API que emite el propio Cliente** desde el panel, tantas como necesite —lo habitual es una por integración—, y que se transmiten en una cabecera de la petición. Toda petición sin clave válida se rechaza con un **401 Unauthorized**, sin ejecutar ninguna operación ni revelar información del Proyecto. El modelo tiene tres propiedades relevantes:

- **Revocación inmediata y granular.** El Cliente elimina una clave desde el panel y la siguiente petición que la use recibe un 401. Revocar una clave no afecta a las demás, de modo que se puede cortar el acceso de una integración concreta —un proveedor que deja de trabajar con la organización, un sistema que se retira— sin interrumpir el resto.
- **Trazabilidad por clave.** El panel muestra, para cada clave, su nombre, la fecha de creación, la **fecha del último uso** y el **número de peticiones acumuladas**. Permite detectar un uso anómalo y saber qué integraciones siguen activas antes de revocar ninguna.
- **Alcance limitado al Proyecto.** Cada clave pertenece a un Proyecto y solo opera sobre sus datos; no existe una clave que abarque varios Proyectos ni la Plataforma.

En el listado del panel la clave aparece enmascarada, mostrando solo sus primeros y últimos caracteres.

**Integraciones: webhooks.** El Cliente puede configurar el envío automático de eventos —alta de usuario, inicio de sesión, aprobación o cancelación de una inscripción, recepción de un formulario— al sistema que él indique. El diseño del envío contempla:

- **Transporte cifrado y verificado.** La entrega se realiza contra la URL del Cliente sobre HTTPS, **verificando el certificado del destino**: si el certificado no es válido, el envío falla en lugar de entregar los datos a un destino no verificado.
- **Autenticación del origen.** El Cliente puede exigir que Helice.app se identifique ante su sistema mediante un token *bearer* o una cabecera secreta propia, de modo que su endpoint pueda rechazar cualquier petición que no provenga de la Plataforma.
- **Exclusión sistemática de datos sensibles.** El contenido enviado se construye a partir de una lista de exclusión: **nunca incluye la contraseña, los tokens de sesión, los datos de tarjeta, los identificadores de la pasarela de pago, los dispositivos ni las direcciones IP** del usuario.
- **Control y trazabilidad.** Cada webhook registra su última respuesta, la fecha de la última ejecución y el número de ejecuciones acumuladas, y puede desactivarse en cualquier momento. Los envíos tienen un tiempo máximo de espera y no se reintentan de forma automática, de modo que un endpoint caído no genera reenvíos repetidos ni colas de datos pendientes.

**Gestión de vulnerabilidades.** Gooveris realiza **revisiones internas de seguridad del código**, cuyo resultado se traduce en un plan de corrección priorizado por gravedad. Las vulnerabilidades detectadas —propias o comunicadas por terceros— se clasifican, se corrigen conforme a esa prioridad y se despliegan siguiendo el procedimiento de cambios. Los componentes de sistema (servidor web, base de datos, servicios de red) se mantienen actualizados tras la comprobación de compatibilidad con la plataforma.

## 7. Resiliencia y continuidad

**Monitorización.** La supervisión se realiza en tres capas complementarias:

- **Disponibilidad desde el exterior**, mediante un servicio independiente (UptimeRobot) que comprueba de forma continua que los dominios responden y que genera un **histórico público** consultable por cualquiera en la [página de estado del servicio](https://stats.uptimerobot.com/f918yFfjFp).
- **Recursos de los servidores**, con las métricas y alertas por umbrales del proveedor de infraestructura (uso de CPU, memoria, disco y disponibilidad de los nodos), que avisan antes de que la saturación se convierta en una caída.
- **Herramientas internas de la propia plataforma**: visor de registros del servidor web y controles automáticos diarios (por ejemplo, del almacenamiento consumido o el ancho de banda servido por cada Proyecto).

El registro de tiempos de respuesta distingue el tiempo consumido por la aplicación del tiempo de transferencia al cliente, lo que permite actuar sobre el origen real de una lentitud en lugar de sobre su síntoma.

**Arquitectura.** El despliegue en servidores independientes limita el alcance de cualquier incidente: una incidencia en un servidor no interrumpe el servicio de los Proyectos alojados en los demás. Los recursos de cada servidor se dimensionan para la carga prevista y pueden ampliarse antes de eventos de gran afluencia, si el Cliente lo comunica con antelación.

**Continuidad.** Ante un fallo grave de un servidor, la recuperación se realiza sobre infraestructura nueva a partir de la última copia de seguridad disponible, conforme al apartado 5.

**Disponibilidad.** Gooveris presta el servicio con la diligencia exigible a una empresa especializada y trabaja con un objetivo de disponibilidad elevado, sin que ello constituya un compromiso contractual de nivel de servicio (SLA) salvo pacto expreso en Condiciones Particulares, conforme a la cláusula 9 de los Términos y Condiciones. Las intervenciones de mantenimiento que puedan afectar al servicio se comunican con antelación razonable siempre que es posible.

## 8. Gestión de incidentes y brechas de seguridad

Gooveris aplica un procedimiento interno con las siguientes fases:

1. **Detección.** A partir de las alertas de monitorización, del análisis de los registros técnicos o de la comunicación de un cliente o un tercero.
2. **Clasificación.** El incidente se califica según su naturaleza (error de software, ataque, fallo de un proveedor) y su gravedad, atendiendo en particular a si afecta a datos personales.
3. **Contención y corrección.** Se aplica la medida inmediata que detiene el impacto —bloqueo del origen, desactivación de la funcionalidad afectada, restauración desde copia— y a continuación la corrección de fondo, que se despliega por el procedimiento de cambios habitual.
4. **Comunicación.** Ante una violación de la seguridad de los datos personales, Gooveris notifica al Cliente **sin dilación indebida y, a más tardar, dentro de las 72 horas** desde que tiene conocimiento, con el contenido del artículo 33.3 del RGPD disponible en ese momento y completándolo por fases si es necesario (cláusula D5.6 del DPA). La notificación a la autoridad de control y a los interesados corresponde al Cliente como responsable del tratamiento, y Gooveris le asiste en ella.
5. **Análisis posterior.** Los incidentes con impacto en el servicio se documentan internamente —cronología, causa raíz y medidas correctoras— y las medidas resultantes se incorporan a la plataforma.

Cualquier persona puede comunicar una vulnerabilidad o un incidente de seguridad escribiendo a **info@helice.app**.

## 9. Subencargados

Los proveedores que tratan datos personales por cuenta de Gooveris y sus garantías se detallan en la [lista de subencargados](/subencargados), Documento Vinculado del DPA. Su alta o sustitución se notifica al Cliente con quince (15) días naturales de antelación, conforme a la cláusula D8.2 del DPA.

## 10. Medidas organizativas

- **Confidencialidad.** El personal con acceso a datos personales está sujeto a un deber de confidencialidad expreso, que subsiste tras el fin de la relación.
- **Mínimo privilegio interno.** El acceso del personal a los datos de un Proyecto se limita a lo necesario para prestar el servicio o el soporte solicitado.
- **Formación y concienciación.** El equipo recibe pautas internas sobre tratamiento de datos, gestión de credenciales y respuesta ante incidentes.
- **Instrucciones del Cliente.** Gooveris trata los datos únicamente conforme a las instrucciones documentadas del Cliente, siendo la configuración y el uso de la Plataforma la instrucción principal; no los utiliza para fines propios ni los cede a terceros distintos de los subencargados publicados.
- **Contacto.** Para cualquier cuestión de seguridad o protección de datos: **info@helice.app**.

## 11. Certificaciones

Gooveris Software, S.L. **no dispone en la actualidad de certificación ISO/IEC 27001 ni de declaración de conformidad con el Esquema Nacional de Seguridad**. Las medidas descritas en este documento constituyen las medidas técnicas y organizativas del artículo 32 del RGPD, son verificables y quedan contractualmente comprometidas a través del DPA, que forma parte de los Términos y Condiciones.

La infraestructura sobre la que se presta el servicio sí está certificada: el centro de datos y los servicios de DigitalOcean cuentan con **ISO/IEC 27001** y **SOC 2**, cuyos certificados pueden aportarse a petición del Cliente.

Conforme a la cláusula D5.8 del DPA, Gooveris pone a disposición del Cliente la información necesaria para demostrar el cumplimiento de sus obligaciones y admite auditorías previo aviso razonable.

---

¿Buscas el resto de condiciones? Consulta los [Términos y Condiciones Generales de Helice.app](/terminos-de-uso).
