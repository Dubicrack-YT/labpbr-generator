# LABPBR Glossy Pack Generator


> Convierte texturas, resource packs ZIP y JARs de Minecraft/mods en **resource packs Glossy planos**, sin enviar los archivos a un servidor.


**[Abrir la versión publicada](https://dubicrack-yt.github.io/labpbr-generator/)**


LABPBR Glossy Pack Generator es una herramienta local de navegador para crear acabados reflectantes, lisos y sin volumen heredado. No tiene modos PBR normales ni familias de material. Parte de una receta **Glossy plano recomendada** y permite ajustar sus canales cuando se necesita una variante controlada.


## Salidas


| Entrada | Operación múltiple | Salida |
| --- | --- | --- |
| Texturas PNG, JPG o WebP | Se pueden seleccionar varias a la vez. | Un resource pack por cada versión elegida, con todas las parejas `_n` y `_s`. |
| Resource packs `.zip` | Se pueden seleccionar varios a la vez. | Un resource pack Glossy por cada combinación de ZIP y versión; mantiene el contenido original y añade los mapas derivados. |
| JARs de mod o de Minecraft | Se pueden seleccionar varios a la vez. | Un resource pack ZIP por cada combinación de JAR y versión. El JAR fuente no se modifica ni se vuelve a empaquetar como ejecutable. |


El preset inicial produce `_n = 128,128,255,255` y `_s = 255,255,0,255`: normal neutra, suavidad y F0 máximos, porosidad nula y emisión apagada. La sección **Receta Glossy** permite ajustar suavidad (R), F0 (G), porosidad (B) y emisión (alfa); esos controles nunca introducen relieve, altura ni parallax.


## Compatibilidad por versión


La aplicación permite marcar varios destinos desde **Minecraft 1.16 hasta 26.2** y crea un ZIP independiente por versión. La metadata usa `pack_format` hasta 1.21.8 y, desde 1.21.9, los campos modernos `min_format` y `max_format`. [1]


| Minecraft Java | Formato de resource pack |
| --- | --- |
| 1.16 – 1.16.1 | 5 |
| 1.16.2 – 1.16.5 | 6 |
| 1.17 – 1.17.1 | 7 |
| 1.18 – 1.18.2 | 8 |
| 1.19 – 1.19.2 | 9 |
| 1.19.3 / 1.19.4 | 12 / 13 |
| 1.20 – 1.20.1 / 1.20.2 | 15 / 18 |
| 1.20.3 – 1.20.4 / 1.20.5 – 1.20.6 | 22 / 32 |
| 1.21 – 1.21.1 / 1.21.2 – 1.21.3 | 34 / 42 |
| 1.21.4 / 1.21.5 / 1.21.6 | 46 / 55 / 63 |
| 1.21.7 – 1.21.8 | 64 |
| 1.21.9 – 1.21.10 / 1.21.11 | 69.0 / 75.0 |
| 26.1 – 26.1.2 / 26.2 | 84.0 / 88.0 |


## Preview antes / después


El panel derecho incorpora un preview permanente con las capturas de referencia aportadas. Su divisor vertical permite revelar **Antes** y **Después · Glossy** sin obligarte a cargar una textura previamente. Las cargas de texturas, ZIP y JAR siguen disponibles en el panel izquierdo y todas las salidas continúan siendo resource packs ZIP.


## Rutas que procesa


En ZIP/JAR, el conversor solo genera mapas para PNG ubicados en rutas de `textures/block`, `textures/blocks`, `textures/item`, `textures/items` o `textures/entity`. Conserva los `.mcmeta` de animación en los mapas derivados y no vuelve a procesar archivos LABPBR existentes.


> Las interfaces, fuentes, pantallas, mapas, pinturas y sonidos quedan fuera de la conversión. Un ZIP los conserva sin cambios. La salida que proviene de un JAR solo incluye los assets necesarios para funcionar como resource pack y nunca incluye clases, manifiestos ni firmas del archivo original.


## Shader recomendado


Para inspeccionar el acabado Glossy se recomienda [Complementary Reimagined](https://modrinth.com/project/HVnmMxH1), disponible también en [CurseForge](https://www.curseforge.com/minecraft/shaders/complementary-reimagined). El shader es opcional: la generación de mapas y de resource packs no depende de él.


## Privacidad


Canvas 2D y compresión ZIP se ejecutan directamente en tu navegador. Ninguna textura, pack o JAR se envía a una API ni se almacena en un servidor. Las descargas se crean como ZIP locales.


## Desarrollo local


```bash
pnpm install
pnpm dev
```


La aplicación usa React, TypeScript, Vite y [JSZip](https://github.com/Stuk/jszip). `pnpm build` genera el bundle de producción y `scripts/export-github-pages.mjs` prepara los archivos estáticos de GitHub Pages.


## Licencia


Este proyecto se distribuye bajo la [licencia MIT](LICENSE).


## Referencias


[1]: https://minecraft.wiki/w/Pack_format "Minecraft Wiki — Pack format"

