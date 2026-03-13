# 🏗️ Rule 10 — Backend Architecture

> Garantiza que todo cambio respete las fronteras de **DDD + Arquitectura Hexagonal**.

---

## Concepto clave: Arquitectura Hexagonal

La arquitectura hexagonal (también llamada *Ports & Adapters*) divide el sistema en tres capas con una dirección de dependencia estricta:

```
┌─────────────────────────────────────────┐
│              Infrastructure             │  ← DB, HTTP, Messaging, Frameworks
│  ┌───────────────────────────────────┐  │
│  │           Application             │  │  ← Casos de uso, orquestación
│  │  ┌─────────────────────────────┐  │  │
│  │  │          Domain             │  │  │  ← Entidades, reglas de negocio
│  │  └─────────────────────────────┘  │  │
│  └───────────────────────────────────┘  │
└─────────────────────────────────────────┘

Dependencias: Infrastructure → Application → Domain
              Domain no depende de nadie ✅
```

---

## Reglas de capas

| Capa | Contiene | No puede depender de |
|------|----------|----------------------|
| **Domain** | Entidades, Value Objects, reglas de negocio, interfaces de puertos | Application, Infrastructure, frameworks |
| **Application** | Casos de uso, command/query handlers, DTOs de app | Infrastructure, frameworks |
| **Infrastructure** | Repositorios, controllers, clientes HTTP, configs | Solo implementa interfaces del Domain/Application |

---

## Restricciones activas

```
❌ No poner lógica de negocio en Infrastructure
❌ No importar clases de Spring/JPA en el Domain
❌ No crear "god services" que mezclan responsabilidades
❌ No inventar capas nuevas sin justificación arquitectónica
✅ Usar lenguaje ubicuo del dominio en todos los nombres
✅ Extender patrones existentes antes de crear nuevos
```

---

## ¿Por qué existe?

Previene la deuda técnica estructural más difícil de revertir:
- Lógica de negocio acoplada a frameworks
- Módulos imposibles de testear en aislamiento
- Cambios en infraestructura que rompen reglas de negocio
