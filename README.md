# Documentos legales de Helice.app
**Versión v1.0-2-g4c21e27**

Textos legales **publicables** de Helice.app, servicio de GOOVERIS SOFTWARE S.L.

Este repositorio es la **fuente única de verdad** de lo que se publica en la web y de lo que acepta cada cliente al contratar. La web y el panel leen de aquí.

---

## Para qué existe

Los Términos y Condiciones establecen (cláusula 3.4) que a cada contratación le aplica **la versión vigente en la fecha del documento o del pago**, en lugar de citar un número de versión en cada factura.

Eso solo es sostenible si la versión es **determinable a posteriori**, lo que exige dos cosas que este repositorio garantiza:

1. Cada versión publicada lleva visible **el identificador exacto del commit del que procede**, del que se obtiene su fecha y hora.
2. Las versiones anteriores quedan **archivadas y accesibles** de forma permanente.

Dicho de otro modo: si dentro de tres años un cliente pregunta qué aceptó exactamente, la respuesta está aquí y es verificable.

---

## Cómo funcionan las versiones

### La línea de versión se escribe sola

En este repositorio, la segunda línea de cada documento se escribe así:

```
**Versión {{version}}**
```

No hay que rellenarla a mano. Tras cada `push` a `main`, el workflow
[`.github/workflows/sellar-version.yml`](.github/workflows/sellar-version.yml) la reescribe
con el identificador real de esa versión, calculado con `git describe --tags --always`:

| Estado del repositorio | Queda escrito en el documento |
|---|---|
| El commit está etiquetado | `**Versión v3.0**` |
| Hay 2 commits después de la etiqueta | `**Versión v3.0-2-g143bf6a**` |
| Todavía no hay ninguna etiqueta | `**Versión 7fd6bdc**` |

Se sellan todos los documentos de [`textos/`](textos/) y también este README. En cada
fichero se reescribe **únicamente la primera línea que tenga esa forma**, de modo que el
ejemplo del bloque de código de aquí arriba no se ve afectado.

Ese identificador es lo que hace verificable cada documento: a partir de él se recupera el
texto exacto que se publicó y su fecha y hora (ver [Consultar una versión concreta](#consultar-una-versión-concreta)).

Como el workflow deja un commit propio en `main`, **hay que hacer `git pull` antes de
volver a editar** (el botón *Sync Changes* de VS Code ya lo hace). Nunca hay conflicto:
esa línea no se toca a mano.

### Publicar una versión

Cada versión publicada se marca con una **etiqueta de Git** con su fecha, y se sube
junto al commit con `--follow-tags`:

```
git tag -a v3.0 -m "Versión publicada el 5 de agosto de 2026"
git push --follow-tags
```

Subir la etiqueta **a la vez** que el commit hace que el workflow la vea a la primera y
deje los documentos sellados como `**Versión v3.0**` con un solo commit. Si se sube después,
por separado, el workflow se ejecuta dos veces y deja dos commits: uno con el hash y otro
con la etiqueta.

También se puede etiquetar un commit ya subido —incluido uno de sellado— y subir después
solo la etiqueta con `git push origin v3.0`: ese push dispara el workflow por su cuenta y
vuelve a sellar los documentos, ahora con `v3.0`.

> **Cuidado con `[skip ci]`.** GitHub salta este workflow en cuanto encuentra esa marca en
> el mensaje del commit, y también al etiquetar un commit que la lleve. No debe usarse en
> los mensajes de commit de este repositorio, ni siquiera mencionada de pasada: desactiva
> el sellado sin previo aviso y sin dejar rastro en la pestaña *Actions*.

Solo se etiqueta cuando **cambia el fondo** de un documento, no en cada corrección: si el
número de versión cambiase en cada push dejaría de identificar nada, y la cláusula 3.4 se
apoya en que sea estable. Entre etiqueta y etiqueta, los documentos muestran
`v3.0-2-g143bf6a`, que se lee como «la v3.0 más dos retoques».

A partir de ahí:

- **La web** muestra siempre la última versión etiquetada.
- **El panel** guarda, en cada aceptación, **la etiqueta de la versión + la fecha y hora**.
- **Cada licencia contratada** queda asociada a la versión que se firmó.
- **El cliente** puede consultar en cualquier momento la suya, mediante un enlace permanente a esa etiqueta o un PDF generado a partir de ella.

---

## Consultar una versión concreta

Partiendo del identificador que aparece en el documento —`7fd6bdc`, `v3.0`, o
`v3.0-2-g143bf6a`— hay tres formas de recuperar el texto exacto que se publicó bajo él.
En los ejemplos se usa el hash `7fd6bdc`; sirve igual una etiqueta (`v3.0`).

### 1. Desde la terminal

```
git show 7fd6bdc:textos/aviso-legal.md
```

Devuelve el documento íntegro tal como estaba en ese commit. Para guardarlo en un fichero:

```
git show 7fd6bdc:textos/aviso-legal.md > aviso-legal-7fd6bdc.md
```

Y para saber la fecha y hora exactas de esa versión:

```
git show -s --format=%ci 7fd6bdc
```

### 2. En la web de GitHub

Sustituyendo `main` por el identificador en la URL de siempre:

```
https://github.com/heliceapp/terms/blob/7fd6bdc/textos/aviso-legal.md
```

Es la forma cómoda de leerlo, ya formateado, sin salir del navegador.

### 3. Enlace permanente al texto en crudo

La misma sustitución sobre la URL del raw:

```
https://raw.githubusercontent.com/heliceapp/terms/7fd6bdc/textos/aviso-legal.md
```

**Este es el enlace que se entrega a un cliente** que pregunta qué aceptó exactamente, y el
que conviene guardar en el panel junto a cada licencia. A diferencia de la URL con `main`,
que devuelve siempre la versión vigente, esta es **inmutable**: apunta a un contenido
concreto y devolverá lo mismo dentro de diez años, pase lo que pase en el repositorio.

### Por qué funciona siempre

Git no guarda «los cambios» de cada commit, sino una **copia completa del repositorio** en
cada uno. Por eso las tres formas funcionan **aunque ese commit no tocara ese documento en
concreto**: el robot sella todos los documentos con el mismo identificador en cada `push`, y
cualquiera de ellos se recupera desde cualquier commit.

Ejemplo real: el commit `e6d64ab` solo modificó `textos/subencargados.md`, y aun así
`git show e6d64ab:textos/aviso-legal.md` devuelve las 66 líneas del aviso legal tal como
estaban en ese momento.

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
| [`textos/seguridad.md`](textos/seguridad.md) | `/seguridad` |
| [`textos/licitaciones.md`](textos/licitaciones.md) | `/licitaciones` |

La política de cookies, el aviso legal, la política de uso razonable, la lista de subencargados y las medidas de seguridad son **Documentos Vinculados** de los Términos y Condiciones: forman parte del contrato aunque se publiquen aparte. El documento de licitaciones es informativo y no forma parte del contrato.

---

**GOOVERIS SOFTWARE S.L.** · CIF B56077100 · Avda. de la Torrecilla 16, Edificio La Torre II, Oficina 210, 14013 Córdoba · info@helice.app
