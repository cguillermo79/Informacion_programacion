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
- **Muestra didáctica:** para que las bases sean manejables en un curso introductorio, cada base contiene una **muestra de celdas completas** (con sus 72 meses) del dataset original: **250 celdas** en las zonas norte y sur, y **500 celdas** (las 250 del norte + las 250 del sur) en Loja completo. Se mantienen **todas las columnas y las mismas zonas**; solo se redujo el número de celdas. La selección fue aleatoria con semilla fija (2026), por zona: 50 celdas con al menos un evento de incendio válido y 200 sin evento. Las celdas elegidas están en `muestra_celdas_didactica.csv`. Por ser una muestra, **los resultados describen estas celdas y no deben presentarse como cifras oficiales de todo el cantón**.
- El CSV entregado es de solo lectura. El programa generará nuevas salidas sin sobrescribirlo.

## Asignación de equipos

| Equipo | Tema | Zona exclusiva | Registros | Celdas | Columnas | Archivo |
|---:|---|---|---:|---:|---:|---|
| 1 | Relieve y accesibilidad | Norte | 18.000 | 250 | 66 | `equipo_01_relieve_zona_norte/base_programacion_equipo_01_relieve_zona_norte_2019_2024.csv` |
| 2 | Relieve y accesibilidad | Sur | 18.000 | 250 | 66 | `equipo_02_relieve_zona_sur/base_programacion_equipo_02_relieve_zona_sur_2019_2024.csv` |
| 3 | Cobertura vegetal y uso del suelo | Loja completo | 36.000 | 500 | 53 | `equipo_03_cobertura_loja_completo/base_programacion_equipo_03_cobertura_loja_completo_2019_2024.csv` |
| 4 | Clima y condiciones atmosféricas | Norte | 18.000 | 250 | 57 | `equipo_04_clima_zona_norte/base_programacion_equipo_04_clima_zona_norte_2019_2024.csv` |
| 5 | Clima y condiciones atmosféricas | Sur | 18.000 | 250 | 57 | `equipo_05_clima_zona_sur/base_programacion_equipo_05_clima_zona_sur_2019_2024.csv` |
| 6 | Incendios forestales y riesgo | Loja completo | 36.000 | 500 | 41 | `equipo_06_incendios_loja_completo/base_programacion_equipo_06_incendios_loja_completo_2019_2024.csv` |

## Regla territorial para los temas compartidos

Los equipos 1–2 comparten relieve y accesibilidad; los equipos 4–5 comparten clima. En cada pareja, las columnas son las mismas, pero la población territorial es distinta:

- **Norte:** `centro_y_m >= 9555250.0` (250 celdas).
- **Sur:** `centro_y_m < 9555250.0` (250 celdas).
- **Loja completo:** 500 celdas; se asigna a los equipos 3 y 6 en temas diferentes.

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

- Implementar una carga que valide las 250 celdas del norte y la regla `centro_y_m >= 9555250.0`.
- Crear funciones para obtener una fila por `cell_id`, validar cobertura ALOS/GHSL/OSM y resumir elevación, pendiente, vías y asentamientos.
- Programar una clasificación configurable de accesibilidad o dificultad territorial y exportar las celdas por nivel.
- Generar una tabla de resumen, gráficos de distribución/relación y una visualización espacial del norte.
- Probar, al menos, la deduplicación temporal, los límites de clase y el conteo final por categoría.

### Equipo 2 — Aplicación de relieve y accesibilidad, zona sur

- Implementar el flujo exclusivamente para las 250 celdas del sur y validar `centro_y_m < 9555250.0`.
- Crear sus propias funciones de control, resumen y clasificación; el código y los parámetros no deben ser una copia del equipo 1.
- Exportar una clasificación de accesibilidad o dificultad derivada de elevación, pendiente, vías y asentamientos del sur.
- Generar tabla, gráficos y visualización espacial propios de la zona sur.
- Probar deduplicación, regla territorial, límites de clase y total de celdas procesadas.

> Las variables de relieve y accesibilidad son esencialmente estáticas y se repiten en los 72 meses. Los equipos 1 y 2 deben programar una reducción controlada a una fila por `cell_id` para el análisis territorial y verificar que los valores repetidos sean consistentes.

### Equipo 3 — Aplicación de cobertura vegetal y uso del suelo, Loja completo

- Validar las nueve proporciones MAATE, `suma_prop_maate_9v`, soporte, año CUT y disponibilidad Sentinel-2.
- Implementar funciones para resumir coberturas, calcular la cobertura dominante y producir series de NDVI, NDMI, NBR o NDWI.
- Permitir seleccionar por parámetro el índice, año o mes que se desea consultar.
- Exportar composición territorial, serie temporal, comparación por cobertura y visualización espacial de Loja.
- Probar sumas de proporciones, categorías dominantes, tratamiento de `sentinel_t1_missing` y filtros temporales.

> Las proporciones MAATE son basales; no deben duplicarse al calcular totales mensuales. Los índices Sentinel-2 sí cambian con el tiempo y deben acompañarse de controles de observabilidad, cobertura válida y `lag_meses`.

### Equipo 4 — Aplicación climática, zona norte

- Validar la zona norte, el calendario 2019–2024 y las columnas CHIRPS/CHELSA requeridas.
- Crear funciones parametrizadas para resumir precipitación, días secos/húmedos y viento por mes y año.
- Implementar una consulta de periodos extremos y una comparación entre `t1`, `prev2m` y `prev3m`.
- Exportar perfiles mensuales, ranking de periodos, relaciones entre variables y distribución espacial del norte.
- Probar meses válidos, historia de tres meses, filtros, unidades y ordenamiento de extremos.

### Equipo 5 — Aplicación climática, zona sur

- Implementar el mismo tipo de producto solo para la zona sur, con arquitectura, funciones y resultados propios.
- Validar `centro_y_m < 9555250.0`, disponibilidad, días válidos e historia completa de CHIRPS/CHELSA.
- Permitir consultar variables, meses y años mediante parámetros; detectar periodos secos, lluviosos o ventosos.
- Exportar perfiles, ranking, gráficos de relación y distribución espacial del sur.
- Probar regla territorial, periodos móviles, filtros y conteos resultantes sin reutilizar salidas del equipo 4.

> Los equipos 4 y 5 no deben sumar entre sí el mes actual y las ventanas previas. Las ventanas móviles se solapan; el programa debe nombrarlas y tratarlas de acuerdo con su definición.

### Equipo 6 — Aplicación de incendios forestales, Loja completo

- Usar `y_incendio_ge7_obs90` como respuesta principal y filtrar registros mediante `y_principal_valida` cuando corresponda.
- Implementar funciones para calcular frecuencias y proporciones por mes, año y celda, además de localizar recurrencia espacial.
- Crear un parámetro para elegir umbrales alternativos `ge7`/`ge8` y `obs80`/`obs95`/`obs100`, sin duplicar el código.
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

- `MANIFIESTO_BASES.csv`: inventario, dimensiones, zona y huellas SHA-256.
- `dataset_maestro_diccionario_grupos_v1_1_0.json`: familias de variables y reglas de gobernanza.
- `dataset_maestro_validacion_v1_1_0.json`: validaciones del dataset maestro.

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
