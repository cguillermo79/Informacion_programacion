# Proyecto integrador FIRELAB_Loja — Programación y Base de Datos

## Propósito

Cada equipo construirá una solución reproducible para leer, validar, transformar, analizar y comunicar información de FIRELAB_Loja. El producto principal no es solo un conjunto de gráficos: debe ser un programa organizado, verificable y capaz de regenerar los resultados a partir del CSV asignado.

El proyecto avanza durante las tres unidades: definición del problema y requisitos, implementación y pruebas preliminares, y entrega final integrada con documentación, resultados y defensa individual.

## Base autorizada y alcance

- Fuente: `dataset_maestro_firelab_loja_2019_2025_v1_1_0.csv`.
- SHA-256 de la fuente: `890423faf91207aa271feb9878b1b379e309c156e8e7128af380a5c1afe674b6`.
- Unidad de observación: una **celda espacial de 500 m en un mes**.
- Periodo: enero de 2019 a diciembre de 2024 (72 meses).
- El año 2025 no está incluido y no deberá obtenerse de otra fuente.
- **Base didáctica reducida:** para que las bases sean manejables en un curso de programación básica (se pueden abrir en VS Code o en una hoja de cálculo y recorrer con un `for`), cada base es una **muestra pequeña** del dataset original:
  - **30 celdas** por zona (norte y sur) y **60 celdas** (las 30 del norte + las 30 del sur) en Loja completo, cada una con sus 72 meses;
  - **solo las columnas del tema** de cada equipo (15 a 22), con sus controles de calidad; se quitaron columnas técnicas de geometría y estadísticas auxiliares (desviación, mínimo, máximo, número de píxeles);
  - valores numéricos **redondeados** (2 decimales si el valor es 10 o mayor; 4 decimales si es menor).
  - Selección aleatoria con semilla fija (2026), por zona: **10 celdas con al menos un incendio** válido y **20 sin incendio**. Las mismas 60 celdas se usan en todas las bases; la lista está en `muestra_celdas_didactica.csv`.
  - Por ser una muestra, **los resultados describen estas celdas y no deben presentarse como cifras oficiales de todo el cantón**.
- El CSV entregado es de solo lectura. El programa generará nuevas salidas sin sobrescribirlo.

## Asignación de equipos

| Equipo | Tema | Zona exclusiva | Registros | Celdas | Columnas | Archivo |
|---:|---|---|---:|---:|---:|---|
| 1 | Relieve y accesibilidad | Norte | 2.160 | 30 | 15 | `equipo_01_relieve_norte/equipo_01_relieve_norte.csv` |
| 2 | Relieve y accesibilidad | Sur | 2.160 | 30 | 15 | `equipo_02_relieve_sur/equipo_02_relieve_sur.csv` |
| 3 | Cobertura vegetal y uso del suelo | Loja completo | 4.320 | 60 | 22 | `equipo_03_cobertura_loja/equipo_03_cobertura_loja.csv` |
| 4 | Clima y condiciones atmosféricas | Norte | 2.160 | 30 | 18 | `equipo_04_clima_norte/equipo_04_clima_norte.csv` |
| 5 | Clima y condiciones atmosféricas | Sur | 2.160 | 30 | 18 | `equipo_05_clima_sur/equipo_05_clima_sur.csv` |
| 6 | Incendios forestales y riesgo | Loja completo | 4.320 | 60 | 15 | `equipo_06_incendios_loja/equipo_06_incendios_loja.csv` |

Todas las bases comparten seis columnas de identificación: `cell_id`, `centro_x_m`, `centro_y_m`, `anio`, `mes` y `anio_mes`. El significado, la unidad y los valores esperados de **cada columna** están en `DICCIONARIO_VARIABLES.csv`.

## Regla territorial para los temas compartidos

Los equipos 1–2 comparten relieve y accesibilidad; los equipos 4–5 comparten clima. En cada pareja, las columnas son las mismas, pero la población territorial es distinta:

- **Norte:** `centro_y_m >= 9555250.0` (30 celdas).
- **Sur:** `centro_y_m < 9555250.0` (30 celdas).
- **Loja completo:** 60 celdas; se asigna a los equipos 3 y 6 en temas diferentes.

La zona ya viene filtrada en el archivo. El programa debe comprobar la regla, pero no volver a dividir ni unir las bases.

