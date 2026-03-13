# 🤖 Agents

Cada agente representa un **rol técnico específico** con responsabilidad única.
Se invocan desde el chat de Cursor con `@nombre-del-agente`.

---

## ⚡ Invocación

```bash
# Modo Ask (consultas, análisis, diseño)
@planner Necesito planificar la implementación de X
@architect ¿Cómo diseñamos el módulo Y?
@reviewer Revisá este código antes del merge

# Modo Agent (generación de código)
@implementer Implementá el caso de uso Z
@test-engineer Agregá tests para el servicio W
```

---

## 📋 Índice

| Agente | Rol | Modo sugerido |
|--------|-----|---------------|
| [`planner`](planner/) | Tech Lead — planificación y alcance | Ask |
| [`architect`](architect/) | Staff Engineer — diseño y estructura | Ask |
| [`implementer`](implementer/) | Senior Engineer — implementación estricta | Agent |
| [`debugger`](debugger/) | Incident Engineer — diagnóstico de errores | Ask / Agent |
| [`refactorer`](refactorer/) | Refactoring Engineer — mejora segura | Agent |
| [`test-engineer`](test-engineer/) | QA Engineer — tests y regresiones | Agent |
| [`reviewer`](reviewer/) | PR Reviewer — revisión antes de merge | Ask |
| [`security-compliance`](security-compliance/) | Security Reviewer — riesgos y compliance | Ask |

---

## 🔄 Pipelines

```
Feature:   @planner → @architect → @implementer → @test-engineer → @reviewer → @security-compliance
Bug fix:   @debugger → @implementer → @test-engineer → @reviewer
Refactor:  @architect → @refactorer → @test-engineer → @reviewer
```

> Todos los agentes respetan las reglas definidas en `.cursor/rules/`.
