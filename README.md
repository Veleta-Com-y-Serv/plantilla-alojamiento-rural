# Plantilla NoExpertise · Casa rural y hotel

Web tranquila y editorial para casas rurales y hoteles, con habitaciones, entorno, fotos y reservas.

- Sectores: casa-rural, hotel, alojamiento, turismo, camping. Estilo: natural. Plan mínimo: presencia.
- Secciones: hero, habitaciones, entorno, galeria, servicios, opiniones, como-llegar, reservas, preguntas, contacto (y `texto` para apartados nuevos).
- Diseño: cabecera con el nombre centrado y el menú debajo, portada a toda altura con el título en serif cursiva y una línea fina, habitaciones en filas alternas foto / texto, tarjetas apaisadas del entorno, retícula asimétrica de fotos, servicios en rejilla de iconos, verde bosque + tierra + crema y pie claro con la dirección en grande y un plano enlazado.
- SEO de base incluido (`src/lib/seo.ts`): canónica, og:image, JSON-LD del negocio y de las preguntas frecuentes, `robots.txt`, `sitemap.xml` y `llms.txt`; `noindex` si `seo.indexable: false`.
- Contenido editable en `site.yaml`; metadatos en `template.yaml`; reglas para el agente en `CLAUDE.md`; fotos a generar en `fotos.json`.

```
npm ci
npm run dev      # desarrollo
npm run build    # web estática en dist/
```

Basada en [AstroWind](https://github.com/onwidget/astrowind) © onWidget, licencia MIT (`LICENSE-ASTROWIND.md`). Imágenes de relleno (`public/placeholders/`) dibujadas para esta plantilla, sin licencias de terceros.
