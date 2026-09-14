# Presupuesto funcional

**Proyecto:** Permutá · **Entrega 1 · 31/08/2026**
Bernal Justino · Marino Lautaro · Kasparian Federico

---

## 1. Criterios de estimación

- **Unidad:** hora-persona de trabajo efectivo (no incluye tiempo de clase ni de estudio teórico).
- **Prioridad (MoSCoW):**
  - **Must** — sin esto la aplicación no cumple su objetivo. Comprometido.
  - **Should** — aporta valor sustancial pero la app funciona sin ello. Se compromete si la capacidad lo permite.
  - **Could** — deseable. Sólo si sobra tiempo.
- **Complejidad:** Baja (mecánico, sin decisiones de diseño) · Media (requiere diseño de solución) · Alta (incertidumbre técnica o integración con terceros).
- Las estimaciones incluyen implementación, prueba manual y ajuste; **no** incluyen la redacción de los informes de cada entrega, que se presupuesta aparte en el módulo M.

---

## 2. Módulos y funcionalidades

### A. Análisis y diseño *(entregas 1 y 2)* — 58 h

| ID | Funcionalidad | Prioridad | Compl. | h |
|---|---|---|---|---|
| A.1 | Propuesta general, presupuesto funcional y temporal, sitemap | Must | Media | 14 |
| A.2 | Wireframes: home, una página por sección y formularios de administración | Must | Alta | 20 |
| A.3 | Definición de arquitectura de la aplicación y justificación del stack | Must | Media | 10 |
| A.4 | Diseño del modelo de objetos y del modelo de datos (back-end) | Must | Alta | 14 |

### B. Infraestructura y base técnica — 42 h

| ID | Funcionalidad | Prioridad | Compl. | h |
|---|---|---|---|---|
| B.1 | Repositorio Git público, estrategia de ramas, convención de commits y tags por entrega | Must | Baja | 4 |
| B.2 | Esqueleto front-end: HTML semántico, router en JS, estructura de módulos | Must | Media | 10 |
| B.3 | Sistema de diseño: tipografía, paleta, componentes y grid responsivo *mobile-first* | Must | Media | 12 |
| B.4 | Setup back-end, conexión a base de datos y estructura de la API REST | Must | Media | 10 |
| B.5 | Entorno de despliegue y publicación del sitio | Must | Media | 6 |

### C. Autenticación y cuenta — 34 h

| ID | Funcionalidad | Prioridad | Compl. | h |
|---|---|---|---|---|
| C.1 | Registro con validación en cliente y en servidor | Must | Media | 6 |
| C.2 | Login / logout y manejo de sesión (hash de contraseña, cookie httpOnly, token CSRF) | Must | Media | 8 |
| C.3 | Verificación de email | Should | Media | 5 |
| C.4 | Recuperación de contraseña | Should | Media | 5 |
| C.5 | Perfil de usuario, edición y ubicación base | Must | Baja | 6 |
| C.6 | Roles y autorización por recurso (usuario / admin) | Must | Media | 4 |

### D. Publicaciones de vehículos — 46 h

| ID | Funcionalidad | Prioridad | Compl. | h |
|---|---|---|---|---|
| D.1 | Modelo de vehículo y catálogo de marcas / modelos / años | Must | Media | 8 |
| D.2 | Alta de publicación con formulario multi-paso y validaciones | Must | Alta | 12 |
| D.3 | Carga múltiple de imágenes con validación de tipo y tamaño y optimización | Must | Alta | 10 |
| D.4 | Edición, pausa y baja de publicación | Must | Baja | 5 |
| D.5 | Página pública de detalle de vehículo | Must | Media | 7 |
| D.6 | Estados de publicación e historial de operaciones (vendido / canjeado) | Must | Media | 4 |

### E. Búsqueda y exploración — 26 h

| ID | Funcionalidad | Prioridad | Compl. | h |
|---|---|---|---|---|
| E.1 | Home / feed de publicaciones con paginación | Must | Media | 8 |
| E.2 | Búsqueda por texto y filtros combinados | Must | Alta | 12 |
| E.3 | Ordenamiento, favoritos y búsquedas guardadas | Could | Baja | 6 |

### F. Mapa y geolocalización — 30 h

| ID | Funcionalidad | Prioridad | Compl. | h |
|---|---|---|---|---|
| F.1 | Geocodificación de la ubicación de la publicación con ofuscación por privacidad | Must | Media | 8 |
| F.2 | Render del mapa con marcadores y agrupamiento | Must | Alta | 12 |
| F.3 | Filtro por radio y cálculo de distancia desde el usuario | Should | Media | 6 |
| F.4 | Vista lista como *fallback* sin mapa | Should | Baja | 4 |

