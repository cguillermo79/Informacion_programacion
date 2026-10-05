# Guía del proyecto integrador — Programación y Base de Datos

**Carrera de Ingeniería Ambiental · Universidad Nacional de Loja · Ciclo septiembre 2026 – febrero 2027**
**Docente:** Carlos Guillermo Chuncho Morocho
**Peso:** 25 % de la nota de cada unidad (2,50 de 10,00), en las tres unidades.

> Esta es la guía **maestra** del proyecto: describe qué deben hacer en las tres unidades. En cada unidad encontrará también una guía breve con el detalle de esa parte:
> [Unidad 2](../../02_unidad_2/05_proyecto_integrador/README.md) · [Unidad 3](../../03_unidad_3/05_proyecto_integrador/README.md).

---

## 1. ¿De qué se trata?

Durante todo el semestre, cada equipo trabaja con un conjunto **real** de datos ambientales georreferenciados del cantón Loja (periodo **2019–2024**) del proyecto **FIRELAB-Loja**: relieve, cobertura vegetal, clima e incendios forestales.

El proyecto es **una sola investigación** que se construye en tres partes, una por unidad:

| Unidad | Parte del proyecto | Pregunta que responde | Producto final de la unidad |
|:---:|---|---|---|
| **1** | **Formulación** | ¿Qué problema vamos a resolver y qué queremos lograr? | Informe de la Parte 1: **problema, pregunta de investigación, hipótesis, objetivo general y máximo tres objetivos específicos**. |
| **2** | **Metodología** | ¿Cómo lo vamos a hacer, objetivo por objetivo? | Informe **unificado Unidad 1 + Unidad 2**: la formulación (corregida) y la metodología por objetivo. |
| **3** | **Resultados y conclusiones** | ¿Qué encontramos y qué concluimos? | Informe **final unificado Unidad 1 + 2 + 3**, con resultados, discusión y conclusiones. |

**Cada parte retoma y corrige la anterior; nunca se empieza desde cero.** El informe de la Unidad 3 contiene los de las Unidades 1 y 2, ya mejorados con la retroalimentación recibida.

Además de la investigación, el proyecto tiene un producto técnico en Python: un programa (o flujo de procesamiento) que lee, valida, transforma, analiza y presenta los datos del equipo. Su desarrollo avanza en paralelo con el curso: en la Unidad 1 se diseña, en la Unidad 2 se implementa y en la Unidad 3 se integra y se prueba.

---

## 2. Formación de los equipos

Los equipos se forman según la **diapositiva 7** de la presentación de la Unidad 1:

- **25 estudiantes** se organizan en **6 equipos de 4 integrantes (uno de 5)**.
- Cada equipo es responsable de un **bloque temático** del dataset.
- Hay más equipos que bloques temáticos: en dos de los cuatro bloques, **dos equipos comparten el tema** (mismas variables y mismo reto), pero cada uno trabaja una **zona distinta** del cantón (norte o sur).

### 2.1 Integrantes de cada equipo

Los equipos quedaron conformados según los grupos que el curso entregó; el **equipo 6** es el de cinco integrantes. Cada estudiante pertenece **a un solo equipo** durante las tres unidades. El equipo 6 es el de cinco integrantes.

| Equipo | Integrantes |
|:--:|-----------------------------------------------------------------------------|
| **1** | Gilmar Ivan Campoverde Sarango · Kevin Josue Jimenez Macau · Carlos Daniel Cajamarca Gordillo · Nelson Sebastian Pullaguari Cuenca |
| **2** | Isidro Francisco Chamba Mendoza · John David Jimenez Troya · Andy Alcides Aguilar Arteaga |
| **3** | Dulce Isabel Barreto Zapata · Mayerly Stefanny Moreno Vera · Jhanine Fernanda Toledo Merino |
| **4** | Barbara Salome Saritama Maldonado · Yulian Jeraldine Guaman Aguirre · Kristel Pauleth Cevallos Azanza · Ana Gabriela Medina Yaguana |
| **5** | Jamileth Stefania Galvez Cornejo · Yurixi Maribel Riofrio Medina · Ibelia Araceli Japon Caillagua · Shislayne Azucena Chalan Jumbo |
| **6** | Carlos Daniel Gonzalez Castillo · Sonia Noemi Rodriguez Jaramillo · Yanira Maily Rojas Vega |

> Los nombres corresponden a la lista oficial del curso. Las personas que mencionaron su grupo pero aún no constan en esa lista se agregarán cuando se confirme su registro. Todo cambio de integrantes debe ser autorizado por el docente.

