# Proyecto integrador — Programación y Base de Datos

Este repositorio contiene las bases y orientaciones para desarrollar el proyecto integrador de Programación con información territorial de **FIRELAB_Loja**. Cada grupo construirá una solución reproducible para cargar, validar, transformar, analizar y presentar los datos asignados.

El producto final no consiste únicamente en gráficos o tablas. Debe incluir un programa organizado, documentación, validaciones, pruebas y resultados que puedan regenerarse desde el archivo CSV original.

## Objetivo general

Desarrollar una aplicación o flujo de procesamiento de datos que:

1. lea correctamente la base asignada;
2. compruebe su estructura, periodo y zona;
3. aplique reglas explícitas de limpieza y calidad;
4. responda una pregunta concreta mediante consultas, resúmenes y visualizaciones;
5. exporte resultados sin modificar la fuente; y
6. pueda instalarse y ejecutarse siguiendo las instrucciones del grupo.

## Datos autorizados

- Dataset: FIRELAB_Loja v1.1.0.
- Periodo permitido: enero de 2019 a diciembre de 2024.
- Unidad de observación: una celda espacial de 500 m en un mes.
- **Base didáctica reducida:** para que las bases sean manejables en un curso de programación básica, cada base es una **muestra pequeña** del dataset original: **30 celdas** por zona (norte y sur) y **60 celdas** en Loja completo, cada una con sus 72 meses, y **solo las columnas del tema** del equipo (15 a 22) con valores redondeados. La selección fue aleatoria con semilla fija (2026), por zona: 10 celdas con al menos un incendio válido y 20 sin incendio. Las celdas elegidas están en `01_unidad_1/05_proyecto_integrador/Unidad_1/bases_datos_proyecto_integrador/muestra_celdas_didactica.csv`. Por ser una muestra, **los resultados describen estas celdas y no deben presentarse como cifras oficiales de todo el cantón**.
- Clave esperada de cada observación: `cell_id`, `anio` y `mes`.
- El año 2025 está reservado como conjunto OOT y no debe incorporarse al proyecto.
- El CSV asignado es de **solo lectura**: no se debe editar, renombrar ni sobrescribir.

La descripción técnica completa está en la [guía de las bases](01_unidad_1/05_proyecto_integrador/Unidad_1/bases_datos_proyecto_integrador/README.md). También están disponibles el [diccionario de variables](01_unidad_1/05_proyecto_integrador/Unidad_1/bases_datos_proyecto_integrador/DICCIONARIO_VARIABLES.csv) (qué significa cada columna), el [manifiesto de archivos](01_unidad_1/05_proyecto_integrador/Unidad_1/bases_datos_proyecto_integrador/MANIFIESTO_BASES.csv), el [diccionario de grupos del dataset maestro](01_unidad_1/05_proyecto_integrador/Unidad_1/bases_datos_proyecto_integrador/dataset_maestro_diccionario_grupos_v1_1_0.json) y el [reporte de validación](01_unidad_1/05_proyecto_integrador/Unidad_1/bases_datos_proyecto_integrador/dataset_maestro_validacion_v1_1_0.json).

## Asignación de grupos

| Grupo | Tema | Zona asignada | Registros | Celdas | Base de trabajo |
|---:|---|---|---:|---:|---|
| 1 | Relieve y accesibilidad | Norte | 2.160 | 30 | [Carpeta del grupo 1](01_unidad_1/05_proyecto_integrador/Unidad_1/bases_datos_proyecto_integrador/equipo_01_relieve_norte) |
| 2 | Relieve y accesibilidad | Sur | 2.160 | 30 | [Carpeta del grupo 2](01_unidad_1/05_proyecto_integrador/Unidad_1/bases_datos_proyecto_integrador/equipo_02_relieve_sur) |
| 3 | Cobertura vegetal y uso del suelo | Loja completo | 4.320 | 60 | [Carpeta del grupo 3](01_unidad_1/05_proyecto_integrador/Unidad_1/bases_datos_proyecto_integrador/equipo_03_cobertura_loja) |
| 4 | Clima y condiciones atmosféricas | Norte | 2.160 | 30 | [Carpeta del grupo 4](01_unidad_1/05_proyecto_integrador/Unidad_1/bases_datos_proyecto_integrador/equipo_04_clima_norte) |
| 5 | Clima y condiciones atmosféricas | Sur | 2.160 | 30 | [Carpeta del grupo 5](01_unidad_1/05_proyecto_integrador/Unidad_1/bases_datos_proyecto_integrador/equipo_05_clima_sur) |
| 6 | Incendios forestales y riesgo | Loja completo | 4.320 | 60 | [Carpeta del grupo 6](01_unidad_1/05_proyecto_integrador/Unidad_1/bases_datos_proyecto_integrador/equipo_06_incendios_loja) |

