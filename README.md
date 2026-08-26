# LABPBR Texture Generator

> Genera mapas LABPBR o convierte resource packs y JARs a un acabado **Glossy plano**, sin enviar archivos a un servidor.

**[Abrir la versión publicada](https://dubicrack-yt.github.io/labpbr-generator/)**

LABPBR Texture Generator es una herramienta de navegador para creadores de resource packs de Minecraft. Puede trabajar con una textura PNG, JPG o WebP individual, o convertir de forma masiva un resource pack `.zip`, un JAR de mod o un JAR de cliente Minecraft. El procesamiento ocurre en el propio navegador; no necesita API, claves ni backend.

## Qué genera

| Flujo | Salida | Alcance |
| --- | --- | --- |
| **Textura individual** | `<nombre>_n.png` y `<nombre>_s.png` | Una textura PNG, JPG o WebP para edición material puntual. |
| **Resource pack ZIP** | `<pack>_glossy.zip` | Conserva el pack original y añade pares Glossy para PNG de bloques, ítems y entidades. |
| **JAR de mod o Minecraft** | `<archivo>_glossy_overlay.zip` | Crea un resource-pack overlay; el JAR original no se modifica ni se vuelve a firmar. |

| Modo | Mapa `_n` | Mapa `_s` | Caso de uso |
| --- | --- | --- | --- |
| **Glossy plano** | Normal neutra `128,128,255,255`; sin relieve, altura ni parallax. | `255,255,0,255`: suavidad máxima, reflexión basada en albedo, sin porosidad y emisión desactivada. | Reflejo liso uniforme, vidrio pulido o acabado espejo. |
| **PBR normal** | Normal local derivada de la luminancia con profundidad graduable. | Suavidad, F0, porosidad y emisión según el material. | Una primera interpretación PBR de madera, piedra, metal y otros materiales. |

Las familias de material disponibles para el flujo individual son madera, piedra, metal, cristal, vegetal, orgánico, suelo y emisivo. La interfaz permite variar F0, suavidad, profundidad y emisión antes de exportar.

## Conversión de archivos completos

El modo **Archivo completo** procesa exclusivamente rutas que contienen `textures/block`, `textures/blocks`, `textures/item`, `textures/items` o `textures/entity`. Para cada albedo PNG elegible genera los pares `_n` y `_s` en la misma carpeta, conserva los metadatos `.mcmeta` de animación en los mapas derivados y omite mapas LABPBR ya existentes para no mezclar variantes.

> Las rutas de GUI, fuentes, pantallas, mapas y pinturas quedan fuera de la conversión. En ZIP también se preservan junto con sonidos y demás archivos del pack sin modificación.

Los ZIP se reempaquetan manteniendo sus archivos originales y añadiendo únicamente los mapas derivados. Los JAR se exportan como **overlay ZIP** que contiene los assets de textura pertinentes y un `pack.mcmeta`; nunca se entrega un JAR ejecutable modificado. Este diseño evita alterar clases, manifiestos o firmas de un mod o del cliente.

El límite de seguridad local es de **300 MB** por archivo y **20 000** texturas convertibles por ejecución. Si un pack excede alguno de esos límites, conviene dividirlo por mod o namespace y procesar las partes por separado.

## Privacidad y funcionamiento

El procesamiento usa Canvas 2D y compresión ZIP en el propio navegador. La textura, pack o JAR seleccionado no se sube a una API ni se guarda en un servidor. Las descargas se construyen localmente como PNG, ZIP o overlay ZIP.

## Uso rápido

### Para una textura individual

1. Abre la página y suelta una textura en **Entrada**.
2. Elige **Glossy plano** o **PBR normal**, y selecciona la familia de material.
3. Ajusta reflectividad, profundidad o emisión si lo necesitas.
4. Descarga `_n` y `_s`, y colócalos junto al albedo original dentro de la misma ruta del resource pack.

### Para un resource pack, mod o cliente

1. En **Archivo completo**, carga un `.zip` de resource pack o un `.jar` de mod/Minecraft.
2. Presiona **Convertir a Glossy** y espera el contador local de texturas procesadas.
3. Descarga el resultado. Para un ZIP, usa el pack Glossy resultante; para un JAR, instala el `*_glossy_overlay.zip` como resource pack por encima del contenido original.
4. Prueba el resultado con el shader que vayas a utilizar y conserva una copia sin modificar del archivo fuente.

## LABPBR

Los sufijos `_n` y `_s`, así como sus canales, siguen LABPBR 1.3 [1]. En particular, el canal alfa del mapa especular controla emisión: `0` equivale a 0 % de luz emitida y `255` se ignora para desactivar la emisión en materiales no emisivos [1]. Iris reconoce LabPBR como el formato PBR preferido y documenta los sufijos de normal y especular [2].

## Desarrollo local

```bash
pnpm install
pnpm dev
```

La aplicación usa React, TypeScript, Vite y [JSZip](https://github.com/Stuk/jszip) para abrir y reempaquetar archivos en el navegador. El comando `pnpm build` genera el bundle de producción. El script `scripts/export-github-pages.mjs` prepara una versión HTML/CSS/JS estática para GitHub Pages.

## Licencia

Este proyecto se distribuye bajo la [licencia MIT](LICENSE).

## Referencias

[1]: https://shaderlabs.org/wiki/LabPBR_Material_Standard "LabPBR Material Standard — shaderLABS"

[2]: https://shaders.properties/current/how-to/pbr_standards/ "Iris Docs — PBR Standards"
