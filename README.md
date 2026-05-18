# Práctica de Desarrollo SPEC: Traductor de Código "Humano" a SQL

## 1. Contexto del Proyecto
En el desarrollo de software y la gestión de datos, el acceso a bases de datos relacionales a menudo se ve limitado por el conocimiento técnico del lenguaje SQL. Para solventar esta barrera, se propone la creación de un **Traductor de Código "Humano" a SQL**, una interfaz web/desktop simple que actúa como puente entre los usuarios de negocio y los repositorios de datos.

A diferencia de un desarrollo tradicional, utilizaremos **SPEC-Driven Development (SDD)**. La labor principal no es escribir el código directamente, sino actuar como **Arquitectos de Software y Product Owners**. Se debe redactar la documentación técnica y las instrucciones del sistema necesarias para que una Inteligencia Artificial (Gemini, Claude, ChatGPT) genere el sistema completo sin errores y bajo reglas de negocio estrictas.

---

## 2. El Reto Técnico
El sistema consiste en una interfaz limpia y minimalista donde el usuario describe en lenguaje natural los datos que desea obtener, y la aplicación devuelve de manera inmediata la sentencia SQL estructurada y optimizada.

### Requisitos Clave de la Interfaz y Flujo
* **Área de texto para Lenguaje Natural:** Componente de entrada donde el usuario describe la consulta de forma coloquial (ej. *"Dame los nombres de los usuarios que se registraron el mes pasado y gastaron más de 50 dólares"*).
* **Botón de Procesar:** Desencadenador de la acción que envía la petición al motor de procesamiento interno.
* **Bloque de Código Resultante:** Componente de salida con formato enriquecido (sintaxis resaltada) que muestra el código SQL generado.
* **Foco del SPEC (Definición del System Prompt):** El núcleo técnico del proyecto radica en diseñar el *System Prompt* óptimo que la aplicación enviará internamente a una API de LLM. Este prompt debe garantizar que el modelo entienda el esquema de la base de datos (hipotética o configurada) y devuelva **únicamente** la sentencia SQL válida, sin texto introductorio ni explicaciones adicionales.

### Modelo de Datos Sugerido para la Gestión de Consultas
Para el control y auditoría de las traducciones dentro de la aplicación, se sugiere el siguiente esquema:

* **Entidad: Usuario/Sesión (Session)**: Representa la sesión activa que realiza las consultas.
    * `id_sesion` (String): Identificador único de la sesión de uso.
    * `fecha_creacion` (Timestamp): Momento en que se inició la sesión.
* **Entidad: Historial de Traducción (TranslationHistory)**: Almacena el flujo de peticiones y respuestas.
    * `id_traduccion` (String): Identificador único alfanumérico.
    * `input_natural` (Text): El texto en lenguaje natural introducido por el usuario.
    * `output_sql` (Text): La sentencia SQL generada por el LLM.
    * `estado` (Enum): ÉXITO, ERROR.
    * `tiempo_respuesta` (Float): Tiempo empleado en segundos por la API.

---

## 3. Entrega y Estructura de Documentación
Se deberá crear una carpeta llamada `/human-to-sql` en el espacio de GitHub con los siguientes archivos Markdown. Cada uno cumple un propósito estricto dentro del marco SDD:

| Archivo | Propósito |
| :--- | :--- |
| **`architecture.md`** | Define la organización del código (Frontend vs Backend/API wrapper) y la conexión con el endpoint del LLM. |
| **`spec.md`** | Define las funciones de traducción, la estructura exacta del **System Prompt**, la gestión de errores de la API y los parámetros de temperatura del modelo. |
| **`agents.md`** | Define roles para la IA: **Prompt Engineer / Senior Developer** (diseño del flujo y código), **QA Tester** (validación de SQL generado) y **Documentador**. |
| **`decisions.md`** | Justifica la pila tecnológica (ej. Python con Streamlit o FastAPI, librerías de clientes oficiales de OpenAI/Google, y validación de sintaxis SQL). |
| **`constitution.md`** | Reglas de estilo y restricciones: Código e interfaces en inglés, comentarios en español, y formateo estricto del bloque de código SQL de salida. |
| **`readme.md`** | Descripción general del proyecto, arquitectura conceptual y guía rápida para levantar la interfaz. |

---

## 4. Flujo de Trabajo (SPEC-Driven Development)
1. **Redacción**: Asegurar la consistencia absoluta entre los archivos (ej. el esquema de prompts definido en `spec.md` debe alinearse con el flujo del agente en `agents.md`).
2. **Prompting**: Subir los archivos Markdown estructurados a la IA de desarrollo con la siguiente instrucción:
   > *"Analiza estos ficheros de especificación. Siguiendo estrictamente sus directrices, genera la aplicación del Traductor de Código 'Humano' a SQL. Asegúrate de que los agentes definidos en agents.md cumplan su función, el System Prompt sea inyectado correctamente y se respete la constitution.md"*.
3. **Validación**: Ejecutar la interfaz web. Probar la generación de código SQL con diferentes niveles de complejidad en lenguaje natural. Si la IA devuelve texto plano explicativo o un SQL erróneo, **no corregir el código fuente a mano**. Se debe ajustar el System Prompt en `spec.md` y solicitar una nueva iteración.

---

## 5. Listado de Tareas de Implementación
Las siguientes actividades representan el roadmap técnico a seguir para el despliegue del proyecto:

- [ ] **Fase 1: Diseño del SPEC**
  - [ ] Escribir el *System Prompt* base incluyendo reglas de "No explicaciones".
  - [ ] Definir el esquema de base de datos de ejemplo que el LLM usará como contexto para traducir.
- [ ] **Fase 2: Estructura del Proyecto**
  - [ ] Crear la estructura de archivos Markdown en la carpeta `/human-to-sql`.
  - [ ] Validar la consistencia de tipos y nombres de funciones en `spec.md`.
- [ ] **Fase 3: Generación y QA**
  - [ ] Pasar las especificaciones a la IA generadora de código.
  - [ ] Verificar que el componente visual de salida renderice correctamente los bloques de código SQL (` ```sql `).
  - [ ] Validar el manejo de excepciones cuando la API del LLM no esté disponible.

---

## 6. Rúbrica de Evaluación
* **Calidad de la Especificación del Prompt**: El prompt del sistema debe ser robusto, mitigar al 100% las alucinaciones de la IA y forzar salidas puramente en formato SQL.
* **Diseño de la Interfaz**: Cumplimiento estricto de los tres componentes visuales requeridos (input, botón, bloque de código estructurado).
* **Modularidad y Decisiones**: Justificación del stack tecnológico elegido para el procesamiento de lenguaje natural en tiempo real.
* **Cumplimiento Normativo (Constitución)**: El código final generado por la IA respeta el idioma de los comentarios, tipado de datos y estilos de nombrado de funciones.
* **Robustez**: El sistema procesa correctamente las respuestas, controlando errores de sintaxis o timeouts con la API del modelo de lenguaje.
