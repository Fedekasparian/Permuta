# Entrega 2 — Arquitectura y modelo de objetos

**Proyecto:** AutoCar
**Entrega 2 · 14/09/2026** · Bernal Justino · Marino Lautaro · Kasparian Federico
Programación en Ambiente Web · UNLu Mercedes · 2026

Este documento cubre los dos puntos teóricos de la entrega 2: la arquitectura de la aplicación y el modelo de objetos del back-end. No incluye código: eso empieza en la entrega 3, cuando se implementa el alcance mínimo acordado.

---

## 1. Arquitectura de la aplicación

### 1.1 Estilo general

Arquitectura **cliente-servidor en tres capas**, sin microservicios ni colas de mensajes: el volumen y la complejidad del proyecto no lo justifican, y la consigna valora poder explicar y modificar cualquier parte de la aplicación.

- **Presentación** — front-end en el navegador, consume la API por HTTP.
- **Aplicación** — API REST que concentra toda la lógica de negocio y las reglas de autorización.
- **Datos** — base de datos relacional, accedida sólo desde la capa de aplicación.

Los servicios de terceros (mapas, LLM, fuentes externas para la meta-búsqueda) se consultan **únicamente desde el back-end**, nunca desde el navegador: así ninguna clave de API queda expuesta en el cliente.

### 1.2 Diagrama de componentes

```
┌────────────┐      HTTP/JSON      ┌──────────────┐      SQL      ┌────────────┐
│  Navegador │ ───────────────────▶│   API REST   │──────────────▶│ PostgreSQL │
│ (front-end)│◀─────────────────── │  (Node.js)   │◀───────────── │            │
└────────────┘                     └──────┬───────┘                └────────────┘
                                           │
                                           │ HTTP (server-to-server)
                                           ▼
                          ┌────────────────────────────────┐
                          │  Servicios externos             │
                          │  · Tiles de mapa (OpenStreetMap)│
                          │  · API de LLM (tasación/asist.) │
                          │  · API de Mercado Libre (meta-  │
                          │    búsqueda)                    │
                          └────────────────────────────────┘
```

### 1.3 Stack y justificación

| Capa | Elección | Por qué |
|---|---|---|
| Front-end | JavaScript nativo (módulos ES) + Web Components, sin framework | Es lo que exige la consigna (JS puro, librerías de terceros sujetas a consulta) y lo que la materia busca ejercitar; evita depender de la aprobación de un framework |
| Back-end | Node.js + API REST | Un solo lenguaje para las tres personas del grupo, buena documentación, amplia oferta de hosting gratuito para el despliegue de la entrega 3 |
| Base de datos | PostgreSQL | El dominio tiene entidades con relaciones claras (usuario, publicación, propuesta, conversación) que se resuelven bien con SQL; soporta los filtros combinados de la búsqueda sin necesidad de un motor aparte |

### 1.4 Capas del back-end

La API se organiza en tres niveles, cada uno con una responsabilidad única:

| Nivel | Responsabilidad |
|---|---|
| Rutas / controladores | Reciben la request, validan la forma de los datos de entrada y devuelven la respuesta HTTP. No contienen reglas de negocio. |
| Servicios | Contienen la lógica de negocio: qué puede hacer cada plan, cómo se calcula una tasación, cómo cambia de estado una propuesta de canje. |
| Acceso a datos | Traduce las operaciones de los servicios en consultas a PostgreSQL. Es la única capa que conoce el esquema de la base. |

Esta separación es deliberadamente simple (no hay capa de dominio ni patrones adicionales): alcanza para que cualquiera de los tres integrantes pueda ubicar y modificar una funcionalidad sin tener que entender todo el sistema primero.

### 1.5 Autenticación y autorización

- **Autenticación**: contraseña con hash (bcrypt), sesión con cookie `httpOnly` y token CSRF en los formularios que cambian estado.
- **Autorización por rol**: cada endpoint valida el plan activo del usuario (Free, Meta-searching, Uso Portal, Ambas, Admin) antes de responder — el control nunca depende de ocultar un botón en el cliente.
- **Autorización por recurso**: un usuario sólo puede editar sus propias publicaciones, ver sus propias conversaciones y sus propias búsquedas guardadas. Se valida comparando el dueño del recurso contra el usuario de la sesión en cada request (prevención de IDOR).

### 1.6 Servicios externos

