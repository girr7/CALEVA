# Caleva Suite — Organización de la carpeta

Última actualización: 2026-08-21

Esta carpeta (`suite_publicar`) es **la raíz que publica Netlify**. Todo lo que esté
aquí y no esté bloqueado en `netlify.toml` se sirve públicamente. Por eso los papeles
de trabajo se separaron del sitio y las carpetas internas se bloquean (404).

## 1. Sitio publicado (NO mover — es el deploy)

| Ruta | Qué es |
|------|--------|
| `index.html` | Portal Caleva Suite (login + accesos a las apps) |
| `cxp/` | Cuentas por Pagar. Se genera con `_cxp_src/build_cxp.py --publicar`; no se edita a mano |
| `nomina/index.html` | App **Nómina** |
| `seguimiento/index.html` | App **Seguimiento de pedidos** |
| `costo-obra/index.html` | App **Control de Obras** (archivo único, autónomo) |
| `404.html` | Página de "no encontrado" |
| `_headers`, `netlify.toml` | Cabeceras de seguridad (CSP) y redirecciones |
| `favicon.ico`, `favicon.png`, `apple-touch-icon.png` | Iconos |

## 2. Fuente para reconstruir Obra (interno, bloqueado)

- `_obra_src/` — código fuente de Control de Obras (`app.js`, `obra-cloud.js`,
  `style.css`, `costo-obra.html`) y el ensamblador `build_obra.py`.
  `costo-obra/index.html` se **genera** desde aquí; no editar el generado a mano.
- `graphify-out/` — grafo de conocimiento del proyecto (herramienta de desarrollo).

## 3. Papeles de trabajo (`_papeles_trabajo/`, bloqueado)

Todo lo generado/usado en el proyecto, organizado por tipo:

- `sql/` — scripts de base de datos Supabase (`04`…`13`). **Se corren en Supabase → SQL Editor.**
- `edge-functions/` — funciones Edge en uso (`suite-create-user`, `hes-imap`) + sus READMEs de despliegue.
- `documentacion/` — documento de referencia/auditoría (`.docx`/`.pdf`), estrategia de respaldos, y el PDF del sistema de seguimiento.
- `business-plan/` — modelo financiero y presentaciones (Business Plan TMV).
- `marca/` — logotipos y emblema.

## 4. Para revisión / archivo (`_revisar/`, bloqueado)

Cosas **no usadas actualmente** — revisar y borrar cuando confirmes:

- `backups/` — copias `*.bak_audit` de Nómina y Seguimiento (respaldo previo a la auditoría universal).
- `legacy/` — versión Gmail-OAuth abandonada (`hes-gmail`), diseño viejo `indexREV 2 CLARO MODERNO.html`, y el monolito previo `nomina_caleva_cloud.html`.
- `_build_scratch/` — andamiaje usado para generar el documento de referencia (`build_doc.js`, `patch.py`, `package*.json`, páginas `pg-*.jpg`).

## Nota de seguridad

`netlify.toml` incluye reglas `[[redirects]]` que devuelven **404** para
`/_papeles_trabajo/*`, `/_revisar/*`, `/_obra_src/*`, `/graphify-out/*`,
`/Bussiness Plan TMV/*` y `/CLAUDE.md`, de modo que aunque esos archivos se suban
con el deploy, **no son accesibles por URL**. Aun así, lo ideal a futuro es mantener
los papeles de trabajo fuera de la carpeta de publicación.
