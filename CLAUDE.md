# Plantilla «Transporte y mudanzas» (NoExpertise)

Web estática Astro 5 + Tailwind 4, derivada de AstroWind (MIT, ver `LICENSE-ASTROWIND.md`). Estilo: **robusto**
(azul marino + amarillo señal + blanco; bandas a todo el ancho; titulares enormes en sans de sistema 900, cursiva y
mayúsculas; «línea de carretera» discontinua amarilla; fotos a sangre con un borde en sesgo; placas amarillas).
Todo en castellano de España, frases cortas, sin jerga.

## Dónde está cada cosa
- **Textos, contacto, menú, SEO y secciones**: `site.yaml` (raíz). Es la única fuente de contenido. `src/data/site.ts` lo carga y lo tipa; no pongas textos fijos en los componentes.
- **Colores**: `site.yaml → colores` (primario, acento, fondo, texto). `src/layouts/Base.astro` los convierte en variables CSS (`--c-primario`…) y Tailwind los expone como `bg-primario`, `text-acento`…
  - `primario` = amarillo de botones, barra de ruta del hero, banda de cobertura, contacto, placas y cifras. La letra encima se calcula sola (`--sobre-primario`: negra si el primario es claro, blanca si es oscuro).
  - `texto` = color de la letra **y** de las bandas oscuras (cabecera, hero, flota, cifras, presupuesto, pie). En ellas la letra usa `fondo`. Si el cliente pide fondo oscuro, el diseño se invierte solo.
  - `acento` = foco de los formularios e iconos de los pasos.
- **Tipografías y aspecto general**: `src/styles/global.css` (titulares en cursiva 900, `.antetitulo` con raya, botones `.btn`/`.btn-sec`/`.btn--marino` con fondo en sesgo, bandas `.banda-oscura`/`.banda-gris`/`.banda-primaria`, `.linea-vial`, `.placa`, partidos a sangre `.partido` + `.partido--foto-der|izq` + `.partido-texto`/`.partido-foto`, cabecera, pie y barra inferior fija de móvil). `--ancho: 90rem` y `--lateral` (margen del contenido en las bandas a sangre). Fuentes del sistema: no añadas fuentes externas.
- **Imágenes**: en `public/`. Las fotos van en `public/fotos/` (lista y descripción en `fotos.json`); las de relleno, en `public/placeholders/`. En `site.yaml` se referencian con ruta absoluta (`/fotos/hero.jpg`).
- **Logo**: `site.yaml → logo` (ruta en `public/`); vacío = inicial en placa amarilla + nombre.
- **Pie «Web creada con NoExpertise»**: `site.yaml → marca_pie` (true en plan gratis).

## Secciones
Cada sección es un componente que solo se pinta si `site.yaml → secciones.<id>.activa` es `true`. Se pintan en el orden en que aparecen en `site.yaml`.
- `hero` → `hero.astro`: partido a sangre. Panel marino con `antetitulo`, `titulo`, `texto`, `cta` (llamar: `url: "tel:+34…"`) y `cta_secundario` (presupuesto); `imagen` a sangre a la derecha con `destacado: {titulo, texto}` en placa amarilla («Seguro a todo riesgo»). Debajo, la barra de ruta amarilla con formulario corto (origen, destino, fecha, teléfono): `formulario_titulo` (si falta, el texto de `cta_secundario`) y `boton_formulario`. Sin imagen, el panel ocupa todo el ancho.
- `servicios` → `servicios.astro`: `items: [{titulo, texto, icono}]` en rejilla de 4 columnas sin tarjetas y `galeria` (lista de fotos) como franja de borde a borde. `cta` opcional.
- `flota` → `flota.astro`: `flota: [{nombre, texto, capacidad, imagen}]` en mosaico a sangre (foto alta, capacidad en placa). **Sin vehículos ni texto no se pinta.** No inventes vehículos ni capacidades.
- `zonas` (Cobertura) → `zonas.astro`: banda amarilla partida; `texto`, `items: [{titulo: localidad}]` como señales de carretera, `cta` e `imagen` a sangre.
- `proceso` → `proceso.astro`: `items: [{titulo, texto, icono}]` como hitos sobre una carretera marino a todo el ancho (vertical en móvil).
- `cifras` → `cifras.astro`: `items: [{titulo: "+300", texto}]` en banda marino. **No se pinta si `items` está vacío.** No inventes cifras.
- `opiniones` → `opiniones.astro`: `testimonios: [{texto, autor, nota}]`; la primera, enorme. No inventes opiniones.
- `preguntas` → `preguntas.astro`: `preguntas: [{pregunta, respuesta}]` en acordeón `details/summary`; sin preguntas no se pinta.
- `presupuesto` → `presupuesto.astro`: partido a sangre (foto a la izquierda, panel marino): `texto`, `items` (garantías con icono), `nota` en placa, `imagen`, `boton_formulario` y `opciones` («Estudio; Piso pequeño; …»: las opciones de «Tamaño de la mudanza»). Formulario: nombre, teléfono, origen, destino, fecha, tamaño y qué hay que mover.
- `contacto` → `contacto.astro`: banda amarilla con el teléfono enorme, WhatsApp, email, dirección y horario de `contacto`, e `imagen` como franja a sangre. Si `presupuesto` no está activa, aquí sale el formulario de contacto.
- `texto` → `texto.astro`: apartado genérico (párrafos, `imagen`, `items`, `cta`). Para apartados nuevos: `tipo: texto`.

