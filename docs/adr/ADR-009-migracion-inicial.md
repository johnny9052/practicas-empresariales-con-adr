# ADR-009: Migración inicial con plantilla normalizada y script de carga única

## Estado

Aceptado (26 de octubre de 2026).

## Contexto

PA-05 y CU-15 piden cargar las prácticas en curso desde archivos de Excel con formatos distintos por docente asesor; la migración está en el alcance de la visión y define el primer despliegue. En la matriz de priorización, PA-05 quedó en el cuadrante de baja importancia y alta dificultad (cuestionar), y se ejecuta una sola vez.

## Alternativas consideradas

| Alternativa | Ventajas | Desventajas |
|---|---|---|
| **A) Digitación manual de las prácticas en curso** | Sin desarrollo | Entre 170 y 250 prácticas activas (S-03): lenta y con errores de transcripción (OB-04) |
| **B) Plantilla de Excel normalizada que cada docente asesor llena, y un script de carga única que valida y reporta errores antes de importar** | Esfuerzo acotado; los errores se detectan antes de cargar | Trabajo adicional para los docentes asesores, una sola vez |
| **C) Importador permanente dentro de la aplicación, capaz de leer cada formato existente** | Reutilizable | Mucho esfuerzo para algo que se usa una vez; contradice el cuadrante en que quedó PA-05 |

## Decisión

Se elige la alternativa B. El script se ejecuta una vez, antes del lanzamiento, y crea las prácticas a través de los mismos casos de uso del dominio, de modo que respeta las reglas de cada programa (ADR-007) y deja rastro en la bitácora (ADR-006). Después del lanzamiento se archiva y no forma parte de la aplicación.

## Consecuencias

**Positivas:** La carga inicial queda validada y controlada, y no queda código de un solo uso dentro de la aplicación.

**Negativas (costos aceptados):** El lanzamiento depende de que los docentes asesores llenen la plantilla a tiempo.

**Riesgos:** Que algunas prácticas no se migren. Mitigación: el script genera un reporte de pendientes por docente asesor, que el director de programa revisa antes del lanzamiento.
