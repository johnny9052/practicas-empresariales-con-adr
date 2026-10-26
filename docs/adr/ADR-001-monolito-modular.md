# ADR-001: Monolito modular con puertos y adaptadores

## Estado

Aceptado (26 de octubre de 2026).

## Contexto

El sistema atiende entre 170 y 250 prácticas activas a la vez, con decenas de usuarios concurrentes (S-03), pero sus reglas cambian por programa y por reglamento (OB-05, S-07), y EAC-01 exige incorporar las reglas de un programa nuevo modificando como máximo 2 módulos. Además, el sistema depende de sistemas que no controla: el SIA, al que solo se accede por sus servicios (RT-03), el proveedor de identidad institucional (RT-02) y el correo institucional. PA-01 pide decidir en qué grandes bloques se divide el sistema y hacia dónde apuntan sus dependencias, y R-04 advierte el riesgo de sobredimensionar la solución.

## Alternativas consideradas

| Alternativa | Ventajas | Desventajas |
|---|---|---|
| **A) Monolito en capas tradicional (presentación, negocio, datos)** | Simple y conocido por cualquier equipo | El negocio depende de la capa de datos y de los detalles de cada integración; un cambio de reglas o del SIA atraviesa varias capas, lo que pone en riesgo EAC-01 |
| **B) Monolito modular con puertos y adaptadores** | Un solo desplegable, dividido en módulos por capacidad (postulación, horas, evaluación, actas, reglas); el dominio define puertos y las integraciones son adaptadores reemplazables | Exige disciplina para que los módulos solo se comuniquen por sus interfaces; más interfaces que en el esquema de capas |
| **C) Microservicios** | Despliegue y escalado independientes por servicio | La carga de S-03 no lo justifica; multiplica la operación para el Área de Sistemas (RT-01) y materializa el riesgo R-04 |

## Decisión

Se elige la alternativa B. Es la única que permite cumplir EAC-01 sin sobredimensionar la solución: la modularidad responde a OB-05 y la distribución no aporta nada con la carga de S-03. Las dependencias apuntan siempre hacia el dominio: el dominio declara los puertos (consulta académica, identidad, notificaciones, persistencia) y los adaptadores los implementan.

## Consecuencias

**Positivas:** Cada cambio del reglamento queda concentrado en el módulo de reglas (EAC-01); el SIA, la identidad y el correo se pueden sustituir o simular sin tocar el dominio; el Área de Sistemas despliega y monitorea un solo artefacto de aplicación.

**Negativas (costos aceptados):** Hay más código de interfaces y adaptadores que en un esquema de capas, y el equipo debe vigilar que ningún módulo use atajos hacia el interior de otro.

**Riesgos:** Si un módulo crece sin control, el monolito se vuelve difícil de mantener. Mitigación: revisar las dependencias entre módulos en cada Pull Request.
