# Zorro-post1-u9 — Suite de Pruebas Unitarias con JUnit 5 y Mockito

Microservicio de gestión de productos con **suite completa de pruebas unitarias**
usando **JUnit 5 + Mockito**, cubriendo escenarios exitosos, de error, de borde
y verificación avanzada con `ArgumentCaptor`.

---

## Pruebas Implementadas

| Prueba | Tipo | Técnica |
|---|---|---|
| `crear_datosValidos_retornaProductoGuardado` | Happy path | `@Mock` + `verify()` |
| `buscarPorId_existente_retornaProducto` | Happy path | `@Mock` + `assertEquals` |
| `buscarPorId_noExistente_lanzaRuntimeException` | Error | `assertThrows` |
| `crear_nombreInvalido_lanzaIllegalArgumentException` | Error | `@ParameterizedTest` + `@NullAndEmptySource` |
| `crear_precioInvalido_lanzaIllegalArgumentException` | Error | `@ParameterizedTest` + `@ValueSource` |
| `crear_nombreConEspacios_guardaNombreNormalizado` | Borde | `ArgumentCaptor` |
| `eliminar_productoExistente_llamaDeleteById` | Verificación | `verify()` + `doNothing()` |

---

## Validaciones de Negocio Cubiertas

- `nombre == null` o en blanco → `IllegalArgumentException`
- `nombre` con espacios al inicio/fin → se normaliza con `strip()` antes de persistir
- `precio == null` o `<= 0` → `IllegalArgumentException`
- `stock == null` o `< 0` → `IllegalArgumentException`
- `id` inexistente en `buscarPorId` → `RuntimeException`
- `verifyNoInteractions(productoRepository)` confirma que el repositorio no es llamado cuando falla una validación

---

## Requisitos

- Java 21+
- Maven 3.9+

---

## Ejecución

```bash
git clone https://github.com/Kevinzorro/Zorro-post1-u9.git
cd Zorro-post1-u9
mvn test
```

