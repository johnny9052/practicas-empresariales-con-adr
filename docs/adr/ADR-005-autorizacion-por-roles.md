# ADR-005: Autorización por roles centralizada en los casos de uso

## Estado

Aceptado (26 de octubre de 2026).

## Contexto

PA-02 exige controlar los permisos de cinco roles: estudiante, docente asesor, director de programa, supervisor y administrador. RN-01 (Ley 1581 de 2012) obliga a restringir el acceso a los datos personales según su finalidad, a registrar la autorización de tratamiento y a cifrar la información en tránsito. CU-10 exige que solo el docente asesor y el director de programa aprueben el acta.

## Alternativas consideradas

| Alternativa | Ventajas | Desventajas |
|---|---|---|
| **A) Verificar permisos en cada pantalla o controlador** | Rápido de empezar | Reglas dispersas y fáciles de olvidar; una sola ruta sin verificación expone datos personales (RN-01) |
| **B) Política de autorización por roles centralizada, aplicada en cada caso de uso, con verificación de pertenencia** | Una sola regla por permiso, fácil de revisar y de probar; un docente asesor solo ve a sus practicantes | Hay que mantener la política al agregar casos de uso |
| **C) Control de acceso basado en atributos con un motor de políticas** | Muy flexible | Complejidad que no exigen cinco roles fijos; un componente más (R-04) |

## Decisión

Se elige la alternativa B. Cada caso de uso declara el rol que lo puede ejecutar y verifica que el dato pertenezca al usuario (por ejemplo, que la práctica sea de un practicante del docente asesor). La tabla de permisos vive en un solo lugar del módulo de aplicación. Todo el tráfico va cifrado (HTTPS) y la postulación (CU-01) registra la autorización de tratamiento de datos del estudiante.

## Consecuencias

**Positivas:** El cumplimiento de RN-01 se puede verificar; cualquier revisor encuentra los permisos en un solo lugar; la aprobación del acta queda restringida a los roles de CU-10.

**Negativas (costos aceptados):** Cada caso de uso nuevo obliga a actualizar la política de autorización.

**Riesgos:** Que un caso de uso nuevo quede sin rol asignado. Mitigación: por defecto se niega el acceso a cualquier caso de uso sin rol declarado.
