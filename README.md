# Satisfacción con la democracia en Chile, 2006-2026

Proyecto del curso ICP5006 Medición y análisis dimensional de datos políticos (Instituto de Ciencia Política, PUC).

Autores: Lucas Bottinelli, Matías Llorens y Benjamín Zúñiga.

## Pregunta

¿Qué grupos están más y menos satisfechos con el funcionamiento de la democracia en Chile, y cómo cambió eso entre 2006 y 2026?

## Datos

Barómetro de las Américas (LAPOP), Chile: diez olas (2006, 2008, 2010, 2012, 2014, 2017, 2019, 2021, 2023 y 2026). La ola 2026 viene en el archivo regional y se filtra para Chile (`pais == 13`).

La licencia de LAPOP no permite publicar ni redistribuir las bases, por lo que no están en este repositorio. El script `scripts/00_descarga.R` las descarga desde el sitio oficial y las guarda en `data/raw/`. También se pueden bajar a mano desde el [directorio de datos de LAPOP](https://www.vanderbilt.edu/center-for-global-democracy/data/directory/).

These data were supplied by LAPOP Lab at Vanderbilt University, which takes no responsibility for any interpretation of the data.

## Estructura

```
lapop_final/
├── lapop_final.Rproj
├── README.md
├── data/
│   └── raw/            bases de LAPOP (se crean con 00_descarga.R)
├── scripts/
│   ├── 00_descarga.R   descarga las diez olas
│   ├── 01_datos.R      armoniza las variables y crea data/lapop.rds
│   ├── 02_tablas.R     tablas descriptivas
│   ├── 03_graficos.R   figuras
│   └── 04_modelo.R     modelos de regresión logística
└── output/
    ├── tables/
    └── figures/
```

## Cómo reproducir el análisis

1. Abrir `lapop_final.Rproj` en RStudio.
2. Instalar los paquetes, una sola vez:

```r
install.packages(c("haven", "dplyr", "tidyr", "ggplot2", "survey", "patchwork", "modelsummary", "tinytable"))
```

3. Correr los scripts en orden: `00_descarga.R`, `01_datos.R`, `02_tablas.R`, `03_graficos.R` y `04_modelo.R`.

`00_descarga.R` solo es necesario la primera vez.

## Resultados

| Archivo | Contenido |
|---|---|
| `output/tables/t1_olas.rds` | Olas: fechas de campo, gobierno, modo y casos |
| `output/tables/t2_satisfaccion_grupos.rds` | % satisfecho por grupo y ola |
| `output/tables/t3_modelos.html` | Razones de odds de los modelos logísticos |
| `output/figures/f1_tendencia_nacional.png` | Satisfacción nacional, 2006-2026 |
| `output/figures/f2_grupos.png` | Satisfacción por grupo y promedio nacional (también por variable: `f2_*.png`) |
| `output/figures/f2b_grupos.png` | Igual que F2, con intervalos como bandas (también `f2b_*.png`) |
| `output/figures/f2c_grupos_un_panel.png` | Grupos seleccionados y promedio nacional en un solo gráfico |
| `output/figures/f3_mapa_calor.png` | Diferencia de cada grupo con el promedio nacional de su ola |

## Notas

- La variable dependiente es el ítem PN4: "En general, ¿usted diría que está muy satisfecho(a), satisfecho(a), insatisfecho(a) o muy insatisfecho(a) con la forma en que la democracia funciona en Chile?". Se usa como binaria: satisfecho o muy satisfecho frente al resto.
- La ola 2021 fue telefónica, no preguntó voto ni zona, y preguntó ingreso a otra mitad de la muestra. Solo aparece en la serie nacional (F1).
- El voto no se preguntó en 2026.
- Todas las estimaciones usan los pesos y el diseño muestral de cada ola (paquete `survey`).
