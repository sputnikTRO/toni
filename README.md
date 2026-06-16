# TONI — sitio oficial

Sitio web estático (HTML + CSS + JavaScript vanilla, sin frameworks ni backend) para el artista musical **TONI**. Mobile-first, blanco y negro, minimalista.

Tiene dos vistas en una sola página, sin recargar:

- **Home** — landing a pantalla completa con la portada del álbum *No Voltees!* (clic → abre el streaming).
- **Shop** — tienda con el merch. El producto (CD) se compra vía **Mercado Pago** (clic → abre el link de pago en la misma pestaña). No hay carrito ni cuentas de usuario: es un sitio estático.

---

## 1. Correr en local

No requiere instalación ni build. Dos opciones:

**Opción A — abrir el archivo directamente:** doble clic en `index.html`.

**Opción B — servidor estático simple** (recomendado):

```bash
cd toni
python3 -m http.server 8000
```

Luego abre <http://localhost:8000>.

---

## 2. Qué reemplazar (lo único que se edita)

### a) Imágenes — carpeta `assets/`

| Archivo            | Qué es                                   |
|--------------------|------------------------------------------|
| `assets/album.jpg` | Portada de *No Voltees!* (cuadrada)      |
| `assets/cd.jpg`    | Foto del CD / producto (cuadrada)        |

Sustituye los archivos manteniendo **el mismo nombre**. Idealmente cuadradas (1:1), ~1000–1500 px de lado, JPG.

> Las imágenes actuales son **placeholders**. Reemplázalas por las reales antes de publicar.

### b) Nombre y precio del producto

El nombre se edita en `index.html` (`<p class="product-name">CD — No Voltees!</p>`).
El precio se controla con la constante `CD_PRICE_MXN` (ver abajo); se renderiza con formato `$000 MXN`.

### c) Constantes de configuración — al inicio del `<script>` en `index.html`

```js
const STREAMING_LINK   = "PEGAR_LINK_STREAMING_DE_TONI";   // álbum "No Voltees!"
const MERCADOPAGO_LINK = "PEGAR_LINK_MERCADOPAGO_DE_TONI"; // link reutilizable mpago.la/...
const CONTACT_EMAIL    = "PEGAR_CORREO_DE_TONI";
const CD_PRICE_MXN     = 0;                                 // precio del CD en MXN
const SOCIALS = {
  instagram: "PEGAR_INSTAGRAM_DE_TONI",
  youtube:   "PEGAR_YOUTUBE_DE_TONI"
};
```

- **`STREAMING_LINK`** — smart link del álbum *No Voltees!*. Es a donde lleva la portada en Home.
- **`MERCADOPAGO_LINK`** — link de pago **reutilizable** del CD. Se genera en la app de **Mercado Pago**: *Herramientas para vender → Link de pago →* crear el link y pegarlo aquí. Mientras no se configure, el botón de compra muestra un aviso de "próximamente" en vez de abrir una página rota.
- **`CONTACT_EMAIL`** — correo real de contacto (aparece como *mailto* en el footer).
- **`CD_PRICE_MXN`** — precio del CD en pesos (solo el número). El sitio convierte a USD en vivo si el visitante cambia la moneda; **el cobro siempre se procesa en MXN** por Mercado Pago.
- **`SOCIALS`** — URL de Instagram y YouTube (reemplaza cada placeholder por el perfil real).

### d) Agregar más productos (opcional, a futuro)

Duplica el bloque `<a class="product product-buy">…</a>` dentro de `.shop-grid`. El grid se acomoda solo.

---

## 3. Deploy en Cloudflare Pages

El sitio es 100% estático: **sin build, sin comando de compilación**.

1. **Sube el repo a GitHub** (`git push`).
2. En **Cloudflare Pages**: **Workers & Pages → Create application → Pages → Connect to Git** y conecta el repo.
3. Configura:
   - **Framework preset:** `None`
   - **Build command:** *(vacío)*
   - **Build output directory:** la raíz → `/`
4. **Deploy.** Cada `git push` vuelve a desplegar automáticamente.

### Conectar un dominio propio (ej. `tonimusica.com`)

En el proyecto de Pages → **Custom domains → Set up a custom domain**, escribe el dominio y sigue los **registros DNS** que indique Cloudflare. HTTPS es automático.

> Recuerda actualizar las URLs de Open Graph en el `<head>` (`og:url` y `og:image`) al dominio real cuando lo conectes.

---

## Estructura del repo

```
toni/
├── index.html        # Todo el sitio (HTML + CSS + JS en un archivo)
├── favicon.ico       # Favicon en la raíz (lo busca Google)
├── assets/
│   ├── album.jpg     # Portada de No Voltees!
│   ├── cd.jpg        # Producto (CD)
│   ├── favicon.png   # 96x96
│   ├── favicon-180.png
│   └── favicon.ico
└── README.md
```
