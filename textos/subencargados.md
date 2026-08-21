# LISTA DE SUBENCARGADOS DE HELICE.APP
**Versión v1.0-2-g4c21e27**

Conforme a la cláusula D8 del [Acuerdo de Encargo de Tratamiento](/terminos-de-uso#dpa), integrado en los Términos y Condiciones Generales de Helice.app, el Cliente autoriza de forma general el recurso de Gooveris a los siguientes subencargados para la prestación del servicio. Gooveris impone a cada uno de ellos, por contrato, obligaciones equivalentes a las de dicho acuerdo, y responde plenamente ante el Cliente de su cumplimiento (art. 28.4 RGPD).

## 1. Subencargados

Proveedores a los que Gooveris recurre para prestar el servicio, con sus propias cuentas.

| Subencargado | Servicio prestado | Ubicación del tratamiento | Instrumento de transferencia | Datos que trata |
|---|---|---|---|---|
| **DigitalOcean** | Alojamiento (hosting) de la Plataforma y de los Proyectos de los Clientes | Frankfurt, Alemania (Espacio Económico Europeo) | No aplica (tratamiento dentro del EEE) | Todos los datos de los Proyectos, incluidos los de asistentes, inscritos y demás interesados gestionados por el Cliente |
| **Brevo** | Envío de correos transaccionales **por cuenta de los Proyectos de los Clientes** (p. ej., confirmaciones de inscripción o acreditaciones a asistentes, recordatorios del evento), cuando el Proyecto no configura un servicio de correo propio | Unión Europea (Francia) | No aplica (tratamiento dentro del EEE) | Datos de contacto necesarios para el envío: nombre y correo electrónico del destinatario, y el contenido del propio correo transaccional |
| **OpenRouter** | Procesamiento de las peticiones de la funcionalidad de inteligencia artificial **ValerIA** (cláusula 6 bis de los Términos y Condiciones), que enruta cada petición al modelo de lenguaje seleccionado | Estados Unidos | Cláusulas Contractuales Tipo (Decisión de Ejecución UE 2021/914) | El texto que el Cliente envía en cada petición, las métricas agregadas del Proyecto cuando solicita un informe de módulo y, en las acciones que lo indican, la imagen que aporta o la captura del diseño que está editando. **No se le envían el nombre, el correo ni el teléfono de los inscritos, asistentes ni demás interesados finales del Proyecto.** ValerIA se activa por iniciativa del Cliente: sin uso de la funcionalidad, no hay tratamiento |

## 2. Servicios que activa el Cliente con sus propias credenciales

La Plataforma permite conectar cada Proyecto con servicios de terceros **usando las cuentas y credenciales del propio Cliente**, que se configuran desde el área de Integraciones del panel. En estos casos el Cliente contrata directamente al proveedor y decide qué datos le envía, de modo que ese proveedor **no es un subencargado de Gooveris**, sino un proveedor propio del Cliente, con quien debe regular su relación.

| Ámbito | Servicios disponibles | Para qué |
|---|---|---|
| **Cobros** | **Redsys**, **Bizum**, **CECA**, **Stripe** | Cobro de inscripciones, entradas, cuotas y compras de la tienda. Los datos de tarjeta se introducen en el entorno de la pasarela, certificado PCI DSS: **Helice.app no los recibe ni los almacena** |
| **Domiciliación bancaria** | Ficheros SEPA (norma ISO 20022) | La Plataforma genera el fichero de adeudos que el Cliente entrega a su propia entidad bancaria; no hay intermediario |
| **Correo electrónico** | **Brevo**, **SendGrid**, **Mailchimp**, **Mailgun**, **Microsoft 365 o Google mediante OAuth**, o cualquier **servidor SMTP propio** | Envío de las comunicaciones del Proyecto desde el dominio y la cuenta del Cliente |
| **SMS** | **Twilio**, **SMSPubli** | Comunicaciones por SMS a los inscritos |
| **Notificaciones push** | **Firebase Cloud Messaging** (Google) y **Apple Push Notification service** | Avisos a la aplicación móvil del Proyecto, con el proyecto de Firebase y la cuenta de desarrollador del Cliente |
| **Posicionamiento y mapas** | **Google Search Console**, **Google Places** | Verificación del sitio del evento y datos de localización |
| **Contenido multimedia** | **YouTube** | Publicación e incrustación de vídeos del evento |
| **Sistemas corporativos** | **Oracle** y otros sistemas del propio Cliente vía API | Sincronización con el ERP, CRM o sistema de gestión del Cliente |

Cuando el Cliente no configura un servicio propio de correo, los envíos del Proyecto se cursan a través del subencargado indicado en el apartado 1.

## 3. Servicios auxiliares que no tratan datos personales

Para completar la información, la Plataforma utiliza además bancos de imágenes y contenido (**Unsplash**, **Pixabay**, **Giphy**) en los editores de diseño. A estos servicios solo se les transmite el término de búsqueda que teclea el usuario del panel; no reciben datos de los interesados ni contenido del Proyecto, por lo que no tienen la condición de subencargados.

## 4. Comunicaciones exigidas por ley

La emisión de facturas mediante el sistema **Veri\*Factu** implica la remisión de los registros de facturación a la **Agencia Estatal de Administración Tributaria**. No se trata de un subencargo, sino de una comunicación de datos impuesta por la normativa tributaria española, en la que la Administración actúa como responsable del tratamiento.

## Notificación de altas y sustituciones

Cualquier alta o sustitución de subencargado se notificará al Cliente (correo designado en su cuenta o aviso en el panel) con una antelación mínima de **quince (15) días naturales** antes de que el nuevo subencargado trate datos, conforme a la cláusula D8.2 del DPA. El Cliente podrá oponerse por motivos justificados relacionados con la protección de datos dentro de ese plazo.

## Contacto

Para cualquier duda sobre esta lista: **info@helice.app**.
