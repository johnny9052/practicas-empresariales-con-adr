# ADR-006: Bitácora de auditoría de solo inserción en la base de datos

## Estado

Aceptado (26 de octubre de 2026).

## Contexto

PA-03 pide decidir qué eventos se registran, dónde y por cuánto tiempo. OB-06 exige entregar a auditoría o acreditación el consolidado de prácticas de cualquier periodo en máximo 1 día hábil; CU-10 requiere saber quién aprobó el acta y cuándo (S-06); EAC-03 exige registrar cada intento de acceso rechazado con fecha, hora y dirección de origen en menos de 1 minuto, y RN-01 exige controlar el acceso a los datos personales.

## Alternativas consideradas

| Alternativa | Ventajas | Desventajas |
|---|---|---|
| **A) Archivos de registro (logs) del servidor** | Ya existen, sin desarrollo adicional | Se rotan y se pierden; son difíciles de consultar para un consolidado (OB-06); no prueban quién aprobó qué |
| **B) Tabla de bitácora de solo inserción en la base de datos, escrita en la misma transacción que la operación** | Consultable y consistente con los datos; el registro es inmediato (EAC-03) | Crece con el tiempo y obliga a definir su conservación |
| **C) Plataforma externa de gestión de eventos de seguridad** | Análisis avanzado de eventos | Fuera del catálogo y con posible costo recurrente (RT-04, RN-05); sobredimensionada (R-04) |

## Decisión

Se elige la alternativa B. Se registran las aprobaciones del acta (quién, cuándo y qué versión), los cambios de estado de cada práctica, los accesos a datos personales y los intentos de acceso rechazados. La aplicación no puede modificar ni borrar registros de la bitácora, que se conserva según la tabla de retención documental (RN-02).

## Consecuencias

**Positivas:** La aprobación electrónica queda trazable (CU-10, S-06); el consolidado de auditoría sale de una consulta (OB-06); el registro de intentos es inmediato (EAC-03); la mesa de ayuda tiene con qué diagnosticar.

**Negativas (costos aceptados):** Cada operación hace una escritura más, y la tabla crece de forma permanente.

**Riesgos:** Que alguien con acceso directo a la base de datos altere registros. Mitigación: el usuario de base de datos de la aplicación solo tiene permiso de inserción sobre la bitácora, administrado por el Área de Sistemas.
