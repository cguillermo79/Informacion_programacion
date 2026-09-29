# Bases de datos del proyecto integrador - Programacion

Estas bases son copias parciales del dataset maestro FIRELAB_Loja v1.1.0.
No se recalcularon, imputaron, agregaron ni corrigieron valores.
Solo se seleccionaron registros de 2019-2024 y las columnas del bloque asignado.
El ano 2025 no esta incluido.

## Fuente y control de integridad

- Fuente: `dataset_maestro_firelab_loja_2019_2025_v1_1_0.csv`
- SHA-256 de la fuente: `890423faf91207aa271feb9878b1b379e309c156e8e7128af380a5c1afe674b6`
- Unidad de observacion: celda de 500 m por mes.
- Periodo entregado: enero de 2019 a diciembre de 2024.

## Asignacion

| Equipo | Bloque tematico | Zona | Registros | Celdas | Columnas | Archivo |
|---:|---|---|---:|---:|---:|---|
| 1 | Relieve y accesibilidad | Norte | 288072 | 4001 | 66 | `equipo_01_relieve_zona_norte/base_programacion_equipo_01_relieve_zona_norte_2019_2024.csv` |
| 2 | Relieve y accesibilidad | Sur | 287712 | 3996 | 66 | `equipo_02_relieve_zona_sur/base_programacion_equipo_02_relieve_zona_sur_2019_2024.csv` |
| 3 | Cobertura vegetal y uso del suelo | Completo | 575784 | 7997 | 53 | `equipo_03_cobertura_loja_completo/base_programacion_equipo_03_cobertura_loja_completo_2019_2024.csv` |
| 4 | Clima y condiciones atmosfericas | Norte | 288072 | 4001 | 57 | `equipo_04_clima_zona_norte/base_programacion_equipo_04_clima_zona_norte_2019_2024.csv` |
| 5 | Clima y condiciones atmosfericas | Sur | 287712 | 3996 | 57 | `equipo_05_clima_zona_sur/base_programacion_equipo_05_clima_zona_sur_2019_2024.csv` |
| 6 | Incendios forestales y riesgo | Completo | 575784 | 7997 | 41 | `equipo_06_incendios_loja_completo/base_programacion_equipo_06_incendios_loja_completo_2019_2024.csv` |

## Division espacial de las parejas

Como los materiales del curso exigen subconjuntos distintos pero no nombran parroquias o sitios especificos, se uso una division equilibrada y reproducible de la malla:

- Norte: `centro_y_m >= 9555250.0` (4.001 celdas).
- Sur: `centro_y_m < 9555250.0` (3.996 celdas).
- Loja completo: 7.997 celdas.

Los archivos conservan los nombres y valores originales de FIRELAB_Loja. La zona se expresa en el nombre del archivo y no se agrego una columna nueva.
