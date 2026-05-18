---
title: Traductor de lenguaje humano a sql
version: 0.1
date: 18/05/2026
---

# Constitución del Proyecto

## 1. Principios Fundamentales
* **La UX es lo primero:** La experiencia en de la aplicacion grafica tiene que ser buena. Los errores deben ser descriptivos y nunca mostrar un volcado de pila (traceback) de Python crudo al usuario final, a menos que esté activo el modo `--debug`.
* **Cero Magia:** El comportamiento de los comandos debe ser predecible y explícito. No se asumen configuraciones ocultas.

## 2. Reglas de Desarrollo y Estilo de Código
* **Tipado Estricto (Type Hinting):** Todo el código en `src/` debe estar estrictamente tipado. `mypy` se ejecutará en la integración continua (CI).
* **Formateo:** Uso obligatorio de `black` y `ruff` para linting y formateo de código.
* **Pruebas (Testing):** Cobertura mínima de pruebas del 80%. Cada nuevo comando debe incluir su respectivo test de integración usando `CliRunner`.

| Regla | Descripción |
|-------|-------------|
| R-01  | Toda función pública debe tener docstring con parámetros y valor de retorno. |
| R-02  | Toda consulta a la base de datos tiene que estar parametrizada para evitar sql injection |

---

## 3. Restricciones de seguridad

- **SQL Injection:** Uso obligatorio de parámetros en todas las consultas.
- **.env:** Uso de fichero .env con todos los datos de la conexion a la bd, api tokens, etc...
- **Seguridad de claves:** Ninguna clave tiene que estar hardcodeada en el codigo

---
