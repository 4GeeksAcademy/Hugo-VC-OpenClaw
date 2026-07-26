# SKILLS_DESIGN.md — Diseño de Skills

> Archivo de diseño previo a la implementación.
> Cada skill responde a tres preguntas: qué hace, qué input necesita, cómo es un buen output.

---

## Skills que crean contenido nuevo

---

### 1. Diario de aprendizaje diario

**¿Qué hace?**
Toma unos pocos puntos sobre lo que aprendiste hoy y los añade como una entrada estructurada a un Google Doc que funciona como diario personal de conocimiento.

**Input que necesita el agente**
- **Del usuario:** Unos puntos sueltos en lenguaje natural (ej: "Hoy aprendí a configurar Auth0 en Angular y a hacer queries con JOIN en PostgreSQL")
- **De la configuración:** El agente sabe:
  - Tu cuenta de Google (`huguitoalovera12@gmail.com`) con Docs activo (TOOLS.md)
  - Tu tono preferido: con humor, cercano, sin rodeos (SOUL.md)
  - Tu perfil como dev full-stack / AI (USER.md)
  - Que el Doc del diario se llama "Diario de Aprendizaje — Hugo" (lo crea la primera vez y guarda su ID en memoria)

**Buen output**
- Una entrada en el Google Doc con:
  - Fecha como encabezado (`## 2026-07-26`)
  - Puntos formateados con bullets y negritas para conceptos clave
  - Una sección "🧠 Takeaways" al final
- **Destino:** Google Doc llamado "Diario de Aprendizaje — Hugo" en Drive raíz
- **Éxito:** El agente confirma por Telegram: "📝 Añadida entrada del 26/07 al diario. 3 conceptos guardados."

---

### 2. Plan de semana

**¿Qué hace?**
Dado un listado de objetivos y compromisos, escribe un plan semanal priorizado como Google Doc y crea los eventos clave en Google Calendar.

**Input que necesita el agente**
- **Del usuario:** Lista de objetivos/compromisos (ej: "Terminar el TFG, preparar la entrevista del martes, avanzar con expense-manager")
- **De la configuración:** El agente sabe:
  - Calendar ID: `primary` (huguitoalovera12@gmail.com), timezone `Europe/Madrid` (TOOLS.md)
  - Tu estilo de trabajo: dev full-stack, proyectos personales + TFG (USER.md)
  - Que prefieres pregunte antes de crear eventos masivos (SOUL.md)

**Buen output**
- Un Google Doc "Plan Semana XX — Julio 2026" con objetivos priorizados, divididos por día
- Eventos en Calendar para los bloques de trabajo clave (con Meet link si aplica)
- **Destino:** Google Doc + Google Calendar
- **Éxito:** "📅 Plan de semana listo. 5 eventos creados en Calendar. [Enlace al doc]"

---

### 3. Notas de reunión

**¿Qué hace?**
Toma apuntes en bruto de una reunión y los estructura como decisiones, tareas pendientes y preguntas abiertas en un Google Doc.

**Input que necesita el agente**
- **Del usuario:** Texto plano con apuntes de reunión, en el formato que sea (viñetas, párrafo suelto, transcripción)
- **De la configuración:** Sabe que los documentos se crean en Drive raíz (TOOLS.md) y tu tono es cercano pero profesional

**Buen output**
- Google Doc con secciones: "📋 Asistentes", "✅ Decisiones", "📌 Pendientes", "❓ Preguntas abiertas"
- Nombre del doc: "Notas — [Tema de la reunión] — [Fecha]"
- **Destino:** Google Doc en Drive raíz
- **Éxito:** "📋 Notas de reunión listas. 3 decisiones, 5 tareas pendientes. [Enlace]"

---

## Skills que afinan comportamientos ya instalados

---

### 4. Eventos de Calendar más inteligentes

**¿Qué hace?**
Permite describir un evento en lenguaje natural ("sesión de estudio el jueves por la tarde, dos horas") y el agente gestiona todos los detalles automáticamente.

**Input que necesita el agente**
- **Del usuario:** Descripción en lenguaje natural. Puede incluir fecha relativa ("el jueves", "pasado mañana"), hora vaga ("por la tarde", "a las 3"), duración y tipo
- **De la configuración:** Calendar ID `primary`, timezone `Europe/Madrid`, prefieres que pregunte si algo es ambiguo (SOUL.md). Sabe que el formato de fecha debe ser ISO 8601 para la tool (TOOLS.md)

**Buen output**
- Evento creado en Calendar con título, hora exacta (resolviendo ambigüedades), duración y Meet link
- Si la descripción es ambigua, el agente pregunta antes (ej: "¿El jueves 28 a las 15:00 o a las 17:00?")
- **Destino:** Google Calendar
- **Éxito:** "✅ Evento creado: 'Sesión de estudio' — jue 28 jul 15:00-17:00. Recordatorio 30min antes."

---

### 5. Borradores de Gmail con tu voz

**¿Qué hace?**
Redacta un borrador de correo con tu estilo, tono y firma, listo para enviar con mínimas correcciones.