| Servicio | Qué resuelve | Quién lo consume |
|---|---|---|
| Tiles de mapa (OpenStreetMap) | Render del mapa de publicaciones | Front-end carga los tiles directamente (son públicos); el back-end sólo entrega las coordenadas ofuscadas |
| API de LLM  (groq)| Tasación por comparables (mejora asistida) y asistente de ayuda | Sólo el back-end; la clave de API no sale del servidor |
| API pública de Mercado Libre o scraper de sitios afines | Meta-búsqueda en fuentes externas | Sólo el back-end, con caché de resultados para no repetir consultas |

### 1.7 Chat entre usuarios

La versión comprometida usa *polling* (el cliente pregunta cada pocos segundos si hay mensajes nuevos), que es simple de implementar y de explicar. Pasar a WebSocket/SSE para entrega en tiempo real queda como mejora condicional: cambia el mecanismo de transporte, no el modelo de datos de la sección 2.

---

## 2. Modelo de objetos (back-end)

### 2.1 Entidades principales

| Entidad | Atributos principales | Notas |
|---|---|---|
| Usuario | id, nombre, email, contraseña (hash), teléfono, localidad, ubicación base, rol, verificado, fecha de alta | El rol distingue sólo usuario / admin; el plan se resuelve con Suscripción |
| Suscripción | id, usuario_id, tipo de plan (Free / Meta-searching / Uso Portal / Ambas), nivel (Bronce/Plata/Oro/Platino, si aplica), estado, fecha inicio, fecha fin | Simulada: no hay pasarela de pago real ???|
| Publicación | id, usuario_id, marca, modelo, año, kilometraje, estado del vehículo, precio, acepta canje (sí/no), ubicación ofuscada, estado de la publicación (activa/pausada/cerrada), fecha | Entidad central del portal |
| Foto | id, publicación_id, url, orden | Cantidad máxima según el plan del publicador |
| CatálogoMarcaModelo | marca, modelo, versión | Mantenido por el admin (ABM) |
| PropuestaCanje | id, publicación_origen_id, publicación_destino_id, usuario_propone_id, diferencia en efectivo, estado, fecha | Sólo aplica si la publicación destino tiene canje habilitado |
| Conversación | id, publicación_id, usuario_1_id, usuario_2_id | Une a un interesado con un publicador alrededor de un vehículo |
| Mensaje | id, conversación_id, usuario_id, texto, fecha, leído | — |
| BúsquedaGuardada | id, usuario_id, criterios (marca, modelo, año, precio máximo, etc.), fecha del último reporte | Sólo para planes Meta-searching / Ambas |
| Coincidencia | id, búsqueda_id, fuente (portal / externa), referencia al origen, fecha | Resultado generado por la meta-búsqueda |
| Tasación | id, publicación_id, valor mínimo estimado, valor máximo estimado, comparables usados, fecha | Se recalcula sólo si cambian los datos del vehículo |
| Reporte | id, tipo (publicación / usuario), objetivo_id, usuario_reporta_id, motivo, estado | Cola de moderación |
| Favorito | usuario_id, publicación_id | Relación simple usuario–publicación |

### 2.2 Relaciones entre entidades

- Usuario 1 — N Suscripción (histórico de planes; una sola vigente a la vez).
- Usuario 1 — N Publicación (según lo permita su plan activo).
- Publicación 1 — N Foto.
- Publicación 1 — N PropuestaCanje, como origen o como destino.
- Publicación 1 — N Conversación; Conversación 1 — N Mensaje.
- Usuario 1 — N BúsquedaGuardada (según lo permita su plan).
- BúsquedaGuardada 1 — N Coincidencia.
- Publicación 1 — 0/1 Tasación vigente.
- Usuario 1 — N Reporte (como quien reporta).
- Usuario N — N Publicación a través de Favorito.

### 2.3 Qué no cambia el alcance condicional

Las funcionalidades que están en el tramo condicional de la entrega 1 (flujo completo de canje, matching con IA, chat en tiempo real) **no agregan entidades nuevas**: reutilizan PropuestaCanje, Publicación y Mensaje, y sólo cambian el comportamiento o el transporte. Esto mantiene el modelo de datos estable aunque el alcance final se ajuste con los docentes en la entrega 2 y 3.

---

## 3. Cumplimiento de la consigna (entrega 2)

| Requisito | Estado |
|---|---|
| Wireframes: homepage, una página por sección y formularios de administración | [wireframes.md](wireframes.md) — contenido base para el archivo de Figma |
| Arquitectura de la aplicación | § 1 de este documento |
| Modelo de objetos (back-end) | § 2 de este documento |
| Repositorio Git público con tag por entrega | Tag `entrega-2` al momento de la entrega |