### 2.2 Qué zona y qué variables trabaja cada equipo

- **Equipo 1:** trabaja la **zona norte** de Loja con las variables de **relieve y accesibilidad**: elevación, pendiente, orientación (northness y eastness), distancia a asentamientos y distancia a vías. Su base tiene 250 celdas.
- **Equipo 2:** trabaja la **zona sur** de Loja con las variables de **relieve y accesibilidad**: elevación, pendiente, orientación (northness y eastness), distancia a asentamientos y distancia a vías. Su base tiene 250 celdas.
- **Equipo 3:** trabaja **todo el cantón Loja** con las variables de **cobertura vegetal y uso del suelo**: proporciones de cobertura (bosque nativo, páramo, área agropecuaria, plantación forestal, etc.) e índices Sentinel-2 (NDVI, NDMI, NBR, NDWI). Su base tiene 500 celdas.
- **Equipo 4:** trabaja la **zona norte** de Loja con las variables de **clima y condiciones atmosféricas**: precipitación acumulada, días secos y húmedos, y velocidad del viento. Su base tiene 250 celdas.
- **Equipo 5:** trabaja la **zona sur** de Loja con las variables de **clima y condiciones atmosféricas**: precipitación acumulada, días secos y húmedos, y velocidad del viento. Su base tiene 250 celdas.
- **Equipo 6:** trabaja **todo el cantón Loja** con las variables de **incendios forestales y riesgo**: evidencia satelital de fuego y ocurrencia de incendios por celda, mes y año (`y_incendio_ge7_obs90` como respuesta principal). Su base tiene 500 celdas.

**Cómo se define la zona** (con la coordenada `centro_y_m` de cada celda):

- **Norte:** `centro_y_m >= 9555250.0`
- **Sur:** `centro_y_m < 9555250.0`
- **Loja completo:** todas las celdas del cantón.

Los equipos 1–2 y 4–5 trabajan con **las mismas variables**, pero cada uno en **su zona**. Las bases ya vienen separadas por zona: no deben volver a dividirse ni unirse; el programa solo debe **comprobar** que se cumple la regla.

### 2.3 Dónde está la base de datos de su equipo

