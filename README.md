# Accidentes aéreos 1970–2020 sobre el planeta Tierra

Visualización en de la evolución de la tasa mundial de accidentes aéreos mortales, sobre un globo terráqueo con miles de aviones en movimiento y un contador de años.

> Autoría: Houyame Liazidi Daoudi · Asignatura: Informática Gráfica

## Vídeo de ejecución
https://youtu.be/6sMtO0hEwiQ

## Enlace de codesandbox
https://codesandbox.io/p/sandbox/qlzj59

## Qué se ha hecho
Un planeta 3D (esfera con textura de la Tierra, halo atmosférico y fondo de estrellas) por el que vuelan unos 1500 aviones a la vez entre 91 aeropuertos reales. Arriba, un **contador de año** recorre de 1970 a 2020 en unos 28 segundos. Cada año:
- se muestra la **tasa mundial real** de accidentes mortales por millón de vuelos.
- la probabilidad de que cada avión sufra un accidente sigue esa tasa. Los aviones accidentados se ponen **rojos**, caen hacia la superficie y dejan un anillo que se expande.
- una **gráfica** en la esquina inferior izquierda dibuja la serie completa, con un cursor que marca el año actual.

El efecto visual es que en los años 70 se ven muchos más accidentes por segundo que en la actualidad, reflejando la mejora de seguridad de la aviación.

## Controles
- **Ratón:** arrastrar para girar, rueda para acercar o alejar.
- **Barra espaciadora:** pausa o reanuda la animación.

## Fuentes
- Práctica 8 de la asignatura (código de referencia).
- Documentación de three.js: https://threejs.org/docs/.
- Texturas de la Tierra: ejemplos oficiales de three.js (examples/textures/planets)
- Datos de los csv: https://www.kaggle.com/
