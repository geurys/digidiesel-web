# digidiesel-web — sitio público de Digi-Diesel

Sitio estático de servicios (diagnóstico y programación de ECU diésel) en `https://digidieselrd.com`.
Existe para que Payoneer y eBay tengan una URL del negocio con contacto y servicios.

## Estructura

- `index.html` = inglés (página por defecto), `es/index.html` = español. Enlazadas con `hreflang`; sin JS.
- `assets/site.css` compartido; logos copiados de `PROYECTO CONTROL DE PAGOS\frontend\logo\final\`
  (`logo.svg` sobre blanco, `logo-blanco.svg` en el footer grafito, `favicon.svg` = icono). `og.png` 1200x630.
- `CNAME` = `digidieselrd.com` (GitHub Pages). `.nojekyll` para servir tal cual.

## Reglas de contenido

- **Sin deletes ni eufemismos** (EGR/DPF/AdBlue, "off-road", "emissions solutions"): eBay prohíbe esos
  servicios y Payoneer puede congelar fondos. Lo que diga el sitio tiene que coincidir con los anuncios de eBay.
- Contacto público: WhatsApp 829-981-6974, `contacto@digidieselrd.com` (alias Fastmail), solo "Bonao, RD" (sin calle, decisión de Geurys). No publicar el RNC
  (es la cédula). Cualquier cambio de teléfono/correo/dirección se hace en las dos páginas y en el JSON-LD.
- Paleta de marca: naranja `#E8491D`, tinta `#2E3238`; estilo sobrio.

## Probar local

`py -m http.server 8765` en esta carpeta → `http://localhost:8765/` y `/es/` (las rutas son absolutas `/assets/...`).
