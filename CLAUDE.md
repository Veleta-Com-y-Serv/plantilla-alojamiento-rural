# Plantilla «Casa rural y hotel» (NoExpertise)

Web estática Astro 5 + Tailwind 4, derivada de AstroWind (MIT, ver `LICENSE-ASTROWIND.md`). Estilo: **natural** (editorial, con mucho aire).
Todo en castellano de España, frases cortas, sin jerga.

## Dónde está cada cosa
- **Textos, contacto, menú, SEO y secciones**: `site.yaml` (raíz). Es la única fuente de contenido. `src/data/site.ts` lo carga y lo tipa; no pongas textos fijos en los componentes.
- **Colores**: `site.yaml → colores` (primario = verde bosque, acento = tierra, fondo = crema, texto). `src/layouts/Base.astro` los convierte en variables CSS (`--c-primario`…) y Tailwind los expone como `bg-primario`, `text-acento`, `bg-primario/10`… Los tonos derivados (`--papel`, `--tierra`, `--linea`, `--acento-legible`) se calculan con `color-mix` en `src/styles/global.css`.
- **Tipografías y aspecto general**: `src/styles/global.css` (Georgia para títulos, sans del sistema para texto, botones rectos `.btn` y enlace con flecha `.btn-sec`, cabecera `.cabecera--editorial`, pie `.pie--editorial`, sombra de fotos `.foto`). Fuentes del sistema: no añadas fuentes externas.
- **Imágenes**: en `public/`. Fotos en `public/fotos/` (se generan a partir de `fotos.json`); si una foto de `/fotos/` falta, `Imagen.astro` muestra `/placeholders/<mismo nombre>.svg`. El plano de situación es `/placeholders/plano.svg` (dibujo propio). Personas: siempre `/placeholders/persona.svg`, nunca caras generadas.
- **Logo**: `site.yaml → logo` (ruta en `public/`); vacío = nombre en texto (en cursiva, centrado). El `eslogan` aparece bajo el nombre en escritorio.
- **Pie «Web creada con NoExpertise»**: `site.yaml → marca_pie` (true en plan gratis; esta plantilla es de plan presencia). El pie muestra en grande `contacto.direccion`, enlazada a Google Maps junto al plano.

## Secciones
Cada sección es un componente que solo se pinta si `site.yaml → secciones.<id>.activa` es `true`. Se pintan en el orden en que aparecen en `site.yaml`.
- `hero` → `src/components/secciones/hero.astro`
- `habitaciones` → `src/components/secciones/habitaciones.astro`
- `entorno` → `src/components/secciones/entorno.astro`
- `galeria` → `src/components/secciones/galeria.astro`
- `servicios` → `src/components/secciones/servicios.astro`
- `opiniones` → `src/components/secciones/opiniones.astro`
- `como-llegar` → `src/components/secciones/como-llegar.astro`
- `reservas` → `src/components/secciones/reservas.astro`
- `contacto` → `src/components/secciones/contacto.astro`
- `texto` → `src/components/secciones/texto.astro` (apartado genérico para `tipo: texto`)

## Campos propios de esta plantilla (además del esquema común)
- `hero`: `cta` (sin él, el botón llama), `cta_secundario` (enlace con flecha), `items` = detalles cortos con `icono` bajo la foto.
- `habitaciones.habitaciones` [{nombre, texto, precio, personas, extras, imagen}]: filas alternas foto / texto. `precio` y `personas` SIEMPRE como cadena (`"desde 95 €/noche"`, `"2 personas"`); vacíos = no se pintan. `extras` es UNA cadena separada por comas (`"Baño propio, chimenea, terraza"`), nunca una lista.
- `entorno.items` [{titulo, texto, imagen, icono}]: tarjetas apaisadas; sin `imagen` se ve el `icono`.
- `servicios.items` [{titulo, texto, icono}]: rejilla de iconos sin tarjeta. Iconos útiles: `taza`, `wifi`, `huella`, `fuego`, `parking`, `piscina`, `cama`, `llave`, `arbol`, `ruta`, `bici` (lista completa en `src/components/ui/Icono.astro`).
- `opiniones.testimonios` [{texto, autor, nota}]: la primera sale grande; `nota` opcional (de dónde viene o cuándo). Sin opiniones, la sección no se pinta. Sin estrellas ni puntuaciones.
- `como-llegar`: `texto`, `imagen` (plano), `items` (en coche / en tren / en bus, con `icono` `coche`, `tren`, `bus`) y botón a Google Maps con `contacto.direccion` (su texto en `cta.texto`; si `cta.url` tiene una dirección web, se usa esa).
- `reservas`: `texto`, `cta` (WhatsApp o teléfono), `nota` (estancia mínima, cancelación…), formulario con llegada, salida y personas por `mailto`. `enlace_reservas` (opcional): web externa de reservas; si tiene una dirección `https://…`, aparece un botón que la abre (texto en `cta_secundario.texto`).

## Reglas para órdenes
1. **Activar o quitar una sección**: cambia `activa: true|false` en `site.yaml`. No borres componentes.
2. **Reordenar secciones**: mueve el bloque dentro de `secciones:` en `site.yaml`.
3. **Cambiar textos, habitaciones, precios, fotos**: solo en `site.yaml`. Si un texto contiene comas o dos puntos dentro de `{ … }`, ponlo entre comillas. Precios siempre entre comillas.
4. **Listas planas**: nunca una lista dentro de un elemento de lista. Varios valores = una cadena separada por comas (`extras`). Máximo 24 elementos por lista.
5. **Nunca inventes** precios, cifras ni opiniones: si el cliente no los da, déjalos vacíos (los componentes lo soportan).
6. **Página nueva**: crea `src/pages/<slug>.astro` con `import Base from '../layouts/Base.astro'` y `<Base titulo="…" descripcion="…">…</Base>`; enlázala en `site.yaml → menu`. Ejemplo: `src/pages/aviso-legal.astro`.
7. **Apartado nuevo**: añade `secciones.<id>` en `site.yaml` con `tipo:` = `texto`, `habitaciones`, `entorno`, `servicios`, `galeria`… (el diseño que quiera reutilizar). `src/pages/index.astro` lo recoge solo; no lo toques.
8. **No tocar** `src/pages/index.astro`, `src/layouts/Base.astro`, `tailwind.config.mjs` ni `src/styles/comun.css` salvo orden explícita de diseño.
9. Mantén: `lang="es-ES"`, imágenes con `Imagen.astro` (carga diferida), sin JavaScript nuevo salvo necesidad real (solo hay el que cierra el menú móvil), 16 px de margen lateral (`.contenedor`), sin scroll horizontal en móvil.
10. El formulario no tiene servidor: abre el correo (`mailto`) con el email de `site.yaml`. Para envío real, cambia `action` en `src/components/ui/FormularioContacto.astro`.

## Construir
```
npm ci && npm run build      # resultado en dist/
npx astro preview            # ver dist/ en http://localhost:4321
```
Antes de dar una orden por buena: `npm run build` sin errores.
