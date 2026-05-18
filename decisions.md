---
title: ""
version: ""
date: ""
---

## 3. `decisions.md` (Registro de Decisiones Arquitectónicas)

# Registro de Decisiones Arquitectónicas (ADR)

## ADR 001: Elección del Framework para la GUI
* **Estado:** ACEPTADO
* **Fecha:** 2026-05-18

### Contexto
Necesitamos un framework en Python para gestionar una interfaz grafica

### Opciones Consideradas
1. **`FLASK`**: Interfaz web grafica 

### Decisión
Se elige **`FLASK`**.

### Consecuencias
* **Pros:** Código más limpio y legible usando type hints nativos de Python. Validación automática.
* **Contras:** Añade una dependencia externa.

## ADR-001: Elección de base de datos — MySQL
**Fecha:** 2026-04-05  

**Estado:** Aceptado

**Contexto:**  
Se necesita un motor de base de datos relacional para persistir los contactos con soporte para consultas de búsqueda, integridad de datos y fácil despliegue local.

**Opciones consideradas:**
- MySQL 8.0
- PostgreSQL 16
- SQLite 3

**Decisión:**  
Se elige **MySQL 8.0**.

**Justificación:**
- Es el requisito explícito del proyecto.
- Amplia documentación, soporte en hosting compartido y herramientas de administración
  maduras (phpMyAdmin, MySQL Workbench).
- Compatible con MariaDB, lo que facilita migraciones a entornos alternativos.

**Consecuencias:**
- Se requiere un servidor MySQL corriendo localmente o accesible en red.
- El driver elegido es `mysql-connector-python` (oficial de Oracle, sin dependencias C).

---
