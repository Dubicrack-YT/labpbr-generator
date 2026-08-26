# LABPBR Glossy Pack Generator

> Convierte texturas, resource packs ZIP y JARs de Minecraft/mods en **resource packs Glossy planos**, sin enviar los archivos a un servidor.

**[Abrir la versión publicada](https://dubicrack-yt.github.io/labpbr-generator/)**

LABPBR Glossy Pack Generator es una herramienta local de navegador para crear acabados reflectantes, lisos y sin volumen heredado. No tiene modos PBR normales, familias de material ni controles que cambien la interpretación visual: utiliza una única receta Glossy estable para cada textura procesada.

## Salidas

| Entrada | Operación múltiple | Salida |
| --- | --- | --- |
| Texturas PNG, JPG o WebP | Se pueden seleccionar varias a la vez. | Un único `texturas_glossy_resource_pack.zip` que incluye todas las parejas `_n` y `_s`. |
| Resource packs `.zip` | Se pueden seleccionar varios a la vez. | Un resource pack Glossy por cada ZIP; mantiene el contenido original y añade los mapas derivados. |
| JARs de mod o de Minecraft | Se pueden seleccionar varios a la vez. | Un resource pack ZIP por cada JAR. El JAR fuente no se modifica ni se vuelve a empaquetar como ejecutable. |

Cada textura se convierte con los siguientes valores LABPBR:

| Mapa | Canales RGBA | Resultado |
| --- | --- | --- |
| `_n` | `128,128,255,255` | Normal completamente neutra: sin relieve, altura, parallax ni AO material. |
| `_s` | `255,255,0,255` | Suavidad y F0 máximos, porosidad nula y emisión desactivada. |

## Rutas que procesa

En ZIP/JAR, el conversor solo genera mapas para PNG ubicados en rutas de `textures/block`, `textures/blocks`, `textures/item`, `textures/items` o `textures/entity`. Conserva los `.mcmeta` de animación en los mapas derivados y no vuelve a procesar archivos LABPBR `_n` o `_s` existentes.

> Las interfaces, fuentes, pantallas, mapas, pinturas y sonidos quedan fuera de la conversión. Un ZIP los conserva sin cambios. La salida que proviene de un JAR solo incluye los assets necesarios para funcionar como resource pack y nunca incluye clases, manifiestos ni firmas del archivo original.

Las imágenes sueltas que no traen una ruta de Minecraft se guardan dentro de `assets/minecraft/textures/block/` en el resource pack resultante. Cuando se cargan desde una carpeta con una ruta `assets/.../textures/...`, el generador intenta conservar esa ruta de asset.

## Uso

### Lote de texturas

1. En **Texturas**, selecciona o arrastra una o más imágenes PNG, JPG o WebP.
2. Revisa la muestra inicial; es solo una inspección visual del Glossy que recibirá todo el lote.
3. Pulsa **Crear resource pack Glossy**.
4. Descarga el único ZIP generado e instálalo como resource pack.

### Lote de packs y JARs

1. En **Packs y JARs**, selecciona uno o varios `.zip` y `.jar`.
2. Pulsa **Convertir archivos a Glossy**. Los archivos se procesan de manera secuencial para no saturar la memoria del navegador.
3. Descarga el resource pack mostrado junto a cada archivo finalizado.
4. Para una salida desde JAR, coloca el ZIP generado por encima del mod o cliente original en el orden de resource packs.

El límite local es de **300 MB** por archivo y **20 000** texturas convertibles por archivo. Si un pack supera el límite, sepáralo por mod o namespace antes de convertirlo.

## Privacidad

Canvas 2D y compresión ZIP se ejecutan directamente en tu navegador. Ninguna textura, pack o JAR se envía a una API ni se almacena en un servidor. Las descargas se crean como ZIP locales.

## Desarrollo local

```bash
pnpm install
pnpm dev
```

La aplicación usa React, TypeScript, Vite y [JSZip](https://github.com/Stuk/jszip) para leer y crear resource packs localmente. `pnpm build` genera el bundle de producción, y `scripts/export-github-pages.mjs` prepara los archivos estáticos de GitHub Pages.

## Licencia

Este proyecto se distribuye bajo la [licencia MIT](LICENSE).

## Referencias

[1]: https://shaderlabs.org/wiki/LabPBR_Material_Standard "LabPBR Material Standard — shaderLABS"

[2]: https://shaders.properties/current/how-to/pbr_standards/ "Iris Docs — PBR Standards"
