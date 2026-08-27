# LABPBR Glossy Pack Generator

> Generador local de **resource packs Glossy planos para Minecraft Java 1.16+**. Lee ZIP/JAR, produce siempre un resource pack ZIP y no sube ni modifica tus archivos originales.

**[Abrir la versión publicada](https://dubicrack-yt.github.io/labpbr-generator/)**

LABPBR Glossy Pack Generator toma assets originales de Java y genera un acabado de reflejo liso. El color y la resolución se conservan; no se genera altura, bump, parallax, AO de material ni emisión artificial. El preview permanente **Antes / Después** muestra el objetivo visual antes de exportar.

## Presets Glossy

La receta usa presets en lugar de sliders. Todos mantienen una normal completamente neutra `128,128,255,255`; por tanto, el efecto no introduce profundidad ni volumen falso.

| Preset | Uso | Suavidad / F0 / Porosidad / Emisión |
| --- | --- | --- |
| **Espejo plano** | Reflejo máximo; opción recomendada. | `255 / 255 / 0 / 0` |
| **Pulido** | Reflejo controlado, todavía sin volumen. | `220 / 200 / 30 / 0` |
| **Satinado** | Brillo más suave para materiales menos especulares. | `160 / 150 / 80 / 0` |

## Alcance de la salida

| Entrada Java | Archivo generado | Mapas generados | Alcance |
| --- | --- | --- | --- |
| Resource pack `.zip` | Un resource pack `.zip` independiente. | `_n` y `_s` LABPBR. | Bloques, ítems y entidades en rutas Java compatibles. |
| Archivo `.jar` | Un resource pack `.zip` independiente. | `_n` y `_s` LABPBR. | Extrae solo los assets elegibles del JAR; el JAR original no se altera. |

La salida usa `pack_format: 5` para priorizar la apertura desde Java 1.16. Un único `pack.mcmeta` no puede expresar todos los formatos históricos; por eso versiones más recientes podrían mostrar el aviso habitual de formato, pero no se generan copias duplicadas por versión.

## Uso

1. Arrastra uno o varios resource packs `.zip` o archivos `.jar` de Minecraft Java.
2. La herramienta procesa únicamente PNG bajo `textures/block`, `textures/blocks`, `textures/item`, `textures/items` y `textures/entity`.
3. Elige un preset Glossy y revisa el preview **Antes / Después**.
4. Pulsa **Convertir a Java Glossy**. Cada archivo de entrada produce un resource pack ZIP separado.

> **No se aceptan PNG, JPG, WebP ni texturas individuales.** GUI, fuentes, pantallas, mapas, pinturas, sonidos y música se excluyen por completo.

Los `.mcmeta` de animación se preservan en los mapas generados. Si el archivo ya contiene mapas `_n` o `_s`, esos mapas no se toman como color fuente. Un JAR se utiliza **solo** como fuente Java: nunca se reempaqueta como JAR ejecutable.

El límite local es de **300 MB por archivo** y **20 000 texturas convertibles por archivo**. Si un pack excede ese límite, sepáralo por mod o namespace antes de convertirlo.

## Privacidad

Canvas 2D y compresión ZIP se ejecutan completamente dentro del navegador. Ninguna textura, pack o JAR se transmite a una API. Las descargas también se crean localmente.

## Inspector recomendado

Para inspeccionar reflejos Glossy se recomienda [Complementary Reimagined][1], disponible en [Modrinth][1] y [CurseForge][2], con Iris u OptiFine.

## Desarrollo local

```bash
pnpm install
pnpm dev
pnpm check
pnpm build
```

La aplicación usa React, TypeScript, Vite y [JSZip](https://github.com/Stuk/jszip) para leer y crear packs locales. `scripts/export-github-pages.mjs` prepara los archivos planos publicados en GitHub Pages.

## Licencia

Este proyecto se distribuye bajo la [licencia MIT](LICENSE).

## Referencias

[1]: https://modrinth.com/project/HVnmMxH1 "Complementary Reimagined — Modrinth"
[2]: https://www.curseforge.com/minecraft/shaders/complementary-reimagined "Complementary Reimagined — CurseForge"
