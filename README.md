# Laboratorio de scanline

Escena 3D renderizada en el navegador con un rasterizador hecho desde cero en JavaScript, sin WebGL ni librerías. Cada píxel se calcula en el código.

**Ver en línea:** https://darian277.github.io/Laboratorio-de-scanline/

## Qué incluye

- **Escena base:** un cubo, una pirámide y un piso, con cámara y luz.
- **Cámara:** proyección en perspectiva con `lookAt`. Se puede girar, subir y alejar con los controles.
- **Luz:** direccional, con control de azimut y elevación.
- **Scanline:** los triángulos se ordenan por Y y se rellenan fila por fila, interpolando los bordes.
- **Z-buffer:** un píxel solo se pinta si está más cerca de la cámara que lo ya dibujado.
- **Sombreado plano (flat shading):** un solo valor de luz por cara, calculado con la normal y la dirección de la luz.

## Cómo funciona

1. Cada vértice se transforma de espacio mundo a espacio de pantalla (vista y perspectiva).
2. Por cada triángulo se calcula la normal y la intensidad de luz: `0.15 + 0.85 * max(0, N · L)`.
3. `rasterTriangle` recorre las filas del triángulo, calcula `x` y `z` en cada borde y rellena el tramo entre ambos.
4. Antes de escribir un píxel se compara su profundidad con el z-buffer.

## Cómo ejecutarlo

No necesita instalación. Descarga el repositorio y abre `index.html` en el navegador.

```powershell
git clone https://github.com/Darian277/Laboratorio-de-scanline.git
```

## Estructura

```
Laboratorio-de-scanline/
├── index.html   # escena, rasterizador y controles
└── README.md
```

## Limitaciones

- No hay *clipping* contra el plano cercano: los triángulos que quedan detrás de la cámara se descartan completos.
- El sombreado es plano, así que se ven las caras. No hay interpolación de normales (Gouraud o Phong).
- Todo corre en la CPU, por lo que no es adecuado para escenas con muchos triángulos.

## Autor

Darian Emmanuel Rodriguez Bonilla