Todas las bases están en el repositorio de GitHub del curso (<https://github.com/cguillermo79/Informacion_programacion>), dentro de la carpeta `bases_datos_proyecto_integrador`. Cómo descargarlo se explica en la guía de `01_unidad_1/06_guia_github_git_vscode`.

Cada equipo usa **únicamente su carpeta y su archivo**:

**Equipo 1**

```text
Carpeta: bases_datos_proyecto_integrador/equipo_01_relieve_zona_norte
Archivo: base_programacion_equipo_01_relieve_zona_norte_2019_2024.csv
```

**Equipo 2**

```text
Carpeta: bases_datos_proyecto_integrador/equipo_02_relieve_zona_sur
Archivo: base_programacion_equipo_02_relieve_zona_sur_2019_2024.csv
```

**Equipo 3**

```text
Carpeta: bases_datos_proyecto_integrador/equipo_03_cobertura_loja_completo
Archivo: base_programacion_equipo_03_cobertura_loja_completo_2019_2024.csv
```

**Equipo 4**

```text
Carpeta: bases_datos_proyecto_integrador/equipo_04_clima_zona_norte
Archivo: base_programacion_equipo_04_clima_zona_norte_2019_2024.csv
```

**Equipo 5**

```text
Carpeta: bases_datos_proyecto_integrador/equipo_05_clima_zona_sur
Archivo: base_programacion_equipo_05_clima_zona_sur_2019_2024.csv
```

**Equipo 6**

```text
Carpeta: bases_datos_proyecto_integrador/equipo_06_incendios_loja_completo
Archivo: base_programacion_equipo_06_incendios_loja_completo_2019_2024.csv
```

En la misma carpeta `bases_datos_proyecto_integrador` están el `README.md` de las bases, el manifiesto (`MANIFIESTO_BASES.csv`), el diccionario de variables (`dataset_maestro_diccionario_grupos_v1_1_0.json`) y el reporte de validación (`dataset_maestro_validacion_v1_1_0.json`).

> **Importante:** trabaje solo con **su** archivo. El CSV es de **solo lectura** (no se edita, renombra ni sobrescribe) y solo contiene registros de **2019 a 2024**.

### 2.4 Reglas para formar y mantener el equipo

1. Cada estudiante pertenece a **un solo equipo** durante las tres unidades.
2. Cada equipo designa, **por unidad y rotando**, un **coordinador** (organiza el trabajo y las entregas) y un **responsable de calidad** (revisa que el código corra y que el informe cumpla la lista de comprobación). Todos escriben código y todos redactan.
3. La nota de las fases 1 a 3 es **grupal**; la **defensa individual (fase 4) es personal**: depende del dominio que demuestre cada estudiante, aunque el proyecto sea grupal.
4. **Compartir tema no significa compartir proyecto.** Los equipos 1–2 y 4–5 trabajan sobre las mismas variables, pero con zonas distintas. Cada equipo formula su propia pregunta, escribe su propio código y redacta sus propias conclusiones. **No se permite intercambiar** bases procesadas, funciones completas, tablas, gráficos ni conclusiones. Una comparación norte–sur solo se hará si el docente la pide como actividad adicional.
5. Todo cambio de integrantes debe ser autorizado por el docente antes de la fase 1.

---

## 3. Estructura de evaluación (se repite en cada unidad)

Dentro de **cada unidad** el proyecto se evalúa en las mismas cuatro fases (escala 0–10 por fase):

| Fase | Peso sobre la unidad | Qué se evalúa | ¿Individual o grupal? |
|:---:|:---:|---|:---:|
| **1. Formulación** | 3 % | Primer planteamiento de la parte de la unidad (ver sección 4). | Grupal |
| **2. Avance** | 4 % | Evidencia de desarrollo posterior a la formulación y atención a la retroalimentación. | Grupal |
| **3. Producto técnico** | 10 % | Documento formal en **LaTeX con normas APA 7** (más el código cuando corresponda). | Grupal |
| **4. Defensa individual** | 8 % | Explicación personal del trabajo, decisiones, resultados y respuestas a preguntas o modificaciones en vivo. | **Individual** |
| **Total** | **25 %** | **2,50 puntos sobre 10,00 en cada unidad.** | |

Interpretación de la escala del proyecto: **0** = sin evidencia · **1–4,9** = insuficiente · **5,0–6,9** = parcial · **7,0–8,9** = adecuado · **9,0–10** = sólido y plenamente sustentado.

> Celda vacía = pendiente; **0 = no presentó evidencia válida**. Nota mínima de aprobación de la unidad: 7/10.

### 3.1 Calendario de entregas (estimado)

Fechas estimadas según el calendario institucional; se confirman en el EVA/SIAAF.

| Fase | Unidad 1 | Unidad 2 | Unidad 3 |
|---|:---:|:---:|:---:|
| 1. Formulación (3 %) | **07-oct** | 17-nov | 12-ene |
| 2. Avance (4 %) | **14-oct** | 24-nov | 19-ene |
| 3. Producto técnico (10 %) | **21-oct** | 01-dic | 26-ene |
| 4. Defensa individual (8 %) | **28-oct** | 08-dic | 02-feb |

---

## 4. PARTE 1 · Unidad 1 — Formulación de la investigación

**Objetivo de la parte:** que el equipo delimite un problema ambiental **resoluble con sus datos y con un programa**, y lo formule con rigor: problema, pregunta, hipótesis, objetivo general y **máximo tres objetivos específicos**.

### 4.1 Qué debe contener el informe de la Parte 1

| # | Sección | Qué debe decir | Extensión orientativa |
|:---:|---|---|---|
| 1 | **Portada y resumen** | Título, equipo, integrantes, tema y zona; resumen de 120–150 palabras. | 1 pág. |
| 2 | **Introducción y contexto** | Dato territorial (Loja), qué es FIRELAB-Loja, por qué importa el tema del equipo. Con citas APA. | 1 pág. |
| 3 | **Planteamiento del problema** | Situación que se quiere resolver, por qué es relevante y qué información falta o es difícil de obtener. Debe poder resolverse con los **datos asignados** y con un **programa**. | 1 pág. |
| 4 | **Pregunta de investigación** | **Una** pregunta, clara, concreta y respondible con la base del equipo. | 2–3 líneas |
| 5 | **Hipótesis** | Una afirmación **contrastable** que anticipa la respuesta (sección 4.3). | 3–5 líneas |
| 6 | **Objetivo general** | **Uno**, que responda la pregunta (sección 4.4). | 1–2 líneas |
| 7 | **Objetivos específicos** | **Máximo tres**, medibles, que en conjunto cumplen el general. | 3 viñetas |
| 8 | **Datos y variables** | Base asignada, periodo (2019–2024), zona y unidad de observación; tabla de variables que se usarán (nombre, significado, unidad, tipo). | 1 pág. |
| 9 | **Alcance y limitaciones** | Qué incluye y qué no (por ejemplo, el año 2025 no se usa). | ½ pág. |
| 10 | **Matriz de coherencia** | Tabla que une problema → pregunta → hipótesis → objetivos (sección 4.6). | 1 pág. |
| 11 | **Referencias** | Formato APA 7. | — |

### 4.2 El problema y la pregunta de investigación

**Cómo construir el problema (en tres pasos):**

1. **Situación:** ¿qué ocurre en el territorio relacionado con su tema y su zona?
2. **Vacío o dificultad:** ¿qué no se sabe, no se mide o es costoso de calcular a mano?
3. **Oportunidad:** ¿cómo ayuda un programa que procese los datos de FIRELAB-Loja?

**Una buena pregunta de investigación:**

- Es **una sola pregunta**, no una lista.
- Menciona **qué** se analiza, **dónde** (zona) y **cuándo** (2019–2024).
- Se puede responder con **cálculos sobre su base** (no con opiniones).
- No se responde con «sí» o «no» sin más, ni es tan amplia que no se pueda cerrar en un semestre.

| Pregunta débil | Pregunta mejorada (ejemplo con un tema ajeno al curso) |
|---|---|
| «¿Cómo está la calidad del agua?» | «¿En qué proporción de las mediciones mensuales de turbidez de la estación A, entre 2019 y 2024, se superó el límite normativo, y en qué meses se concentran los excedentes?» |
| «¿Sirve el programa?» | «¿Qué reglas de validación detectan el mayor número de registros inconsistentes en la base de la estación A?» |

> **No copie estos ejemplos.** Su pregunta debe salir de **su** bloque temático y **su** zona. Las «preguntas guía» de la diapositiva 9 son un punto de partida, no la pregunta final.

**Orientación por bloque temático (punto de partida):**

| Equipos | Bloque | Pregunta guía de la diapositiva 9 (en clave de programación) |
|:---:|---|---|
| 1 y 2 | Relieve y accesibilidad: elevación, pendiente, orientación, distancia a asentamientos y vías | ¿Qué algoritmo clasifica automáticamente el grado de pendiente de cada celda del relieve? |
| 3 | Cobertura vegetal y uso del suelo: bosque nativo, páramo, área agropecuaria, plantación forestal, índices espectrales | ¿Qué programa calcula la proporción de cobertura vegetal por categoría a partir de los datos crudos? |
| 4 y 5 | Clima y condiciones atmosféricas: precipitación acumulada, días secos y húmedos, velocidad del viento | ¿Qué algoritmo cuenta los días secos y húmedos de un periodo a partir de los registros de precipitación? |
| 6 | Incendios forestales y riesgo: evidencia satelital de fuego y ocurrencia por celda, mes y año | ¿Qué programa identifica y cuenta los eventos de incendio por celda, mes y año? |

Las condiciones técnicas de cada equipo (validaciones, resultados mínimos y pruebas por tema) están en el [README general](../../README.md) y en la [guía de las bases de datos](../../bases_datos_proyecto_integrador/README.md). **Léalas antes de formular los objetivos**: los objetivos deben ser coherentes con lo que su programa debe producir.

### 4.3 La hipótesis

Una hipótesis es una **respuesta anticipada y verificable** a la pregunta. Debe poder **confirmarse o refutarse con sus resultados** de la Unidad 3.

Reglas:

1. Debe estar escrita como **afirmación** (no como pregunta).
2. Debe incluir **variable(s), zona y periodo**.
3. Debe tener un **criterio de decisión** cuantitativo (un umbral, una comparación, un orden de magnitud).
4. No debe ser obvia ni imposible de comprobar con sus datos.

Plantilla: *«Si [condición/regla/método aplicado a la base de la zona], entonces [resultado esperado cuantificable], medido con [indicador] en el periodo 2019–2024.»*

Ejemplo con un tema ajeno al curso: *«La estación A supera el límite de turbidez en menos del 10 % de las mediciones mensuales del periodo 2019–2024, y los excedentes se concentran en los meses de mayor precipitación.»*

> La hipótesis **no es un deseo ni una conclusión adelantada**. Si sus resultados la refutan, eso también es un hallazgo válido, siempre que esté bien sustentado.

### 4.4 Objetivo general y objetivos específicos

**Objetivo general (uno):**

- Empieza con un **verbo en infinitivo** de nivel alto (analizar, determinar, caracterizar, evaluar, desarrollar).
- Responde directamente la pregunta de investigación.
- Indica **qué**, **dónde** y **con qué datos**.

**Objetivos específicos (máximo tres):**

- **No más de tres.** Un cuarto objetivo es una señal de que el alcance es excesivo.
- Cada uno empieza con un **verbo medible** (validar, calcular, clasificar, identificar, comparar, visualizar, probar).
- Son **etapas** que, juntas, cumplen el objetivo general; no repiten el general con otras palabras.
- Cada uno debe producir una **salida verificable** (una tabla, una función, una figura, un resultado numérico).
- Siguen un orden lógico. El patrón más frecuente en este proyecto es:
  1. **Preparar y validar** los datos (lectura, esquema, calidad).
  2. **Calcular o clasificar** (la transformación o el análisis central).
  3. **Presentar y comprobar** (consultas, visualizaciones, pruebas, interpretación).

| Verbo a evitar | Por qué | Alternativa medible |
|---|---|---|
| Conocer, entender, estudiar | No se puede verificar | Identificar, calcular, clasificar |
| Mejorar, optimizar | Requiere un punto de comparación | Reducir, comparar, cuantificar |
| Hacer un programa | Es un medio, no un objetivo | Implementar una función que calcule X y validar su resultado con Y |

**Ejemplo con un tema ajeno al curso:**

- *Objetivo general:* Determinar la frecuencia y la estacionalidad de los excedentes de turbidez en la estación A entre 2019 y 2024 mediante un programa en Python.
- *OE1:* Validar la estructura, el periodo y la calidad de los registros de la estación A.
- *OE2:* Calcular la proporción mensual de mediciones que superan el límite normativo.
- *OE3:* Identificar los meses con mayor concentración de excedentes y representarlos en una figura.

### 4.5 Fases de la Unidad 1 — qué entregar y cuándo

| Fase | Fecha | Qué se entrega | Criterios principales |
|:---:|:---:|---|---|
| **1. Formulación (3 %)** | 07-oct | **Ficha de formulación** (1–2 páginas): tema y zona; descripción del problema en 5–8 líneas; **borrador** de la pregunta; lista de 5–8 variables candidatas con su significado. | Pertinencia con el tema y la zona; problema resoluble con los datos; variables correctamente identificadas. |
| **2. Avance (4 %)** | 14-oct | **Exploración preliminar de los datos** que sustente la pregunta (sección 4.5.1) y **versión mejorada** de la pregunta, tras la retroalimentación de la fase 1. Borrador de hipótesis y objetivos. | Evidencia real de haber abierto y revisado los datos; atención a la retroalimentación; el avance es verificable, no solo intención. |
| **3. Producto técnico (10 %)** | 21-oct | **Informe de la Parte 1 en LaTeX con normas APA 7** (secciones de 4.1) + **PDF compilado**. | Coherencia entre problema, pregunta, hipótesis y objetivos; calidad de la redacción; formato APA; uso de datos y variables; presentación formal. |
| **4. Defensa individual (8 %)** | 28-oct | **Sustentación oral individual**: problema, pregunta, hipótesis y objetivos; por qué se eligieron; qué se hará en la Unidad 2. | Dominio personal; justificación de decisiones; respuesta a preguntas y a pequeñas modificaciones («¿cómo cambiaría su objetivo 2 si…?»). |

#### 4.5.1 ¿Qué es la «exploración preliminar» en la Unidad 1?

En la Unidad 1 todavía no se maneja pandas ni archivos (eso es Unidad 3). La exploración se hace con herramientas simples y debe quedar **documentada**:

1. **Abra su CSV de solo lectura** (en VS Code, o en una hoja de cálculo sin guardar cambios) y registre: número de columnas, nombres de las que usará, número de filas visibles y 5 filas de ejemplo.
2. **Consulte el diccionario** (`dataset_maestro_diccionario_grupos_v1_1_0.json`) y la guía de las bases: complete una **tabla de variables** (nombre, significado, unidad, tipo, rango observado en las filas revisadas).
3. Identifique **al menos tres hechos observados** que justifiquen su pregunta (por ejemplo: valores faltantes visibles, rangos, variables que se repiten por mes, una regla territorial).
4. Si ya lo desea, puede leer una muestra con `pandas.read_csv(..., nrows=100)`; **es opcional** y debe poder explicar cada línea.
5. **Nunca modifique, renombre ni sobrescriba el CSV.** No incorpore datos de 2025.

### 4.6 Matriz de coherencia (obligatoria en el informe)

Complete esta tabla; el docente la usará para evaluar la coherencia de su propuesta:

| Elemento | Redacción del equipo | ¿Se puede verificar con la base asignada? |
|---|---|---|
| Problema |  |  |
| Pregunta de investigación |  |  |
| Hipótesis |  |  |
| Objetivo general |  |  |
| OE1 |  | Salida esperada: |
| OE2 |  | Salida esperada: |
| OE3 (opcional) |  | Salida esperada: |

### 4.7 Lista de comprobación de la Parte 1

- [ ] La pregunta corresponde al tema y a la zona asignados.
- [ ] Hay **una** pregunta, **una** hipótesis y **un** objetivo general.
- [ ] Hay **máximo tres** objetivos específicos, con verbos medibles.
- [ ] La hipótesis es contrastable y tiene un criterio cuantitativo.
- [ ] Cada objetivo específico produce una salida verificable.
- [ ] Solo se usa el periodo 2019–2024 y la base asignada.
- [ ] El informe está en LaTeX, compila sin errores y sigue APA 7 (citas y referencias).
- [ ] Todas las personas del equipo pueden explicar cualquier sección.

---

## 5. PARTE 2 · Unidad 2 — Metodología por objetivo

**Objetivo de la parte:** definir y poner a prueba **cómo se cumplirá cada objetivo específico**, con un método reproducible, y entregar el **informe unificado de las Unidades 1 y 2**.

### 5.1 Qué debe contener la metodología

La metodología se escribe **por objetivo**, no como un texto general. Para **cada** objetivo específico (OE1, OE2, OE3) el informe incluye una subsección con:

| Elemento | Qué debe decir |
|---|---|
| **Objetivo** | Se copia el objetivo tal como quedó en la Parte 1 (corregido). |
| **Entradas** | Variables y columnas necesarias, con tipo de dato y unidad. |
| **Procedimiento** | Pasos **numerados** (pseudocódigo o diagrama de flujo) del algoritmo que lo cumple. |
| **Reglas y parámetros** | Condiciones (`if/elif/else`), umbrales, constantes y su justificación; manejo de datos faltantes y de valores imposibles. |
| **Estructura del código** | Funciones previstas (nombre, parámetros, valor devuelto), uso de iteraciones, listas, diccionarios, tuplas o cadenas, según corresponda. |
| **Verificación** | Cómo se comprobará que el procedimiento es correcto: casos de prueba con resultado calculado a mano, comprobaciones de totales y de rangos. |
| **Salida** | Qué se producirá (tabla, resultado numérico, figura, mensaje) y en qué archivo. |

Además, una sección **general** de metodología con: descripción de los datos y su validación, diagrama del **flujo completo** (lectura → validación → transformación → análisis → exportación), estructura de carpetas del proyecto y plan de pruebas.

> Cada procedimiento debe **trazarse** a un objetivo: si un paso no sirve a ningún objetivo, sobra; si un objetivo no tiene procedimiento, está incompleto.

### 5.2 Relación con los contenidos de la Unidad 2

| Contenido de la unidad | Dónde se aplica en el proyecto |
|---|---|
| Condicionales | Reglas de clasificación, validación y filtrado. |
| Funciones | Una función por tarea (cargar, validar, calcular, clasificar, exportar). |
| Iteraciones (`for`, `while`) | Recorrer registros, celdas, meses o años. |
| Cadenas | Procesar identificadores, nombres de columnas y mensajes. |
| Listas y diccionarios | Almacenar resultados parciales, conteos por categoría, parámetros. |
| Tuplas | Registros inmutables, valores de retorno múltiples. |

### 5.3 Fases de la Unidad 2

| Fase | Fecha | Qué se entrega |
|:---:|:---:|---|
| **1. Formulación (3 %)** | 17-nov | **Matriz metodológica** (una fila por objetivo: entradas, procedimiento, reglas, verificación, salida) y diagrama del flujo general. |
| **2. Avance (4 %)** | 24-nov | **Implementación parcial**: código que ya ejecuta al menos el OE1 y parte del OE2, con sus primeras pruebas; informe de la Parte 1 corregido según retroalimentación. |
| **3. Producto técnico (10 %)** | 01-dic | **Informe unificado Unidad 1 + Unidad 2 en LaTeX/APA** (secciones de 5.4) + PDF + código funcional con instrucciones de ejecución. |
| **4. Defensa individual (8 %)** | 08-dic | **Sustentación oral individual** de la metodología de cada objetivo y modificación en vivo de una función o regla. |

### 5.4 Estructura del informe unificado (Unidades 1 + 2)

1. Resumen
2. **Capítulo 1 — Formulación** *(Parte 1 corregida: problema, pregunta, hipótesis, objetivos)*
3. **Capítulo 2 — Metodología** *(datos y validación; metodología por objetivo; plan de pruebas)*
4. Cronograma de la Unidad 3 (qué se medirá y cómo se presentarán los resultados)
5. Referencias (APA 7)
6. Anexos (matriz de coherencia, matriz metodológica, diagramas)

---

## 6. PARTE 3 · Unidad 3 — Resultados y conclusiones

**Objetivo de la parte:** ejecutar el método, presentar los **resultados por objetivo**, contrastar la hipótesis, concluir y entregar el **informe final unificado de las Unidades 1, 2 y 3**.

### 6.1 Qué debe contener la parte de resultados

Los resultados también se organizan **por objetivo**:

| Elemento | Qué debe decir |
|---|---|
| **Resultado del OE1, OE2, OE3** | Tablas y figuras generadas **por el programa** (con título, unidades, periodo y zona), y su interpretación breve. |
| **Verificación** | Pruebas ejecutadas (mínimo cinco entre todo el proyecto) y su resultado. |
| **Calidad de los datos** | Registros iniciales, aceptados, descartados y motivo. |
| **Contraste de la hipótesis** | Se **confirma, se confirma parcialmente o se refuta**, con los números que lo sustentan. |
| **Discusión** | Qué significan los resultados para el territorio; limitaciones y sesgos posibles. |
| **Conclusiones** | Una conclusión por objetivo específico, una general que responda la pregunta, y recomendaciones (incluidas mejoras al programa). |

> Las conclusiones **solo pueden afirmar lo que los resultados muestran**. No introduzca resultados nuevos en las conclusiones.

### 6.2 Relación con los contenidos de la Unidad 3

| Contenido | Dónde se aplica |
|---|---|
| Manejo de archivos (`.txt`, `.csv`, rutas) | Lectura de la base y exportación de resultados sin sobrescribir la fuente. |
| Bases de datos y SQL | Consultas que respondan los objetivos (si el equipo las usa). |
| Transformación y agregación (pandas) | Cálculo de resúmenes por celda, mes y año. |
| Porciones indexadas | Filtros por zona, periodo, categoría o calidad. |
| Visualización (matplotlib) | Figuras de resultados y distribución espacial. |

### 6.3 Fases de la Unidad 3

| Fase | Fecha | Qué se entrega |
|:---:|:---:|---|
| **1. Formulación (3 %)** | 12-ene | **Plan de resultados**: lista de tablas y figuras que responderán cada objetivo, y estado de la implementación. |
| **2. Avance (4 %)** | 19-ene | **Resultados preliminares** de todos los objetivos y primeras pruebas; informe de Unidades 1 y 2 corregido. |
| **3. Producto técnico (10 %)** | 26-ene | **Informe final unificado Unidad 1 + 2 + 3 en LaTeX/APA** + programa completo y reproducible (`README`, `requirements.txt`, pruebas, `resultados/`). |
| **4. Defensa individual (8 %)** | 02-feb | **Sustentación individual de todo el proyecto**, con modificación en vivo del código y respuesta a preguntas de resultados y conclusiones. |

### 6.4 Estructura del informe final unificado (Unidades 1 + 2 + 3)

1. Resumen (con resultados principales)
2. **Capítulo 1 — Formulación** *(corregido)*
3. **Capítulo 2 — Metodología** *(corregida y alineada con lo realmente ejecutado)*
4. **Capítulo 3 — Resultados** *(por objetivo)*
5. **Capítulo 4 — Discusión y conclusiones** *(contraste de hipótesis, conclusiones, limitaciones y recomendaciones)*
6. Referencias (APA 7)
7. Anexos (matrices, diagramas, tablas completas, registro de ejecución)

---

## 7. Trazabilidad: un objetivo, tres momentos

La coherencia del proyecto se verifica siguiendo cada objetivo a lo largo de las tres unidades. Complete esta tabla desde la Unidad 1 y manténgala actualizada:

| Objetivo | Unidad 1: formulación | Unidad 2: metodología | Unidad 3: resultado y conclusión |
|---|---|---|---|
| **OE1** | Enunciado y salida esperada | Procedimiento, reglas y verificación | Resultado, prueba ejecutada y conclusión |
| **OE2** | … | … | … |
| **OE3** *(si aplica)* | … | … | … |
| **Objetivo general / hipótesis** | Enunciados | Cómo se contrastará | Contraste y conclusión general |

---

## 8. Formato, entrega y organización del trabajo

### 8.1 Informe

- **LaTeX** compilable (puede partir de la [plantilla de la carpeta `plantilla_latex`](plantilla_latex/)) y **PDF** compilado. Se entregan ambos.
- **Normas APA 7**: citas en el texto, lista de referencias, tablas y figuras numeradas con título y fuente.
- Cite como mínimo: el dataset FIRELAB-Loja v1.1.0 y las fuentes técnicas que respalden el problema y los métodos. **No invente referencias**: toda cita debe poder verificarse.
- Redacción impersonal, clara, sin copiar texto de otras fuentes ni de herramientas de IA sin reescribirlo y sin entenderlo.

### 8.2 Estructura recomendada del repositorio del equipo

```text
equipo_XX/
├── README.md              # integrantes, pregunta, zona, instalación y ejecución
├── requirements.txt
├── informe/               # .tex, .bib y PDF
├── src/                   # código (desde Unidad 2)
├── tests/                 # pruebas (desde Unidad 2)
└── resultados/            # tablas y figuras generadas por el programa
```

- No suba entornos virtuales (`.venv`), cachés ni copias del CSV.
- No incluya rutas personales fijas en el código.

### 8.3 Reglas de datos

- Base autorizada: **solo** la carpeta del equipo; **solo registros 2019–2024**.
- El año **2025** está reservado para validación externa del proyecto científico y **no debe usarse**.
- El CSV es de **solo lectura**: las salidas se guardan en archivos nuevos.
- No suba los datos del proyecto a herramientas externas de IA.

### 8.4 Uso de inteligencia artificial

Puede usar IA como apoyo para entender errores, explorar sintaxis o revisar redacción. Debe:

1. **Declarar** en el informe (anexo «Uso de IA») para qué la usó.
2. **Verificar** todo resultado: la IA puede equivocarse con total confianza.
3. **Poder explicar cada línea** de código y cada párrafo que entrega como propio. La defensa individual comprobará esto con modificaciones en vivo.

---

## 9. Defensa individual (8 %)

Cada estudiante responde, por separado y en vivo, preguntas sobre la parte de la unidad. La nota depende **solo** de su dominio.

| Nivel | Descripción |
|:---:|---|
| **9–10 · Sólido** | Explica con claridad el trabajo completo, justifica decisiones, responde variaciones y realiza una modificación en vivo sin ayuda. |
| **7–8,9 · Adecuado** | Explica los elementos centrales y responde la mayoría de preguntas; quedan vacíos menores. |
| **5–6,9 · Parcial** | Explica fragmentos; requiere ayuda constante o comete errores importantes en la modificación. |
| **1–4,9 · Insuficiente** | No logra explicar el trabajo ni modificarlo; contradicciones importantes. |
| **0** | No se presenta o no demuestra autoría. |

Preguntas típicas: «¿Por qué eligió esta pregunta y no otra?», «¿Cómo se relaciona el objetivo 2 con la hipótesis?», «¿Qué haría esta función si el dato fuera negativo?», «Cambie el umbral a X y diga qué resultado espera».

---

## 10. Preguntas frecuentes

**¿Puedo cambiar la pregunta después de la Unidad 1?**
Se puede **refinar** con justificación y aprobación del docente antes de la fase 1 de la Unidad 2. Cambiarla por completo en la Unidad 3 no es posible.

**¿Y si mi hipótesis se refuta?**
Es un resultado válido. Se reporta con honestidad y se discute por qué.

**¿Cuántas variables debo usar?**
Las necesarias para responder su pregunta; normalmente entre 5 y 10. Cada variable debe tener un propósito explicado.

**¿Puedo trabajar con el otro equipo del mismo tema?**
Pueden conversar sobre conceptos generales, **no** compartir archivos, código, tablas, figuras ni conclusiones.

**¿El código se evalúa en la Unidad 1?**
Se evalúa la formulación y la exploración de datos; el código completo se desarrolla en las unidades 2 y 3. Si el equipo ya tiene código exploratorio, puede incluirlo como anexo.

---

## 11. Lista de comprobación general antes de cada entrega

- [ ] El informe compila en LaTeX y el PDF coincide con el `.tex`.
- [ ] Incluye todas las secciones exigidas para la unidad.
- [ ] Usa APA 7 en citas, tablas, figuras y referencias.
- [ ] Atiende la retroalimentación de la unidad anterior (y se indica cómo).
- [ ] Se respeta la base, la zona y el periodo asignados.
- [ ] La fuente de datos no fue modificada.
- [ ] La trazabilidad de los objetivos está actualizada.
- [ ] Se declaró el uso de IA.
- [ ] Todas las personas del equipo se preparan para la defensa individual.