## Regla para los grupos que comparten tema

Los grupos 1 y 2 comparten el tema **Relieve y accesibilidad**, mientras que los grupos 4 y 5 comparten **Clima y condiciones atmosféricas**. Sin embargo, sus territorios son distintos:

- Zona norte: `centro_y_m >= 9555250.0`.
- Zona sur: `centro_y_m < 9555250.0`.

Las bases ya están separadas; no deben volver a dividirse ni unirse.

> **Compartir tema no significa compartir proyecto.** Cada grupo debe trabajar exclusivamente con su zona, formular su propia pregunta, escribir su código, producir sus resultados y redactar sus conclusiones. No se permite intercambiar bases procesadas, funciones completas, tablas, gráficos ni conclusiones. Una comparación norte–sur solo se realizará si el docente la solicita como actividad adicional.

## Trabajo común para todos los grupos

### 1. Planteamiento

Cada grupo deberá:

- formular una pregunta que pueda responderse con su tema y zona;
- definir el usuario o propósito de la solución;
- establecer entradas, procesos y salidas;
- seleccionar las variables necesarias y explicar su significado;
- definir al menos tres consultas o resultados que producirá el programa; y
- especificar las reglas de calidad que aplicará antes del análisis.

### 2. Carga y validación

El programa deberá comprobar automáticamente:

- existencia y lectura del archivo;
- presencia de las columnas requeridas;
- tipos de datos esperados;
- periodo 2019–2024 y meses del 1 al 12;
- cantidad de registros y celdas únicas;
- unicidad de `cell_id`–`anio`–`mes`;
- cumplimiento de la zona asignada; y
- valores faltantes, rangos imposibles y campos de control de calidad.

Cuando una validación crítica falle, el programa debe detenerse con un mensaje comprensible. Las exclusiones no críticas deben contarse y registrarse.

### 3. Procesamiento

- Separar la carga, validación, transformación, análisis y exportación en funciones o módulos.
- Convertir tipos de datos de manera explícita.
- Conservar un registro de filas iniciales, aceptadas, descartadas y motivo de exclusión.
- Evitar código duplicado y valores “mágicos”; los umbrales deben definirse como parámetros o constantes documentadas.
- No alterar silenciosamente datos faltantes ni sustituirlos sin justificación.
- Diferenciar las variables analíticas de los campos de cobertura, disponibilidad, soporte, observabilidad y validez.

### 4. Resultados mínimos

Cada solución generará automáticamente:

- un resumen de calidad de la base;
- al menos dos tablas analíticas exportadas en CSV;
- al menos tres figuras con título, unidades, periodo y zona;
- una salida principal relacionada con la pregunta del grupo; y
- un registro breve de ejecución o reporte final.

Los archivos se guardarán en `resultados/tablas` y `resultados/figuras`. Una ejecución nueva debe regenerarlos sin pasos manuales.

### 5. Pruebas y documentación

- Incluir al menos cinco pruebas o verificaciones reproducibles.
- Probar la regla territorial, el esquema, las claves, los filtros de calidad y un cálculo principal.
- Entregar `requirements.txt` o equivalente.
- Escribir instrucciones de instalación y ejecución desde cero.
- Documentar funciones, parámetros, archivos generados y limitaciones.
- No subir `.venv`, cachés, archivos temporales o copias innecesarias de los CSV.

## Actividades específicas por grupo

### Grupo 1 — Relieve y accesibilidad de la zona norte

El grupo desarrollará una aplicación para caracterizar la accesibilidad y dificultad territorial del norte de Loja.

Debe:

- validar que las 30 celdas cumplan `centro_y_m >= 9555250.0`;
- reducir de manera controlada las variables estáticas a una fila por `cell_id`;
- comprobar la consistencia de elevación, pendiente, orientación, vías y asentamientos entre meses;
- crear funciones para resumir elevación, pendiente, distancia a vías y distancia a asentamientos;
- implementar una clasificación configurable de accesibilidad o dificultad;
- permitir consultar una celda o un nivel de clasificación; y
- exportar el inventario clasificado, una tabla resumen y una visualización espacial del norte.

Las pruebas deben cubrir la deduplicación temporal, la regla norte, los límites de clase y el total final de celdas.