> **Compartir tema no significa compartir solución.** Cada equipo implementará su propio código, pruebas, salidas e interpretación con la zona asignada. Se puede conversar sobre conceptos generales, pero no intercambiar archivos procesados, funciones completas, tablas, gráficos ni conclusiones. Una eventual comparación norte–sur será un producto adicional indicado por el docente, no un reemplazo del trabajo independiente.

## Requisitos comunes de la solución

### 1. Entrada y configuración

- Leer la ruta del CSV desde una configuración, argumento o constante claramente ubicada; evitar rutas absolutas personales.
- Validar que estén presentes las columnas requeridas antes de ejecutar el análisis.
- Comprobar cantidad de registros, celdas únicas, periodo y regla territorial.
- Emitir mensajes de error comprensibles cuando falte el archivo o el esquema no sea válido.

### 2. Procesamiento

- Separar el código en funciones con una responsabilidad clara: carga, validación, limpieza, transformación, resumen y visualización/exportación.
- Seleccionar únicamente las columnas necesarias para la pregunta del equipo.
- Convertir tipos de manera explícita y documentar el tratamiento de valores faltantes.
- Aplicar reglas de calidad mediante columnas de cobertura, disponibilidad, soporte u observabilidad; conservar un conteo de registros aceptados y descartados.
- No modificar silenciosamente los valores originales ni usar el año 2025.

### 3. Salidas

- Generar, como mínimo, un archivo tabular procesado o resumido, dos tablas analíticas y tres figuras útiles.
- Guardar las salidas en carpetas separadas (`resultados/tablas` y `resultados/figuras`) con nombres estables.
- Incluir títulos, unidades, periodo y zona en tablas y gráficos.
- Evitar depender de pasos manuales: una ejecución completa debe regenerar las salidas.

### 4. Calidad del software

- Usar nombres descriptivos, funciones documentadas y comentarios solo donde aclaren decisiones.
- Evitar bloques duplicados; reutilizar funciones para operaciones repetidas.
- Incluir al menos cinco verificaciones o pruebas: esquema, tipos/rangos, zona, unicidad de claves y resultado de una transformación.
- Entregar `requirements.txt` o equivalente, instrucciones de instalación y un comando claro de ejecución.
- No incluir entornos virtuales, archivos temporales ni copias innecesarias de la base en la entrega.

## Actividades específicas por equipo

### Equipo 1 — Aplicación de relieve y accesibilidad, zona norte

- Implementar una carga que valide las 30 celdas del norte y la regla `centro_y_m >= 9555250.0`.
- Crear funciones para obtener una fila por `cell_id`, validar cobertura ALOS/GHSL/OSM y resumir elevación, pendiente, vías y asentamientos.
- Programar una clasificación configurable de accesibilidad o dificultad territorial y exportar las celdas por nivel.
- Generar una tabla de resumen, gráficos de distribución/relación y una visualización espacial del norte.
- Probar, al menos, la deduplicación temporal, los límites de clase y el conteo final por categoría.

### Equipo 2 — Aplicación de relieve y accesibilidad, zona sur

- Implementar el flujo exclusivamente para las 30 celdas del sur y validar `centro_y_m < 9555250.0`.
- Crear sus propias funciones de control, resumen y clasificación; el código y los parámetros no deben ser una copia del equipo 1.
- Exportar una clasificación de accesibilidad o dificultad derivada de elevación, pendiente, vías y asentamientos del sur.
- Generar tabla, gráficos y visualización espacial propios de la zona sur.
- Probar deduplicación, regla territorial, límites de clase y total de celdas procesadas.

> Las variables de relieve y accesibilidad son esencialmente estáticas y se repiten en los 72 meses. Los equipos 1 y 2 deben programar una reducción controlada a una fila por `cell_id` para el análisis territorial y verificar que los valores repetidos sean consistentes.

### Equipo 3 — Aplicación de cobertura vegetal y uso del suelo, Loja completo

- Validar las nueve proporciones MAATE, `suma_prop_maate_9v` y la disponibilidad Sentinel-2 (`sentinel_t1_missing`, `s2_cobertura_valida_pct`).
- Implementar funciones para resumir coberturas, calcular la cobertura dominante y producir series de NDVI, NDMI, NBR o NDWI.
- Permitir seleccionar por parámetro el índice, año o mes que se desea consultar.
- Exportar composición territorial, serie temporal, comparación por cobertura y visualización espacial de Loja.
- Probar sumas de proporciones, categorías dominantes, tratamiento de `sentinel_t1_missing` y filtros temporales.

