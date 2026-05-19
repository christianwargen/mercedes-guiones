# Visor de Guiones — Mercedes Ponte

Sitio estático para que Mer lea los guiones de reels desde celular o compu, con bloques diferenciados (a cámara / B-roll / texto en pantalla) e indicaciones de toma.

## Estructura

```
visor-guiones/
├── index.html              # Listado de reels disponibles
├── styles.css              # Estilos compartidos (modo oscuro, mobile-first)
├── reels/
│   ├── 01-cuarto-bebe.html
│   └── 02-cuando-llora.html
└── README.md
```

## Ver localmente

Abrir `index.html` directo en el navegador (doble click) ya funciona. Para preview "real" con servidor:

```powershell
cd visor-guiones
python -m http.server 8080
```

Después abrir `http://localhost:8080` en el navegador.

## Deploy a Vercel (repo nuevo)

### 1. Crear repo local

```powershell
cd visor-guiones
git init
git add .
git commit -m "Visor de guiones — setup inicial con reels 01 y 02"
```

### 2. Subir a GitHub

Crear repo nuevo en github.com (privado o público, da igual). Después:

```powershell
git remote add origin https://github.com/<TU-USUARIO>/mercedes-guiones.git
git branch -M main
git push -u origin main
```

### 3. Conectar a Vercel

1. Entrar a [vercel.com/new](https://vercel.com/new)
2. Importar el repo `mercedes-guiones`
3. Framework Preset: **Other** (es HTML estático puro, no requiere build)
4. Deploy

Vercel asigna una URL del tipo `mercedes-guiones.vercel.app`. Cada `git push` actualiza automáticamente.

### Dominio custom (opcional)

Si después se quiere algo más prolijo tipo `guiones.mercedesponte.com`, se configura en Vercel → Settings → Domains.

## Agregar un reel nuevo

1. Copiar uno de los archivos en `reels/` como base (`02-cuando-llora.html` es el más completo)
2. Renombrar a `03-nombre-corto.html`
3. Editar título, meta, escenas y brief
4. Agregar una `<li>` nueva en `index.html` apuntando al archivo
5. `git add . && git commit -m "Agrega reel 03" && git push`

## Convenciones de bloques

| Bloque | Clase CSS | Color | Uso |
|---|---|---|---|
| 🎙️ A cámara | `block-camera` | Dorado | Lo que Mer dice frente a cámara |
| 📹 B-roll | `block-broll` | Azul gris | Lo que se ve cubriendo el monólogo |
| ✍️ Texto en pantalla | `block-overlay` | Rosa apagado | Sobreimpresos / frases flotantes |

Cada bloque incluye un `block-direction` con la indicación técnica (toma, plano, luz, ritmo).

## Estructura de un reel — 3 partes secuenciales

Cada reel se divide en **3 partes grandes** que Mer puede grabar por separado. Esta estructura le saca a Mer la carga de pensar en cortes/escenas — solo graba dos cosas y nosotros montamos en edición.

### Parte 1 — A cámara (lo que decís)
Un único bloque `block-camera` con TODO lo que Mer dice, de corrido, sin cortes. El contenido va en `<div class="block-content">` con `<p>` por párrafos y `<span class="cue">…</span>` para indicaciones intercaladas (pausas, intenciones, bajadas de ritmo). El label del bloque debe ser **"Lo que decís"** (voseo, casual — nunca "monólogo" ni "guion hablado").

Ejemplo:
```html
<div class="block-content">
  <p>"Cuando un bebé llora y no encontrás la razón…"</p>
  <span class="cue">Pausa. Mirá fuera de cámara y volvé.</span>
  <p>"Pero hay un lugar donde casi nadie mira primero…"</p>
</div>
```

El `block-direction` al final indica encuadre, luz y tono general para todo el monólogo.

### Parte 2 — B-rolls (lista de tomas)
Una secuencia de bloques `block-broll`, uno por cada toma. Numerados en el label: `B-roll 1 — [descripción corta]`. Pueden grabarse en cualquier orden. Cada uno con su descripción + `block-direction` técnica.

### Parte 3 — Texto en pantalla
Bloques `block-overlay` con las frases sobreimpresas. Cada uno indica tipografía y momento (sobre qué B-roll aparece, cuánto dura).

**Importante:** este formato es deliberadamente simple. Mer no necesita pensar en qué B-roll cubre qué frase del monólogo — eso se decide en edición. Ella solo se preocupa por grabar bien el monólogo y los B-rolls por separado.