### Grupo 2 — Relieve y accesibilidad de la zona sur

El grupo desarrollará su propia solución para las 30 celdas del sur de Loja.

Debe:

- validar `centro_y_m < 9555250.0`;
- obtener una fila consistente por `cell_id` para las variables estáticas;
- analizar elevación, pendiente, vías y asentamientos exclusivamente del sur;
- diseñar una clasificación propia de accesibilidad o dificultad, con parámetros justificados;
- implementar consultas por celda y categoría; y
- exportar resultados, gráficos y representación espacial correspondientes al sur.

El código, los puntos de corte y las conclusiones no deben copiarse del grupo 1. Las pruebas verificarán zona, deduplicación, clasificación y conteos finales.

### Grupo 3 — Cobertura vegetal y uso del suelo de Loja

El grupo construirá una aplicación para consultar la composición de coberturas y la evolución de índices Sentinel-2 en todo el cantón.

Debe:

- validar las nueve proporciones MAATE y `suma_prop_maate_9v`;
- revisar la disponibilidad y los faltantes de Sentinel-2 (`sentinel_t1_missing`, `s2_cobertura_valida_pct`);
- calcular la cobertura dominante por celda sin duplicar las proporciones basales en cada mes;
- crear series temporales parametrizadas de NDVI, NDMI, NBR o NDWI;
- permitir filtrar por índice, año, mes o cobertura dominante;
- comparar al menos dos tipos de cobertura o periodos; y
- exportar composición territorial, series, tablas comparativas y visualización espacial.

Las pruebas cubrirán suma de proporciones, cobertura dominante, filtros temporales y tratamiento de `sentinel_t1_missing`.

### Grupo 4 — Clima de la zona norte

El grupo desarrollará una aplicación para consultar precipitación, sequedad y viento en la zona norte.

Debe:

- validar las 30 celdas y la regla territorial norte;
- comprobar disponibilidad, días válidos e historia completa de CHIRPS, y disponibilidad de CHELSA;
- resumir precipitación, días secos, días húmedos y viento por mes y año;
- permitir seleccionar variable, año y mes mediante parámetros;
- comparar correctamente el mes actual (`t1`) con los antecedentes `prev2m` y `prev3m`;
- identificar y ordenar periodos lluviosos, secos o ventosos; y
- exportar perfiles mensuales, ranking de extremos, gráficos de relación y distribución espacial norte.

Las ventanas móviles se solapan y no deben sumarse. Las pruebas cubrirán calendario, historia completa, filtros, unidades y ordenamiento de extremos.

### Grupo 5 — Clima de la zona sur

El grupo implementará una solución independiente para analizar las condiciones atmosféricas del sur.

Debe:

- validar las 30 celdas y `centro_y_m < 9555250.0`;
- revisar calidad y disponibilidad de CHIRPS/CHELSA;
- crear funciones propias para resumir precipitación, sequedad y viento;
- implementar consultas configurables por variable y periodo;
- distinguir `t1`, `prev2m` y `prev3m` sin duplicar o sumar ventanas solapadas;
- detectar periodos extremos según parámetros derivados de la zona sur; y
- exportar tablas, rankings, figuras y distribución espacial del sur.

No debe reutilizar código ni resultados del grupo 4. Las pruebas cubrirán regla sur, periodos móviles, filtros de calidad y conteos resultantes.

### Grupo 6 — Incendios forestales y riesgo en Loja

El grupo construirá una aplicación para describir la frecuencia y recurrencia espacial y temporal de incendios.

Debe:

- usar `y_incendio_ge7_obs90` como respuesta principal;
- aplicar `y_principal_valida` y documentar las observaciones excluidas;
- calcular frecuencias y proporciones por mes, año y celda usando denominadores correctos;
- identificar celdas y periodos con mayor recurrencia;
- permitir seleccionar mediante un parámetro la definición alternativa de incendio (`ge8_obs90`, `ge7_obs80`, `ge7_obs95` o `ge7_obs100`);
- comparar la estabilidad de los resultados entre definiciones; y
- exportar tabla principal, serie temporal, ranking espacial, visualización territorial y tabla de sensibilidad.

Las variables VIIRS de cobertura, disponibilidad y evidencia son campos de trazabilidad; no deben utilizarse automáticamente para predecir el resultado del que proceden. Las pruebas cubrirán valores binarios, validez, denominadores, umbrales y consistencia de totales.

## Desarrollo por unidades

