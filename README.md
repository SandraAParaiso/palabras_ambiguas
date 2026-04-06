# Experimento de decisión léxica cross-modal

Implementación web del paradigma de **decisión léxica cross-modal con SOA variable**, basado en Swinney (1979). Permite replicar de forma individual, en ordenador, móvil o tablet, el efecto clásico de activación léxica múltiple ante palabras ambiguas en contexto oracional.

---

## Fundamento teórico

El experimento reproduce el diseño de Swinney (1979) *"Lexical Access during Sentence Comprehension: (Re)Consideration of Context Effects"*. La pregunta central es si el contexto oracional previo puede restringir el acceso léxico a un único significado de una palabra ambigua, o si todos los significados se activan momentáneamente con independencia del contexto.

El paradigma enfrenta dos hipótesis:

- **Hipótesis predecisión**: el contexto dirige el acceso léxico y solo se activa el significado relevante.
- **Hipótesis postdecisión** (respaldada por Swinney): el acceso es autónomo y exhaustivo; todos los significados se activan inicialmente y el contexto actúa solo en una fase posterior de selección.

La evidencia a favor de la hipótesis postdecisión proviene del patrón de facilitación cruzada: inmediatamente tras la palabra ambigua (SOA 200 ms), tanto palabras relacionadas con el significado contextual como con el significado alternativo producen tiempos de reacción menores que una palabra no relacionada. A los 700 ms, solo el significado contextualmente apropiado sigue facilitado.

---

## Diseño experimental

### Diseño factorial 2 × 2

| Factor | Niveles |
|---|---|
| **Ambigüedad** | Palabra ambigua (*plantas*) / Palabra control no ambigua (*especies*) |
| **Contexto** | Con contexto sesgado / Sin contexto (oración neutra) |

Esto produce **4 condiciones de oración**, cada una con su propio archivo de audio.

### SOA (Stimulus Onset Asynchrony)

El SOA es el tiempo transcurrido entre el final de la palabra crítica (final del audio de la oración) y la aparición de la palabra diana visual.

| SOA | Equivalencia aproximada | Corresponde a |
|---|---|---|
| **200 ms** | Acceso inmediato | Swinney (1979), Experimento 1 y replicación del Experimento 2 |
| **700 ms** | ~3 sílabas tras la palabra crítica | Swinney (1979), Experimento 2 extensión |

### Palabras diana

Cada ensayo presenta una de las siguientes palabras visuales:

| Palabra | Tipo | Relación |
|---|---|---|
| FLORES | Relacionada | Significado contextual (*plantas* = vegetales) |
| PISOS | Inapropiada | Significado alternativo (*plantas* = pisos de edificio) |
| RUEDAS | No relacionada | Línea base |
| FRULA, TOPAS, BLOME, XARTA, GRUTO, PANSE, TRALB, FOSCI | Pseudopalabras | Relleno, mantienen la tarea de decisión léxica real |

### Ensayos

- **24 ensayos críticos**: 4 condiciones de oración × 2 SOAs × 3 tipos de diana
- **8 ensayos relleno**: pseudopalabras distribuidas entre condiciones y SOAs
- **3 ensayos de práctica** al inicio
- **4 preguntas de comprensión** intercaladas cada ~8 ensayos para verificar atención

---

## Estructura de archivos

```
├── experimento_plantas.html   ← archivo principal del experimento
└── audios/
    ├── ambigua_contexto.mp3        ← oración con contexto sesgado, termina en «plantas»
    ├── ambigua_sin_contexto.mp3    ← oración neutra, termina en «plantas»
    ├── noambigua_contexto.mp3      ← oración con contexto sesgado, termina en «especies»
    ├── noambigua_sin_contexto.mp3  ← oración neutra, termina en «especies»
    └── continuacion.mp3            ← «que hay en ellos» (continuación común a todas)
```

### Requisitos de grabación de los audios

- Los cuatro archivos de oración deben terminar exactamente al final de la palabra crítica (*plantas* / *especies*), sin pausa posterior. El SOA se mide desde ese punto.
- `continuacion.mp3` debe comenzar con entonación de continuación natural, como si fuera la prosecución directa de cualquiera de las cuatro oraciones.
- Misma persona, micrófono y condiciones acústicas para todos los archivos.
- Formato recomendado: MP3, 44.1 kHz, mono o estéreo.

### Textos grabados

| Archivo | Texto |
|---|---|
| `ambigua_contexto.mp3` | *Uno de los problemas de mantenimiento de las grandes oficinas es el de la limpieza, sobre todo si se tiene en cuenta la gran cantidad de ficus, palmeras y otras* **plantas** |
| `ambigua_sin_contexto.mp3` | *El tema del que hablaban tenía que ver con las* **plantas** |
| `noambigua_contexto.mp3` | *Uno de los problemas de mantenimiento de las grandes oficinas es el de la limpieza, sobre todo si se tiene en cuenta la gran cantidad de ficus, palmeras y otras* **especies** |
| `noambigua_sin_contexto.mp3` | *El tema del que hablaban tenía que ver con las* **especies** |
| `continuacion.mp3` | *que hay en ellos* |

---

## Uso

1. Clonar o descargar el repositorio manteniendo la estructura de carpetas.
2. Colocar los archivos de audio en la carpeta `audios/`.
3. Abrir `experimento_plantas.html` desde un servidor local o desde GitHub Pages. **No funciona correctamente abierto como archivo local** (`file://`) en algunos navegadores debido a restricciones de carga de audio — usar un servidor HTTP.

```bash
# Servidor local rápido con Python
python3 -m http.server 8000
# Abrir en navegador: http://localhost:8000/experimento_plantas.html
```

4. La pantalla inicial verifica que los cinco archivos de audio estén disponibles e indica cuáles faltan.

---

## Resultados

Al finalizar los ensayos el experimento muestra automáticamente:

- **Tabla de tiempos de reacción medios** por condición de oración, SOA y tipo de diana, con los valores de referencia de Swinney (1979).
- **Gráfico de barras** comparando los datos del participante con la referencia clásica, separado por SOA, para la condición ambigua con contexto.
- **Interpretación automática** de los patrones observados en los tres bloques relevantes: acceso inmediato (SOA 200 ms), selección postacceso (SOA 700 ms) y comparación con la condición control.
- **Puntuación en preguntas de comprensión** como indicador de atención durante el experimento.

---

## Limitaciones

Este experimento está diseñado como herramienta demostrativa o de prácticas. Presenta **1 repetición por celda experimental**, frente a las 36 repeticiones por condición y 84–144 participantes de Swinney (1979). Los datos individuales son ilustrativos y no permiten inferencias estadísticas. Para uso en investigación sería necesario aumentar el número de ítems por condición, contrabalancear los estímulos entre participantes y recoger datos de múltiples sujetos.

---

## Referencia

Swinney, D. A. (1979). Lexical access during sentence comprehension:(Re) consideration of context effects. Journal of verbal learning and verbal behavior, 18(6), 645-659.
