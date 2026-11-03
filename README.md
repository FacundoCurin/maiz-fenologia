# Hojas y Floración en Maíz

App web para estimar el **número total de hojas** y la **fecha de floración** de un híbrido de maíz, para la campaña en curso, a partir de datos de temperatura y el submodelo fenológico de CERES-Maize (Kiniry).

🌱 **App en vivo:** https://facundocurin.github.io/maiz-fenologia/

## Qué hace

- Toma la temperatura de **NASA POWER** para el punto (lat/lon) que elijas.
- Corre el submodelo de número de hojas de **CERES-Maize (Kiniry)**: tiempo térmico diario, fase juvenil, fase inductiva por fotoperíodo y fijación del número total de hojas en iniciación de panoja. La floración se estima como fin de crecimiento foliar (VT–R1).
- Para la campaña en curso combina:
  - **Datos observados** de este año (los días ya transcurridos).
  - **Estimación del futuro**, por uno de dos métodos:
    - **Pronóstico estacional CFSv2** (Open-Meteo, 50 miembros de ensamble).
    - **Análogo ENSO**: promedio de los años históricos de la fase elegida (Niño / Niña / Neutral), clasificados por el índice ONI NDJ (NOAA CPC, umbral ±0,5 °C).
- Devuelve número de hojas, fecha de floración, días a floración, °Cd y rangos de incertidumbre, con gráficos de: aparición de hojas y etapas, temperatura de la campaña (observado vs estimado), dispersión del ensamble/años análogos, y climatología del sitio.
- Un deslizador de **escenario de calentamiento** (±°C) permite explorar un clima más cálido.

## Cómo funciona por dentro

`index.html` es una app autónoma (HTML + JavaScript, **sin backend ni claves**). Las APIs se consultan directamente desde el navegador (tienen CORS habilitado):

- **NASA POWER** — temperatura y radiación diarias (histórico y observado reciente).
- **Open-Meteo Seasonal Forecast** — pronóstico estacional del modelo NOAA CFSv2.

El índice ONI para la clasificación ENSO está embebido en el código (NOAA no lo sirve en vivo por CORS).

## Actualizar la web

Editá `index.html` y subí los cambios:

```bash
git add index.html && git commit -m "Describí el cambio" && git push
```

GitHub Pages republica solo en ~1 minuto.

## Fuentes

- Jones, C.A. & Kiniry, J.R. (1986). *CERES-Maize: A Simulation Model of Maize Growth and Development.*
- DSSAT-CSM, `Plant/CERES-Maize/MZ_PHENOL.for` (submodelo de número de hojas).
- NASA POWER (https://power.larc.nasa.gov/).
- Open-Meteo Seasonal Forecast (https://open-meteo.com/).
- NOAA CPC — Oceanic Niño Index (ONI).
