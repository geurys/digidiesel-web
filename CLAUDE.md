# digidiesel-web — sitio público de Digi-Diesel

Sitio estático de servicios (diagnóstico y programación de ECU diésel) en `https://digidieselrd.com`.
Existe para que Payoneer y eBay tengan una URL del negocio con contacto y servicios.

## Estructura

- `index.html` = inglés (página por defecto), `es/index.html` = español. Enlazadas con `hreflang`; sin JS.
- `assets/site.css` compartido; logos copiados de `PROYECTO CONTROL DE PAGOS\frontend\logo\final\`
  (`logo.svg` sobre blanco, `logo-blanco.svg` en el footer grafito, `favicon.svg` = icono). `og.png` 1200x630.
- `CNAME` = `digidieselrd.com` (GitHub Pages). `.nojekyll` para servir tal cual.

## Hosting y DNS

- GitHub Pages del repo público `geurys/digidiesel-web`, rama `main`, raíz. Publicar = `git push` (token en
  `.secrets\github.env`); Pages reconstruye solo en ~1 min. Custom domain `digidieselrd.com`, HTTPS forzado.
- Cloudflare (zona `digidieselrd.com`, todo DNS only): apex y `www` = 4 registros A cada uno a
  `185.199.108-111.153`. **`www` va con A, no CNAME**: `www` tiene MX de Fastmail y un CNAME no puede convivir
  con ellos. No tocar MX/DKIM/SPF/DMARC/SRV/`mail`/wildcards (correo Fastmail) ni `ecf` (túnel del receptor e-CF).
- Dominio **verificado en la cuenta GitHub** `geurys` (Settings → Pages): TXT
  `_github-pages-challenge-geurys` en Cloudflare. No borrarlo; impide que otra cuenta publique Pages en el dominio.
- El panel de Cloudflare no acepta escrituras por `fetch` a su API interna (devuelve HTML); editar por la UI.
  Si el ícono de 1Password se abre en un campo, la extensión de Chrome pierde el teclado: llenar los campos con
  el setter nativo de `value` + evento `input` por JavaScript, sin enfocarlos.
- Estado de Pages: `gh api repos/geurys/digidiesel-web/pages` y `.../pages/health`.
- Certificado Let's Encrypt (apex + www) emitido por GitHub, se renueva solo. Gotcha: tras cambiar el DNS pasó
  1 h sin emitirse (`https_certificate: null`); lo destrabó quitar y volver a poner el dominio
  (`PUT .../pages -F cname=null` y luego `-f cname=digidieselrd.com`). Eso crea commits "Delete/Create CNAME"
  en `main` del remoto: hacer `git pull` antes del siguiente push.

## Reglas de contenido

- **Sin deletes ni eufemismos** (EGR/DPF/AdBlue, "off-road", "emissions solutions"): eBay prohíbe esos
  servicios y Payoneer puede congelar fondos. Lo que diga el sitio tiene que coincidir con los anuncios de eBay.
- Contacto público: WhatsApp 829-981-6974, `contacto@digidieselrd.com` (alias Fastmail), solo "Bonao, RD" (sin calle, decisión de Geurys). No publicar el RNC
  (es la cédula). Cualquier cambio de teléfono/correo/dirección se hace en las dos páginas y en el JSON-LD.
- Paleta de marca: naranja `#E8491D`, tinta `#2E3238`; estilo sobrio.

## Probar local

`py -m http.server 8765` en esta carpeta → `http://localhost:8765/` y `/es/` (las rutas son absolutas `/assets/...`).
