# Práctica S8 IG · Accidentes aéreos 1970–2020 sobre el planeta Tierra

Visualización en **three.js** de la evolución de la tasa mundial de accidentes aéreos mortales, sobre un globo terráqueo con miles de aviones en movimiento y un contador de años.

> **Vídeo de la visualización:** _(pega aquí el enlace o añade el archivo, máx. 30 s)_
>
> **Autor/a:** _(nombre y apellidos)_

---

## Qué muestra

Un planeta 3D (esfera con textura de la Tierra, halo atmosférico y fondo de estrellas) por el que vuelan unos 1500 aviones a la vez entre 91 aeropuertos reales. Arriba, un **contador de año** recorre de 1970 a 2020 en unos 28 segundos. Cada año:

- se muestra la **tasa mundial real** de accidentes mortales por millón de vuelos (dato del CSV);
- la probabilidad de que cada avión sufra un accidente sigue esa tasa. Los aviones accidentados se ponen **rojos**, caen hacia la superficie y dejan un anillo que se expande;
- una **gráfica** en la esquina inferior izquierda dibuja la serie completa, con un cursor que marca el año actual.

El efecto visual es que en los años 70 se ven muchos más accidentes por segundo que en la actualidad, reflejando la mejora de seguridad de la aviación.

## Datos

| Archivo | Contenido | Origen |
|---|---|---|
| `src/accidentes_aereos.csv` | Accidentes mortales por millón de vuelos comerciales, mundo, 1970–2020 (sin 1972). Separador `,` | Our World in Data, descargado de Kaggle (sin modificar) |
| `src/aeropuertos.csv` | 91 aeropuertos: código, nombre, latitud, longitud y peso de tráfico. Separador `;` | Elaboración propia: coordenadas aproximadas; el peso de tráfico es una estimación orientativa para concentrar rutas en los grandes hubs |

Los CSV se cargan con `fetch` y se procesan en `procesarCSVAccidentes` y `procesarCSVAeropuertos`, siguiendo el esquema de las prácticas con Sitycleta. Para 1972, que no aparece en el CSV, se usa el valor de 1971.

### Limitaciones y qué es simulación

- El CSV **solo contiene el dato mundial por año**, sin ubicación de los accidentes. Por tanto, **las rutas y los puntos donde ocurren los accidentes son simulados**: son aviones entre aeropuertos reales y no accidentes reales localizados.
- La probabilidad real de accidente (≈ 1 entre un millón de vuelos) no sería visible, así que se **multiplica por 600** (`EXAGERACION`). Lo que se conserva es la proporción entre años. Esto también se indica en pantalla.
- No se representa el número real de vuelos de cada año: la cantidad de aviones es constante.

## Técnicas de three.js utilizadas

- `SphereGeometry` + `MeshPhongMaterial` con textura de color y mapa especular, y conversión latitud/longitud a coordenadas 3D coincidiendo con el mapeo UV de la esfera.
- Rutas por **círculos máximos** (interpolación esférica) y orientación de cada avión con una base de vectores (normal a la esfera, rumbo del vuelo).
- `InstancedMesh` con la textura PNG de un avión (`avion.png`, con canal alfa) y color por instancia, para mover 1500 aviones con buen rendimiento.
- `ShaderMaterial` con efecto Fresnel para el halo de la atmósfera, y `Points` para las estrellas.
- `OrbitControls` con giro automático, y luces ligadas a la cámara.
- Elementos HTML superpuestos (contador de año, textos, gráfica en `canvas`).

## Estructura

```
index.html
script_27_aviones.js
src/
  accidentes_aereos.csv
  aeropuertos.csv
  avion.png
  earth_atmos_2048.jpg
  earth_specular_2048.jpg
```

## Cómo ejecutarlo

1. Coloca los archivos de `src/` en la carpeta `src/` del proyecto y `script_27_aviones.js` junto a `index.html`.
2. En `index.html` deja activo solo este script:
   ```html
   <script src="script_27_aviones.js" type="module"></script>
   ```
3. Arranca el proyecto con el mismo entorno de las prácticas anteriores (los imports de `three` y `OrbitControls` son los mismos).

## Controles

- **Ratón:** arrastrar para girar, rueda para acercar o alejar.
- **Barra espaciadora:** pausa o reanuda la animación.

## Créditos

- Datos de accidentes: Our World in Data (a través de Kaggle). Comprueba la licencia y cita en la página de origen.
- Texturas de la Tierra (`earth_atmos_2048.jpg`, `earth_specular_2048.jpg`): ejemplos oficiales de three.js (`examples/textures/planets`).
- Icono de avión (`avion.png`): dibujo propio generado para esta práctica.
- Parte del código se ha desarrollado con ayuda de Claude (Anthropic), a partir del código de referencia del profesorado (`script_21`, `script_24`, `script_25`).
