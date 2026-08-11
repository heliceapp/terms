# MEDIDAS DE SEGURIDAD DE HELICE.APP

**Versión: [n.º] · Fecha de publicación: [fecha]**

Este documento describe las **medidas técnicas y organizativas** que Helice.app aplica para garantizar un nivel de seguridad adecuado al riesgo, conforme al **artículo 32 del RGPD**. Forma parte del [Acuerdo de Encargo de Tratamiento (DPA)](/terminos-de-uso#dpa) de los [Términos y Condiciones](/terminos-de-uso). Las medidas se revisan y actualizan periódicamente, sin reducir el nivel de seguridad ofrecido.

## 1. Alojamiento y ubicación de los datos

La infraestructura de Helice.app está alojada en **DigitalOcean**, en su centro de datos de **Frankfurt (Alemania)**, de modo que los datos se tratan dentro del Espacio Económico Europeo.

> ⚠️ **MAQUETA · PENDIENTE** — Pendiente: confirmar regiones exactas, redundancia geográfica y si algún servicio auxiliar (correo, CDN, copias) trata datos fuera del EEE.

## 2. Cifrado

> ⚠️ **MAQUETA · PENDIENTE** — Pendiente: cifrado en tránsito (TLS/HTTPS, versión mínima, HSTS), cifrado en reposo de base de datos y almacenamiento, y gestión de claves y secretos.

## 3. Control de accesos

El panel de gestión, reservado al equipo organizador, admite inicio de sesión corporativo (**SSO**) con Google, Microsoft Azure AD o LinkedIn, además del acceso con usuario y contraseña propios. Este inicio de sesión corporativo aplica solo al equipo que administra el evento: los asistentes e inscritos se identifican siempre con su email, sin necesidad de SSO.

> ⚠️ **MAQUETA · PENDIENTE** — Pendiente: modelo de roles y permisos por área/evento (mínimo privilegio), políticas de contraseña y código de un solo uso, doble factor del equipo interno, y gestión de altas/bajas de accesos.

## 4. Registro de actividad y trazabilidad

> ⚠️ **MAQUETA · PENDIENTE** — Pendiente: qué se registra en los logs de acceso y actividad, y durante cuánto tiempo se conservan y cómo se protegen.

## 5. Copias de seguridad y recuperación

> ⚠️ **MAQUETA · PENDIENTE** — Pendiente: frecuencia de las copias, retención y cifrado de las mismas, y pruebas de restauración (objetivos RPO/RTO).

## 6. Seguridad de la aplicación y del desarrollo

> ⚠️ **MAQUETA · PENDIENTE** — Pendiente: prácticas de desarrollo seguro y revisión de código, gestión de vulnerabilidades y actualizaciones, protección frente a ataques comunes, y separación de entornos.

## 7. Resiliencia y continuidad

La disponibilidad de la plataforma se monitoriza de forma continua y puede consultarse públicamente en la [página de estado del servicio](#estado).

> ⚠️ **MAQUETA · PENDIENTE** — Pendiente: disponibilidad y resiliencia de los sistemas (redundancia, monitorización) y plan de continuidad / recuperación ante desastres.

## 8. Gestión de incidentes y brechas de seguridad

Ante una violación de seguridad de los datos personales, Gooveris notifica al Cliente sin dilación indebida (a más tardar, 72 horas desde que tiene conocimiento), conforme a la cláusula D5.f del DPA.

> ⚠️ **MAQUETA · PENDIENTE** — Pendiente: describir el procedimiento interno de detección, respuesta y notificación.

## 9. Subencargados

Los proveedores que tratan datos personales por cuenta de Gooveris y sus garantías se detallan en la [lista de subencargados](/subencargados), Documento Vinculado del DPA.

## 10. Medidas organizativas

> ⚠️ **MAQUETA · PENDIENTE** — Pendiente: compromisos de confidencialidad del personal, formación y concienciación, políticas internas de seguridad y contacto responsable de seguridad/privacidad.

---

¿Buscas el resto de condiciones? Consulta los [Términos y Condiciones Generales de Helice.app](/terminos-de-uso).

---

## Notas de cierre (no publicables)
