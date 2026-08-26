# LABPBR Glossy Pack Generator

> Crea localmente **resource packs Glossy planos** para Java Edition y **resource packs PBR para Bedrock**. Los archivos no se envían a un servidor y la herramienta no modifica ni incluye APKs.

**[Abrir la versión publicada](https://dubicrack-yt.github.io/labpbr-generator/)**

LABPBR Glossy Pack Generator mantiene los assets originales y genera reflejos lisos sin altura, parallax, bump falso ni emisión accidental. El preview permanente **Antes / Después** usa las capturas de referencia para mostrar el acabado antes de exportar.

## Presets Glossy

La receta se selecciona con presets seguros. Todos mantienen normal neutra 128/128/255/255 y no introducen profundidad.

| Preset | Uso | Suavidad / F0 / Porosidad / Emisión |
| --- | --- | --- |
| **Espejo plano** | Recomendado; reflejo máximo. | 255 / 255 / 0 / 0 |
| **Pulido** | Reflejo controlado, sin volumen. | 220 / 200 / 30 / 0 |
| **Satinado** | Brillo más suave, sin relieve. | 160 / 150 / 80 / 0 |

## Salidas

| Destino | Archivo generado | Mapas | Alcance |
| --- | --- | --- | --- |
| **Java 1.16+** | Un ZIP | _n y _s LABPBR | Bloques, ítems y entidades de packs, ZIP y JAR. |
| **Bedrock PBR** | Un MCPACK | Color, _normal, _mer y texture set JSON | Bedrock RTX y Vibrant Visuals. |

### Java 1.16+: un ZIP universal

El selector de versiones fue retirado. La salida Java usa pack_format 5 para priorizar la apertura desde 1.16 en adelante. Java Edition no permite declarar en un solo pack.mcmeta todos los formatos históricos; los lanzamientos recientes pueden mostrar su aviso normal de compatibilidad, pero no se generan copias por versión.

La salida procesa PNG de textures/block, textures/blocks, textures/item, textures/items y textures/entity. Conserva animaciones y deja intactos GUI, fuentes, pantallas, mapas, pinturas y sonidos.

### Bedrock: RTX y Vibrant Visuals

La opción Bedrock crea un **resource pack**, no un APK. Cada textura genera color PNG, normal plana y MER, donde RGB es metalness, emissive y roughness. El manifest establece min_engine_version 1.21.120 y las capabilities pbr y raytraced, conforme a la documentación de Microsoft para Vibrant Visuals y RTX. [1] [2]

> **Límite de plataformas:** RTX requiere hardware compatible. Vibrant Visuals es la alternativa PBR multiplataforma. La correspondencia con texturas vanilla depende de que las rutas y nombres del origen coincidan con los identificadores Bedrock; prueba el MCPACK en el juego antes de usarlo en un mundo importante.

## Uso

1. Selecciona uno o más PNG, JPG o WebP, o varios ZIP/JAR.
2. Elige Espejo plano, Pulido o Satinado.
3. Elige Java 1.16+ o Bedrock PBR.
4. Revisa el preview Antes / Después, genera y descarga el ZIP o MCPACK local.

Un JAR fuente **nunca se modifica ni se vuelve a empaquetar como ejecutable**. Para Java se extraen solo assets convertibles; para Bedrock se produce un MCPACK independiente. El límite local es de **300 MB por archivo** y **20 000 texturas convertibles**.

## Privacidad

Canvas 2D y la compresión ZIP se ejecutan en el navegador. Ninguna textura, pack o JAR se transmite a una API; las descargas se crean localmente.

## Inspector recomendado

Para Java, usa [Complementary Reimagined][5], disponible en [Modrinth][5] y [CurseForge][6]. Para Bedrock, importa el MCPACK y habilita **Vibrant Visuals** o **ray tracing** en un dispositivo compatible.

## Desarrollo local

~~~bash
pnpm install
pnpm dev
pnpm check
pnpm build
~~~

La aplicación usa React, TypeScript, Vite y [JSZip](https://github.com/Stuk/jszip). El script scripts/export-github-pages.mjs prepara los archivos estáticos de GitHub Pages.

## Licencia

Este proyecto se distribuye bajo la [licencia MIT](LICENSE).

## Referencias

[1]: https://learn.microsoft.com/en-us/minecraft/creator/documents/vibrantvisuals/vvresourcepacks?view=minecraft-bedrock-stable "Microsoft Learn — Vibrant Visuals Resource Packs"
[2]: https://learn.microsoft.com/en-us/minecraft/creator/reference/content/texturesetsreference/texturesetsconcepts/texturesetsintroduction?view=minecraft-bedrock-stable "Microsoft Learn — Texture Set JSON"
[3]: https://learn.microsoft.com/en-us/minecraft/creator/documents/vibrantvisuals/pbroverview?view=minecraft-bedrock-stable "Microsoft Learn — Overview of Physically Based Rendering"
[4]: https://minecraft.wiki/w/Pack_format "Minecraft Wiki — Pack format"
[5]: https://modrinth.com/project/HVnmMxH1 "Complementary Reimagined — Modrinth"
[6]: https://www.curseforge.com/minecraft/shaders/complementary-reimagined "Complementary Reimagined — CurseForge"
