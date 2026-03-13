# 📌 Rule 00 — Project Base

> Restricciones no negociables que aplican a **toda** interacción de Cursor con el backend.

---

## ¿Qué es una rule en Cursor?

Las rules son instrucciones que Cursor aplica automáticamente en cada respuesta.
No hay que invocarlas: están siempre activas (`alwaysApply: true`).

---

## Alcance

Esta regla aplica a todos los contextos:

- ✅ Features nuevas
- ✅ Bug fixes
- ✅ Refactors
- ✅ Revisiones de código

---

## Principios base

| Principio | Descripción |
|-----------|-------------|
| **Cambios mínimos** | Tocar solo lo necesario para cumplir el objetivo |
| **Código explícito** | Preferir claridad sobre ingeniosidad |
| **Contratos respetados** | No romper APIs, DTOs ni métodos públicos |
| **Seguridad por defecto** | Nunca exponer secretos ni datos sensibles |

---

## Restricciones clave

```
❌ No agregar dependencias sin aprobación explícita
❌ No romper contratos públicos (endpoints, DTOs, métodos)
❌ No inventar módulos, paquetes o capas nuevas
❌ No exponer credenciales, tokens o API keys
❌ No hacer refactors especulativos en archivos no relacionados
```

---

## ¿Por qué existe?

Previene los errores más comunes al usar AI en codebases reales:

- Refactors destructivos no pedidos
- PRs que tocan decenas de archivos sin necesidad
- Alucinaciones de módulos o dependencias inexistentes
- Incidentes de seguridad por exposición accidental de secrets
