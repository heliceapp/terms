# INFORMACIÓN PARA LICITACIONES Y PLIEGOS
**Versión dcb6d1d**

## 1. Datos de la entidad

| Dato | Valor |
|---|---|
| **Razón social** | GOOVERIS SOFTWARE, S.L. |
| **Nombre comercial** | Helice.app (helice es un servicio de Gooveris) |
| **CIF** | B56077100 |
| **Domicilio social** | Avda. de la Torrecilla 16, Oficina 210. 14013 Córdoba (España) |
| **Datos registrales** | Registro Mercantil de Córdoba, tomo 2.585, folio 31, hoja CO-38.259, inscripción 1.ª |
| **Contacto** | info@helice.app |
| **Sitio web** | https://www.helice.app |

Los mismos datos, con el detalle exigido por el artículo 10 de la LSSI, están publicados en el [aviso legal](/aviso-legal).

## 2. Objeto del servicio

Helice.app es una **plataforma SaaS de gestión integral de eventos**: inscripciones y acreditaciones, control de accesos, web y app del evento, agenda y programa, revisión científica, networking, certificados, facturación y comunicaciones, entre otros módulos. El catálogo completo está publicado en la [página de funcionalidades](/funcionalidades), con valor descriptivo.

La contratación es por **licencia anual y por evento**, con precios públicos consultables en la [página de precios](/precios), lo que facilita justificar económicamente una oferta sin tener que solicitar presupuesto aparte.

## 3. Alojamiento y ubicación de los datos

| Dato | Valor |
|---|---|
| **Proveedor de infraestructura** | DigitalOcean |
| **Ubicación del centro de datos** | Frankfurt (Alemania) |
| **Tratamiento dentro del EEE** | Sí — los datos del servicio se tratan en el Espacio Económico Europeo |
| **Modelo de despliegue** | Multi-tenant en la nube (SaaS), sobre varios servidores independientes |
| **Copias de seguridad** | Replicadas en instalación propia de Gooveris, en sus oficinas de Córdoba (España), con acceso físico restringido |
| **Certificaciones del proveedor** | ISO/IEC 27001 y SOC 2 (aportables a petición) |
| **Estado del servicio** | Histórico de disponibilidad de consulta pública: https://stats.uptimerobot.com/f918yFfjFp |

Los Proyectos de un mismo cliente residen en un servidor concreto de la plataforma. Este reparto aporta **contención**: una incidencia en un servidor no afecta a los Proyectos alojados en los demás.

**Servicios auxiliares fuera del EEE.** El único tratamiento fuera del Espacio Económico Europeo es el de la funcionalidad de inteligencia artificial **ValerIA**, cuyas peticiones se procesan a través de un proveedor establecido en Estados Unidos, amparado en las Cláusulas Contractuales Tipo. Es una funcionalidad de activación voluntaria: si el Cliente no la utiliza, no se produce ninguna transferencia internacional. El alojamiento, el envío de correo transaccional y las copias de seguridad se realizan íntegramente dentro del EEE. Todo ello se detalla en la [lista de subencargados](/subencargados).

## 4. Stack tecnológico

