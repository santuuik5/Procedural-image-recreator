# [APP_TITLE]

> Aplicación web en un **único archivo (`index.html`)** que vuelve a dibujar cualquier imagen de forma procedural y visible en tiempo real sobre Canvas 2D. Cero dependencias, cero Python, cero backend, cero llamadas a API de pago.

[![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat-square&logo=html5&logoColor=white)](https://developer.mozilla.org/es/docs/Web/HTML)
[![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat-square&logo=css3&logoColor=white)](https://developer.mozilla.org/es/docs/Web/CSS)
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)](https://developer.mozilla.org/es/docs/Web/JavaScript)
[![Sin dependencias](https://img.shields.io/badge/dependencias-cero-success?style=flat-square)](https://github.com/santuuik5/Procedural-image-recreator)
[![GitHub Pages](https://img.shields.io/badge/GitHub%20Pages-Activo-2bbf84?style=flat-square)](https://[GITHUB_USERNAME].github.io/[REPO_NAME]/)

---

## Demo / Previsualización en vivo

Prueba la aplicación directamente desde GitHub Pages:

👉 **https://[GITHUB_USERNAME].github.io/[REPO_NAME]/**

> Reemplaza `[GITHUB_USERNAME]` y `[REPO_NAME]` por tu usuario y nombre de repositorio de GitHub (ver sección **Despliegue en GitHub**).

---

## 🖼️ Vista previa

| Modo | Resultado |
|------|-----------|
| **Puntillismo adaptativo** | Miles de puntos cuyo tamaño y densidad responden a la luminosidad local de la imagen. |
| **Pinceladas de óleo** | Trazos dinámicos orientados por el gradiente de color, estilo pintura al óleo. |
| **Hilorama / Constelaciones** | Nodos sobre los bordes conectados progresivamente como un hilo estirado. |
| **Teselado geométrico** | Polígonos rellenos con el color promedio de cada región, estilo low-poly. |

---

## Ejecución local (`localhost`)

No necesitas instalar nada: el proyecto es estático. Abre una terminal en la carpeta del repositorio y usa **uno** de estos comandos:

### Con `npx serve` (recomendado)
```bash
npx serve -l 3000
```
Luego abre `http://localhost:3000` en el navegador.

### Con Python 3
```bash
python3 -m http.server 3000
```
Luego abre `http://localhost:3000`.

### Con PHP
```bash
php -S localhost:3000
```

### Con VS Code
Instala la extensión **Live Server**, haz clic derecho sobre `index.html` → *Open with Live Server*.

---

## Características clave

- **Archivo único**: HTML, CSS y JS embebidos en `index.html`; nada que instalar.
- **Drag & Drop y selector de archivos**: carga cualquier PNG/JPG/WebP y comienza al instante.
- **Renderizado a 60 FPS** mediante `requestAnimationFrame`, con reconstrucción paso a paso visible en tiempo real.
- **Cuatro algoritmos generativos nativos** implementados píxel a píxel / trazo a trazo sobre Canvas 2D (sin filtros CSS que simulen el efecto).
- **Controles de usuario**: selector de estilo, ajuste de velocidad y densidad, botones Pausa / Reanudar / Reiniciar y exportación del resultado a PNG.
- **Interfaz Glassmorphism**: tema oscuro, paneles translúcidos con desenfoque y animaciones fluidas.
- **Diseño responsive**: funciona en móvil y escritorio.

---

## Guía de uso paso a paso

1. Abre `index.html` (local o en GitHub Pages).
2. Arrastra una imagen al área de marcado o haz clic y selecciona un archivo.
3. Elige un **estilo procedural** en el panel derecho.
4. Ajusta **Densidad** (cantidad de trazos/puntos) y **Velocidad** (trazos por frame).
5. Pulsa **Pausar** / **Reanudar** para controlar el dibujo en tiempo real.
6. Pulsa **Reiniciar** para empezar el estilo desde cero con la misma imagen.
7. Pulsa **Exportar PNG** para descargar el resultado en la resolución de procesamiento.

---

## Explicación técnica de los algoritmos

Toda la lógica vive en `index.html` y opera así:

1. **Carga**: la imagen se decodifica en un `ImageData` y se reduce internamente a un máximo de 700 px en su lado largo para mantener los 60 FPS.
2. **Mapas auxiliares**: se precalculan una tabla de luminosidad y un mapa de bordes (gradiente simple) que guían los algoritmos adaptativos.
3. **Bucle principal**: `requestAnimationFrame` ejecuta un lote de trazos por frame (ajustable con *Velocidad*), dibujando directamente sobre el lienzo de trabajo Canvas 2D.

### 1. Puntillismo adaptativo
Para cada punto candidato se elige una posición aleatoria y se acepta con una probabilidad proporcional a `255 − luminosidad` (las zonas oscuras reciben más puntos). El radio del punto varía ligeramente, generando un efecto de stippling orgánico que respeta la composición original.

### 2. Pinceladas de óleo
Se toma un punto aleatorio, se calcula su gradiente de color local y se dibuja un trazo lineal en la **tangente** al borde (perpendicular al gradiente). El largo y grosor del trazo crecen con la intensidad del borde, y el color se muestrea de la imagen fuente, imitando pinceladas dinámicas de óleo.

### 3. Hilorama / Constelaciones
Se colocan nodos sobre los puntos de borde de la imagen. Cada nuevo nodo se conecta con los nodos previos cercanos mediante líneas finas del color muestreado, y se dibuja el punto del nodo. El resultado progresivo recuerda a un hilo estirado entre clavos o a una constelación.

### 4. Teselado geométrico
Se genera una red de celdas poligonales con vértices ligeramente perturbados. Cada celda se rellena con el **color promedio** de la región correspondiente de la imagen fuente, produciendo un efecto low-poly / teselado geométrico que se revela celda a celda.

---

## Estructura del repositorio

```
procedural-canvas-art/
├── index.html      # Aplicación completa (HTML + CSS + JS embebidos)
├── README.md       # Esta documentación
└── .gitignore      # Archivos ignorados por Git
```

---

## Despliegue en GitHub

Sube el código al repositorio remoto con esta secuencia exacta:

```bash
# 1. Inicializa Git (si aún no está inicializado)
git init

# 2. Añade todos los archivos
git add .

# 3. Crea el primer commit
git commit -m "feat: release CanvasForge procedural art generator"

# 4. Asigna el repositorio remoto
git remote add origin https://github.com/[GITHUB_USERNAME]/[REPO_NAME].git

# 5. Renombra la rama principal a main y sube
git branch -M main
git push -u origin main
```

### Activar GitHub Pages

1. Ve a tu repositorio en GitHub → **Settings** → **Pages**.
2. En **Build and deployment** → **Branch**, selecciona `main` y la carpeta `/ (root)`.
3. Haz clic en **Save**.
4. En breve tendrás la aplicación en:
   `https://[GITHUB_USERNAME].github.io/[REPO_NAME]/`

---

## Tecnologías

- HTML5 Canvas 2D API
- CSS3 moderno (Glassmorphism, `backdrop-filter`, variables CSS)
- JavaScript vanilla (ES6+), sin frameworks ni librerías externas

---

## Licencia

MIT — úsalo, modifícalo y despliégalo libremente.

---

Hecho con ❤️ y Canvas 2D · [APP_TITLE]
