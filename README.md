# KAFU · Landing

Landing estática (HTML + CSS, sin JavaScript ni build) para KAFU, lácteos artesanales de cabra de Antioquia. Su único objetivo es llevar a la gente a WhatsApp (principal) e Instagram (secundaria).

## Estructura

```
index.html            Toda la página (9 secciones)
css/styles.css        Estilos y tokens de marca (colores, tipografía, radios)
assets/img/           Logo, fotos de producto (WebP), textura de papel, íconos, imagen para compartir
favicon.png
robots.txt
```

## Antes de publicar: reemplaza los marcadores

Busca y reemplaza en `index.html` (Ctrl/Cmd + Shift + H en VS Code):

| Marcador | Reemplazar por | Ejemplo |
| --- | --- | --- |
| `NUMERO_WHATSAPP` | Celular sin +57, sin espacios | `3001234567` |
| `USUARIO_INSTAGRAM` | Usuario sin @ | `kafu.co` |
| `DOMINIO` | Dominio final | `kafu.com.co` |

O desde la terminal:

```bash
sed -i '' 's/NUMERO_WHATSAPP/3001234567/g; s/USUARIO_INSTAGRAM/kafu.co/g; s/DOMINIO/kafu.com.co/g' index.html   # macOS
sed -i    's/NUMERO_WHATSAPP/3001234567/g; s/USUARIO_INSTAGRAM/kafu.co/g; s/DOMINIO/kafu.com.co/g' index.html   # Linux
```

Textos pendientes entre corchetes (búscalos con `[`): `[CIUDADES]`, `[presentación]` del arequipe sin azúcar, finca/municipio, duración, formas de pago, registro INVIMA, reseñas.

### Fotos de la finca
En la sección Origen, cambia cada `<div class="ph">…</div>` por una imagen:

```html
<img class="wide" src="assets/img/finca.webp" alt="Finca KAFU en Antioquia" loading="lazy">  <!-- la primera, ancha -->
<img src="assets/img/cabras.webp" alt="Nuestras cabras" loading="lazy">
```

Exporta las fotos en WebP, de unos 1200 px de ancho y menos de 200 KB.

### Mensajes de WhatsApp
Cada botón de producto abre un mensaje distinto (`?text=…`, codificado para URL). Para cambiar un texto usa un codificador de URL (espacio = `%20`, coma = `%2C`, á = `%C3%A1`, é = `%C3%A9`).

## Ver en local

```bash
python3 -m http.server 8000
# abre http://localhost:8000
```

## Crear el repo y publicar

```bash
git init
git add .
git commit -m "Landing KAFU"
git branch -M main
git remote add origin git@github.com:TU_USUARIO/kafu-landing.git
git push -u origin main
```

Luego conecta el repo a cualquiera de estos (todos gratis para un sitio estático, sin configuración de build):

- **Vercel / Netlify / Cloudflare Pages:** importa el repo, framework “Other / None”, comando de build vacío, carpeta de salida `/` (raíz).
- **GitHub Pages:** Settings → Pages → Deploy from branch → `main` / root.

Después apunta tu dominio desde el panel del proveedor.

## Marca

Colores (en `:root` de `css/styles.css`): verde oliva `#2F4A2A`, dorado `#B5791A`, papel `#F3EEE2`, marrón `#4A2E1A`.
Tipografías de Google Fonts: Vollkorn (títulos), Cormorant Garamond (mayúsculas espaciadas), Mulish (texto).
El logo es el archivo original con el fondo removido; no lo redibujes.
