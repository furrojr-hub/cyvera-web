# cyvera.es

Sitio estático de una página para Cyvera. Sin dependencias ni build: `index.html` es el sitio.

| Archivo | Para qué sirve |
|---|---|
| `index.html` | La web completa (CSS y JS en línea, tipografías desde Google Fonts) |
| `404.html` | Página de error, misma identidad |
| `CNAME` | Dominio propio para GitHub Pages: `cyvera.es` |
| `robots.txt` / `sitemap.xml` | Indexación; apuntan a `https://cyvera.es` |

Ver en local: `python3 -m http.server 8000` y abrir http://localhost:8000

## Publicar en GitHub Pages

```sh
gh auth login                      # paso interactivo (hazlo tú)
gh repo create cyvera-web --public --source=. --push
gh api -X POST repos/:owner/cyvera-web/pages -f source[branch]=main -f source[path]=/
```

Después, en GitHub → Settings → Pages → Custom domain: `cyvera.es` y marcar *Enforce HTTPS*.

## DNS en GoDaddy

En GoDaddy → Mis productos → cyvera.es → DNS → Gestionar zonas.
Borrar el registro `A` de tipo *Parked*/*Aparcado* que GoDaddy crea por defecto y dejar:

| Tipo | Nombre | Valor | TTL |
|---|---|---|---|
| A | @ | 185.199.108.153 | 600 |
| A | @ | 185.199.109.153 | 600 |
| A | @ | 185.199.110.153 | 600 |
| A | @ | 185.199.111.153 | 600 |
| CNAME | www | furrojr-hub.github.io. | 600 |

GitHub confirma estas IP en Settings → Pages una vez añadido el dominio.
Propagación: entre 10 minutos y 2 horas. El certificado HTTPS lo emite GitHub solo.

## Pendiente antes de publicar

- Sustituir cifras y casos de muestra por datos reales (marcados en la página).
- Conectar el formulario a un endpoint real (Formspree, HubSpot, tu CRM).
- Email, teléfono y dirección actuales son de relleno.
- Añadir `og:image` (1200×630) para las vistas previas en redes.
- Aviso legal, privacidad y cookies: los enlaces del pie están vacíos.
