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
- El prompt que se enviara a la IA sera el siguiente:
```text
Prompt a traducir del usuario
Esquema de la BBDD
Dado este prompt en lenguaje humano y este esquema completo de base de datos, traduceme el prompt a lenguaje sql y devuleveme unicamente el prompt traducido en formato SQL, no es requirido ningun otro tipo de informacion, unicamente el prompt traducido
```

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
- El usuario introducira en el input de la web que prompt quiere traducir
- El usuario le dara al boton de traducir
- La web hara una peticion al backend de flask
- El backend hara una llamada a la api del LLM con el prompt del usuario y un prompt mas detallado (ver mas arriba)
- Si el llm no esta disponible mostrara un error formateado en la web
- El llm devolvera la respesta y se guardara en la BBDD
- El backend devolvera la respuesta a la web

### CU-02: Ver todas las traducciones de la BBDD
- El usuario le dara a un boton para ver las traducciones de la base de datos
- La web hara una llamada al backend
- El backend consultara la BBDD
- Devolvera el resultado a la web
- La web mostrara todos los datos de manera bonita y estructurada


## 4. Reglas de validacion

## 5. Reglas de validación

| Campo | Regla|
|-------|------|
| id* | No vacío. Longitud 2–100 caracteres. alfanumerico |
| input_natural | No puede estar vacio, Logintid 10 - 50 caracteres, detallado |
| output_sql | Tiene que ser una conuslta sql |

