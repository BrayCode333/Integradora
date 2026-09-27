# UniBot — Primera Fase de Desarrollo

## ¿Qué contiene este documento?

Este documento presenta la **primera fase de desarrollo de UniBot**, enfocada en el pensamiento sistémico y la ingeniería de requisitos. Su propósito es definir cómo se caracteriza el sistema, cómo se propone desarrollarlo, cuáles son sus requerimientos iniciales y cómo interactúan sus usuarios antes de comenzar la implementación. Esta fase no contempla código fuente.

## 1. Caracterización del sistema

UniBot busca modernizar la atención a estudiantes de primer ingreso mediante un asistente virtual que proporcione orientación académica y técnica de acuerdo con la carrera del estudiante. También busca disminuir las consultas repetitivas y evitar respuestas correspondientes a otras carreras.

El documento identifica:

- **Entradas:** código institucional, credenciales administrativas, preguntas del estudiante, archivos de estudiantes, carreras y registro de sesiones, además de la configuración y credenciales de la API de IA.
- **Procesos:** autenticación, identificación del estudiante y su carrera, recuperación de temas permitidos, construcción del contexto y prompt, consulta al modelo de IA, registro de mensajes, conteo de caracteres, cálculo de costos, almacenamiento del historial, auditoría y cierre forzado de sesiones.
- **Salidas:** respuestas del asistente, mensajes de acceso denegado o error, sesiones registradas, costos calculados, estadísticas de auditoría e historiales de conversaciones en archivos de texto.
- **Subsistemas:** interfaz de consola, autenticación, gestión de estudiantes, gestión de carreras y temas, gestión de sesiones, PromptBuilder, integración con la API de IA, persistencia en archivos y auditoría.
- **Entorno:** universidad, estudiantes de primer ingreso, administradores, Node.js, sistema de archivos local y un proveedor externo de inteligencia artificial.

## 2. Modelo de proceso y marco de trabajo

Se propone combinar **Desarrollo Incremental** con prácticas de **Scrum**. La idea es construir UniBot mediante versiones funcionales sucesivas y organizar el trabajo en ciclos cortos llamados Sprints.

El documento plantea cinco Sprints:

1. **Sprint 1 — Fundamentos y acceso:** requisitos consolidados, estructura conceptual, menú principal y autenticación de los dos tipos de usuario.
2. **Sprint 2 — Gestión académica:** registro de estudiantes y consulta de carreras, directores, edificios y temas permitidos.
3. **Sprint 3 — Sesiones y auditoría:** creación de sesiones, conteo de mensajes y caracteres, cálculo de costos, auditoría y cierre forzado.
4. **Sprint 4 — Chat y RAG simplificado:** construcción del PromptBuilder, restricción por carrera y conexión con la API de inteligencia artificial.
5. **Sprint 5 — Trazabilidad y calidad:** guardado del historial, manejo de errores, documentación, pruebas y preparación de la entrega.

## 3. Product Backlog inicial

El documento incluye una sección destinada al **Product Backlog inicial**. En el archivo proporcionado, esta sección aparece como encabezado, pero no contiene el listado detallado de elementos.

## 4. Modelo de casos de uso

Se identifican dos actores principales:

- **Estudiante**
- **Administrador del Sistema**

### Casos de uso del estudiante

- **Autenticarse:** introduce su código institucional y el sistema verifica si está registrado.
- **Consultar al asistente virtual:** realiza una pregunta durante una sesión de chat activa.
- **Recibir respuesta restringida:** el sistema proporciona a la IA el nombre, carrera y temas permitidos del estudiante para restringir el contexto.
- **Finalizar sesión:** el estudiante indica la palabra de salida; el sistema calcula el costo, cierra la sesión y guarda el historial.

### Casos de uso del administrador

- **Autenticarse:** ingresa la contraseña maestra obtenida desde la configuración de entorno.
- **Registrar estudiantes:** agrega nuevos estudiantes al archivo `estudiantes.csv`.
- **Gestionar temas permitidos:** administra las reglas de temas asociados a cada carrera.
- **Auditar sesiones:** consulta la cantidad de sesiones activas y cerradas.
- **Cerrar sesiones activas:** ejecuta un cierre forzado de las sesiones activas y calcula los costos acumulados.

## 5. Reglas de negocio

El documento establece las siguientes reglas:

1. Un estudiante solo puede acceder si su código existe en `estudiantes.csv`.
2. La carrera del estudiante determina los temas que puede consultar.
3. `PromptBuilder` debe incluir el nombre, la carrera y el arreglo exacto de temas permitidos.
4. Las preguntas que estén fuera del listado deben rechazarse amablemente.
5. El costo se calcula únicamente cuando una sesión cambia a estado **Cerrada**.
6. El costo corresponde a **caracteres totales × 2 COP**.
7. El administrador puede cerrar forzosamente las sesiones activas.
8. El historial de conversación debe conservarse al finalizar la sesión.

## 6. Tablero Kanban

El documento también incluye una sección destinada al **Tablero Kanban** como parte de la organización del desarrollo del proyecto.

---

### Resumen

En conjunto, esta primera fase define las bases de UniBot antes de programarlo: qué problema busca atender, cuáles son sus entradas, procesos y salidas, cómo se organizará su desarrollo, qué usuarios interactúan con el sistema, qué acciones puede realizar cada uno y cuáles son las reglas que debe cumplir el sistema.
