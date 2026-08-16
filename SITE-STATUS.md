> ## ⛔ HOSTING DADO DE BAJA — 2026-08-16
> El proyecto `ferox` de **Vercel fue eliminado** y **GitHub Pages deshabilitado**. `www.feroxmetales.com`,
> `ferox-six.vercel.app` y `hpcoolsense.github.io/ferox/` devuelven **404** (verificado 2026-08-16).
> El dominio `feroxmetales.com` sigue registrado en **Hostinger** (vence 2027-06-16) con DNS apuntando a Vercel.
>
> **Para volver a hostear:** en Vercel → *Add New Project* → importar `hpcoolsense/ferox` (Framework: *Other*,
> Root Directory `.`, sin build), asignar los dominios `feroxmetales.com` (redirect → www) y `www.feroxmetales.com`
> (los DNS en Hostinger ya apuntan a Vercel), y prender el sitio (`cp site-live.html index.html` → push).
> Vercel auto-deployaba este repo en cada push a `main`.
>
> Todo lo de abajo describe el mecanismo ON/OFF que había mientras estuvo hosteado.

# Estado del sitio FEROX — Switch ON/OFF

**Estado actual: 🔴 OFF (apagado)** — motivo: cuota de hosting impaga.

La web está en producción en **Vercel** (dominio `www.feroxmetales.com`), desplegada
automáticamente desde este repo `hpcoolsense/ferox` (rama `main`). El interruptor es
el archivo `index.html`: lo que esté ahí es lo que ve el público.

## Archivos del sistema
- `index.html`        → lo que se sirve ahora mismo (el "interruptor")
- `site-live.html`    → respaldo de la web REAL (no se publica, está en `.vercelignore`)
- `site-offline.html` → página de "fuera de servicio" (no se publica)

## Apagar (OFF)
```bash
cp site-offline.html index.html
git add -A && git commit -m "chore: sitio OFF" && git push origin main
```

## Encender (ON)
```bash
cp site-live.html index.html
git add -A && git commit -m "chore: sitio ON" && git push origin main
```

Vercel redespliega solo en ~30–60 s tras el push. Verificar:
`curl -s https://www.feroxmetales.com | grep -i "fuera de servicio"`
(si aparece → está OFF; si no → está ON)
