# 🧪 Rule 30 — Testing & Quality

> Cada cambio de comportamiento tiene validación automática. Sin tests, no hay merge.

---

## Qué se testea y cómo

```
Domain logic      → Unit tests (JUnit 5 + Mockito)
Use cases         → Integration tests (Spring Test)
Repositories      → Integration tests con DB real o H2
Edge cases        → En todos los niveles
```

### Ejemplos de edge cases que siempre se cubren

```
- null en parámetros obligatorios
- lista vacía cuando se esperaba al menos un elemento
- valores en el límite exacto (ej: balance == amount)
- inputs inválidos (strings vacíos, negativos, fuera de rango)
```

---

## Tests estables vs. tests frágiles

```java
// ✅ Test estable: valida comportamiento observable
@Test
void shouldRejectLoanWhenIncomeBelowMinimum() {
    var result = service.evaluate(applicantWithIncome(500));
    assertThat(result.isEligible()).isFalse();
}

// ❌ Test frágil: valida implementación interna
@Test
void shouldCallRepositoryOnce() {
    service.evaluate(applicant);
    verify(repository, times(1)).findById(any()); // Se rompe con cualquier refactor
}
```

| ✅ Hacer | ❌ Evitar |
|----------|-----------|
| Mockear dependencias externas (DB, HTTP) | Mockear entidades de dominio |
| Assertar en outputs y estado observable | Assertar en llamadas internas |
| Tests deterministas | Tests dependientes de orden o tiempo |

---

## PR Checklist (antes de merge)

```
[ ] El código compila sin errores ni warnings relevantes
[ ] Todos los tests pasan
[ ] Se agregaron tests para el comportamiento nuevo o modificado
[ ] No hay archivos modificados fuera del scope del PR
[ ] No se agregaron dependencias sin aprobación
[ ] No se rompieron contratos públicos
[ ] No hay datos sensibles en el código ni en los tests
```

---

## ¿Por qué existe?

Previene los problemas más costosos en producción:
- Bugs que regresan porque no había test de regresión
- PRs que se mergean sin validación automática
- Refactors que rompen comportamiento sin que nadie lo detecte
