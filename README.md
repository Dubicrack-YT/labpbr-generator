# LABPBR Glossy Pack Generator

> Crea localmente **resource packs Glossy planos** para Java Edition y **resource packs PBR para Bedrock**. Los archivos nunca se envían a un servidor y la herramienta no modifica ni incluye APKs.

**[Abrir la versión publicada](https://dubicrack-yt.github.io/labpbr-generator/)**

LABPBR Glossy Pack Generator parte de los assets originales y genera reflexión lisa sin altura, parallax, bump falso ni emisión accidental. El preview permanente **Antes / Después** usa las capturas aportadas para mostrar el objetivo visual antes de exportar.

## Presets Glossy

La receta ya no se edita con sliders. En su lugar, se selecciona uno de tres presets seguros. Todos mantienen una normal completamente neutra `128,128,255,255`, por lo que no introducen profundidad.

| Preset | Uso | Suavidad / F0 / Porosidad / Emisión |
| --- | --- | --- |
| **Espejo plano** | Opción recomendada; reflejo máximo. | `255 / 255 / 0 / 0` |
| **Pulido** | Reflejo controlado, todavía sin volumen. | `220 / 200 / 30 / 0` |
| **Satinado** | Brillo más suave para materiales menos especulares. | `160 / 150 / 80 / 0` |

## Salidas

| Destino | Archivo generado | Mapas | Alcance |
| --- | --- | --- | --- |
| **Java 1.16+** | Un único `.zip` | `_n` y `_s` LABPBR | Bloques, ítems y entidades de packs/ZIP/JAR. |
| **Bedrock PBR** | Un `.mcpack` | Color, `_normal`, `_mer` y `*.texture_set.json` | Releases oficiales Mojang o Custom ZIP/MCPACK; RTX y Vibrant Visuals. |

### Java 1.16+: un solo ZIP

El selector de versiones fue retirado. La salida Java genera un único overlay con `pack_format: 5`, priorizando la apertura desde 1.16 en adelante. Java Edition no permite expresar en un único `pack.mcmeta` toda la matriz histórica de formatos; en versiones recientes el juego puede mostrar su aviso normal de compatibilidad, pero no se necesitan copias por versión.

La salida Java solo procesa PNG dentro de `textures/block`, `textures/blocks`, `textures/item`, `textures/items` y `textures/entity`. Conserva los `.mcmeta` de animación en los mapas generados, ignora `_n` y `_s` ya existentes y deja intactos GUI, fuentes, pantallas, mapas, pinturas y sonido.

### Bedrock: RTX y Vibrant Visuals

La opción Bedrock crea un **resource pack**, no un APK. Cada textura genera color PNG, normal plana y mapa MER, donde RGB representa metalness, emissive y roughness. El manifest usa `min_engine_version: [1, 21, 120]` y las capabilities `pbr` y `raytraced`, según la guía oficial de Microsoft para Vibrant Visuals y RTX. [1] [2]

> **Límite de plataformas:** RTX requiere hardware RTX compatible. Vibrant Visuals es la alternativa PBR multiplataforma. La correspondencia exacta con texturas vanilla de Bedrock depende de que los nombres y rutas de origen coincidan con los identificadores de Bedrock; revisa el pack importado en el juego antes de usarlo en un mundo importante.

## Uso

### Entradas empaquetadas únicamente

La aplicación **no acepta PNG, JPG, WebP ni texturas individuales**. Sube siempre un archivo empaquetado completo y elige el destino antes de cargarlo.

| Destino seleccionado | Entradas admitidas | No admitido |
| --- | --- | --- |
| **Java 1.16+** | Resource packs `.zip` y archivos `.jar` de Java. | Imágenes individuales. |
| **Bedrock PBR · Repositorio oficial** | La aplicación consulta las releases de `Mojang/bedrock-samples` y ofrece los assets `full.zip`. | `min.zip`, imágenes individuales, APK y `.jar`. |
| **Bedrock PBR · Custom** | Un ZIP de resource pack o un `.mcpack` propio. | Imágenes individuales, APK y `.jar`. |

1. Elige **Java 1.16+** o **Bedrock PBR**; la zona de trabajo solo muestra formatos compatibles con ese destino.
2. Para Java, arrastra uno o varios ZIP/JAR. Para Bedrock, el origen predeterminado es el **Repositorio oficial**: selecciona una release estable o Preview de Mojang y pulsa **Usar esta release oficial**. La herramienta siempre señala el asset `full.zip`, que sí conserva texturas y otros binarios; nunca selecciona `min.zip`.
3. GitHub no permite que un navegador estático lea en todos los casos el ZIP de release de forma cruzada. Cuando ocurra, el botón iniciará la descarga oficial y el panel indicará cambiar a **Custom** para subir ese mismo ZIP. Custom queda reservado exclusivamente para ZIP de resource pack o MCPACK propios.
4. Selecciona un preset Glossy y revisa el preview permanente **Antes / Después**. Pulsa convertir; cada archivo produce una salida independiente: ZIP para Java o MCPACK para Bedrock.

Un JAR fuente **nunca se modifica ni se vuelve a empaquetar como ejecutable**. Solo puede usarse como entrada Java: se extraen únicamente los assets de bloques, ítems y entidades necesarios para el resource pack ZIP. En Bedrock, los JAR no son una entrada válida; el resultado siempre procede de un Vanilla ZIP o MCPACK y se descarga como MCPACK separado.

El límite local es de **300 MB por archivo** y **20 000 texturas convertibles por archivo**. Si un pack supera ese límite, sepáralo por mod o namespace antes de convertirlo.

## Privacidad

Canvas 2D y compresión ZIP se ejecutan en el navegador. Ninguna textura, pack o JAR se transmite a una API. Las descargas se crean localmente.

## Inspector recomendado

Para Java, se recomienda [Complementary Reimagined][5], disponible en [Modrinth][5] y [CurseForge][6]. Para Bedrock, importa el MCPACK y habilita **Vibrant Visuals** o **ray tracing** en un dispositivo compatible.

## Desarrollo local

```bash
pnpm install
pnpm dev
pnpm check
pnpm build
```

La aplicación usa React, TypeScript, Vite y [JSZip](https://github.com/Stuk/jszip) para leer y crear packs localmente. `scripts/export-github-pages.mjs` prepara los archivos estáticos que se publican en GitHub Pages.

## Licencia

Este proyecto se distribuye bajo la [licencia MIT](LICENSE).

## Referencias

[1]: https://learn.microsoft.com/en-us/minecraft/creator/documents/vibrantvisuals/vvresourcepacks?view=minecraft-bedrock-stable "Microsoft Learn — Vibrant Visuals Resource Packs"
[2]: https://learn.microsoft.com/en-us/minecraft/creator/reference/content/texturesetsreference/texturesetsconcepts/texturesetsintroduction?view=minecraft-bedrock-stable "Microsoft Learn — Texture Set JSON"
[3]: https://learn.microsoft.com/en-us/minecraft/creator/documents/vibrantvisuals/pbroverview?view=minecraft-bedrock-stable "Microsoft Learn — Overview of Physically Based Rendering"
[4]: https://minecraft.wiki/w/Pack_format "Minecraft Wiki — Pack format"
[5]: https://modrinth.com/project/HVnmMxH1 "Complementary Reimagined — Modrinth"
[6]: https://www.curseforge.com/minecraft/shaders/complementary-reimagined "Complementary Reimagined — CurseForge"
[7]: https://aka.ms/resourcepacktemplate "Vanilla Resource Pack oficial — Mojang bedrock-samples releases"
[8]: https://github.com/Mojang/bedrock-samples/releases "Mojang — Bedrock Samples Releases"
