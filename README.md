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
| 🎬 A cámara | `block-camera` | Dorado | Lo que Mer dice frente a cámara |
| 📹 B-roll | `block-broll` | Azul gris | Lo que se ve mientras habla |
| ✍️ Texto en pantalla | `block-overlay` | Rosa apagado | Sobreimpresos / frases flotantes |

Cada bloque incluye un `block-direction` con la indicación técnica (toma, plano, luz, ritmo).
