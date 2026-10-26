# Documento de arquitectura: Sistema de Gestión de Prácticas Empresariales

Este documento consolida la arquitectura y enlaza a los demás archivos de `docs/` en lugar de copiar su contenido.

## 1. Introducción y objetivos

Los objetivos de negocio están en [vision.md, sección 2](vision.md#2-objetivos-de-negocio) (OB-01 a OB-06).

## 2. Restricciones

Las restricciones técnicas (RT-01 a RT-04) y de negocio (RN-01 a RN-05), con su tipo, origen e impacto arquitectónico, están en [drivers.md, sección 3](drivers.md#3-restricciones).

## 3. Contexto del sistema

*Pendiente.* Se completa en el tema de vistas.

## 4. Estrategia de solución

*Pendiente.*

## 5. Vistas

*Pendiente.* Se completa en el tema de vistas.

## 6. Conceptos transversales

*Pendiente.*

## 7. Decisiones de diseño

Índice de los ADR, que viven en la carpeta [adr/](adr/).

| ID | Decisión | Estado |
|---|---|---|
| [ADR-001](adr/ADR-001-monolito-modular.md) | Monolito modular con puertos y adaptadores | Aceptado |
| [ADR-002](adr/ADR-002-plataforma-institucional.md) | Plataforma tecnológica y despliegue en la infraestructura institucional | Aceptado |
| [ADR-003](adr/ADR-003-integraciones-cola-mensajes.md) | Integraciones externas mediante adaptadores y cola de mensajes con reintentos | Aceptado |
| [ADR-004](adr/ADR-004-autenticacion.md) | Autenticación con la cuenta institucional y enlaces de un solo uso para supervisores | Aceptado |
| [ADR-005](adr/ADR-005-autorizacion-por-roles.md) | Autorización por roles centralizada en los casos de uso | Aceptado |
| [ADR-006](adr/ADR-006-bitacora-auditoria.md) | Bitácora de auditoría de solo inserción en la base de datos | Aceptado |
| [ADR-007](adr/ADR-007-reglas-por-programa.md) | Reglas de práctica por programa como configuración con vigencia | Aceptado |
| [ADR-008](adr/ADR-008-acta-final.md) | Acta final generada desde una plantilla externa y conservada como documento inmutable | Aceptado |
| [ADR-009](adr/ADR-009-migracion-inicial.md) | Migración inicial con plantilla normalizada y script de carga única | Aceptado |

## 8. Requisitos de calidad

Los escenarios de atributos de calidad (EAC-01 a EAC-03) están en [drivers.md, sección 2](drivers.md#2-escenarios-de-atributos-de-calidad).

## 9. Riesgos y deuda técnica

*Pendiente.*
