# Plantilla NoExpertise · Transporte y mudanzas

Web robusta a todo el ancho para mudanzas y transporte: flota, cobertura, proceso y presupuesto de ruta.

- Sectores: transporte, mudanzas, logística, mensajería, taxi, grúa. Estilo: robusto. Plan mínimo: gratis. Orden 400.
- Secciones: hero, servicios, flota, zonas (cobertura), proceso, cifras, opiniones, preguntas, presupuesto, contacto (+ `texto` para apartados nuevos).
- Campos propios: `hero.destacado`, `hero.formulario_titulo`, `hero.boton_formulario` (barra de ruta: origen, destino, fecha, teléfono); `servicios.galeria` (franja de fotos); `flota[]` (`nombre, texto, capacidad, imagen`, no se pinta vacía); `presupuesto.opciones` (tamaños de mudanza, con «; »), `presupuesto.nota`, `presupuesto.imagen`; `cifras.items` (no se pinta vacía).
- Ejemplo: Mudanzas Penyagolosa, Castelló de la Plana (negocio ficticio, teléfonos ficticios).
- SEO de base incluido (`src/lib/seo.ts`): canónica, og:image, JSON-LD (`MovingCompany`) y de las preguntas frecuentes, `robots.txt`, `sitemap.xml` y `llms.txt`; `noindex` si `seo.indexable: false`.
- Contenido editable en `site.yaml`; metadatos y guion del asistente en `template.yaml`; reglas para el agente en `CLAUDE.md`; brief de diseño en `DISEÑO.md`; fotos a generar en `fotos.json`.

```
npm ci
npm run dev      # desarrollo
npm run build    # web estática en dist/
```

Basada en [AstroWind](https://github.com/onwidget/astrowind) © onWidget, licencia MIT (`LICENSE-ASTROWIND.md`). Imágenes de relleno (`public/placeholders/`) generadas para esta plantilla, sin licencias de terceros.

## Páginas propias
- Cada elemento de `secciones.servicios.items` con `detalle` tiene su página en `/servicios/<slug>/` (`src/pages/[coleccion]/[slug].astro`).
- Cada zona de `secciones.zonas.items` con `texto` tiene su página en `/zonas/<slug>/` (`src/pages/zonas/[slug].astro`); en la sección, `titulo_pagina` y `texto_pagina` con {zona} y {negocio}.
- Campos opcionales de los elementos con ficha: `detalle` (párrafos separados por una línea en blanco), `slug` e `imagenes` («/fotos/a.jpg; /fotos/b.jpg»).
