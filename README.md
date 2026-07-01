# Sitio web TINDAB S.A. — tindabsa.com

Sitio estático construido con [Astro](https://astro.build). Rápido, sin base de datos, y editable con Claude Code.

## Estructura

```
sitio/
├── src/
│   ├── data/productos.json      ← LOS PRODUCTOS SE EDITAN AQUÍ (nombre, categoría, descripción…)
│   ├── pages/                   ← una carpeta/archivo = una página del sitio
│   │   ├── index.astro          (home)
│   │   ├── limpieza-neque/      (catálogo + página por producto, generadas desde productos.json)
│   │   ├── quimicos-industriales.astro
│   │   ├── maquila.astro
│   │   ├── nosotros.astro
│   │   ├── contacto.astro
│   │   └── blog/                (los posts son archivos .md — agregar uno = nueva entrada)
│   ├── layouts/Base.astro       (header, footer, menú, WhatsApp flotante, SEO)
│   ├── drafts/                  (sosa y ácido clorhídrico — OCULTOS hasta tener permisos)
│   └── styles/global.css        (colores e identidad de marca)
└── public/                      (favicon, robots.txt; aquí irán fotos y PDFs de fichas técnicas)
```

## Comandos

```bash
npm install      # primera vez
npm run dev      # ver el sitio en http://localhost:4321
npm run build    # generar el sitio final en dist/
```

## Tareas pendientes antes de publicar

1. **Formularios**: crear cuenta gratis en https://web3forms.com con ventas@tindabsa.com,
   copiar el Access Key y reemplazar `PON_AQUI_TU_ACCESS_KEY_DE_WEB3FORMS` en
   `src/pages/contacto.astro` y `src/pages/maquila.astro`. (2 minutos, gratis, las
   solicitudes llegan al correo.)
2. **Fotos**: cuando esté la sesión de fotos, subirlas a `public/fotos/` y reemplazar
   los placeholders "Foto" en las páginas.
3. **Fichas técnicas**: subir los PDF a `public/fichas/` y enlazarlos en las páginas
   de producto (hoy dicen "solicítalas con tu cotización").
4. **Google Analytics**: crear propiedad GA4 y agregar el script en `src/layouts/Base.astro`.

## Publicar en Cloudflare Pages (gratis)

1. Subir esta carpeta a un repositorio de GitHub (privado está bien).
2. En el panel de Cloudflare: **Workers & Pages → Create → Pages → Connect to Git** y elegir el repo.
3. Configuración del build: Framework preset **Astro** · Build command `npm run build` · Output `dist`.
4. Deploy. Cloudflare da una URL temporal (xxx.pages.dev) para revisar.
5. En **Custom domains** del proyecto Pages, agregar `tindabsa.com` y `www.tindabsa.com` —
   como el dominio ya está en Cloudflare, el DNS se configura solo.
6. Cada vez que se suba un cambio al repo, el sitio se actualiza automáticamente.

## Reglas de contenido (importante)

- Hipoclorito: el sitio público SIEMPRE dice **10%** y **250 kg** (igual que la etiqueta).
  Nunca mencionar 10.5% ni "lleno total" — eso es solo para venta directa.
- Productos que NO van en el sitio: sosa y ácido clorhídrico (hasta permisos, borradores
  en `src/drafts/`), lubricante íntimo, y productos revendidos de terceros.
- MilanCare no se menciona hasta su relanzamiento (~nov 2026); entonces se agrega
  pestaña con enlace a su sitio propio.

## Cómo agregar un producto nuevo

Agregar un objeto a `src/data/productos.json` con: slug, nombre, categoria, presentaciones,
descripcion y aplicaciones. La página del producto y su tarjeta en el catálogo se generan solas.

## Cómo agregar un artículo al blog

Crear un archivo `.md` en `src/pages/blog/` copiando el formato (frontmatter) de los existentes.
