# LABPBR Texture Generator

> Genera mapas LABPBR directamente desde una textura, sin enviar el archivo a ningún servidor.

**[Abrir la versión publicada](https://dubicrack-yt.github.io/labpbr-generator/)**

LABPBR Texture Generator es una herramienta de navegador para creadores de resource packs de Minecraft. Carga una textura PNG, JPG o WebP, selecciona una familia de material y descarga los pares LABPBR `_n` y `_s` con el nombre correcto. Está pensada para crear una base reproducible para shaders compatibles con Iris u Oculus, no para sustituir el ajuste artístico final por textura.

## Qué genera

| Modo | Mapa `_n` | Mapa `_s` | Caso de uso |
| --- | --- | --- | --- |
| **Glossy plano** | Normal neutra `128,128,255,255`; sin relieve, altura ni parallax. | Suavidad máxima y reflectividad graduable. | Superficies de reflejo liso, vidrio pulido o acabado espejo. |
| **PBR normal** | Normal local derivada de la luminancia con profundidad graduable. | Suavidad, F0, porosidad y emisión según el material. | Una primera interpretación PBR de madera, piedra, metal y otros materiales. |

Las familias disponibles son madera, piedra, metal, cristal, vegetal, orgánico, suelo y emisivo. La interfaz permite variar F0, suavidad, profundidad y emisión antes de exportar.

## Privacidad y funcionamiento

El procesamiento usa Canvas 2D en el propio navegador. La imagen seleccionada no se sube a una API ni se guarda en un servidor. Las descargas se crean localmente como `<nombre>_n.png` y `<nombre>_s.png`.

## Uso rápido

1. Abre la página publicada y suelta una textura en la zona **Entrada**.
2. Elige **Glossy plano** o **PBR normal**, y selecciona la familia de material.
3. Ajusta los controles de reflectividad, profundidad o emisión según el acabado que busques.
4. Descarga los mapas `_n` y `_s`, y colócalos junto al albedo original dentro de la misma ruta del resource pack.

> Para no mezclar resultados, utiliza una sola variante de PBR por textura y prueba el pack en el shader que vayas a usar.

## Desarrollo local

```bash
pnpm install
pnpm dev
```

La aplicación principal usa React, TypeScript y Vite. El comando `pnpm build` genera el bundle de producción. El script `scripts/export-github-pages.mjs` prepara una versión HTML/CSS/JS estática para repositorios que se publiquen desde una rama de GitHub Pages.

## LABPBR

Los sufijos `_n` y `_s`, así como la lectura de sus canales, siguen el estándar LABPBR [1] y las recomendaciones PBR de Iris [2]. El generador declara `format=lab-pbr/1.3` en los paquetes exportados por el flujo de resource pack.

## Licencia

Este proyecto se distribuye bajo la [licencia MIT](LICENSE).

## Referencias

[1]: https://shaderlabs.org/wiki/LabPBR_Material_Standard "LabPBR Material Standard — shaderLABS"

[2]: https://shaders.properties/current/how-to/pbr_standards/ "Iris Docs — PBR Standards"