## Reglas para órdenes
1. **Activar o quitar una sección**: cambia `activa: true|false` en `site.yaml`. No borres componentes.
2. **Reordenar secciones**: mueve el bloque dentro de `secciones:` en `site.yaml`. Procura alternar bandas: evita poner seguidas dos marino (`flota`, `cifras`, `presupuesto`) o dos amarillas (`zonas`, `contacto`).
3. **Cambiar textos, teléfonos, horarios, fotos**: solo en `site.yaml`. Si un texto contiene comas o dos puntos dentro de `{ … }`, ponlo entre comillas.
4. **Listas planas**: nunca una lista dentro de un elemento de lista. Precios, capacidades y cifras siempre como texto entre comillas (`"+300"`, `"25 m³ · 3.500 kg"`). Varios valores en una cadena con «; » (`opciones`). Máximo 24 elementos por lista.
5. **Página nueva**: crea `src/pages/<slug>.astro` usando `import Base from '../layouts/Base.astro'` y `<Base titulo="…" descripcion="…">…</Base>`; enlázala en `site.yaml → menu` (`{ texto: …, url: "/<slug>" }`). Ejemplo: `src/pages/aviso-legal.astro`.
6. **Sección nueva**: mejor un apartado con `tipo:` (`tipo: texto`, `tipo: servicios`, `tipo: flota`…) y su propio id. Si hace falta un diseño nuevo, crea `src/components/secciones/<id>.astro` con `seccion(Astro.props.id)` y `Titular`, como banda a todo el ancho. `src/pages/index.astro` la recoge sola: no lo toques.
7. **No tocar** `src/layouts/Base.astro`, `src/pages/index.astro`, `tailwind.config.mjs` ni `src/styles/comun.css` salvo orden explícita de diseño. Los ids `hero` y `contacto` son obligatorios. Tampoco `src/lib/seo.ts` ni `src/pages/robots.txt.ts`, `sitemap.xml.ts` y `llms.txt.ts`: son el SEO de base (canónica, og:image, `noindex` si `seo.indexable: false`, JSON-LD del negocio y de las preguntas, robots, sitemap y llms.txt), salen solos de `site.yaml` y el fichero es el mismo en todas las plantillas. `seo.url` y `seo.indexable` los pone la plataforma: no los cambies.
8. Mantén: `lang="es-ES"`, imágenes con `Imagen.astro` (carga diferida), sin JavaScript nuevo salvo necesidad real, 16 px de margen lateral del texto en móvil (las fotos y fondos sí tocan el borde), sin scroll horizontal a 375 px, botones de 44 px, barra inferior fija de móvil («Llamar» / «WhatsApp»: sale sola si hay teléfono o WhatsApp). Imágenes de contenido con `alt` sacado del contenido (`altHero`, `altFicha`, `altGaleria`, `altSeccion` de `src/lib/seo.ts`); las decorativas, `alt=""`.
9. Los formularios no tienen servidor: abren el correo (`mailto`) con el email de `site.yaml`. Para envío real, cambia `action` en `src/components/ui/FormularioContacto.astro`.
10. Iconos disponibles: ver `src/components/ui/Icono.astro` (de transporte: `camion, furgoneta, caja, almacen, elevador, ruta, taxi, grua, paquete, mundo`; y `casa, maletin, herramienta, escudo, euro, usuarios, telefono, camara, mapa, reloj`…).
11. Nada de «contenedor», «Docker», «IA» ni términos técnicos en los textos de la web.

## Construir
```
npm ci && npm run build      # resultado en dist/
npx astro preview            # ver dist/ en http://localhost:4321
```
Antes de dar una orden por buena: `npm run build` sin errores.