**Input que necesita el agente**
- **Del usuario:** Tema del correo y puntos clave (ej: "Escríbele a María sobre la reunión del lunes, confirmando asistencia y preguntando si necesita algo de mí")
- **De la configuración:** Sabe que usas tono con humor pero sin pasarte (SOUL.md). Tu perfil: desarrollador, proyectos propios (USER.md). La conexión Gmail es vía OAuth, sin firma personalizada configurable (TOOLS.md)

**Buen output**
- Borrador en Gmail (o texto listo para copiar, si no se puede crear borradores directamente) con:
  - Asunto claro
  - Cuerpo con tu voz: cercano, sin formalismos excesivos, con chispa
  - Separado en párrafos con los puntos clave
- **Destino:** Gmail (borrador) o texto en chat para que tú lo revises
- **Éxito:** Te muestra el borrador y pregunta "¿Lo envío tal cual o quieres cambiar algo?" antes de mandarlo

---

### 6. Resumen diario de GitHub

**¿Qué hace?**
Lee tus issues abiertos y commits recientes y te envía un briefing breve por Telegram.

**Input que necesita el agente**
- **Del usuario:** Ninguno (o un "actualiza" para forzar refresco). La skill se activa bajo demanda
- **De la configuración:** Sabe tu usuario de GitHub (`Hugo-VC`), tus repos destacados (`Mi-empresa`, `expense-manager`, `Mi-TFG`), tus lenguajes principales (USER.md). Telegram está disponible (TOOLS.md)

**Buen output**
- Mensaje de Telegram con:
  - 📌 Issues abiertos sin asignar (número y título)
  - 🔨 Últimos commits del día (repo + mensaje)
  - 🏆 Repo más activo de la semana
  - Resumen en 4-5 líneas como máximo
- **Destino:** Telegram
- **Éxito:** Recibes un mensaje como: "🐙 Resumen GitHub — Hoy: 3 commits en expense-manager, 1 issue abierto en Mi-TFG. Todo tranquilo."

---

## Skills que conectan herramientas entre sí

---

### 7. Tarea → Calendar

**¿Qué hace?**
Lee tus tareas pendientes en Google Tasks y crea bloques de tiempo en Google Calendar para las que no tienen evento asignado.

**Input que necesita el agente**
- **Del usuario:** Opcional — puede pedir "pasa mis tareas a Calendar" o la skill se ejecuta bajo demanda
- **De la configuración:** Task list default (TOOLS.md), Calendar ID `primary`, timezone `Europe/Madrid. Sabe que debe preguntar antes de crear eventos masivos (SOUL.md)

**Buen output**
- Para cada tarea sin evento asociado, un bloque en Calendar de 1h (o la duración que tenga sentido)
- Las tareas con fecha de vencimiento se programan antes de esa fecha
- **Destino:** Google Tasks → Google Calendar
- **Éxito:** "📅 Encontré 4 tareas sin bloquear. ¿Te creo eventos de 1h para cada una esta semana?"
  (pregunta antes de actuar)

---

### 8. Triaje de bandeja de entrada

**¿Qué hace?**
Lee tus correos no leídos en Gmail, identifica los que requieren acción y crea una Google Task para cada uno.

**Input que necesita el agente**
- **Del usuario:** "Revisa mi bandeja de entrada" o similar
- **De la configuración:** Cuenta Gmail activa (huguitoalovera12@gmail.com), Tasks default list, tu tono con humor pero profesional en comunicaciones (SOUL.md)

**Buen output**
- Tasks creadas con:
  - Título: asunto del correo (truncado)
  - Descripción: 1-2 líneas sobre qué acción se necesita y quién lo envió
  - Fecha de vencimiento: si el correo sugiere urgencia
- Resumen por Telegram con el conteo
- **Destino:** Gmail → Google Tasks + Telegram
- **Éxito:** Mensaje: "📬 Triaje completo: 8 no leídos → 3 requieren acción. Tasks creadas. ¿Quieres que te resuma cada una?"

---

## Prioridad sugerida para implementar

Basado en tu perfil (dev full-stack, TFG en curso, proyectos con IA, transición a proyectos propios):

| Prioridad | Skill | Por qué |
|-----------|-------|---------|
| 🥇 | #4 — Eventos inteligentes | La usas cada vez que necesitas agendar algo — máxima frecuencia |
| 🥇 | #6 — Resumen GitHub | Eres dev, tienes 19 repos — visibilidad diaria de tu código |
| 🥈 | #1 — Diario de aprendizaje | Estás en etapa de aprendizaje activo (TFG, nuevas tecnologías) |
| 🥈 | #8 — Triaje de bandeja | Gmail activo, Tasks activo — buena combinación productiva |
| 🥉 | #2 — Plan de semana | Útil cuando arrancas la semana |
| 🥉 | #5 — Borradores Gmail | Cuando necesites escribir correos formales |
| 🐢 | #3 — Notas de reunión | Menos frecuente para tu perfil actual |
| 🐢 | #7 — Tarea → Calendar | Interesante pero requiere configuración fina |

---

*Diseño completado. Pendiente de tu aprobación para empezar a implementar las que elijas.*