### G. Canje / permuta — 38 h

| ID | Funcionalidad | Prioridad | Compl. | h |
|---|---|---|---|---|
| G.1 | Modelo de propuesta de canje (uno a uno, con diferencia en efectivo) | Must | Alta | 8 |
| G.2 | Flujo completo: enviar, recibir, aceptar, rechazar y contraofertar | Must | Alta | 16 |
| G.3 | Bandeja de propuestas, máquina de estados y notificaciones | Must | Media | 8 |
| G.4 | Cierre de operación y registro en el historial | Should | Media | 6 |

### H. Chat entre usuarios — 32 h

| ID | Funcionalidad | Prioridad | Compl. | h |
|---|---|---|---|---|
| H.1 | Modelo de conversaciones y mensajes ligados a una publicación | Must | Media | 6 |
| H.2 | Bandeja de entrada y vista de conversación | Must | Media | 8 |
| H.3 | Entrega en tiempo real (WebSocket / SSE, con *polling* como plan B) | Must | Alta | 12 |
| H.4 | Indicadores de no leído, bloqueo y reporte de usuario | Should | Media | 6 |

### I. Tasación con IA — 24 h

| ID | Funcionalidad | Prioridad | Compl. | h |
|---|---|---|---|---|
| I.1 | Definición de variables de tasación y carga de la base de comparables | Must | Media | 6 |
| I.2 | Servicio de tasación (LLM sobre comparables) con caché de resultados | Must | Alta | 12 |
| I.3 | Interfaz de tasación: rango estimado, comparables, factores y *disclaimer* | Must | Media | 6 |

### J. Matching y recomendaciones con IA — 26 h

| ID | Funcionalidad | Prioridad | Compl. | h |
|---|---|---|---|---|
| J.1 | Captura de preferencias del usuario | Should | Baja | 5 |
| J.2 | Motor de compatibilidad de canje: score y brecha de valor entre vehículos | Should | Alta | 13 |
| J.3 | Interfaz de matches con la explicación de la recomendación | Should | Media | 8 |

### K. Asistente LLM y ayuda — 22 h

| ID | Funcionalidad | Prioridad | Compl. | h |
|---|---|---|---|---|
| K.1 | FAQ estática organizada por categorías | Must | Baja | 5 |
| K.2 | Asistente conversacional con contexto de la app y límite de uso por usuario | Should | Alta | 12 |
| K.3 | Formulario de contacto y reporte de problemas | Should | Baja | 5 |

### L. Administración y moderación — 20 h

| ID | Funcionalidad | Prioridad | Compl. | h |
|---|---|---|---|---|
| L.1 | Panel de moderación de publicaciones y cola de reportes | Must | Media | 8 |
| L.2 | Gestión de usuarios: suspender, restituir, asignar rol | Should | Media | 6 |
| L.3 | ABM de catálogo de marcas y modelos | Should | Baja | 6 |

### M. Calidad, seguridad y documentación — 38 h

| ID | Funcionalidad | Prioridad | Compl. | h |
|---|---|---|---|---|
| M.1 | Validación W3C de HTML y CSS y corrección de hallazgos | Must | Baja | 5 |
| M.2 | Pruebas crossbrowser y multipantalla | Must | Media | 8 |
| M.3 | Hardening: XSS, inyección SQL, CSRF, rate limiting, cabeceras de seguridad | Must | Alta | 12 |
| M.4 | Informe de consideraciones de seguridad por capa, en cada entrega | Must | Media | 8 |
| M.5 | README con requisitos y pasos de deployment | Must | Baja | 5 |

### N. Entrega final y exposición — 18 h

| ID | Funcionalidad | Prioridad | Compl. | h |
|---|---|---|---|---|
| N.1 | Datos de demostración y guion de la demo | Must | Baja | 6 |
| N.2 | Presentación audiovisual (máx. 15 min) y ensayo | Must | Media | 12 |

---

## 3. Resumen del presupuesto funcional

| Módulo | Must | Should | Could | Total |
|---|---:|---:|---:|---:|
| A. Análisis y diseño | 58 | — | — | **58** |
| B. Infraestructura y base técnica | 42 | — | — | **42** |
| C. Autenticación y cuenta | 24 | 10 | — | **34** |
| D. Publicaciones de vehículos | 46 | — | — | **46** |
| E. Búsqueda y exploración | 20 | — | 6 | **26** |
| F. Mapa y geolocalización | 20 | 10 | — | **30** |
| G. Canje / permuta | 32 | 6 | — | **38** |
| H. Chat entre usuarios | 26 | 6 | — | **32** |
| I. Tasación con IA | 24 | — | — | **24** |
| J. Matching con IA | — | 26 | — | **26** |
| K. Asistente LLM y ayuda | 5 | 17 | — | **22** |
| L. Administración y moderación | 8 | 12 | — | **20** |
| M. Calidad, seguridad y documentación | 38 | — | — | **38** |
| N. Entrega final y exposición | 18 | — | — | **18** |
| **TOTAL** | **361** | **87** | **6** | **454 h** |

