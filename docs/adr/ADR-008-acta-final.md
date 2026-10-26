# ADR-008: Acta final generada desde una plantilla externa y conservada como documento inmutable

## Estado

Aceptado (26 de octubre de 2026).

## Contexto

CU-09 genera el acta final, razón de ser del sistema, de la que dependen OB-01 y OB-04 (menos del 1% de actas reemitidas por errores). RN-03 obliga a seguir el formato del reglamento de prácticas, que puede cambiar por decisión del Consejo de Facultad, y RN-02 obliga a conservar actas y evidencias según la tabla de retención documental. Según S-06, basta la aprobación electrónica trazable del docente asesor y del director de programa (CU-10), aunque R-03 advierte que podría exigirse firma digital certificada.

## Alternativas consideradas

| Alternativa | Ventajas | Desventajas |
|---|---|---|
| **A) Acta construida directamente en el código** | Sin dependencias adicionales | Cambiar el formato (RN-03) exige programar y desplegar |
| **B) Plantilla del acta separada del código, llenada con los datos de la práctica y convertida a PDF; el PDF aprobado se guarda como documento inmutable con su huella (hash)** | El formato cambia sin reprogramar; el acta aprobada no se altera (RN-02, OB-04) | Hay que versionar las plantillas y mantener el componente de conversión a PDF |
| **C) Generar un archivo de Word para que el docente asesor lo complete a mano** | Fácil de implementar | Reintroduce los errores de transcripción que OB-04 busca eliminar |

## Decisión

Se elige la alternativa B. El acta se genera con los datos registrados en el sistema y pasa por dos aprobaciones: primero la del docente asesor y luego la del director de programa (CU-10), ambas registradas en la bitácora (ADR-006). Una vez aprobada, el acta no se modifica ni se borra; un error se corrige emitiendo una nueva acta que referencia a la anterior.

## Consecuencias

**Positivas:** El formato sigue al reglamento sin reprogramar (RN-03); las actas aprobadas se conservan íntegras (RN-02); desaparece la transcripción manual (OB-04).

**Negativas (costos aceptados):** Se agrega un componente de generación de PDF y la gestión de versiones de la plantilla.

**Riesgos:** Que se exija firma digital certificada (R-03). Mitigación: la aprobación está aislada detrás de un puerto (ADR-001); agregar la firma sería un adaptador nuevo y un ADR que reemplace parcialmente a este.
