# AURA / 2040 — Realidad Aumentada UNAM

Micrositio estático para presentar **AURA 2040**, un objeto especulativo concebido como una unidad personal de regulación ambiental y biométrica. El sitio combina narrativa de diseño, un visor 3D con WebGL/Three.js y apertura de un modelo USDZ mediante Apple Quick Look en iPhone/iPad.

## Estado actual

El sitio ya funciona aunque los modelos 3D todavía no estén conectados. Mientras `modelGLB` esté vacío, se muestra el render de referencia y un proxy geométrico WebGL. Cuando se añada la URL del GLB, el visor cargará automáticamente el modelo real.

## Modelos 3D en otro repositorio

Edita `config.js` y pega las URLs públicas servidas por GitHub Pages:

```js
export const ASSETS = {
  modelGLB: "https://TU-USUARIO.github.io/REPO-MODELO/device.glb",
  modelUSDZ: "https://TU-USUARIO.github.io/REPO-MODELO/device.usdz"
};
```

- `device.glb` → visor 3D interactivo en la página.
- `device.usdz` → realidad aumentada en Safari mediante Apple Quick Look.

> USDZ no sustituye al GLB dentro de WebGL. Para una experiencia completa conviene exportar el mismo objeto en ambos formatos.

## Estructura

```text
/
├─ index.html
├─ styles.css
├─ app.js
├─ config.js
├─ .nojekyll
└─ assets/
   └─ device-reference.jpg
```

## GitHub Pages

Este repositorio está preparado para publicarse desde `main` y la raíz `/`. En GitHub: **Settings → Pages → Deploy from a branch → main → /(root)**.

La URL esperada, una vez activado Pages, es:

`https://brunososal.github.io/Realidad-Aumentada-UNAM/`

## Recomendaciones para los modelos

- GLB idealmente menor de 10–15 MB.
- Texturas 1K–2K cuando sea suficiente.
- Origen cerca del centro geométrico.
- Escala real en metros para que USDZ se coloque correctamente en AR.
- Materiales PBR simples y compatibles con glTF/USDZ.
- Servir ambos modelos por HTTPS desde GitHub Pages para evitar problemas de CORS y para que Quick Look pueda acceder al USDZ.

## Nota técnica

En navegador se utiliza **WebGL**, no OpenGL directamente. El render se realiza con `THREE.WebGLRenderer`. En iPhone/iPad, la capa de realidad aumentada se delega a **Apple Quick Look** mediante el archivo USDZ.
