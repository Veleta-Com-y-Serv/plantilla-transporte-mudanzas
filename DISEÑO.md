# Transporte y mudanzas: brief de diseño

Plantilla `transporte-mudanzas` creada el 29/10/2026 a partir de `reformas-oficios` con `php artisan plantillas:nueva`
y rediseñada entera (fila 24 del brief de la tanda «a ancho completo»). Este fichero se queda en el repo: es lo que lee
quien (persona o agente) rediseñe la plantilla.

## Brief

- **Para quién**: empresas de mudanzas, portes, transporte de mercancías, mensajería, taxi y grúas
  (`sectores: transporte, mudanzas, logistica, mensajeria, taxi, grua`). Quien entra quiere saber si le llevan de A a B,
  con qué vehículo, cuánto tarda en tener precio y si va asegurado.
- **Qué tiene que conseguir la web**: pedir presupuesto (barra de ruta del hero y formulario completo) o llamar
  (teléfono en la cabecera, en el hero, enorme en contacto y barra fija de móvil «Llamar / WhatsApp»).
- **Tono y estilo** (`estilo: robusto`): fuerte, fiable, en movimiento. Sí: señalética de carretera, rotulación de
  camión, logística seria. No: la caja centrada estrecha con tarjetas blancas; tampoco el amarillo obra con diagonales
  de sección de `reformas-oficios` ni el naranja con chaflanes y letra estrecha de `taller-mecanico`.
- **Paleta de ejemplo**: primario `#f8c20a` (amarillo señal), acento `#1f5fd1` (azul de foco), fondo `#ffffff`,
  texto `#0b1e3c` (azul marino: letra y bandas oscuras). El diseño aguanta los cuatro del cliente: las bandas oscuras
  son `--c-texto` con letra `--c-fondo`; la letra sobre el primario se calcula (negra o blanca); derivados con `color-mix`.
- **Tipografía**: sans de sistema (system-ui: Segoe UI, SF Pro, Roboto) en peso 900, **cursiva y mayúsculas** para
  todos los titulares, botones y placas (sensación de velocidad); texto en system-ui normal. Títulos de 2,6 rem en móvil
  a 5-6,75 rem en escritorio. Antetítulos pequeños en mayúsculas espaciadas con una raya amarilla delante.
- **Firma visual**: la «línea de carretera» (`.linea-vial`, discontinua amarilla) entre bandas, bajo el título del hero
  y en el proceso; fotos a sangre con un borde en sesgo (`--sesgo`, solo desde tableta); placas amarillas en sesgo
  (`.placa`) para capacidades, autores y notas; botones con el fondo en sesgo (el foco se ve en el rectángulo).
- **Ritmo de bandas** (todas de borde a borde, contenido hasta `--ancho: 90rem`):
  hero marino partido 50/50 con foto + barra de ruta amarilla → servicios claro + franja de fotos a sangre → flota
  marino con mosaico a sangre → cobertura amarilla partida con foto → proceso claro con carretera marino a todo el
  ancho → cifras marino → opiniones gris azulado → preguntas claro → presupuesto partido (foto + marino) → contacto
  amarillo + franja de foto → pie marino hondo con columnas.

## Apartados

1. `hero`: panel marino (antetítulo, título enorme, línea vial, texto, «Llamar ahora» y «Presupuesto gratis») y foto
   del camión a sangre a la derecha con `destacado` en placa; barra de ruta amarilla con origen, destino, fecha,
   teléfono y botón. En móvil y tableta, texto arriba y foto debajo a todo el ancho.
2. `servicios`: titular partido; rejilla 4/2/1 columnas sin tarjetas, celdas con líneas finas, número e icono en placa;
   la celda se vuelve marino al pasar el ratón. `galeria`: franja de 4 fotos cuadradas de borde a borde (2×2 en móvil).
3. `flota` (lista propia `flota: {nombre, texto, capacidad, imagen}`): mosaico de borde a borde con 3 px de junta;
   fotos altas con velo marino abajo, capacidad en placa, nombre y texto.
4. `zonas` (Cobertura): localidades como señales de carretera (marino, borde blanco interior); foto a sangre.
5. `proceso`: hitos numerados (placas amarillas en sesgo) sobre una carretera marino de borde a borde con línea
   discontinua; en móvil, la carretera va en vertical a la izquierda.
6. `cifras`: números de hasta 6 rem en amarillo cursiva, separados por líneas discontinuas (no se pinta sin cifras).
7. `opiniones`: la primera opinión enorme en cursiva con comilla amarilla; las demás en columna con líneas.
8. `preguntas`: titular fijo a la izquierda y acordeón a la derecha (escritorio).
9. `presupuesto`: foto a sangre a la izquierda con sesgo; panel marino con garantías, nota en placa y formulario
   de mudanza (tamaño con `opciones`). En tableta la foto pasa arriba (21:9).
10. `contacto`: teléfono enorme, datos en 4 columnas con raya superior, foto de la nave como franja a sangre.

## Fotos (`fotos.json`, 12)

Camión de mudanzas en una calle mediterránea (hero, 4:3), embalaje, carga, montaje y guardamuebles (1:1, franja),
furgoneta, camión con trampilla, camión grande y elevador exterior (3:4, flota), autovía por la Plana de Castellón
(4:3, cobertura), salón con cajas (4:3, presupuesto) y nave con camión (16:9, contacto). Sin texto legible, sin
logotipos, sin matrículas legibles, sin personas reconocibles.

## Qué no hacer

- Nada de cajas centradas estrechas ni tarjetas blancas flotando; cada sección es una banda de borde a borde.
- No quitar la cursiva ni la línea vial: son lo que la distingue de `reformas-oficios` y `energia-solar` (misma base).
- No poner cifras, capacidades ni precios en los componentes: solo en `site.yaml`.

## Hecho

- [x] `site.yaml` de ejemplo (Mudanzas Penyagolosa, Castelló de la Plana), todo activo, al menos un elemento por lista.
- [x] Secciones rediseñadas y nuevas (`flota`); `trabajos` de la base quitada; `texto.astro` adaptado.
- [x] `template.yaml` con sectores con nombre, secciones y guion del asistente (11 pasos).
- [x] `fotos.json` (12) y placeholders propios; previews provisionales con los placeholders.
- [x] `php artisan plantillas:comprobar transporte-mudanzas --construir`: Cumple (0 errores, 0 avisos).
- [ ] Fotos generadas y previews definitivas (paso de fotos), etiqueta `v1.0.0` y repo `Veleta-Com-y-Serv/plantilla-transporte-mudanzas`.
- [ ] En la plataforma: `config/plantillas.php` (`repos` y `refs`) y `php artisan plantillas:sync --demos`.