| Unidad | Resultado esperado |
|---|---|
| **Unidad 1 — Formulación** | Problema, pregunta de investigación, hipótesis, objetivo general y máximo tres objetivos específicos; variables y exploración preliminar de los datos. Informe de la Parte 1. |
| **Unidad 2 — Metodología** | Proceso metodológico por objetivo (entradas, procedimiento, reglas, verificación, salida) e implementación parcial. **Informe unificado Unidad 1 + 2.** |
| **Unidad 3 — Resultados y conclusiones** | Resultados por objetivo, pruebas, contraste de hipótesis, discusión y conclusiones. **Informe final unificado Unidad 1 + 2 + 3** y defensa individual. |

Cada unidad debe incorporar la retroalimentación recibida. El producto final integra y corrige los avances anteriores; no empieza nuevamente desde cero.

**Guía completa del proyecto (equipos, fases, fechas, estructura de informes):** [GUIA_PROYECTO_INTEGRADOR.md](01_unidad_1/05_proyecto_integrador/Unidad_1/05_Guia_de_presentacion/GUIA_PROYECTO_INTEGRADOR.md).

## Contenido por unidad

| Carpeta | Qué encontrará |
|---|---|
| `01_unidad_1/00_guia_instalacion` | Guía de instalación del entorno (VS Code y Python). |
| `01_unidad_1/01_guias` | Cuaderno y guía práctica de clase de la unidad. |
| `01_unidad_1/02_micro_retos` | 4 micro-retos (MR1–MR4), escala 0–3, 5 %. |
| `01_unidad_1/03_trabajo_tecnico` | 3 trabajos técnicos (TT1–TT3), escala 0–3, 5 %. |
| `01_unidad_1/04_sustentacion_validacion` | Cómo prepararse para las 2 sustentaciones/validaciones, 5 %. |
| `01_unidad_1/05_proyecto_integrador/Unidad_1` | Guía maestra del proyecto (`05_Guia_de_presentacion`), plantilla LaTeX del informe (`06_plantilla_latex`) y **bases de datos de los equipos** (`bases_datos_proyecto_integrador`). |
| `01_unidad_1/06_guia_github_git_vscode` | Guía paso a paso para descargar este repositorio con Git, crear el entorno virtual y trabajar en Visual Studio Code. |
| `02_unidad_2/05_proyecto_integrador` | Guía de la Parte 2 (metodología). |
| `03_unidad_3/05_proyecto_integrador` | Guía de la Parte 3 (resultados y conclusiones). |

Las lecciones y los exámenes no se publican en este repositorio.

## Estructura recomendada de la entrega

```text
equipo_XX/
├── README.md
├── requirements.txt
├── src/
│   ├── main.py
│   ├── carga.py
│   ├── validacion.py
│   ├── transformacion.py
│   └── analisis.py
├── tests/
├── resultados/
│   ├── tablas/
│   └── figuras/
└── informe/
```

El `README.md` de cada grupo incluirá integrantes, pregunta, zona, variables, requisitos, instalación, comando de ejecución, salidas generadas, pruebas y limitaciones.

Ejemplo de ejecución esperada:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
python src\main.py --input "ruta\a\la_base.csv" --output "resultados"
```

El comando definitivo podrá variar, pero deberá funcionar de acuerdo con la documentación entregada y no contener rutas personales fijas.

## Criterios de revisión

Se comprobará que:

- el programa utilice únicamente la base y zona asignadas;
- el CSV original permanezca intacto;
- las validaciones se ejecuten antes del análisis;
- el código sea modular, legible y sin duplicación innecesaria;
- las decisiones de limpieza y los umbrales estén documentados;
- las tablas y gráficos se generen automáticamente;
- las pruebas cubran las reglas críticas del tema;
- las conclusiones correspondan a los resultados obtenidos; y
- cada integrante pueda explicar y modificar el código durante la defensa.

## Lista de comprobación final

- [ ] La pregunta corresponde al tema y a la zona asignada.
- [ ] Solo se utilizaron registros de 2019–2024.
- [ ] La fuente no fue modificada ni sobrescrita.
- [ ] El programa valida esquema, claves, periodo, zona y calidad.
- [ ] Las transformaciones están implementadas en funciones documentadas.
- [ ] Las tablas y figuras se regeneran con una sola ejecución.
- [ ] Existen al menos cinco pruebas reproducibles.
- [ ] El repositorio no contiene entornos virtuales ni archivos temporales.
- [ ] El README permite instalar y ejecutar la solución desde cero.
- [ ] Los resultados son propios del grupo, aunque otro equipo comparta el tema.
- [ ] Todos los integrantes están preparados para la defensa individual.
