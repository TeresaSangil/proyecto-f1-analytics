# Proyecto F1 Analytics

Pipeline de extracción, limpieza y consolidación de datos históricos de Fórmula 1 (2012–2024), combinando **scraping web** y **una API pública** de resultados de carrera.

## Estructura del repositorio

```
.
├── f1spiders.py            # Crawler (Scrapy) para extraer resultados por temporada
├── funciones_api.py        # Descarga de datos de pitstops vía API (jolpi.ca / Ergast)
├── merge_data.py           # Combinación de las distintas fuentes en un dataset único
├── merge_limpio.py         # Limpieza y normalización del dataset combinado
├── data/                   # Datos crudos por temporada (2012–2024) + pitstops
│   ├── 2012/ ... 2024/
│   └── pitstops/
└── merged_data/            # Datasets ya combinados y listos para análisis
    ├── f1_clean_dataset.csv
    ├── f1_clean_dataset_metadata.json
    ├── f1_complete_dataset.csv
    └── f1_complete_dataset_metadata.json
```

## Requisitos

```bash
pip install scrapy pandas requests
```

## Flujo de ejecución

1. **Extracción**
   ```bash
   python f1spiders.py       # scraping de resultados por temporada -> data/
   python funciones_api.py   # descarga de pitstops vía API -> data/pitstops/
   ```
2. **Combinación**
   ```bash
   python merge_data.py      # une las fuentes en un dataset completo
   ```
3. **Limpieza**
   ```bash
   python merge_limpio.py    # genera la versión limpia final en merged_data/
   ```

## Datos

- `merged_data/f1_complete_dataset.csv`: dataset combinado sin procesar.
- `merged_data/f1_clean_dataset.csv`: versión limpia, lista para análisis/modelado.
- Cada CSV combinado trae su `*_metadata.json` describiendo las columnas.

## Notas

- El `.gitignore` incluido excluye entornos virtuales, cachés de Python y artefactos de construcción habituales.