### Contraste con la capacidad disponible

| Concepto | Horas |
|---|---:|
| Capacidad planificada (3 personas × 10 h/semana × 13 semanas) | 390 |
| Alcance **Must** (comprometido) | 361 |
| Margen sobre el núcleo | **29 h (7,4 %)** |
| Alcance **Should + Could** (condicional) | 93 |

**Lectura honesta de estos números:** el núcleo obligatorio entra en la capacidad del grupo con un margen del 7 %, que es poco. Por eso el alcance se compromete en dos niveles:

1. **Comprometido (365 h):** los 361 h de Must más F.4 (vista lista sin mapa, 4 h), que es barato y reduce el riesgo del mapa.
2. **Condicional (89 h):** el resto de Should y Could. Se confirma con los docentes en cada entrega, tal como prevé la consigna al decir que las funcionalidades de cada entrega se convienen en la anterior.

Las funcionalidades de IA con mayor riesgo — **J (matching)** y **K.2 (asistente)** — están deliberadamente en el tramo condicional: son los objetivos más vistosos del proyecto pero también los que dependen de decisiones externas (aprobación docente del uso de una API de terceros). La **tasación con IA (I)** sí queda comprometida, porque es la que sostiene la propuesta de valor del canje.

---

## 4. Presupuesto económico

### 4.1 Costos de infraestructura y servicios *(desembolso real del cuatrimestre)*

| Concepto | Opción sin costo | Opción paga | Estimado 3,5 meses |
|---|---|---|---|
| Hosting de la aplicación | Capa gratuita de un PaaS, o equipo propio con DNS dinámico / Ngrok | USD 5–7 / mes | USD 0 – 25 |
| Base de datos | Capa gratuita gestionada | USD 5 / mes | USD 0 – 18 |
| Almacenamiento de imágenes | Capa gratuita (~1 GB) | USD 1–3 / mes | USD 0 – 10 |
| Tiles del mapa | OpenStreetMap, respetando su política de uso | Proveedor de tiles con capa gratuita de 100k req/mes | USD 0 |
| Dominio propio | Subdominio gratuito del hosting | USD 10–15 / año | USD 0 – 15 |
| **Subtotal infraestructura** | | | **USD 0 – 68** |

### 4.2 Costo de la API de LLM

Volumen estimado para todo el cuatrimestre, incluyendo desarrollo, pruebas, carga de datos de demo y la exposición final:

| Uso | Llamadas | Tokens aprox. (entrada / salida) |
|---|---:|---|
| Tasación de vehículos | 1.500 | 2.000 / 500 |
| Asistente de ayuda | 1.000 | 3.000 / 400 |
| Matching de canje | 800 | 2.500 / 600 |

| Modelo | Precio (entrada / salida por millón de tokens) | Costo total estimado |
|---|---|---:|
| Claude Haiku 4.5 | USD 1 / USD 5 | **≈ USD 16** |
| Claude Sonnet 5 | USD 3 / USD 15 | **≈ USD 48** |
| Claude Opus 5 | USD 5 / USD 25 | **≈ USD 81** |

Palancas para bajar este costo sin resignar funcionalidad: **caché de tasaciones** por vehículo (una tasación se recalcula sólo si cambian los datos), *prompt caching* del contexto fijo del asistente, y límite de consultas por usuario y por día.

**Desembolso total estimado del proyecto: USD 16 – 150**, según cuántos servicios se paguen y qué modelo se elija.

### 4.3 Valorización del esfuerzo *(referencia, no un costo del TP)*

Si el proyecto se cotizara como trabajo profesional, a una tarifa de referencia de USD 10/hora para perfil junior:

| Concepto | Cálculo | Valor |
|---|---|---:|
| Alcance comprometido | 365 h × USD 10 | USD 3.650 |
| Alcance total presupuestado | 454 h × USD 10 | USD 4.540 |

Se expresa en dólares a propósito: la conversión a pesos debe hacerse al tipo de cambio del día de la presentación. **Esta sección es ilustrativa** — el TP no tiene costo de mano de obra real. Queda incluida porque un presupuesto funcional en un contexto profesional la lleva, y porque permite dimensionar el proyecto frente a un cliente.
