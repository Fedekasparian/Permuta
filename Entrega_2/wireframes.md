# Entrega 2 — Wireframes

**Proyecto:** AutoCar
**Entrega 2 · 14/09/2026** · Bernal Justino · Marino Lautaro · Kasparian Federico
Programación en Ambiente Web · UNLu Mercedes · 2026

Los wireframes se armaron en Figma a partir de este documento y del [sitemap de la entrega 1](../entrega-1/sitemap.pdf). Acá se detalla qué contiene cada pantalla, para que el archivo de Figma sea trazable a las rutas ya definidas.

**Archivo de Figma:** _[completar con el link antes de entregar]_

---

## 0. Convenciones usadas en todas las pantallas

- *Mobile-first*: cada pantalla se diseña primero a 375px de ancho y después se adapta a escritorio (~1024px+).
- Navegación: barra inferior de 5 ítems en mobile (Home, Mapa, Meta-búsqueda o Mis publicaciones según el plan, Mensajes, Cuenta) y barra superior en escritorio, tal como define el sitemap.
- Escala de grises y bloques placeholder — sin definición de marca ni tipografía final; eso corresponde al sistema de diseño (módulo B.3), no al wireframe.
- Todo formulario muestra su estado de error inline (no sólo en un resumen arriba).

---

## 1. Homepage — `/` (pública)

- Barra superior: logo, enlaces a Planes, Ayuda, Ingresar / Registrarme.
- Hero: propuesta de valor de una línea + CTA a registro.
- Franja de planes destacados (resumen de precios, link a `/planes`).
- Grilla de vehículos de ejemplo (sin filtros, sólo para dar contexto — el visitante no navega el catálogo real).
- Footer: legales, contacto.

## 2. Pantallas por sección

### 2.1 Feed / Home autenticado — `/home`
- Barra superior/inferior de navegación.
- Barra de filtros rápidos (marca, precio, tipo de operación).
- Grilla paginada de publicaciones (foto, precio, ubicación aproximada, ícono si acepta canje).
- Estado vacío: mensaje + CTA a `/buscar`.

### 2.2 Detalle de vehículo — `/vehiculo/:id`
- Galería de fotos.
- Ficha técnica (marca, modelo, año, km, estado).
- Rango de tasación de referencia.
- Mapa pequeño con ubicación ofuscada.
- Datos del publicador + reputación.
- Acciones: Consultar por chat, Proponer canje (sólo si el aviso lo acepta), Guardar en favoritos, Reportar.

### 2.3 Búsqueda — `/buscar`
- Buscador de texto arriba.
- Panel de filtros (marca, modelo, año, km, precio, combustible, tipo de operación, localidad).
- Resultados en grilla, igual que el feed.

### 2.4 Mapa — `/mapa`
- Mapa a pantalla completa con marcadores agrupados (clustering).
- Mismos filtros que la búsqueda, colapsables en mobile.
- Popup al tocar un marcador: tarjeta resumen + link al detalle.
- Botón para alternar a `/mapa/lista` (fallback sin mapa).

### 2.5 Meta-búsqueda — `/meta-busqueda` (planes Meta-searching / Ambas)
- Listado de búsquedas guardadas: criterio, fecha del último reporte, botón "ver resultados".
- Botón "Nueva búsqueda" → `/meta-busqueda/nueva`: formulario de criterios (marca, modelo, año, precio máximo).
- `/meta-busqueda/:id`: lista de coincidencias con indicador de fuente (portal propio / externa) y link al origen.

### 2.6 Mis publicaciones — `/mis-publicaciones` (planes Uso Portal / Ambas)
- Listado por estado (activas, pausadas, cerradas) con indicador de cupo del plan ("3 de 5 anuncios usados").
- Botón "Publicar vehículo" → formulario multi-paso en `/mis-publicaciones/nueva`:
  1. Marca / modelo / año
  2. Ficha técnica y estado
  3. Fotos (cantidad según plan)
  4. Precio y si acepta canje
  5. Ubicación
  6. Revisión y publicación
- `/mis-publicaciones/:id/tasacion`: rango estimado, comparables usados, disclaimer de estimación no vinculante.
- `/mis-publicaciones/propuestas`: bandeja de propuestas de canje recibidas / enviadas, con su estado.

### 2.7 Mensajes — `/mensajes`
- Listado de conversaciones: contraparte, vehículo asociado, último mensaje, no leídos.
- `/mensajes/:id`: hilo de mensajes + tarjeta contextual del vehículo + acceso rápido a proponer canje.

### 2.8 Mi cuenta — `/cuenta`
- Formulario de datos personales (nombre, teléfono, localidad, ubicación base).
- `/cuenta/plan`: plan activo, cupo usado, botones para subir/bajar de nivel o cancelar.
- `/cuenta/seguridad`: cambio de contraseña, cierre de sesión.

### 2.9 Planes y precios — `/planes` (pública)
- Tabla comparativa: Free, Meta-searching, Uso Portal (4 niveles), Ambas funcionalidades.
- CTA a registro / alta de plan en cada columna.

---

## 3. Formularios de administración — rol admin

### 3.1 Tablero — `/admin`
- Métricas: usuarios por plan, publicaciones activas, reportes pendientes.

### 3.2 Moderación de publicaciones — `/admin/publicaciones`
- Cola de revisión con vista previa de cada aviso.
- Formulario de acción: Aprobar / Dar de baja + motivo (si se da de baja).

### 3.3 Gestión de usuarios — `/admin/usuarios`
- Buscador de usuarios.
- Formulario por usuario: suspender / restituir cuenta, asignar rol.

### 3.4 Gestión de suscripciones — `/admin/suscripciones`
- Buscador de usuarios.
- Formulario: cambiar plan y nivel manualmente (suscripción simulada, sin pasarela real).

### 3.5 Reportes — `/admin/reportes`
- Cola de denuncias (publicación o usuario) con motivo.
- Formulario de resolución: marcar como resuelto + acción tomada.

### 3.6 ABM de catálogo — `/admin/catalogo`
- Listado de marcas / modelos / versiones.
- Formulario de alta / edición: marca, modelo, versión.
- Confirmación antes de dar de baja un ítem del catálogo.

---

## 4. Cumplimiento de la consigna (entrega 2)

| Requisito | Estado |
|---|---|
| Homepage | § 1 |
| Una página por sección de la aplicación | § 2 |
| Formularios de administración del sitio | § 3 |
| Arquitectura y modelo de objetos | [arquitectura-y-modelo.md](arquitectura-y-modelo.md) |
