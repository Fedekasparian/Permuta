# Sitemap

**Proyecto:** Permutá — plataforma de canje, compra y venta de vehículos
**Entrega 1 · 31/08/2026** · Bernal Justino · Marino Lautaro · Kasparian Federico

La consigna pide un mínimo de 5 secciones. Este sitemap define **8 secciones públicas/privadas + 1 panel de administración**.

---

## 1. Estructura general

```
                                  ┌──────────────────────┐
                                  │   Landing pública /  │
                                  └───────────┬──────────┘
                                              │
        ┌─────────────────────────────────────┼─────────────────────────────────────┐
        │                                     │                                     │
   ┌────┴─────┐                     ┌─────────┴─────────┐                   ┌───────┴────────┐
   │ 0. ACCESO│                     │  ZONA AUTENTICADA │                   │ 6. AYUDA       │
   └────┬─────┘                     └─────────┬─────────┘                   └───────┬────────┘
        │                                     │                                     │
   /registro                    ┌─────────────┼─────────────┐                  /ayuda
   /login                       │             │             │                  /ayuda/faq
   /recuperar                   │             │             │                  /ayuda/asistente
   /verificar/:token       1. HOME      2. MAPA      3. MATCH IA               /ayuda/contacto
                            /home        /mapa         /match
                                 │             │             │
                                 └──────┬──────┴──────┬──────┘
                                        │             │
                                 /vehiculo/:id   4. MIS VEHÍCULOS
                                        │          /mis-vehiculos
                                        │             │
                                        └──────┬──────┘
                                               │
                                        5. MENSAJES          7. MI CUENTA
                                          /mensajes            /cuenta
                                               │
                                     ┌─────────┴──────────┐
                                     │ 8. ADMINISTRACIÓN  │
                                     │       /admin       │
                                     └────────────────────┘
```

---

## 2. Detalle por sección

### 0. Acceso  *(público)*

| Ruta | Página | Contenido / formularios |
|---|---|---|
| `/` | Landing | Propuesta de valor, vehículos destacados, CTA a registro |
| `/registro` | Registro | Formulario: nombre, email, contraseña, localidad, aceptación de términos |
| `/login` | Ingreso | Formulario: email + contraseña |
| `/recuperar` | Recuperar contraseña | Solicitud por email y formulario de nueva contraseña |
| `/verificar/:token` | Verificación de cuenta | Confirmación de email |
| `/terminos`, `/privacidad` | Legales | Términos y condiciones, política de privacidad |

### 1. Home / Explorar  *(autenticado; lectura parcial en público)*

| Ruta | Página | Contenido |
|---|---|---|
| `/home` | Feed de publicaciones | Grilla paginada de vehículos, orden por relevancia / fecha / precio |
| `/buscar` | Resultados de búsqueda | Búsqueda por texto + filtros: marca, modelo, año, kilometraje, precio, combustible, tipo de operación (venta / canje / ambos), localidad y radio |
| `/vehiculo/:id` | Detalle de vehículo | Galería, ficha técnica, rango de tasación de referencia, ubicación aproximada, datos del publicador. Acciones: **Proponer canje**, **Consultar por chat**, **Guardar en favoritos**, **Reportar publicación** |

### 2. Mapa  *(autenticado)*

| Ruta | Página | Contenido |
|---|---|---|
| `/mapa` | Mapa de vehículos | Marcadores agrupados (clustering), filtro por radio desde la ubicación del usuario y por los mismos criterios que la búsqueda |
| `/mapa?vehiculo=:id` | Mapa centrado | Popup con tarjeta resumen y enlace al detalle |
| `/mapa/lista` | Vista lista | Alternativa accesible y *fallback* si el mapa no carga (progressive enhancement) |

> Por privacidad la ubicación se muestra **ofuscada**: se publica el centroide de la zona, no la dirección exacta.

### 3. Matchear con IA  *(autenticado)*

| Ruta | Página | Contenido |
|---|---|---|
| `/match` | Panel de recomendaciones | Dos pestañas: **para comprar** y **para canjear** |
| `/match/preferencias` | Preferencias | Formulario: uso previsto, presupuesto, marcas/modelos de interés, antigüedad y kilometraje máximos |
| `/match/:id` | Detalle del match | Score de compatibilidad, explicación de por qué se recomienda, brecha de valor estimada entre ambos vehículos y CTA a **Proponer canje** |

### 4. Mis vehículos  *(autenticado)*

