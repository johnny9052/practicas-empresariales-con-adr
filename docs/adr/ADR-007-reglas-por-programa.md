# ADR-007: Reglas de práctica por programa como configuración con vigencia

## Estado

Aceptado (26 de octubre de 2026).

## Contexto

CU-12 permite al director de programa configurar las reglas de práctica de su programa, porque los requisitos y las horas mínimas varían entre programas (S-07). OB-05 exige aplicar un cambio del reglamento desde el periodo siguiente sin suspender las prácticas en curso, y EAC-01 exige incorporar un programa nuevo en máximo 16 horas de trabajo, modificando como máximo 2 módulos y con 0 prácticas en curso de otros programas que cambien de estado o de reglas.

## Alternativas consideradas

| Alternativa | Ventajas | Desventajas |
|---|---|---|
| **A) Reglas escritas en el código, con condicionales por programa** | Rápido para el primer programa | Cada programa nuevo exige modificar y desplegar código en varios lugares: incumple EAC-01 |
| **B) Reglas como datos parametrizados (horas mínimas, requisitos académicos, plazos), versionadas por programa y periodo de vigencia, y evaluadas por el módulo de reglas** | El director de programa configura sin programar (CU-12); cada práctica queda ligada a la versión de reglas vigente cuando inició | Solo cubre los tipos de regla previstos; un tipo nuevo de regla sí exige programar |
| **C) Motor de reglas de propósito general** | Expresa cualquier regla | Curva de aprendizaje alta, reglas difíciles de verificar y posiblemente fuera del catálogo (RT-04) |

## Decisión

Se elige la alternativa B. Cada práctica guarda la referencia a la versión de reglas con la que inició, de modo que publicar una versión nueva nunca altera las prácticas en curso. Un tipo nuevo de regla se agrega solo en el módulo de reglas (ADR-001).

## Consecuencias

**Positivas:** Un programa nuevo es configuración y no código, lo que hace cumplible EAC-01; las prácticas en curso conservan sus reglas (OB-05).

**Negativas (costos aceptados):** Hay que construir y mantener la interfaz de configuración, y validar que una versión no tenga reglas contradictorias.

**Riesgos:** Que el director de programa publique reglas erróneas. Mitigación: cada versión nueva queda como borrador hasta que se publica, y solo aplica desde el periodo siguiente.
