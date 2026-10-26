# ADR-003: Integraciones externas mediante adaptadores y cola de mensajes con reintentos

## Estado

Aceptado (26 de octubre de 2026).

## Contexto

CU-01 verifica los requisitos académicos del estudiante contra los servicios del SIA (RT-03), que pueden no responder o fallar (R-02). EAC-02 exige 0 postulaciones perdidas, confirmación al estudiante en menos de 3 segundos en el 95% de los casos y verificación completada en máximo 30 minutos después de que el SIA se recupera. PA-04 pide una estrategia única para las fallas del SIA y del correo institucional, que también usa CU-08 para los recordatorios. La carga es baja (S-03).

## Alternativas consideradas

| Alternativa | Ventajas | Desventajas |
|---|---|---|
| **A) Llamada sincrónica al SIA, con error al usuario si falla** | Simple, sin componentes adicionales | Si el SIA cae, la postulación se pierde o el estudiante debe reintentar: incumple EAC-02 |
| **B) Tabla de tareas pendientes en la base de datos, procesada por una tarea programada con reintentos** | Cumple EAC-02 sin agregar infraestructura | Reintentos y fallos definitivos se programan a mano, y cada integración podría resolverlos distinto (PA-04) |
| **C) Cola de mensajes con un bróker dedicado, consumida por un proceso en segundo plano (worker)** | Cumple EAC-02; el bróker resuelve reintentos y cola de fallidos de forma estándar para el SIA y el correo (PA-04) | Un componente de infraestructura más que operar (RT-01), para una carga hoy baja (S-03, R-04) |

## Decisión

Se elige la alternativa C. Cada sistema externo (SIA y correo) tiene su adaptador detrás de un puerto (ADR-001). Cada verificación y cada notificación se publica como mensaje en una cola persistente que consume un worker; si la llamada falla o supera 5 segundos, el mensaje se reintenta con espera creciente (máximo 5 minutos entre intentos, lo que asegura los 30 minutos de EAC-02) y, si agota sus reintentos, pasa a una cola de fallidos. Mientras tanto, la postulación queda "pendiente de verificación" y el estudiante recibe la confirmación de recepción. Se prefiere sobre B, pese a la carga baja (S-03), porque los reintentos y los fallos los resuelve un componente probado, de la misma forma para todas las integraciones (PA-04). El bróker será de software libre (RN-05), desplegado en la infraestructura institucional (RT-01) y elegido con el Área de Sistemas (ADR-002).

## Consecuencias

**Positivas:** Se cumple EAC-02; el SIA y el correo se tratan con una sola estrategia (PA-04); una caída del SIA o del correo no detiene la recepción de postulaciones.

**Negativas (costos aceptados):** Un bróker más que el Área de Sistemas debe instalar, operar y monitorear, aunque la carga actual no lo exige (S-03, R-04), y un estado intermedio, "pendiente de verificación", que la interfaz debe explicar.

**Riesgos:** Que la cola crezca sin control en una caída larga del SIA (mitigación: alerta al superar 100 mensajes pendientes) o que el catálogo no incluya un bróker (RT-04; mitigación: un ADR que reemplace a este y adopte la alternativa B). Si el SIA no ofrece servicios de consulta (R-02), se reemplaza el adaptador sin tocar el dominio.
