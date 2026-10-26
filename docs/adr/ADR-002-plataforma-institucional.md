# ADR-002: Plataforma tecnológica y despliegue en la infraestructura institucional

## Estado

Aceptado (26 de octubre de 2026). Decisión impuesta por restricciones.

## Contexto

RT-01 obliga a desplegar en la infraestructura que administra la Universidad; RT-04 obliga a usar el motor de base de datos y las tecnologías del catálogo institucional, y RN-05 prohíbe requerir licencias comerciales de pago recurrente. S-09 supone que estas políticas están vigentes y que se confirman con el Área de Sistemas y la Decanatura en la primera semana.

## Alternativas consideradas

No hay alternativas libres: la decisión viene impuesta por RT-01, RT-04 y RN-05. Se registra igual para que nadie la discuta después como si hubiera sido una elección. Quedan descartadas de entrada:

| Alternativa descartada | Restricción que la descarta |
|---|---|
| **Servicios gestionados de nube pública (funciones sin servidor, base de datos como servicio)** | RT-01 |
| **Plataformas comerciales de flujos de trabajo o de bajo código por suscripción** | RN-05 |
| **Lenguajes, frameworks o motores de base de datos fuera del catálogo institucional** | RT-04 |

## Decisión

Se construye una aplicación web desplegada en los servidores que administra el Área de Sistemas, con el lenguaje, el framework y el motor de base de datos del catálogo institucional, y solo con componentes de software libre o sin costo recurrente. La elección concreta dentro del catálogo se registrará en un ADR posterior, una vez confirmado el catálogo con el Área de Sistemas (S-09).

## Consecuencias

**Positivas:** El Área de Sistemas puede operar, respaldar y dar soporte al sistema con su propio personal; la solución no genera costos de licencias.

**Negativas (costos aceptados):** El equipo queda limitado a las tecnologías del catálogo, aunque existan otras más convenientes, y la capacidad de crecimiento depende de los servidores institucionales.

**Riesgos:** Que el catálogo no incluya algo que el sistema necesita, por ejemplo la generación de PDF (ADR-008) o un bróker de mensajes (ADR-003). Mitigación: verificarlo en la primera semana, junto con S-09.
