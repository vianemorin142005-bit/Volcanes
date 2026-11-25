# Volcanes · Equipo 6 · Grupo 9IDGSB

Proyecto de la Universidad Tecnológica de Coahuila. Datos: catálogo *Volcanoes of the World* del Smithsonian Global Volcanism Program (Global Volcanism Program, 2026).

## Unidad 2 · Preparación de datos
| Archivo | Contenido |
|---|---|
| `GVP_Eruption_List_Holocene_20260424 (1).xlsx`, `GVP_Volcano_List_Holocene_202610152245.xls` | **Datasets originales** (descargas del GVP) |
| `erupciones_plano.csv` | **Dataset limpio** (9,918 erupciones, 33 columnas) |
| `fact_erupcion.csv`, `dim_*.csv` | Modelo dimensional |
| `bitacora_limpieza.csv`, `calidad_por_volcan.csv`, `evidencia_antes_despues.csv` | Documentación de la limpieza y la calidad |

## Unidad 3 · Análisis supervisado
| Archivo | Contenido |
|---|---|
| `U3_Analisis_Supervisado_VEI.ipynb` | **Notebook completo** (código, tablas y gráficas ya ejecutados) |
| `resultados/*.csv`, `resultados/resumen.json` | Tablas de resultados exportadas por el notebook |
| `figuras/*.png` | Gráficas usadas en el documento |

**Problemas:** (1) regresión: estimar el VEI; (2) clasificación binaria: VEI ≥ 3 frente a VEI < 3.
**Entradas:** `latitud`, `longitud`, `elevacion_m`, `anio_inicio`. **Excluidas por fuga:** `vei_modificador`, `categoria_explosividad`, `vei_incierto`.
**Modelos:** línea base, Ridge / regresión logística, Random Forest, Gradient Boosting.
**Optimización:** `GridSearchCV` con validación cruzada de 5 pliegues (solo entrenamiento) y ajuste del umbral con probabilidades fuera de pliegue. La prueba se usa una sola vez.

### Cómo ejecutarlo
```bash
pip install pandas numpy scikit-learn matplotlib jupyter
jupyter notebook U3_Analisis_Supervisado_VEI.ipynb   # ejecutar todas las celdas (≈5 min en un solo núcleo)
```
Semilla fija (`SEED = 42`): los resultados son reproducibles con la misma versión de scikit-learn.

## Unidad 4 · Análisis no supervisado

| Archivo | Contenido |
| --- | --- |
| `U4_Analisis_No_Supervisado_Volcanes.ipynb` | **Notebook completo** (código, tablas y gráficas ya ejecutados) |
| `U4_Analisis_No_Supervisado_Volcanes.py` | Mismo código en formato script |
| `resultados_u4/dataset_transformado_volcanes.csv` | **Dataset transformado** (682 volcanes, una fila por volcán) |
| `resultados_u4/*.csv`, `*.json` | Tablas de resultados (métricas, perfiles, PCA) |
| `figuras_u4/*.png` | Gráficas usadas en el documento |

**Problema:** agrupar volcanes según su comportamiento eruptivo, sin etiquetas.
**Algoritmos:** PCA, K-Means (k=3), Ward, DBSCAN y t-SNE para visualización.
**Métricas:** Silhouette, Calinski-Harabasz, Davies-Bouldin y ARI de estabilidad.

### Cómo ejecutarlo
    pip install pandas numpy scikit-learn matplotlib seaborn jupyter
    jupyter notebook U4_Analisis_No_Supervisado_Volcanes.ipynb

Semilla fija (`SEED = 42`).

## Referencia
Global Volcanism Program. (2026). *Volcanoes of the World* (versión 5.4.0; 7 de agosto de 2026) [Base de datos]. Smithsonian Institution. https://doi.org/10.5479/si.GVP.VOTW5-2026.5.4
