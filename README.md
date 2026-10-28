# KAFU · Landing

Landing estática (HTML + CSS, sin JavaScript ni build) para KAFU, lácteos artesanales de cabra de Antioquia. Su único objetivo es llevar a la gente a WhatsApp (principal) e Instagram (secundaria).

## En vivo

| | |
| --- | --- |
| **Sitio** | https://lacteoskafu.com |
| URL de respaldo (Vercel) | https://kafu-landing.vercel.app |
| Repositorio | https://github.com/Cristobaltrujillo19/kafu-landing |
| Panel de Vercel | https://vercel.com/cristobal-trujillo-s-projects/kafu-landing |

## Cómo publicar un cambio

El repositorio está conectado a Vercel: **cada push a `main` publica el sitio solo**, en menos de un minuto. No hay que entrar a Vercel para nada.

```bash
git add .
git commit -m "Describe aquí qué cambiaste"
git push
```

Luego abre https://lacteoskafu.com y refresca con `Ctrl + F5` para saltarte la caché del navegador.

Si algo sale mal, en el panel de Vercel → pestaña **Deployments** puedes volver a la versión anterior con **"..." → Promote to Production**.

## Ver los cambios antes de publicar

```bash
python -m http.server 8000
# abre http://localhost:8000
```

Lo que veas ahí es exactamente lo que se publicará. Mientras no hagas `git push`, el sitio en vivo no cambia.

## Cómo editar los textos

Todo el contenido está en `index.html`. Ábrelo con cualquier editor de texto y busca la frase que quieres cambiar.

### Textos pendientes

Búscalos con `[` en `index.html`. Siguen sin definir:

| Marcador | Dónde | Qué va |
| --- | --- | --- |
| `NUMERO_WHATSAPP` | 12 botones | Celular sin +57 ni espacios, ej. `3001234567` |
| `[CIUDADES]` | Hero, Cómo pedir, FAQ | Ciudades con domicilio |
| `[presentación]` | Arequipe sin azúcar | Tamaño del frasco |
| `[NOMBRE DE LA FINCA / MUNICIPIO]` | Origen | Nombre de la finca |
| `[Reseña de cliente]`, `[Nombre]`, `[Ciudad]` | Testimonios | 3 reseñas reales |
| `[Confirmar temperaturas.]` | FAQ | Temperaturas de conservación |
| `[X] días`, `[X] semanas` | FAQ | Duración de cada producto |
| `[Costo o pedido mínimo.]` | FAQ | Si cobras domicilio |
| `[Nequi, Daviplata…]` | FAQ | Formas de pago reales |
| `[Vereda / Municipio]` | Footer | Dirección a mostrar |
| `[RSA-XXXXXX-AAAA]` | Footer | Registro sanitario INVIMA |

El número de WhatsApp aparece 12 veces, así que cámbialo de una vez desde la terminal:

```bash
sed -i 's/NUMERO_WHATSAPP/3001234567/g' index.html
grep -c NUMERO_WHATSAPP index.html   # debe decir 0
```

### Mensajes de WhatsApp

Cada botón abre un mensaje distinto, escrito en la parte `?text=…` del enlace y codificado para URL. Si quieres cambiar un texto, usa un codificador de URL: espacio = `%20`, coma = `%2C`, á = `%C3%A1`, é = `%C3%A9`, ñ = `%C3%B1`.

## Cómo cambiar las fotos

Las imágenes van en `assets/img/`. Expórtalas en **WebP**, de unos 1200 px de ancho y menos de 200 KB.

> ⚠️ **Importante: no reutilices el mismo nombre de archivo.**
> Las imágenes se guardan en la caché del navegador durante un año. Si reemplazas `kefir-800.webp` por otra foto con el mismo nombre, quien ya visitó el sitio seguirá viendo la vieja durante meses.
> **Súbela siempre con un nombre nuevo** (`kefir-800-v2.webp`) y actualiza la referencia en `index.html`.

### Fotos de la finca

En la sección Origen hay tres recuadros grises esperando foto. Cambia cada `<div class="ph">…</div>` por una imagen:

```html
<img class="wide" src="assets/img/finca.webp" alt="Finca KAFU en Antioquia" loading="lazy">  <!-- la primera, ancha -->
<img src="assets/img/cabras.webp" alt="Nuestras cabras" loading="lazy">
<img src="assets/img/proceso.webp" alt="Elaboración artesanal" loading="lazy">
```

## Estructura

```
index.html            Toda la página (9 secciones)
css/styles.css        Estilos y tokens de marca (colores, tipografía, radios)
assets/img/           Logo, fotos de producto (WebP), textura, íconos, imagen para compartir
vercel.json           cleanUrls, caché de assets y headers de seguridad
sitemap.xml           Para Google (enlazado desde robots.txt)
robots.txt
favicon.png
```

## Marca

Colores (en `:root` de `css/styles.css`): verde oliva `#2F4A2A`, dorado `#B5791A`, papel `#F3EEE2`, marrón `#4A2E1A`.
Tipografías de Google Fonts: Vollkorn (títulos), Cormorant Garamond (mayúsculas espaciadas), Mulish (texto).
El logo es el archivo original con el fondo removido; no lo redibujes.