| Ruta | Página | Contenido / formularios |
|---|---|---|
| `/mis-vehiculos` | Mis publicaciones | Listado por estado: activas, pausadas, cerradas |
| `/mis-vehiculos/nuevo` | Publicar vehículo | **Formulario multi-paso**: (1) marca/modelo/año, (2) ficha técnica y estado, (3) fotos, (4) tipo de operación y precio / expectativa de canje, (5) ubicación, (6) revisión y publicación |
| `/mis-vehiculos/:id/editar` | Editar publicación | Mismo formulario en modo edición; acciones pausar / reactivar / eliminar |
| `/mis-vehiculos/:id/tasacion` | Tasar con IA | Rango de valor estimado, comparables usados, factores que suben o bajan el precio y *disclaimer* de estimación no vinculante |
| `/mis-vehiculos/propuestas` | Propuestas de canje | Bandeja de propuestas **recibidas** y **enviadas**, con estados: pendiente, contraofertada, aceptada, rechazada, cancelada |
| `/mis-vehiculos/historial` | Historial de operaciones | Vehículos vendidos, comprados y canjeados con fecha y contraparte |

### 5. Mensajes  *(autenticado)*

| Ruta | Página | Contenido |
|---|---|---|
| `/mensajes` | Bandeja de conversaciones | Listado con último mensaje, contraparte, vehículo asociado e indicador de no leídos |
| `/mensajes/:id` | Conversación | Hilo en tiempo real, tarjeta contextual del vehículo, acceso rápido a proponer canje, bloquear o reportar usuario |
| `/notificaciones` | Notificaciones | Propuestas nuevas, cambios de estado, mensajes sin leer |

### 6. Ayuda  *(público)*

| Ruta | Página | Contenido |
|---|---|---|
| `/ayuda` | Centro de ayuda | Índice por categorías |
| `/ayuda/faq` | Preguntas frecuentes | Cómo publicar, cómo funciona el canje, cómo se calcula la tasación, seguridad en la transacción presencial |
| `/ayuda/asistente` | Asistente LLM | Chat que responde sobre el uso de la aplicación con el contexto de la documentación del sitio |
| `/ayuda/contacto` | Contacto | Formulario de consulta o reporte de problema |

### 7. Mi cuenta  *(autenticado)*

| Ruta | Página | Contenido / formularios |
|---|---|---|
| `/cuenta` | Datos personales | Formulario de perfil: nombre, teléfono, localidad, ubicación base |
| `/cuenta/seguridad` | Seguridad | Cambio de contraseña, sesiones activas, cierre de sesión en todos los dispositivos |
| `/cuenta/notificaciones` | Preferencias | Qué avisos recibir y por qué canal |
| `/cuenta/favoritos` | Favoritos | Vehículos guardados y búsquedas guardadas |
| `/usuario/:id` | Perfil público | Publicaciones activas, operaciones cerradas y reputación |

### 8. Administración  *(rol admin)*

| Ruta | Página | Contenido / formularios |
|---|---|---|
| `/admin` | Tablero | Métricas: usuarios, publicaciones activas, canjes cerrados, reportes pendientes |
| `/admin/publicaciones` | Moderación de publicaciones | Cola de revisión, aprobar / dar de baja, ver reportes asociados |
| `/admin/usuarios` | Gestión de usuarios | Buscar, suspender, restituir, asignar rol |
| `/admin/reportes` | Reportes | Cola de denuncias de publicaciones y usuarios con su resolución |
| `/admin/catalogo` | ABM de catálogo | Alta / baja / modificación de marcas, modelos y versiones |

### Transversales

`/404` · `/500` · `/mantenimiento`

---

## 3. Reglas de navegación y acceso

| Nivel | Secciones accesibles |
|---|---|
| **Visitante** | Landing, Ayuda, Legales, detalle de vehículo en modo lectura limitada |
| **Usuario registrado** | Todo excepto Administración |
| **Administrador** | Todo, incluida la sección 8 |

- Toda ruta autenticada se valida **en el servidor**, no sólo ocultando el enlace en el cliente.
- La autorización se comprueba **por recurso**: un usuario sólo puede editar sus propias publicaciones y leer sus propias conversaciones (prevención de IDOR).
- Diseño *mobile-first*: la navegación principal es una barra inferior de 5 ítems en móvil (Home, Mapa, Match, Mis vehículos, Mensajes) y una barra superior en escritorio.
