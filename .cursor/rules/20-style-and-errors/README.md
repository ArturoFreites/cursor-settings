# ✍️ Rule 20 — Style, Errors & Logging

> Mantiene el código consistente, los errores accionables y los logs seguros.

---

## Estilo de código

```java
// ✅ Métodos pequeños con nombres expresivos
private boolean hasEnoughFunds(BigDecimal amount) {
    return balance.compareTo(amount) >= 0;
}

// ❌ Métodos largos con lógica mezclada
public void process(Request req) {
    // 80 líneas de validación, lógica y persistencia mezcladas
}
```

| Principio | Detalle |
|-----------|---------|
| **Métodos pequeños** | Una responsabilidad por método |
| **Nombres expresivos** | El nombre debe explicar el qué, no el cómo |
| **Inyección por constructor** | Preferir sobre field injection (`@Autowired`) |
| **Sin side effects en mappers** | Los métodos de conversión no deben tener efectos secundarios |

---

## Manejo de errores

```java
// ✅ Excepción de dominio con mensaje accionable
throw new InsufficientFundsException(
    "Cannot transfer " + amount + ": balance is " + balance
);

// ❌ RuntimeException genérica
throw new RuntimeException("error");
```

- Usar las **excepciones de dominio existentes** en el repo
- Mensajes de error: **qué falló + por qué + qué input lo causó**
- No lanzar `RuntimeException` genérica salvo que sea el estándar del proyecto

---

## Logging seguro

```java
// ✅ Log en el borde del sistema con info útil
log.info("Loan application received: applicationId={}", applicationId);

// ❌ Log con datos sensibles
log.info("User {} applied with SSN {}", userId, ssn);  // NUNCA
```

| Regla | Detalle |
|-------|---------|
| **Loguear en los bordes** | Controllers, adapters, gateways — no en domain logic |
| **Sin PII en logs** | Nunca loguear emails, DNI, contraseñas, tokens |
| **Respetar niveles** | ERROR para fallas reales, INFO para eventos de negocio, DEBUG para desarrollo |

---

## ¿Por qué existe?

Previene los problemas de mantenibilidad y seguridad más frecuentes:
- Logs que exponen datos de usuarios en producción
- Errores imposibles de debuggear por mensajes vacíos
- Código difícil de leer y mantener por el equipo
