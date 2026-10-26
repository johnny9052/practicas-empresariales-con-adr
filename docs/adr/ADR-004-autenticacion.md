# ADR-004: Autenticación con la cuenta institucional y enlaces de un solo uso para supervisores

## Estado

Aceptado (26 de octubre de 2026).

## Contexto

RT-02 obliga a autenticar a estudiantes, docentes asesores y personal con la cuenta institucional (inicio de sesión único). RN-04 prohíbe exigir a los supervisores de empresa una cuenta o un registro con contraseña, porque un trámite pesado pone en riesgo OB-02 (R-01). Los supervisores intervienen en CU-05 (validar horas) y en CU-07 (evaluar al practicante), y EAC-03 exige rechazar el 100% de los accesos con enlaces usados, con más de 15 días de emitidos o alterados, sin mostrar datos personales. PA-02 pide decidir cómo conviven estas dos formas de acceso.

## Alternativas consideradas

| Alternativa | Ventajas | Desventajas |
|---|---|---|
| **A) Cuentas locales con contraseña para todos** | Un solo mecanismo de acceso | Incumple RT-02 y RN-04, y obliga al sistema a guardar contraseñas |
| **B) Inicio de sesión institucional para todos, con cuentas de invitado para los supervisores** | Un solo mecanismo, con control central de identidades | Incumple RN-04: el supervisor tendría que registrarse |
| **C) Inicio de sesión institucional para usuarios internos y enlace de un solo uso para supervisores** | Cumple RT-02 y RN-04; el supervisor entra con un clic, lo que favorece OB-02 | Dos mecanismos de acceso que mantener y probar |

## Decisión

Se elige la alternativa C. Los usuarios internos entran por el proveedor de identidad institucional mediante un adaptador (ADR-001), y el sistema no guarda contraseñas. Para cada validación de horas o evaluación se genera un enlace con un identificador aleatorio, de un solo uso, que vence a los 15 días; el sistema guarda solo el resumen criptográfico (hash) del identificador. Todo intento con un enlace usado, vencido o alterado se rechaza sin mostrar datos, se registra en la bitácora (ADR-006) y se avisa al docente asesor.

## Consecuencias

**Positivas:** Se cumplen RT-02, RN-04 y EAC-03; el supervisor no crea cuentas, lo que reduce el riesgo R-01.

**Negativas (costos aceptados):** Hay dos mecanismos de acceso que mantener, y quien tenga el enlace antes de que se use puede actuar en nombre del supervisor.

**Riesgos:** Que el correo con el enlace se reenvíe a otra persona. Mitigación: el enlace sirve una sola vez y para una sola práctica, y el docente asesor revisa la evaluación antes de solicitar el acta (CU-09).
