# Documentos legales de Helice.app

Textos legales **publicables** de Helice.app, servicio de GOOVERIS SOFTWARE S.L.

Este repositorio es la **fuente única de verdad** de lo que se publica en la web y de lo que acepta cada cliente al contratar. La web y el panel leen de aquí.

---

## Para qué existe

Los Términos y Condiciones establecen (cláusula 3.4) que a cada contratación le aplica **la versión vigente en la fecha del documento o del pago**, en lugar de citar un número de versión en cada factura.

Eso solo es sostenible si la versión es **determinable a posteriori**, lo que exige dos cosas que este repositorio garantiza:

1. Cada versión publicada lleva **fecha visible**.
2. Las versiones anteriores quedan **archivadas y accesibles** de forma permanente.

Dicho de otro modo: si dentro de tres años un cliente pregunta qué aceptó exactamente, la respuesta está aquí y es verificable.

---

## Cómo funcionan las versiones

Cada versión publicada se marca con una **etiqueta de Git** con su fecha:

```
git tag -a v3.0 -m "Versión publicada el 5 de agosto de 2026"
git push origin v3.0
```

A partir de ahí:

- **La web** muestra siempre la última versión etiquetada.
- **El panel** guarda, en cada aceptación, **la etiqueta de la versión + la fecha y hora**.
- **Cada licencia contratada** queda asociada a la versión que se firmó.
- **El cliente** puede consultar en cualquier momento la suya, mediante un enlace permanente a esa etiqueta o un PDF generado a partir de ella.

⚠️ **No se modifica una versión ya etiquetada.** Cualquier cambio, por pequeño que sea, es una versión nueva. Es lo que hace que la remisión "la versión vigente en la fecha X" tenga valor probatorio.

---

## Qué contiene

| Documento | Publicado en |
|---|---|
| [`textos/terminos-y-condiciones.md`](textos/terminos-y-condiciones.md) | `/terminos-de-uso` |
| [`textos/politica-de-privacidad.md`](textos/politica-de-privacidad.md) | `/politica-de-privacidad` |
| [`textos/politica-de-cookies.md`](textos/politica-de-cookies.md) | `/politica-de-cookies` |
| [`textos/aviso-legal.md`](textos/aviso-legal.md) | `/aviso-legal` |
| [`textos/politica-de-uso-razonable.md`](textos/politica-de-uso-razonable.md) | `/uso-razonable` |
| [`textos/subencargados.md`](textos/subencargados.md) | `/subencargados` |

Los cuatro últimos son **Documentos Vinculados** de los Términos y Condiciones: forman parte del contrato aunque se publiquen aparte.

---

## Reglas de este repositorio

**Aquí solo entra texto publicable.** Nunca notas de trabajo, comentarios para el abogado, dudas pendientes ni registros de decisiones. Todo eso vive en el repositorio privado del proyecto (`helice-nueva-web`, carpeta `legal/`), que es donde se redacta.

El flujo es: **se redacta en privado → se revisa → se publica aquí ya limpio → se etiqueta**.

---

## Estado actual

⚠️ **Versión de trabajo, pendiente de revisión por abogado.** Todavía no hay ninguna etiqueta publicada: la primera se creará cuando el abogado valide el paquete, justo antes del lanzamiento de la web.

Al publicarlos por primera vez hay que **avisar a todos los clientes** de la actualización de los Términos y Condiciones: cambian condiciones sustanciales.

---

**GOOVERIS SOFTWARE S.L.** · CIF B56077100 · Avda. de la Torrecilla 16, Edificio La Torre II, Oficina 210, 14013 Córdoba · info@helice.app
