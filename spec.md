---
title: Traductor de lenguaje humano a sql
version: 0.1
date: 18/05/2026
---

# Especificacion: Human To Sql Translator

# spec.md - Especificacion funcional

## 1. Descripcion general

La aplicacion es una herramienta grafica escrita en python que permite introducir una consulta en lenguaje natural (ej: Dame los primeros 50 usuarios) y te lo traduce a sql usando una api de LLM.

## 2. Funcionalidades

- Iniciar sesion, cerrar sesion, escribir prompt, listar traducciones

## 3. Modelo de datos

### Entidad: usuarios

| Campo | Tipo | Obligatorio | Descripcion |
| ----- | ---- | ----------- | ----------- |
|  id   | string primary key | si | Identificador único de la sesión de uso. |
| fecha_creacion | datetime | si | Momento en el que se inicio sesion |

### Entidad: historial_traduccion

| Campo | Tipo | Obligatorio | Descripcion |
| ----- | ---- | ----------- | ----------- |
|  id_traduccion   | string primary key | si | Identificador único alfanumerico |
| input_natural | text | si | El texto en lenguaje natural introducico por el usuario |
| output_sql | text | si | Sentencia sql generada por el llm |
| estado | enum("exito","error" | si | Si ha sido un exito o error la traduccion |
| tiempo_respuesta | float | si | Tiempo que ha tardado la api en responder |

## 4. Casos de uso

### CU-01: Introducir prompt en lenguaje humano
- El sistema pedira la sentencia en lenguaje humano
- El sistema comprobara que la sentencia no este vacia
- El sistema hara una llamada a la api del llm
- El sistema comprobara si la respuesta del llm ha sido exitosa o no
- En caso de haber sido exitosa el sistema introducira en la tabla historial_traduccion los datos correspondientes (input_natural, output_sql, estado, tiempo_respuesta)
