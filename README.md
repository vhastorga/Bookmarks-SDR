# 📡 Bookmarks RTL-SDR — AM/FM Buenos Aires (CABA)

Repositorio con los **bookmarks (marcadores) de frecuencias de radios y emisoras argentinas visibles desde la Ciudad Autónoma de Buenos Aires**, listos para usar en **GQRX** y **SDR++**, y perfectamente adaptables a cualquier otro receptor SDR (SDR#, HDSDR, CubicSDR, SDRangel, etc.).

El objetivo del proyecto es **aportar y disponibilizar la radio SDR en esta zona**: un set de frecuencias ordenado, etiquetado y con los modos/anchos de banda correctos, para que cualquiera pueda sintonizar AM, FM, aeronáutica, marítima y radioaficionados de CABA y alrededores sin tener que armar la lista desde cero.

---

## 📑 Índice

- [Sobre el proyecto](#-sobre-el-proyecto)
- [Contenido del repositorio](#-contenido-del-repositorio)
- [Cobertura de frecuencias](#-cobertura-de-frecuencias)
- [Instalación en GQRX](#-instalación-en-gqrx)
- [Instalación en SDR++](#-instalación-en-sdr)
- [Uso en otros programas](#-uso-en-otros-programas)
- [Formato de los datos](#-formato-de-los-datos)
- [Cómo agregar o corregir estaciones](#-cómo-agregar-o-corregir-estaciones)
- [Herramientas y créditos](#-herramientas-y-créditos)
- [Consideraciones legales](#-consideraciones-legales)
- [Contribuir](#-contribuir)
- [Licencia](#-licencia)

---

## 📡 Sobre el proyecto

Este repositorio fue creado a partir de un **barrido/escaneo de frecuencias con [RTLSDR Scanner](https://github.com/eartoearoak/rtlsdr-scanner)** sobre la zona de la Ciudad Autónoma de Buenos Aires y su área metropolitana, y fue organizado, depurado y documentado con la asistencia de **Gemini 3.8 Flash**.

El resultado son **dos archivos equivalentes** —uno por programa— con **79 estaciones**:

| Programa | Formato | Archivo |
|---|---|---|
| **GQRX** | CSV con etiquetas (tags) y colores | [`bookmarks.csv`](./bookmarks.csv) |
| **SDR++** | JSON (plugin *Frequency Manager*) | [`frequency_manager_config.json`](./frequency_manager_config.json) |

Ambos archivos contienen **exactamente las mismas 79 frecuencias** (verificado): AM broadcast, FM stereo/mono, tráfico aeronáutico, canal marítimo y simplex de radioaficionados, todos con su modo de demodulación y ancho de banda recomendados.

---

## 📦 Contenido del repositorio

```
.
├── README.md                        # Documentación (este archivo)
├── bookmarks.csv                    # Marcadores para GQRX (con tags y colores)
└── frequency_manager_config.json    # Marcadores para SDR++ (Frequency Manager)
```

| Archivo | Formato | Cant. de entradas | Destino |
|---|---|---|---|
| `bookmarks.csv` | CSV (`;` como separador) | 79 frecuencias + 15 tags con colores | GQRX |
| `frequency_manager_config.json` | JSON | 79 frecuencias (lista `General`) | SDR++ |

---

## 📶 Cobertura de frecuencias

| Banda | Rango | Cantidad | Modo | Ejemplos |
|---|---|---|---|---|
| **Ondas medias (AM)** | 540 – 1 070 kHz | 9 | AM · 10 kHz | Radio Continental 590, Rivadavia 630, Mitre 790, Nacional 870 |
| **FM broadcast** | 87,5 – 107,9 MHz | 59 | WFM estéreo/mono · 142–160 kHz | Rock&Pop 95.9, La 100 98.7, Metro 95.1, Vorterix 92.1 |
| **Aeronáutica (airband)** | 118,85 – 129,5 MHz | 9 | AM · 25 kHz | Aeroparque TWR 118.85, Ezeiza TWR 119.9, Ezeiza CTR 125.9, Guardia 121.5 |
| **Marítimo** | 156,8 MHz | 1 | NFM · 12,5 kHz | Canal 16 — Prefectura Naval |
| **Radioaficionados** | 146,52 MHz | 1 | NFM · 12,5 kHz | Simplex FM Región 2 (LU) |

**Tags disponibles:** `AM`, `Aeronautica`, `CABA`, `Clasica`, `Comunitaria`, `Cultura`, `Deportes`, `HamRadio`, `La Plata`, `Maritimo`, `Noticias`, `Pop`, `Publica`, `Rock`, `Rock Nacional`.

---

## 🚀 Instalación en GQRX

1. **Localizá la carpeta de configuración de GQRX** (donde se encuentra tu archivo `gqrx.conf`):
   - **Linux / macOS:** `~/.config/gqrx/`
   - **Windows:** `%APPDATA%\gqrx\` o `C:\Users\<tu-usuario>\.config\gqrx\`
2. **Hacé una copia de seguridad** de tu `bookmarks.csv` actual (si existe).
3. **Reemplazá o fusioná** el archivo `bookmarks.csv` de este repositorio con el de esa carpeta.
   > ⚠️ Si ya tenés marcadores propios, **no lo reemplaces a ciegas**: el CSV tiene dos secciones (primero la definición de tags con sus colores, luego las frecuencias). Copiá las filas de frecuencias nuevas debajo de las existentes para conservar tus bookmarks.
4. **Reiniciá GQRX**. Los bookmarks aparecen en el menú **Bookmarks**, agrupados y coloreados según sus tags.

---

## 📻 Instalación en SDR++

1. Abrí SDR++ y asegurate de tener habilitado el plugin **Frequency Manager** (en *Source / Plugins*).
2. **Localizá la carpeta de configuración de SDR++** (donde está tu `frequency_manager_config.json`):
   - **Windows:** junto al ejecutable `sdrpp.exe` (carpeta `config/` o la carpeta base del programa).
   - **Linux:** `~/.config/sdrpp/`
3. **Hacé una copia de seguridad** del `frequency_manager_config.json` existente.
4. **Reemplazá** el archivo por el de este repositorio (o fusioná la lista `"General"` con tus listas existentes).
5. **Reiniciá SDR++** y abrí el panel **Frequency Manager**: vas a ver la lista `General` con las 79 estaciones. Un clic sintoniza la frecuencia y aplica modo y ancho de banda automáticamente.

> **Tip:** la lista queda visible sobre el waterfall (`"showOnWaterfall": true`), lo que permite saltar entre estaciones directamente desde el espectro.

---

## 💻 Uso en otros programas

Los datos son deliberadamente **genéricos y portables**: frecuencia (Hz), nombre, modo y ancho de banda. Para adaptarlos a cualquier otro receptor:

| Programa | Cómo importar |
|---|---|
| **SDR#** | Usá el plugin *Frequency Manager* / *Bookmarks* y cargá frecuencia, ancho de banda y modo desde la tabla de abajo. |
| **HDSDR** | Menú *Options → Bookmark Editor* (formato similar de importación). |
| **CubicSDR / SDRangel** | Importación de listas CSV/JSON; mapear `Modulation` → modo del programa. |
| **SdrPlay / SDRuno, GQRX en otros SO** | Los números son universales: solo hay que respetar modo y ancho de banda. |

### Mapeo de modos

| Etiqueta en CSV | Valor `mode` en JSON (SDR++) | Modo |
|---|---|---|
| `WFM (stereo)` / `WFM (mono)` | `1` | FM ancha (broadcast) |
| `AM` | `2` | AM (ondas medias y aeronáutica) |
| `NFM` | `0` | FM estrecha (marítimo / ham) |

---

## 🧩 Formato de los datos

### `bookmarks.csv` (GQRX)

```csv
# Tag name          ;  color
AM                  ; #c0c0c0
...

# Frequency ; Name         ; Modulation     ;  Bandwidth; Tags
      590000; Radio Continental ; AM        ;      10000; AM,Noticias,CABA
```

- Separador: **punto y coma (`;`)**
- `Frequency`: en **Hz**
- `Bandwidth`: en **Hz**
- `Tags`: lista separada por comas (debe existir en la sección de tags)

### `frequency_manager_config.json` (SDR++)

```json
{
  "lists": {
    "General": {
      "bookmarks": {
        "Radio Continental": {
          "bandwidth": 10000.0,
          "frequency": 590000.0,
          "mode": 2
        }
      },
      "showOnWaterfall": true
    }
  },
  "selectedList": "General"
}
```

---

## 📝 Cómo agregar o corregir estaciones

1. Editá **ambos archivos** para mantener la equivalencia (GQRX y SDR++).
2. Verificá la frecuencia en **Hz** (`kHz × 1 000`, `MHz × 1 000 000`).
3. Respetá el ancho de banda típico de la banda:
   - AM broadcast → `10000`
   - FM broadcast → `160000` (o `142000` si es mono)
   - Aeronáutica → `25000`
   - NFM (marítimo/ham) → `12500`
4. Agregá los tags correspondientes en el CSV si creás una categoría nueva.
5. Abrí un **Pull Request** describiendo la estación (nombre, frecuencia, ubicación de la emisora).

---

## 🔧 Herramientas y créditos

- **[RTLSDR Scanner](https://github.com/eartoearoak/rtlsdr-scanner)** — herramienta utilizada para el descubrimiento y barrido de frecuencias de la zona.
- **Gemini 3.8 Flash** — asistencia en la organización, limpieza, etiquetado y documentación de los datos.
- **[GQRX](https://github.com/gqrx-sdr/gqrx)** y **[SDR++](https://github.com/AlexandreRouma/SDRPlusPlus)** — receptores SDR para los cuales están pensados estos bookmarks.
- Comunidad RTL-SDR argentina: gracias a quienes comparten y validan frecuencias.

---

## 📜 Consideraciones legales

- Este repositorio tiene fines **educativos, de hobby y de investigación** sobre radioaficionado y radiodifusión.
- El uso de receptores SDR y la escucha de emisiones están sujetos a la **normativa vigente** (Enacom / Ley 25.920 y su reglamentación en Argentina). Verificá la legislación aplicable en tu jurisdicción antes de utilizar estos datos.
- Las frecuencias pueden variar: las estaciones cambian de frecuencia, potencia o dejan de emitir. **Los datos se ofrecen "tal cual", sin garantía de exactitud o vigencia.**

---

## 🤝 Contribuir

Las correcciones y altas de estaciones son bienvenidas:

1. Fork del repositorio.
2. Editar `bookmarks.csv` **y** `frequency_manager_config.json`.
3. Abrir un Pull Request con la descripción del cambio.

Si encontrás una frecuencia desactualizada, ¡avisá abriendo un *Issue*!

---

## 📄 Licencia

Se distribuye como **aporte comunitario** para la comunidad SDR argentina. Podés copiarlo, modificarlo y reutilizarlo libremente citando el origen de este repositorio.