| Capa | Tecnología |
|---|---|
| **Backend** | PHP con framework Laravel, bajo arquitectura MVC |
| **Base de datos** | MySQL |
| **Servidor web** | nginx con PHP-FPM, sobre sistema operativo Linux (Ubuntu Server) |
| **Frontend web** | HTML5, CSS3 y JavaScript; diseño responsive, sin requisitos de complementos ni instalación en el puesto del usuario |
| **Aplicaciones móviles** | Apps nativas para iOS y Android generadas por proyecto, con notificaciones push |
| **Tareas programadas y procesos en segundo plano** | Ejecución programada mediante cron del sistema (recordatorios, automatizaciones, sincronizaciones, mantenimiento diario) |
| **Cifrado en tránsito** | HTTPS con TLS 1.2 y TLS 1.3 (certificados Let's Encrypt con renovación automática) |
| **APIs** | API REST propia para integración con CRM, ERP y sistemas de terceros, con autenticación por token |
| **Control de versiones** | Git, con entornos de desarrollo, pruebas y producción separados |

**Requisitos en el puesto del cliente:** ninguno más allá de un navegador web actualizado. La plataforma no requiere instalación local, licencias adicionales ni componentes en el equipo del usuario.

**Sobre las versiones concretas de los componentes:** por política de seguridad, Gooveris no publica el número de versión exacto de los componentes de su infraestructura, ya que esa información facilita la búsqueda de vulnerabilidades conocidas contra un objetivo determinado. Se facilita al órgano de contratación que lo requiera, dentro del procedimiento y con el tratamiento de confidencialidad que corresponda.

## 5. Protección de datos

En la prestación del servicio, Gooveris actúa como **encargado del tratamiento** respecto de los datos que el cliente gestiona en su evento, y como **responsable** respecto de los datos de su propia relación comercial. El reparto está detallado en la [política de privacidad](/politica-de-privacidad).

| Dato | Valor |
|---|---|
| **Acuerdo de encargo (DPA)** | Incorporado a los [Términos y Condiciones](/terminos-de-uso) — no requiere firma de un documento aparte |
| **Medidas del art. 32 RGPD** | Publicadas en [medidas de seguridad](/seguridad), como Documento Vinculado |
| **Subencargados** | Publicados y versionados en [la lista de subencargados](/subencargados) |
| **Notificación de brechas** | Sin dilación indebida y, a más tardar, en 72 horas desde su conocimiento |
| **Categorías especiales de datos** | Admitidas las accesorias habituales en eventos (alergias, accesibilidad, salud declarada voluntariamente), bajo responsabilidad del cliente (cláusula D4.2 del DPA) |
| **Auditorías del cliente** | Admitidas previo aviso razonable, conforme a la cláusula D5.8 del DPA |
| **Fin del contrato** | Supresión o devolución de los datos a elección del cliente, con supresión cierta a los 90 días |

**Cliente que actúa por cuenta de un tercero.** Si quien contrata es una agencia, un OPC o una entidad que organiza el evento para un tercero, el DPA contempla expresamente esa cadena: el cliente es encargado del responsable final y Gooveris subencargado (cláusula D7 del DPA). Es la figura habitual cuando la adjudicataria de un contrato público organiza el congreso de un organismo.

## 6. Conservación, borrado y devolución de los datos

| Momento | Qué ocurre |
|---|---|
| **Durante la licencia** | El cliente puede exportar en cualquier momento los datos de su proyecto (inscritos, usuarios, contactos, acreditaciones, informes) a Excel y CSV desde el propio panel, sin coste ni solicitud previa |
| **Al expirar la licencia** | El sitio web y la app dejan de ser públicos, pero el cliente conserva el acceso al panel y puede seguir trabajando o reactivar el proyecto |
| **Periodo de conservación** | 90 días desde la expiración, durante los cuales puede reactivarse el proyecto o solicitarse la exportación de los datos |
| **Transcurrido el plazo** | Eliminación definitiva de los datos, incluidos los personales, y de las copias existentes conforme al ciclo técnico de las copias de seguridad, salvo obligación legal de conservación |
| **A petición del cliente** | El cliente puede eliminar su proyecto en cualquier momento; queda en la papelera, desde donde puede recuperarlo o vaciarla para una eliminación irreversible |

El régimen completo está en las cláusulas 12.3 de los Términos y D5.7 del DPA. **La titularidad de los contenidos y datos del proyecto es del cliente en todo momento** (cláusula 27); Gooveris no los utiliza para fines propios.

## 7. Seguridad

Las medidas técnicas y organizativas están descritas en detalle en la página de [medidas de seguridad](/seguridad), que incluye alojamiento, cifrado, control de accesos, trazabilidad, copias de seguridad, seguridad del desarrollo, resiliencia y gestión de incidentes.

Resumen de lo que suele pedirse en un pliego:

- **Cifrado en tránsito** con TLS 1.2/1.3 en todos los dominios y **sin almacenamiento de datos de tarjeta** (delegados en la pasarela certificada PCI DSS).
- **Autenticación sin contraseña en el panel**: el acceso del equipo organizador se realiza con **código de un solo uso (OTP)** enviado al correo o con **inicio de sesión corporativo (SSO)** de Google, Microsoft (Azure AD) o LinkedIn. La plataforma **no almacena contraseñas de los usuarios del panel** —no existe campo para ellas— ni dispone de flujo de recuperación de contraseña, con lo que desaparecen el robo de credenciales en una filtración, la fuerza bruta y el secuestro de cuentas por el mecanismo de restablecimiento. Las contraseñas de los usuarios finales, cuando el proyecto las habilita, se almacenan con hash bcrypt.
- **Baja centralizada**: con SSO, dar de baja a una persona en el directorio corporativo del cliente cierra automáticamente su acceso a la plataforma.
- **Política de contraseñas propia por proyecto**, validada en servidor en todos los puntos de alta (web, panel, formularios, importaciones y API): longitud mínima configurable, exigencia de letras, mayúsculas, números y de caracteres especiales definidos por el cliente; restricción del registro a dominios de correo autorizados; sesión única por cuenta para impedir credenciales compartidas; y recuperación de contraseña habilitable o desactivable.
- **Autenticación delegada**: un proyecto puede validar a sus usuarios contra un sistema propio del cliente mediante la API, sin que la plataforma custodie credenciales.
- **API REST con claves revocables**: las emite el propio cliente desde el panel (una por integración), se transmiten en cabecera y toda petición sin clave válida se rechaza con **401 Unauthorized**. Cada clave registra su último uso y su número de peticiones, y se revoca de forma inmediata e independiente de las demás.
- **Webhooks seguros**: entrega por HTTPS con verificación del certificado del destino, autenticación del origen mediante token o cabecera secreta que define el cliente, y exclusión sistemática de datos sensibles del contenido enviado (contraseñas, tokens, tarjetas, identificadores de pasarela, dispositivos e IPs).
- **Roles y permisos** por áreas funcionales y por proyecto, gestionados por el propio cliente, con altas y bajas inmediatas y criterio de mínimo privilegio. Los niveles de administración transversal de la plataforma no pueden concederse desde la interfaz ni desde la API, solo mediante intervención directa en base de datos: **una cuenta comprometida no puede elevar sus privilegios a través de la aplicación**.
- **Protección perimetral**: limitación de peticiones por IP y por dominio, bloqueo automático de direcciones ante patrones de ataque, bloqueo de rastreadores abusivos y de rutas sensibles, restricción de métodos HTTP.
- **Trazabilidad**: historial de acciones por usuario y proyecto consultable desde el panel (hasta 12 meses) y registros técnicos de servidor y aplicación.
- **Copias de seguridad**: copia completa diaria de la base de datos y semanal de los ficheros de los proyectos, replicadas cifradas fuera del servidor de origen, con 30 días de retención y restauración tanto total como parcial.
- **Gestión de incidentes** con procedimiento documentado y notificación de brechas en 72 horas.

## 8. Certificaciones y acreditación del cumplimiento

Gooveris Software, S.L. **no dispone actualmente de certificación ISO/IEC 27001 ni de declaración de conformidad con el Esquema Nacional de Seguridad (ENS)**.

Lo que sí puede acreditar en un procedimiento de licitación:

1. **Certificaciones de la infraestructura**: el centro de datos y los servicios de DigitalOcean, donde se aloja la plataforma, cuentan con ISO/IEC 27001 y SOC 2; los certificados se aportan a petición.
2. **Medidas del artículo 32 del RGPD** publicadas, versionadas y **contractualmente vinculantes** a través del DPA integrado en los Términos y Condiciones — es decir, no una declaración de intenciones, sino una obligación exigible referida a la plataforma y a los servicios concretos objeto del contrato.
3. **Acuerdo de encargo de tratamiento** ya formalizado con la aceptación de las condiciones, sin necesidad de firma adicional, y **lista de subencargados publicada y versionada** con notificación previa de cambios.
4. **Declaración responsable** firmada por el representante legal sobre las medidas de seguridad aplicadas, adaptada al pliego que la solicite.
5. **Derecho de auditoría** del cliente sobre el servicio prestado (cláusula D5.8 del DPA).
6. **Declaración responsable del sistema informático de facturación** conforme a Veri\*Factu, disponible en el centro de ayuda.

> **Nota para el órgano de contratación:** cuando un pliego exige ISO 27001 o conformidad ENS como criterio de solvencia técnica, Gooveris lo indica expresamente en su oferta en lugar de sustituirlo por certificaciones de terceros. La certificación de la infraestructura acredita el centro de datos, no la organización.

## 9. Cumplimiento fiscal y medios de pago

La facturación que emite la plataforma cumple con **Veri\*Factu**, el sistema de facturación verificable de la Agencia Tributaria española: los registros de facturación se generan encadenados e inalterables y se remiten a la AEAT. Existe **declaración responsable del sistema informático de facturación**, disponible para el cliente que la requiera.

Los medios de cobro soportados para las inscripciones incluyen Redsys, Bizum, CECA, Stripe, transferencia bancaria, efectivo y domiciliación SEPA para cuotas. La plataforma no recibe ni almacena datos de tarjeta.

## 10. Disponibilidad y soporte

**Disponibilidad.** La plataforma se monitoriza de forma continua —disponibilidad desde el exterior con un servicio independiente, recursos de los servidores con alertas por umbrales del proveedor y controles internos propios—, y el **histórico de disponibilidad es de consulta pública** en https://stats.uptimerobot.com/f918yFfjFp, sin necesidad de solicitarlo.

Gooveris trabaja con un objetivo de disponibilidad elevado, sin que las condiciones generales constituyan un compromiso contractual de nivel de servicio (SLA): conforme a la cláusula 9 de los Términos y Condiciones, **el SLA se pacta expresamente en Condiciones Particulares** cuando el cliente lo requiere, y es en ese documento donde se fijan el porcentaje comprometido, las exclusiones y las consecuencias de su incumplimiento. Es el mecanismo previsto para las licitaciones que exigen niveles de servicio garantizados.

**Mantenimiento.** Las intervenciones que puedan afectar al servicio se comunican con antelación razonable siempre que es posible, y se planifican fuera de las fechas críticas del evento cuando el cliente las traslada.

**Soporte.**

| Nivel | Canal | Horario |
|---|---|---|
| **Estándar** (incluido en toda licencia) | Sistema de tickets del panel y correo a info@helice.app, con trazabilidad completa de cada incidencia | Horario laboral |
| **Reforzado** (contratable por proyecto) | Los anteriores más contacto directo y horario ampliado durante las fechas críticas del evento | A convenir en Condiciones Particulares |

Se complementa con el **centro de ayuda** (help.helice.app), con documentación, guías y vídeos.

## 11. Accesibilidad

Las salidas públicas de la plataforma —web del evento y aplicación móvil— se construyen con HTML semántico y diseño responsive, y se prueban en los navegadores y dispositivos de uso mayoritario. Gooveris realiza **revisiones internas puntuales de accesibilidad** sobre criterios como el contraste de color, la estructura de encabezados y los textos alternativos de las imágenes.

Los contenidos concretos de cada proyecto (textos, imágenes, documentos, textos alternativos) los introduce el cliente desde el panel, por lo que el nivel de accesibilidad final depende también de su edición.

**Gooveris no dispone actualmente de una auditoría externa ni de una declaración formal de conformidad con la norma EN 301 549 / WCAG 2.1.** Cuando un pliego lo exija —caso habitual de los sujetos obligados por el Real Decreto 1112/2018—, la conformidad y su alcance se acuerdan en Condiciones Particulares, incluyendo, si procede, la revisión del proyecto concreto y la publicación de su declaración de accesibilidad.

## 12. Documentación aportable

A petición del órgano de contratación o del cliente:

- Certificados ISO/IEC 27001 y SOC 2 del proveedor de infraestructura.
- Términos y Condiciones con el DPA integrado (documento único, con control de versiones).
- Medidas de seguridad del artículo 32 RGPD y lista de subencargados.
- Declaración responsable de medidas de seguridad, firmada por el representante legal.
- Declaración responsable del sistema informático de facturación (Veri\*Factu).
- Escritura de constitución, poderes del firmante y datos registrales.
- Detalle de versiones de componentes, bajo el régimen de confidencialidad del apartado 4.
