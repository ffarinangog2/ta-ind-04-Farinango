# TA-IND-04 — Análisis de Rendimiento Paralelo aplicado al PFC

Trabajo Autónomo Individual correspondiente a la **Unidad 4 — Cómputo Paralelo y Distribuido** de la asignatura **Aplicaciones Distribuidas (ISR-701)**.

El presente repositorio contiene el informe técnico individual TA-IND-04, desarrollado a partir de los resultados experimentales obtenidos en la práctica grupal **GA-SUM-05 / PE-U4**, con énfasis en el análisis del rendimiento paralelo de la transformación **T2 — Agrupación y agregación** y su posible integración en el Proyecto Fin de Curso.

---

## Datos del estudiante

- **Universidad:** Universidad Técnica Estatal de Quevedo
- **Facultad:** Facultad de Ciencias de la Computación
- **Carrera:** Ingeniería de Software
- **Asignatura:** Aplicaciones Distribuidas (ISR-701)
- **Unidad:** Unidad 4 — Cómputo Paralelo y Distribuido
- **Actividad:** TA-IND-04 — Informe Técnico Individual
- **Estudiante:** Freddy Vladimir Farinango Guandinango
- **Correo institucional:** ffarinangog2@uteq.edu.ec
- **Docente:** Gleiston C. Guerrero-Ulloa, M.Sc.
- **Período académico:** 2026–2027 PPA
- **Equipo PE-U4:** Equipo C — Farinango, Gaibor y Villamarín
- **PFC de referencia:** FUVV — Sistema de Control de Laboratorios Informáticos (SCLI)
- **Transformación foco individual:** T2 — Agrupación y agregación

---

## Objetivo

Analizar individualmente los resultados de rendimiento obtenidos en PE-U4, contrastando el *speedup* experimental con la Ley de Amdahl, diagnosticando la fracción no escalable mediante la métrica de Karp-Flatt y determinando la viabilidad de utilizar procesamiento distribuido para un proceso concreto del Sistema de Control de Laboratorios Informáticos (SCLI).

El análisis se concentra en la transformación **T2**, correspondiente a una operación de agrupación y agregación por laboratorio.

---

## Repositorio de origen de los datos

Los datos experimentales utilizados como base para este informe proceden del repositorio grupal de PE-U4:

**Repositorio PE-U4:**  
https://github.com/ffarinangog2/pe-u4-spark-equipo-c

**Commit utilizado como referencia:**  
`a5ffcd92dc9228512f42d7a55004391ba771daf3`

**SHA corto:**  
`a5ffcd9`

Este commit contiene las mediciones consolidadas utilizadas en el informe, incluyendo las mediciones adicionales realizadas para la transformación T2 con diferentes números de executors.

Las mediciones individuales de T2 para **N = 1** y **N = 2 executors** fueron incorporadas inicialmente mediante el commit:

`bbe19c8bd0a268b52a26f18a8738197aa6248d5f`

Posteriormente fueron integradas en `main` mediante el commit `a5ffcd9`.

---

## Transformación analizada

La transformación seleccionada como foco individual es:

### T2 — Agrupación y agregación

La operación procesa las solicitudes de reserva y realiza una agrupación por laboratorio para obtener resultados agregados.

El análisis compara la implementación secuencial realizada con **pandas** frente a la implementación distribuida con **PySpark**, utilizando configuraciones de:

- N = 1 executor
- N = 2 executors
- N = 4 executors

Los tiempos corresponden a medianas obtenidas a partir de cinco repeticiones válidas por configuración, siguiendo el protocolo experimental utilizado en PE-U4.

---

## Principales aspectos analizados

El informe desarrolla los siguientes elementos:

- cálculo de *speedup* para las transformaciones T1–T5;
- cálculo de eficiencia del paralelismo;
- contraste experimental frente a la Ley de Amdahl;
- cálculo de la desviación entre el rendimiento experimental y el teórico;
- análisis del caso de *speedup* inferior a uno;
- cálculo e interpretación de la métrica de Karp-Flatt;
- identificación de mecanismos de sobrecarga de Spark;
- análisis del efecto del *shuffle* en T2;
- estimación del umbral de rentabilidad del procesamiento distribuido;
- propuesta de integración al PFC;
- análisis de alternativas tecnológicas;
- postura crítica sobre la conveniencia de utilizar Spark en el SCLI.

---

## Integración propuesta al PFC

El caso de uso analizado corresponde a la generación periódica de un **reporte de demanda por laboratorio** dentro del Sistema de Control de Laboratorios Informáticos (SCLI).

El proceso contempla:

1. lectura de solicitudes de reserva almacenadas en PostgreSQL;
2. agrupación de solicitudes por laboratorio;
3. cálculo de demanda y ocupación;
4. almacenamiento de los resultados en una capa de *reporting*;
5. presentación de los resultados en el panel de coordinación del SCLI.

La salida permitiría apoyar decisiones relacionadas con:

- planificación de mantenimiento preventivo;
- identificación de laboratorios con mayor demanda;
- redistribución de cupos y horarios.

A partir de los resultados obtenidos, el informe concluye que **Spark no resulta conveniente actualmente para este proceso**, debido al volumen de datos esperado y a la sobrecarga observada en la operación T2.

---

## Estructura del repositorio

```text
ta-ind-04-Farinango/
│
├── README.md
├── LICENSE
│
├── docs/
│   ├── TA_IND_04_Informe.tex
│   ├── TA_IND_04_Informe.pdf
│   └── references.bib
│
├── datos/
│   └── tiempos_base.csv
│
└── figuras/
    └── fig_speedup.png


## Instrucciones exactas de compilación

Requisitos: distribución LaTeX con `pdflatex` y `biber` (TeX Live 2023+ o
Overleaf, que ya los incluye).

Desde la carpeta `docs/`, ejecutar en este orden exacto:

```bash
pdflatex TA_IND_04_Informe.tex
biber TA_IND_04_Informe
pdflatex TA_IND_04_Informe.tex
pdflatex TA_IND_04_Informe.tex
```

En Overleaf: subir la carpeta completa del repositorio, verificar que el
compilador esté configurado como **pdfLaTeX** (Menu → Settings →
Compiler) y compilar normalmente; Overleaf detecta `biblatex` y ejecuta
`biber` automáticamente.

La figura `figuras/fig_speedup.png` se referencia desde el `.tex` con ruta
relativa `../figuras/fig_speedup.png`, por lo que la estructura de carpetas
debe conservarse tal como se entrega.

## Declaración de uso de inteligencia artificial generativa

Ver la sección "Declaración de uso de inteligencia artificial generativa"
al final de `docs/TA_IND_04_Informe.pdf`.


