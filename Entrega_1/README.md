# Entrega 1 — Propuesta general

**Programación en Ambiente Web · UNLu Mercedes · 2026**
**Grupo:** Bernal Justino · Marino Lautaro · Kasparian Federico
**Fecha de entrega:** 31/08/2026

---

## Contenido de esta entrega

| Documento | Qué contiene |
|---|---|
| [Presupuesto funcional](presupuesto-funcional.md) | Módulos, funcionalidades, prioridad MoSCoW, complejidad, horas y presupuesto económico |
| [Presupuesto temporal](presupuesto-temporal.md) | Cronograma de 13 semanas, hitos por entrega, riesgos, organización del equipo y consideraciones de seguridad |
| [Sitemap](sitemap.md) | 8 secciones + panel de administración, con rutas y contenido de cada página |

---

## 1. La aplicación

**Permutá** es una aplicación web para **canjear, comprar y vender vehículos entre particulares**.

El mercado de usados en Argentina ya funciona con permuta —"acepto permuta" es una frase corriente en cualquier aviso de venta— pero los sitios de clasificados existentes están construidos alrededor de la **venta**: publicás un precio y esperás un comprador. La permuta queda como una negociación informal en los comentarios, sin ninguna herramienta que la sostenga.

Permutá invierte esa relación: **el canje es la operación de primera clase**. El sistema entiende que cada usuario tiene un vehículo *y* quiere otro, y usa esa doble condición para encontrar coincidencias, estimar la brecha de valor entre ambos vehículos y sostener la negociación hasta el cierre.

### Objetivos funcionales

1. **Canjear** vehículos propios por otros publicados por diferentes usuarios.
2. **Vender** vehículos propios.
3. **Tasar** vehículos con IA para saber qué se tiene antes de negociar.
4. **Ubicar** en un mapa los vehículos cercanos, porque un canje se cierra en persona.
5. **Recomendar** con IA qué vehículos conviene canjear o comprar.
6. **Chatear** con los usuarios interesados.
7. **Asistir** al usuario con un LLM que responde preguntas sobre el uso de la aplicación.

### La tasación es lo que hace posible el canje

Vale detenerse en esto porque es el eje del proyecto. En una venta hay un solo precio y las dos partes lo discuten. **En un canje hay dos vehículos y ninguno tiene precio de lista**, así que la negociación arranca sin referencia: cada parte sobrevalora lo propio y desvalora lo ajeno. Ahí se traban la mayoría de las permutas.

La tasación con IA le da a las dos partes una referencia común, y de ella se deriva lo único que realmente hay que negociar: **la diferencia en efectivo**. Por eso la tasación (módulo I) está comprometida en el cronograma y el matching (módulo J) queda como condicional: sin tasación, el canje no tiene sobre qué apoyarse; sin matching, sigue funcionando.

---

## 2. Alcance comprometido

| | Horas | Contenido |
|---|---:|---|
| **Comprometido** | 365 | Registro y sesión, publicación de vehículos con fotos, búsqueda con filtros, mapa, propuestas de canje con contraoferta, chat en tiempo real, tasación con IA, moderación, y la calidad y documentación que pide la consigna |
| **Condicional** | 89 | Matching con IA, asistente LLM, y funcionalidades secundarias de cuenta, administración y búsqueda |
| **Total presupuestado** | **454** | |

Capacidad del grupo: **390 h** (3 personas × 10 h/semana × 13 semanas). El detalle del contraste está en el [presupuesto funcional](presupuesto-funcional.md#contraste-con-la-capacidad-disponible).

El alcance se presenta en dos niveles a propósito, porque la propia consigna prevé que las funcionalidades de cada entrega se convengan con los docentes en la entrega anterior. Comprometer las 454 h sería prometer más de lo que la capacidad del grupo permite.

---

## 3. Decisiones pendientes

Tres definiciones quedan abiertas en esta entrega. Las dos primeras necesitan una consulta al equipo docente **en la primera clase posterior al 31/8**, porque de ellas dependen módulos enteros del cronograma.

### 3.1 Nombre del proyecto

El documento de trabajo del grupo tenía el nombre sin definir. Se propone **Permutá**, por ser el término que efectivamente se usa en el mercado argentino de usados. Alternativas consideradas: *Trocar*, *AutoCanje*, *Rueda*.

### 3.2 Stack tecnológico

La consigna fija el front-end en JavaScript y exige consultar cualquier librería de terceros. La propuesta, a confirmar en la entrega 2 con su justificación completa:

| Capa | Propuesta | Justificación |
|---|---|---|
| Front-end | JavaScript nativo con módulos ES y Web Components, sin framework | Riesgo cero de aprobación, cumplimiento directo de los estándares W3C que la consigna exige validar, y es lo que la asignatura busca ejercitar |
| Back-end | Node.js con una API REST | Un solo lenguaje para todo el equipo, alineado con la bibliografía de *RESTful Web Services*, y con amplias opciones de hosting gratuito |
| Base de datos | PostgreSQL relacional | El modelo tiene entidades bien definidas y relaciones claras (usuario, vehículo, propuesta, conversación); las consultas geográficas y los filtros combinados se resuelven mejor en SQL |

### 3.3 Consultas que condicionan el cronograma

| Consulta | Módulos afectados | Plan B si la respuesta es negativa |
|---|---|---|
| ¿Se acepta una librería de mapas de terceros con tiles de OpenStreetMap? | F (30 h) | Mapa propio en SVG/Canvas sobre tiles, con la vista lista (F.4) como salida garantizada |
| ¿Se acepta consumir una API de LLM de terceros? | I (24 h), J (26 h), K.2 (12 h) | Tasación por comparables propios: media ponderada por año, kilometraje y estado sobre una base cargada a mano. Es defendible académicamente y elimina la dependencia externa |

Ambos planes B están dimensionados en el mismo orden de horas que los planes A, así que **el cronograma no cambia según la respuesta**. Lo que cambia es la técnica, no el calendario.

---

## 4. Cumplimiento de la consigna

| Requisito | Estado |
|---|---|
| Grupo de 2 a 4 participantes | 3 integrantes |
| Presupuesto funcional y temporal | [presupuesto-funcional.md](presupuesto-funcional.md) · [presupuesto-temporal.md](presupuesto-temporal.md) |
| Sitemap con mínimo 5 secciones | [sitemap.md](sitemap.md) — 8 secciones + administración |
| Repositorio Git público con tag por entrega | Tag `entrega-1` al momento de la entrega |
| README con requisitos y pasos de deployment | Se incorpora en la entrega 3, cuando exista despliegue (M.5) |
| Consideraciones de seguridad por capa | [presupuesto-temporal.md § 7](presupuesto-temporal.md#7-consideraciones-de-seguridad-por-capa) |
| Diseño crossbrowser, multipantalla y responsivo | *Mobile-first* desde el sistema de diseño (B.3); pruebas presupuestadas en M.2 |
| Front-end en JavaScript, librerías consultadas | Propuesta en § 3.2; consultas pendientes en § 3.3 |
| Código 100 % de autoría propia | Sin scraping ni código de terceros; la base de comparables se carga a mano |