> Las proporciones MAATE son basales; no deben duplicarse al calcular totales mensuales. Los índices Sentinel-2 sí cambian con el tiempo y deben acompañarse de los controles `sentinel_t1_missing` y `s2_cobertura_valida_pct`.

### Equipo 4 — Aplicación climática, zona norte

- Validar la zona norte, el calendario 2019–2024, las columnas CHIRPS/CHELSA requeridas y sus controles de disponibilidad.
- Crear funciones parametrizadas para resumir precipitación, días secos/húmedos y viento por mes y año.
- Implementar una consulta de periodos extremos y una comparación entre `t1`, `prev2m` y `prev3m`.
- Exportar perfiles mensuales, ranking de periodos, relaciones entre variables y distribución espacial del norte.
- Probar meses válidos, historia de tres meses, filtros, unidades y ordenamiento de extremos.

### Equipo 5 — Aplicación climática, zona sur

- Implementar el mismo tipo de producto solo para la zona sur, con arquitectura, funciones y resultados propios.
- Validar `centro_y_m < 9555250.0`, disponibilidad, días válidos e historia completa de CHIRPS.
- Permitir consultar variables, meses y años mediante parámetros; detectar periodos secos, lluviosos o ventosos.
- Exportar perfiles, ranking, gráficos de relación y distribución espacial del sur.
- Probar regla territorial, periodos móviles, filtros y conteos resultantes sin reutilizar salidas del equipo 4.

> Los equipos 4 y 5 no deben sumar entre sí el mes actual y las ventanas previas. Las ventanas móviles se solapan; el programa debe nombrarlas y tratarlas de acuerdo con su definición.

### Equipo 6 — Aplicación de incendios forestales, Loja completo

- Usar `y_incendio_ge7_obs90` como respuesta principal y filtrar registros mediante `y_principal_valida` cuando corresponda.
- Implementar funciones para calcular frecuencias y proporciones por mes, año y celda, además de localizar recurrencia espacial.
- Crear un parámetro para elegir la definición alternativa de incendio (`y_incendio_ge8_obs90`, `y_incendio_ge7_obs80`, `y_incendio_ge7_obs95` o `y_incendio_ge7_obs100`), sin duplicar el código.
- Exportar resumen principal, serie temporal, ranking espacial y tabla comparativa de sensibilidad.
- Probar valores binarios, denominadores, cambio de umbral, exclusión de observaciones inválidas y consistencia de totales.

> Las variables VIIRS de cobertura, disponibilidad y evidencia documentan la procedencia de la respuesta. No deben introducirse automáticamente como predictores del resultado, porque producirían fuga de información.

## Estructura mínima recomendada

```text
equipo_XX/
├── README.md
├── requirements.txt
├── src/
│   ├── main.py
│   ├── carga.py
│   ├── validacion.py
│   └── analisis.py
├── tests/
├── resultados/
│   ├── tablas/
│   └── figuras/
└── informe/
```

El `README.md` del equipo indicará integrantes, pregunta, zona, requisitos, instalación, comando de ejecución, estructura de salidas y decisiones de limpieza.

## Archivos auxiliares

- `DICCIONARIO_VARIABLES.csv`: significado, unidad, tipo y valores esperados de cada columna (punto de partida para la tabla de variables del informe).
- `MANIFIESTO_BASES.csv`: inventario, dimensiones, zona, tamaño y huellas SHA-256.
- `muestra_celdas_didactica.csv`: las 60 celdas de la muestra, su zona y si tuvieron incendio.
- `dataset_maestro_diccionario_grupos_v1_1_0.json`: familias de variables del dataset maestro completo (incluye columnas que no están en las bases reducidas).
- `dataset_maestro_validacion_v1_1_0.json`: validaciones del dataset maestro completo.

## Lista de comprobación final

- [ ] El programa usa únicamente el CSV y la zona asignados.
- [ ] No contiene rutas personales ni sobrescribe la fuente.
- [ ] Valida esquema, periodo, claves, zona y calidad de datos.
- [ ] Las funciones separan carga, transformación, análisis y salida.
- [ ] Una sola ejecución regenera tablas y figuras.
- [ ] Las pruebas cubren las reglas críticas del tema.
- [ ] El README permite instalar y ejecutar el proyecto desde cero.
- [ ] Los resultados y conclusiones pertenecen al equipo, aunque otro grupo comparta el tema.
- [ ] Cada integrante puede explicar y modificar el código durante la defensa.
