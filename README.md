# LABPBR Glossy Pack Generator

> Convierte texturas, resource packs ZIP y JARs de Minecraft/mods en resource packs Glossy configurables, sin subir los archivos a un servidor.

**[Abrir la versión publicada](https://dubicrack-yt.github.io/labpbr-generator/)**

La aplicación genera un acabado Glossy plano sin relieve heredado. Puede trabajar con lotes de imágenes, resource packs ZIP y JARs de mods o del cliente; todas las salidas son resource packs ZIP listos para colocar en Minecraft.

## Funciones

| Entrada | Operación | Salida |
| --- | --- | --- |
| Texturas PNG, JPG o WebP | Selecciona varias imágenes. | Un resource pack ZIP con todos los pares _n y _s. |
| Resource packs ZIP | Selecciona uno o más archivos. | Un resource pack Glossy por cada ZIP y por cada versión elegida. |
| JARs de mod o Minecraft | Selecciona uno o más archivos. | Un overlay ZIP por JAR y por cada versión elegida; nunca modifica el JAR original. |

En ZIP y JAR se procesan únicamente texturas de bloques, ítems y entidades. Las rutas de GUI, fuentes, pantallas, mapas, pinturas y sonidos se excluyen. Las salidas desde JAR no contienen clases, manifiestos ni firmas.

## Receta Glossy configurable

El preset inicial conserva el Glossy plano validado. Puedes modificar la receta cuando un material necesite menos espejo o una respuesta específica, sin añadir normal con relieve.

| Control | Canal LABPBR | Predeterminado |
| --- | --- | --- |
| Suavidad | R | 255 |
| F0 / reflectancia | G | 255 |
| Porosidad | B | 0 |
| Emisión | Alfa | 0, apagada |
| Normal | RGBA | 128, 128, 255, 255 |

La configuración se refleja en las vistas de Albedo, Normal y Especular, así como en cada ZIP exportado. La receta toma como referencia el estándar LabPBR [1].

## Compatibilidad por versión

Marca una o más versiones: el generador crea un ZIP independiente para cada destino con el pack_format correspondiente. Los valores de metadata proceden de la tabla de formatos de resource packs de Minecraft Java [2].

| Minecraft Java | pack_format |
| --- | --- |
| 1.19.4 | 13 |
| 1.20 – 1.20.1 | 15 |
| 1.20.2 | 18 |
| 1.20.3 – 1.20.4 | 22 |
| 1.20.5 – 1.20.6 | 32 |
| 1.21 – 1.21.1 | 34 |
| 1.21.2 – 1.21.3 | 42 |
| 1.21.4 | 46 |
| 1.21.5 | 55 |
| 1.21.6 | 63 |
| 1.21.7 – 1.21.8 | 64 |

## Comparación antes / después

El banco de inspección incorpora un divisor vertical entre la textura original y su mapa Glossy. Sirve para contrastar el acabado de referencia y ajustar la receta antes de exportar el lote definitivo.

## Shader recomendado

**Complementary Reimagined** es el shader recomendado para inspeccionar reflejos y acabados Glossy. Está disponible en [Modrinth](https://modrinth.com/project/HVnmMxH1) y [CurseForge](https://www.curseforge.com/minecraft/shaders/complementary-reimagined) [3] [4].

## Uso rápido

Primero carga texturas o archivos completos. Después ajusta la receta si lo necesitas, marca las versiones de Minecraft objetivo y genera los packs. Instala cada ZIP resultante como resource pack; para una salida nacida desde JAR, colócala por encima del mod o cliente original.

## Privacidad

Canvas 2D y compresión ZIP se ejecutan localmente en el navegador. Ninguna textura, pack ni JAR se envía a una API o servidor.

## Licencia

Este proyecto se distribuye bajo la [licencia MIT](LICENSE).

## Referencias

[1]: https://shaderlabs.org/wiki/LabPBR_Material_Standard "LabPBR Material Standard"
[2]: https://minecraft.wiki/w/Pack_format "Minecraft Wiki: Pack format"
[3]: https://modrinth.com/project/HVnmMxH1 "Complementary Reimagined en Modrinth"
[4]: https://www.curseforge.com/minecraft/shaders/complementary-reimagined "Complementary Reimagined en CurseForge"
