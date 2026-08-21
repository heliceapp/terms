# Dossier de seguridad, protección de datos e infraestructura

**Helice.app — plataforma de gestión integral de eventos**
GOOVERIS SOFTWARE, S.L. · CIF B56077100
**Versión 1.0-1-g2f53ffd**

Este dossier responde a los requisitos de seguridad, protección de datos e infraestructura que habitualmente se solicitan en procesos de licitación, homologación de proveedores y evaluaciones de riesgo. Todo lo que aquí se describe se refiere al **servicio concreto que se contrata** —la plataforma Helice.app y los proyectos alojados en ella—, no a políticas genéricas de la organización.

---

## 1. Respuesta rápida

| Requisito | Respuesta | Detalle |
|---|---|---|
| **Certificación ISO/IEC 27001** | **No.** Gooveris no está certificada. La infraestructura donde se aloja el servicio (DigitalOcean) sí lo está, junto con SOC 2 | [§9](#9-certificaciones-y-acreditación-del-cumplimiento) |
| **Conformidad ENS** | **No.** No existe declaración de conformidad con el Esquema Nacional de Seguridad | [§9](#9-certificaciones-y-acreditación-del-cumplimiento) |
| **Ubicación de los datos** | Centro de datos de Frankfurt (Alemania), dentro del EEE. Copias replicadas en instalación propia en Córdoba (España) | [§3](#3-alojamiento-y-ubicación-de-los-datos) |
| **DPA y RGPD** | Acuerdo de encargo de tratamiento **ya integrado** en los Términos y Condiciones, formalizado con su aceptación, sin firma adicional | [§4](#4-protección-de-datos) |
| **Subprocesadores** | Lista pública y versionada, con notificación previa de 15 días ante cualquier alta o sustitución | [§5](#5-subencargados-subprocesadores) |
| **SSO** | Sí: Google, Microsoft (Azure AD) y LinkedIn. El panel funciona **sin contraseñas**: OTP o SSO, sin credenciales almacenadas ni flujo de recuperación | [§6.2](#62-autenticación) |
| **Roles y permisos** | Sistema por áreas funcionales y por proyecto, gestionado por el propio cliente, con criterio de mínimo privilegio | [§6.3](#63-roles-y-permisos) |
| **Política de contraseñas** | Configurable por proyecto y validada en servidor: longitud, mayúsculas, números, caracteres especiales, dominios autorizados y sesión única | [§6.2](#62-autenticación) |
| **Copias de seguridad** | Copia completa diaria de base de datos y semanal de ficheros, replicadas cifradas fuera del servidor de origen, con 30 días de retención | [§7](#7-copias-de-seguridad-y-continuidad) |
| **Respuesta ante incidentes** | Procedimiento documentado de detección, contención, corrección y comunicación. Notificación de brechas en 72 h | [§8](#8-gestión-de-incidentes-y-brechas) |
| **Conservación, borrado y devolución** | Exportación autónoma en cualquier momento; 90 días de conservación tras la expiración; supresión definitiva después | [§10](#10-conservación-borrado-y-devolución-de-los-datos) |
| **Disponibilidad (SLA)** | Objetivo de disponibilidad elevado con monitorización continua e **histórico público** en https://stats.uptimerobot.com/f918yFfjFp; el compromiso contractual con porcentaje garantizado se pacta en Condiciones Particulares | [§11](#11-disponibilidad-y-soporte) |

---

## 2. La entidad y el servicio

| Dato | Valor |
|---|---|
| **Razón social** | GOOVERIS SOFTWARE, S.L. |
| **Nombre comercial** | Helice.app |
| **CIF** | B56077100 |
| **Domicilio social** | Avda. de la Torrecilla 16, 14013 Córdoba (España) |
| **Datos registrales** | Registro Mercantil de Córdoba, tomo 2.585, folio 31, hoja CO-38.259, inscripción 1.ª |
| **Contacto** | info@helice.app · https://www.helice.app |

**Objeto del servicio.** Plataforma SaaS de gestión integral de eventos: inscripciones y acreditaciones, control de accesos, web y app del evento, agenda y programa, revisión científica, networking, certificados, facturación y comunicaciones. El servicio se presta en modalidad de licencia anual por evento e incluye tres componentes: **panel de gestión** para el equipo organizador, **web pública** del evento y **aplicación móvil nativa** para iOS y Android.

**Requisitos en el puesto del cliente:** ninguno más allá de un navegador actualizado. No requiere instalación local, licencias adicionales ni componentes en el equipo del usuario.

---

## 3. Alojamiento y ubicación de los datos

| Dato | Valor |
|---|---|
| **Proveedor de infraestructura** | DigitalOcean |
| **Ubicación del centro de datos** | Frankfurt (Alemania) |
| **Tratamiento dentro del EEE** | Sí |
| **Modelo de despliegue** | Multi-tenant en la nube (SaaS), sobre varios servidores independientes |
| **Copias de seguridad** | Replicadas en instalación propia de Gooveris, en sus oficinas de Córdoba (España), con acceso físico restringido |
| **Certificaciones del proveedor** | ISO/IEC 27001 y SOC 2 |

La seguridad física del centro de datos —control de acceso, energía, climatización, protección contra incendios— corresponde al proveedor y está cubierta por sus certificaciones, aportables a petición.

**Aislamiento entre clientes.** La plataforma se despliega sobre **varios servidores independientes**, cada uno con su propia base de datos y su propio almacenamiento. Los proyectos de un cliente residen en un servidor concreto. Dentro de cada servidor, los datos de cada proyecto están separados lógicamente y el acceso está mediado por el sistema de permisos: un usuario solo alcanza los proyectos en los que ha sido dado de alta. Este reparto aporta contención: una incidencia en un servidor no afecta a los proyectos alojados en los demás.

**Transferencias internacionales.** El alojamiento, el envío de correo transaccional y las copias de seguridad se realizan íntegramente dentro del Espacio Económico Europeo. El único tratamiento fuera del EEE es el de la funcionalidad de inteligencia artificial **ValerIA**, de activación voluntaria, amparado en las Cláusulas Contractuales Tipo (Decisión de Ejecución UE 2021/914). Si el cliente no utiliza esa funcionalidad, no se produce ninguna transferencia internacional.

### 3.1 Arquitectura técnica

| Capa | Tecnología |
|---|---|
| **Backend** | PHP con framework Laravel, arquitectura MVC |
| **Base de datos** | MySQL |
| **Servidor web** | nginx con PHP-FPM sobre Linux (Ubuntu Server) |
| **Frontend web** | HTML5, CSS3 y JavaScript; responsive |
| **Aplicaciones móviles** | Apps nativas iOS y Android por proyecto, con notificaciones push |
| **Procesos programados** | Ejecución mediante cron del sistema (recordatorios, automatizaciones, sincronizaciones, mantenimiento) |
| **Integración** | API REST propia con autenticación por token, para conexión con CRM, ERP y sistemas de terceros |
| **Control de versiones** | Git, con entornos de desarrollo, pruebas y producción separados |

Por política de seguridad, el número de versión exacto de cada componente no se publica —facilita la búsqueda de vulnerabilidades conocidas contra un objetivo concreto—, pero se facilita al órgano de contratación que lo requiera dentro del procedimiento, con el tratamiento de confidencialidad que corresponda.

---

## 4. Protección de datos

**Roles.** En la prestación del servicio, **el cliente es el responsable del tratamiento** de los datos que gestiona en su evento (inscritos, asistentes, ponentes) y **Gooveris es el encargado**. Gooveris es responsable únicamente respecto de los datos de la relación comercial con el cliente.

**Acuerdo de encargo (DPA).** El DPA está **integrado en los Términos y Condiciones** como Parte VIII y queda formalizado electrónicamente con su aceptación, previa al inicio del tratamiento, sin necesidad de firmar un documento aparte (art. 28.9 RGPD). Regula:

| Cláusula | Contenido |
|---|---|
| D3–D4 | Naturaleza, finalidad y operaciones del tratamiento; categorías de interesados y de datos, incluidas las categorías especiales accesorias habituales en eventos (alergias, accesibilidad, salud declarada voluntariamente) |
| D5 | Obligaciones del encargado: tratamiento solo conforme a instrucciones documentadas, prohibición de uso para fines propios, confidencialidad del personal, medidas del art. 32, asistencia en derechos y evaluaciones de impacto, notificación de brechas en 72 h, devolución o supresión al final, y derecho de auditoría del cliente |
| D7 | Cliente que actúa por cuenta de un tercero: prevé expresamente la cadena responsable → encargado → subencargado, habitual cuando una agencia u OPC organiza el evento de un organismo |
| D8 | Subencargados: autorización general, lista publicada y versionada, y notificación previa de 15 días naturales con derecho de oposición |
| D9 | Localización y transferencias: almacenamiento en el EEE y, para cualquier transferencia fuera, garantías del Capítulo V del RGPD |

**Derechos de los interesados.** Gooveris asiste al cliente en la atención de los derechos de sus interesados y le traslada sin dilación cualquier solicitud que reciba directamente, sin responderla por sí. La plataforma facilita la localización, exportación, rectificación y supresión de los datos de un interesado concreto desde el panel.

**Auditoría.** El cliente puede auditar el cumplimiento previo aviso razonable, en horario laboral, sin acceso a datos de otros clientes (cláusula D5.8).

---

## 5. Subencargados (subprocesadores)

| Subencargado | Servicio | Ubicación | Instrumento de transferencia |
|---|---|---|---|
| **DigitalOcean** | Alojamiento de la plataforma y de los proyectos | Frankfurt, Alemania (EEE) | No aplica |
| **Brevo** | Envío de correo transaccional por cuenta de los proyectos (confirmaciones, acreditaciones, recordatorios) | Francia (EEE) | No aplica |
| **OpenRouter** | Procesamiento de las peticiones de la funcionalidad de IA (ValerIA), de activación voluntaria | Estados Unidos | Cláusulas Contractuales Tipo (UE 2021/914) |

La lista está publicada y versionada en https://www.helice.app/subencargados. Cualquier alta o sustitución se notifica con **15 días naturales** de antelación, con derecho de oposición del cliente y, si esta no puede atenderse, resolución sin penalización y reembolso proporcional.

**Servicios que activa el cliente con sus propias credenciales.** Desde el área de Integraciones del panel, cada proyecto puede conectarse con servicios de terceros **usando las cuentas del propio cliente**, que entonces es quien contrata al proveedor y decide qué datos le envía — no son subencargados de Gooveris:

| Ámbito | Servicios |
|---|---|
| Cobros | Redsys, Bizum, CECA, Stripe (datos de tarjeta en el entorno de la pasarela, nunca en la plataforma) |
| Domiciliación | Generación de ficheros SEPA que el cliente entrega a su banco, sin intermediario |
| Correo | Brevo, SendGrid, Mailchimp, Mailgun, Microsoft 365 o Google vía OAuth, o SMTP propio |
| SMS | Twilio, SMSPubli |
| Push | Firebase Cloud Messaging y Apple Push Notification service |
| SEO y mapas | Google Search Console, Google Places |
| Multimedia | YouTube |
| Sistemas corporativos | Oracle y otros sistemas del cliente vía API |

Los editores de diseño usan además bancos de imágenes (Unsplash, Pixabay, Giphy), a los que solo se transmite el término de búsqueda que teclea el usuario del panel: no reciben datos de interesados ni contenido del proyecto.

**Comunicaciones exigidas por ley.** La emisión de facturas mediante Veri\*Factu implica la remisión de los registros de facturación a la Agencia Tributaria; no es un subencargo, sino una comunicación impuesta por la normativa tributaria.

---

## 6. Seguridad de la plataforma

### 6.1 Cifrado

- **En tránsito:** HTTPS con **TLS 1.2 y TLS 1.3** en todos los dominios (panel, webs de proyecto, apps y API); no se admiten versiones anteriores. Certificados Let's Encrypt con renovación automática y redirección de HTTP a HTTPS.
- **Credenciales del panel: no existen.** El acceso del equipo organizador es por código de un solo uso (OTP) o SSO, de modo que **no se almacena ninguna contraseña** de los usuarios del panel: la base de datos no dispone siquiera de un campo donde guardarlas (ver §6.2).
- **Credenciales de usuarios finales:** cuando un proyecto habilita el acceso con contraseña para sus inscritos, se almacena con **hash bcrypt** con sal. No se guarda en claro ni es recuperable, solo restablecible.
- **Datos de pago:** **no se almacenan**. El pago se realiza en el entorno de la pasarela, certificado PCI DSS, que devuelve únicamente el resultado de la operación.
- **En reposo:** el almacenamiento combina el disco de los propios servidores con volúmenes de bloque del proveedor, que aplica cifrado en reposo sobre estos últimos. Los soportes físicos y su ciclo de vida, incluida la destrucción segura al retirarlos, están bajo control del proveedor certificado.

### 6.2 Autenticación

El panel de gestión se basa en dos mecanismos, y **ninguno de ellos requiere que el usuario mantenga una contraseña**:

1. **Código de un solo uso (OTP)** enviado al correo del usuario. Verifica en cada acceso la titularidad de la dirección, caduca por sí solo y no deja ningún secreto permanente almacenado.
2. **Inicio de sesión corporativo (SSO)** con **Google, Microsoft (Azure AD) y LinkedIn**. La identidad la valida el proveedor corporativo del cliente, que aplica sus propias políticas de doble factor y dispositivos autorizados; dar de baja a una persona en ese directorio cierra automáticamente su acceso a Helice.app.

Para los **usuarios finales** (asistentes e inscritos), cada proyecto elige entre cuatro modos de identificación: código de un solo uso al correo, usuario y contraseña, un campo identificador del propio registro (número de colegiado, DNI, identificador corporativo) o **autenticación delegada** en un sistema del propio cliente a través de la API.

**Políticas de acceso configurables por proyecto.** Cuando el proyecto habilita el acceso con contraseña, el cliente define su política, que la plataforma **valida en el servidor** en todos los puntos donde puede crearse o cambiarse una contraseña —web pública, panel, formularios de inscripción, importaciones y API—, no solo en el navegador:

| Control | Qué permite |
|---|---|
| Longitud mínima | Entre 5 y 16 caracteres |
| Complejidad | Exigir letras, al menos una mayúscula y al menos un número |
| Caracteres especiales | Exigir al menos uno de los símbolos que el propio cliente define |
| Dominios autorizados | Restringir el registro a los dominios de correo de la organización |
| Sesión única | Un dispositivo activo por cuenta: impide compartir credenciales |
| Recuperación de contraseña | Por correo o **desactivada por completo** |

**Por qué esto es una ventaja de seguridad, y no solo una comodidad**

| Riesgo habitual | Situación en Helice.app |
|---|---|
| Robo de credenciales en una filtración de la base de datos | **No aplica al panel**: no hay contraseñas almacenadas, ni siquiera cifradas |
| Reutilización de credenciales contra otros servicios del usuario | **No aplica**: no hay nada reutilizable que extraer |
| Fuerza bruta y relleno de credenciales automatizado | **Sin objetivo**: no hay contraseña que adivinar |
| Secuestro mediante el flujo de «he olvidado mi contraseña» | **No existe ese flujo**: no hay enlace de restablecimiento que interceptar |
| Contraseñas débiles o compartidas dentro del equipo del cliente | **Irrelevante**: cada acceso exige el código del momento o la validación del proveedor de SSO |

### 6.3 Roles y permisos

El acceso al panel se organiza por **áreas funcionales** (inscripciones, contenidos, comunicaciones, facturación, control de accesos, etc.). El administrador del cliente da de alta a sus colaboradores y les asigna permisos **por área y por proyecto**, de modo que cada persona ve solo lo que necesita — mínimo privilegio. Las altas y bajas son inmediatas y las gestiona el propio cliente sin intervención de Gooveris.

Los niveles de administración transversal de la plataforma (**superadministrador** y **master**) están sujetos a un control adicional: **no pueden concederse desde la interfaz ni desde la API**, sino únicamente mediante intervención directa en la base de datos por personal autorizado, y su acceso se realiza con código de un solo uso. Una cuenta comprometida no puede elevar sus privilegios a través de la aplicación.

El acceso administrativo de Gooveris a los servidores se realiza exclusivamente mediante **clave pública SSH**, sin contraseña, desde equipos autorizados; cualquier otro intento se rechaza y bloquea. El acceso del personal a los datos de un proyecto se limita a lo necesario para prestar el soporte solicitado, y todo el personal está sujeto a deber de confidencialidad recogido en su contrato.

### 6.4 Protección perimetral

Varias capas de defensa actúan antes de que una petición alcance la aplicación:

- **Limitación de peticiones (rate limiting)** por dirección IP y por dominio, que absorbe picos legítimos y frena la automatización abusiva.
- **Bloqueo automático de direcciones IP** ante patrones característicos de ataque: rastreo de rutas inexistentes, exploración de rutas de WordPress y de paneles ajenos, peticiones malformadas, accesos denegados repetidos e intentos de conexión SSH. Las duraciones de bloqueo crecen con la gravedad.
- **Bloqueo de rastreadores abusivos** y de agentes conocidos por consumo indebido de recursos.
- **Restricción de métodos HTTP** a los necesarios y bloqueo de rutas y extensiones sensibles (configuración, copias, volcados de base de datos, ficheros ocultos).
- **Ocultación de la versión del servidor** y separación estricta entre directorio público y código de aplicación.

Como el bloqueo automático puede alcanzar a un usuario legítimo, Gooveris publica un servicio independiente en **seguridad.helice.app** donde cualquier usuario puede comprobar si su dirección está bloqueada y solicitar el desbloqueo inmediato, que se concede automáticamente si la dirección está vinculada a una sesión real. Todas las solicitudes quedan registradas.

### 6.5 Integraciones: API REST y webhooks

**API REST.** El acceso programático se realiza con **claves de API que emite el propio cliente** desde el panel, tantas como integraciones tenga, transmitidas en una cabecera de la petición. Toda petición sin clave válida se rechaza con **401 Unauthorized**, sin ejecutar operación alguna.

| Propiedad | Detalle |
|---|---|
| **Revocación** | Inmediata y granular: eliminar una clave corta esa integración en la siguiente petición, sin afectar a las demás |
| **Trazabilidad** | Cada clave muestra nombre, fecha de creación, fecha de último uso y número de peticiones acumuladas |
| **Alcance** | Cada clave opera solo sobre su proyecto; no existen claves transversales |
| **Custodia** | En el panel la clave se muestra enmascarada, con solo sus primeros y últimos caracteres |

**Webhooks.** El cliente puede recibir automáticamente los eventos del proyecto (alta de usuario, inicio de sesión, aprobación o cancelación de inscripción, recepción de formulario) en el sistema que indique:

- **Transporte cifrado y verificado**: entrega por HTTPS con **verificación del certificado del destino**; si el certificado no es válido, el envío falla en vez de entregar los datos.
- **Autenticación del origen**: el cliente puede exigir un token *bearer* o una cabecera secreta propia, de modo que su endpoint rechace cualquier petición que no venga de la plataforma.
- **Exclusión de datos sensibles**: el contenido enviado nunca incluye contraseña, tokens de sesión, datos de tarjeta, identificadores de la pasarela de pago, dispositivos ni direcciones IP.
- **Control**: cada webhook registra última respuesta, fecha y número de ejecuciones, y se desactiva en cualquier momento. Los envíos tienen tiempo máximo de espera y no se reintentan automáticamente, así que un endpoint caído no genera reenvíos ni colas pendientes.

### 6.6 Desarrollo seguro y gestión de vulnerabilidades

- Código gestionado con **Git**, con ramas separadas y despliegue controlado.
- **Entornos de desarrollo y pruebas separados** del de producción.
- El framework aplica de serie **consultas parametrizadas** —lo que neutraliza la inyección SQL—, validación de entradas y separación entre lógica de negocio y ficheros públicos.
- **Revisiones internas de seguridad del código**, cuyo resultado se traduce en un plan de corrección priorizado por gravedad.
- Componentes de sistema actualizados tras comprobación de compatibilidad.
- Canal de comunicación de vulnerabilidades: **info@helice.app**.

### 6.7 Trazabilidad

- **Historial de actividad** del proyecto: acciones relevantes del panel asociadas a usuario y fecha, consultables por el cliente, conservadas hasta **12 meses**.
- **Registros técnicos** de servidor y aplicación: cada petición con origen, recurso, resultado y tiempo de respuesta; errores e incidencias de ejecución.
- **Registro de bloqueos y desbloqueos** de direcciones IP, con motivo y resultado.

---

## 7. Copias de seguridad y continuidad

Cada servidor de producción realiza copias de seguridad automáticas programadas, que se replican **fuera del servidor de origen**, en la instalación propia de Gooveris en España.

| Elemento | Frecuencia | Alcance |
|---|---|---|
| Base de datos | Diaria | Copia completa |
| Ficheros de los proyectos (documentos, imágenes, adjuntos) | Cada 7 días | Copia completa |

- **Retención:** 30 días, con eliminación automática posterior.
- **Transferencia:** replicación cifrada mediante SSH.
- **Restauración:** total o parcial —un proyecto, una tabla, un conjunto de ficheros—. Las restauraciones parciales forman parte de la operación ordinaria (recuperación de datos borrados por error), lo que verifica de forma continua que las copias son utilizables.
- **Efecto sobre la supresión:** cuando un proyecto se elimina, sus datos dejan de estar accesibles de inmediato y desaparecen de las copias conforme estas rotan, en un plazo máximo de 30 días.

**Monitorización.** La supervisión se realiza en tres capas: **disponibilidad desde el exterior** con un servicio independiente (UptimeRobot), cuyo **histórico es público** en https://stats.uptimerobot.com/f918yFfjFp; **recursos de los servidores**, con métricas y alertas por umbrales del proveedor de infraestructura (CPU, memoria, disco, disponibilidad del nodo); y **controles internos de la propia plataforma**, incluido el visor de registros del servidor web y comprobaciones automáticas diarias.

**Continuidad.** Ante un fallo grave de un servidor, la recuperación se realiza sobre infraestructura nueva a partir de la última copia disponible. El despliegue en servidores independientes limita el alcance de cualquier incidente. Los recursos de cada servidor se dimensionan para la carga prevista y pueden ampliarse antes de eventos de gran afluencia si el cliente lo comunica con antelación.

---

## 8. Gestión de incidentes y brechas

| Fase | Actuación |
|---|---|
| **1. Detección** | Alertas de monitorización, análisis de registros técnicos o comunicación de un cliente o un tercero |
| **2. Clasificación** | Según naturaleza (error de software, ataque, fallo de proveedor) y gravedad, atendiendo especialmente a si afecta a datos personales |
| **3. Contención** | Medida inmediata que detiene el impacto: bloqueo del origen, desactivación de la funcionalidad afectada o restauración desde copia |
| **4. Corrección** | Corrección de fondo desplegada por el procedimiento de cambios habitual |
| **5. Comunicación** | Ante una brecha de datos personales, notificación al cliente **sin dilación indebida y como máximo en 72 horas** desde su conocimiento, con el contenido del art. 33.3 RGPD disponible, completándolo por fases si es necesario (cláusula D5.6 del DPA). La notificación a la autoridad de control y a los interesados corresponde al cliente, con la asistencia de Gooveris |
| **6. Análisis posterior** | Los incidentes con impacto en el servicio se documentan internamente —cronología, causa raíz y medidas correctoras— y las medidas resultantes se incorporan a la plataforma |

---

## 9. Certificaciones y acreditación del cumplimiento

**Gooveris Software, S.L. no dispone actualmente de certificación ISO/IEC 27001 ni de declaración de conformidad con el Esquema Nacional de Seguridad.** Lo indicamos de forma expresa: cuando un pliego exige esa certificación como criterio de solvencia, no la sustituimos por la de nuestros proveedores.

Lo que sí acreditamos, referido al servicio concreto que se contrata:

1. **Certificaciones de la infraestructura.** El centro de datos y los servicios de DigitalOcean cuentan con ISO/IEC 27001 y SOC 2. Los certificados se aportan a petición. Acreditan el alojamiento, no la organización.
2. **Medidas del artículo 32 del RGPD** publicadas, versionadas y **contractualmente vinculantes** a través del DPA: no son una declaración de intenciones, sino una obligación exigible, y su actualización no puede reducir el nivel de seguridad ofrecido.
3. **DPA formalizado** con la aceptación de las condiciones y **lista de subencargados publicada**, con notificación previa de cambios.
4. **Declaración responsable** de medidas de seguridad firmada por el representante legal, adaptable al pliego que la solicite.
5. **Derecho de auditoría** del cliente sobre el servicio prestado.
6. **Declaración responsable del sistema informático de facturación** conforme a Veri\*Factu.

### 9.1 Accesibilidad

Las salidas públicas —web del evento y aplicación móvil— se construyen con HTML semántico y diseño responsive, y Gooveris realiza revisiones internas puntuales sobre criterios como contraste de color, estructura de encabezados y textos alternativos. Los contenidos concretos los introduce el cliente desde el panel, por lo que el resultado final depende también de su edición.

**No existe auditoría externa ni declaración formal de conformidad con la norma EN 301 549 / WCAG 2.1.** Cuando un pliego lo exija —caso de los sujetos obligados por el Real Decreto 1112/2018—, la conformidad y su alcance se acuerdan en Condiciones Particulares.

---

## 10. Conservación, borrado y devolución de los datos

**Titularidad.** Los contenidos y datos del proyecto son del cliente en todo momento. Gooveris no los utiliza para fines propios ni los cede a terceros distintos de los subencargados publicados.

| Momento | Qué ocurre |
|---|---|
| **Durante la licencia** | Exportación autónoma a Excel y CSV desde el panel (inscritos, usuarios, contactos, acreditaciones, informes), en cualquier momento, sin coste ni solicitud previa |
| **Al expirar la licencia** | La web y la app dejan de ser públicas; el cliente conserva el acceso al panel, puede seguir trabajando y reactivar el proyecto conservando todo el trabajo realizado |
| **Periodo de conservación** | **90 días** desde la expiración, para reactivar el proyecto o solicitar la exportación de los datos |
| **Transcurrido el plazo** | Eliminación definitiva de los datos, incluidos los personales, y de las copias existentes conforme al ciclo técnico de las copias de seguridad, salvo obligación legal de conservación (con bloqueo ex art. 32 LOPDGDD) |
| **A petición del cliente** | Eliminación del proyecto en cualquier momento: queda en la papelera, desde donde puede recuperarse o vaciarse para una eliminación irreversible |
| **Elección al finalizar** | Devolución (exportación) o supresión, **a elección del cliente**, conforme a la cláusula D5.7 del DPA |

---

## 11. Disponibilidad y soporte

**Disponibilidad.** La plataforma se monitoriza de forma continua con alertas automáticas, y su **histórico de disponibilidad es de consulta pública** en https://stats.uptimerobot.com/f918yFfjFp, sin necesidad de solicitarlo. Gooveris presta el servicio con la diligencia exigible a una empresa especializada y trabaja con un objetivo de disponibilidad elevado. Conforme a la cláusula 9 de los Términos y Condiciones, **las condiciones generales no constituyen un compromiso contractual de nivel de servicio: el SLA con porcentaje garantizado, exclusiones y consecuencias se pacta en Condiciones Particulares** cuando el cliente lo requiere. Es el mecanismo previsto para contratos que exigen niveles de servicio garantizados.

**Mantenimiento.** Las intervenciones que puedan afectar al servicio se comunican con antelación razonable siempre que es posible y se planifican fuera de las fechas críticas del evento cuando el cliente las traslada.

**Soporte.**

| Nivel | Canal | Horario |
|---|---|---|
| **Estándar** (incluido) | Sistema de tickets del panel y correo a info@helice.app, con trazabilidad de cada incidencia | Horario laboral |
| **Reforzado** (contratable) | Los anteriores más contacto directo y horario ampliado durante las fechas críticas del evento | A convenir en Condiciones Particulares |

Complementado por el **centro de ayuda** en help.helice.app, con documentación, guías y vídeos.

---

## 12. Cumplimiento fiscal

La facturación emitida por la plataforma cumple con **Veri\*Factu**, el sistema de facturación verificable de la Agencia Tributaria española: los registros de facturación se generan encadenados e inalterables y se remiten a la AEAT. Existe declaración responsable del sistema informático de facturación, disponible para el cliente que la requiera.

Medios de cobro soportados para inscripciones: Redsys, Bizum, CECA, Stripe, transferencia bancaria, efectivo y domiciliación SEPA para cuotas. La plataforma no recibe ni almacena datos de tarjeta.

---

## 13. Documentación aportable y contacto

A petición del cliente o del órgano de contratación:

- Certificados ISO/IEC 27001 y SOC 2 del proveedor de infraestructura
- Términos y Condiciones con el DPA integrado
- Medidas de seguridad del art. 32 RGPD y lista de subencargados
- Declaración responsable de medidas de seguridad, firmada por el representante legal
- Declaración responsable del sistema informático de facturación (Veri\*Factu)
- Escritura de constitución, poderes del firmante y datos registrales
- Detalle de versiones de componentes, bajo régimen de confidencialidad

**Contacto para cuestiones de seguridad y protección de datos:** info@helice.app

**Documentos vinculados, públicos y versionados:**
[Términos y Condiciones](https://www.helice.app/terminos-de-uso) · [Medidas de seguridad](https://www.helice.app/seguridad) · [Subencargados](https://www.helice.app/subencargados) · [Política de privacidad](https://www.helice.app/politica-de-privacidad)
