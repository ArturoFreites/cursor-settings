# 🤖 Cursor AI Config — Backend Agents & Rules

> Sistema de agentes especializados y reglas globales para desarrollo backend con **Java + Spring Boot**, **DDD** y **Arquitectura Hexagonal**.

---

## 📁 Estructura

```
.cursor/
├── agents/              # Agentes con roles específicos
│   ├── planner/         # Tech Lead — planificación de entregas
│   ├── architect/       # Staff Engineer — diseño y estructura
│   ├── implementer/     # Senior Engineer — implementación estricta
│   ├── debugger/        # Incident Engineer — diagnóstico de bugs
│   ├── refactorer/      # Refactoring Engineer — mejora sin romper
│   ├── test-engineer/   # QA Engineer — tests útiles y estables
│   ├── reviewer/        # PR Reviewer — revisión antes de merge
│   └── security-compliance/ # Security Reviewer — riesgos y compliance
└── rules/               # Reglas globales aplicadas a todos los agentes
    ├── 00-project/      # Restricciones base del proyecto
    ├── 10-backend-architecture/ # DDD + Hexagonal
    ├── 20-style-and-errors/     # Estilo, errores y logs
    └── 30-testing-and-quality/  # Testing y PR checklist
```

---

## 🧠 Agentes disponibles

| Agente | Rol | Cuándo usarlo |
|--------|-----|---------------|
| [`@planner`](.cursor/agents/planner/) | Tech Lead | Antes de implementar algo complejo |
| [`@architect`](.cursor/agents/architect/) | Staff Engineer | Cambios estructurales o nuevos módulos |
| [`@implementer`](.cursor/agents/implementer/) | Senior Engineer | Cuando necesitás código escrito |
| [`@debugger`](.cursor/agents/debugger/) | Incident Engineer | Para diagnosticar errores |
| [`@refactorer`](.cursor/agents/refactorer/) | Refactoring Engineer | Mejorar estructura sin cambiar comportamiento |
| [`@test-engineer`](.cursor/agents/test-engineer/) | QA Engineer | Agregar tests de regresión y edge cases |
| [`@reviewer`](.cursor/agents/reviewer/) | PR Reviewer | Antes de hacer merge |
| [`@security-compliance`](.cursor/agents/security-compliance/) | Security Reviewer | Revisión de seguridad y compliance |

---

## 🔄 Pipelines recomendados

### ✨ Nueva feature
```
@planner → @architect → @implementer → @test-engineer → @reviewer → @security-compliance
```

### 🐛 Bug fix
```
@debugger → @implementer → @test-engineer → @reviewer
```

### ♻️ Refactor
```
@architect → @refactorer → @test-engineer → @reviewer
```

---

## 📐 Reglas globales

Todas las reglas se aplican automáticamente a cada agente (`alwaysApply: true`):

| Regla | Descripción |
|-------|-------------|
| [`00-project`](.cursor/rules/00-project/) | Restricciones base: no romper contratos, no agregar deps sin aprobación |
| [`10-backend-architecture`](.cursor/rules/10-backend-architecture/) | Respeto estricto de capas DDD + Hexagonal |
| [`20-style-and-errors`](.cursor/rules/20-style-and-errors/) | Estilo consistente, errores accionables, logs seguros |
| [`30-testing-and-quality`](.cursor/rules/30-testing-and-quality/) | Tests estables, PR checklist antes de merge |

---

## ⚡ Uso rápido

```
# Planificar antes de implementar
@planner Necesito implementar un nuevo endpoint de pagos con validación

# Diseñar la solución
@architect ¿Cómo modelamos la entidad Payment respetando el dominio actual?

# Implementar
@implementer Implementá el caso de uso CreatePaymentUseCase según el diseño acordado

# Testear
@test-engineer Agregá tests de regresión para CreatePaymentUseCase

# Revisar antes de merge
@reviewer Revisá el PR del flujo de pagos
```

---

## 📏 Regla de oro

> **Un agente = un rol.**
> Nunca pedirle a un agente que haga trabajo de otro.
> El contexto del pipeline garantiza calidad sin caos.

---

## 🛠 Stack asumido

- **Lenguaje:** Java 17
- **Framework:** Spring Boot 3
- **Arquitectura:** Hexagonal / DDD / Clean Architecture
- **Build:** Gradle o Maven (según el repo)
- **Tests:** JUnit 5 + Mockito + Spring Test
