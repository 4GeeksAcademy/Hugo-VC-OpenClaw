# TOOLS.md - Servicios disponibles vía Composio

Skills definen _cómo_ funcionan las tools. Este archivo es para _mis_ notas — los servicios, defaults y configuraciones específicas de tu ecosistema.

---

## 📡 Servicios Composio disponibles

| Servicio | Estado | Tool Slug (principal) |
|----------|--------|----------------------|
| ✅ **Google Docs** | ACTIVE | `GOOGLEDOCS_CREATE_DOCUMENT_MARKDOWN` |
| ✅ **Google Calendar** | ACTIVE | `GOOGLECALENDAR_CREATE_EVENT` |
| ✅ **Gmail** | ACTIVE | `GMAIL_SEND_EMAIL` |
| ✅ **Google Drive** | ACTIVE | `GOOGLEDRIVE_UPLOAD_FILE` |
| ✅ **Google Tasks** | ACTIVE | `GOOGLETASKS_CREATE_TASK` |
| ✅ **GitHub** | ACTIVE | `GITHUB_CREATE_ISSUE` |
| ✅ **Telegram** | Via OpenClaw directo | `sessions_send` a Telegram |

---

## 📝 Google Docs

- **Cuenta conectada:** `huguitoalovera12@gmail.com`
- **Tool principal:** `GOOGLEDOCS_CREATE_DOCUMENT_MARKDOWN`
  - `title` (requerido) — título del documento
  - `markdown_text` — contenido en Markdown
  - `image_assets` — imágenes opcionales referenciables
- **Tool para editar:** `GOOGLEDOCS_UPDATE_DOCUMENT_SECTION_MARKDOWN`
  - `document_id` (requerido) — ID del documento
  - `markdown_text` (requerido) — contenido a insertar/reemplazar
  - `start_index` — para reemplazar una sección (omitir = append al final)
- **Ver contenido:** `GOOGLEDOCS_GET_DOCUMENT_PLAINTEXT`
- **Default:** Siempre crear en Drive raíz (a menos que se indique otra carpeta)

---

## 📅 Google Calendar

- **Cuenta conectada:** `huguitoalovera12@gmail.com` (owner)
- **Calendar ID default:** `primary` → `huguitoalovera12@gmail.com`
- **Timezone default:** `Europe/Madrid`
- **Tool principal:** `GOOGLECALENDAR_CREATE_EVENT`
  - `start_datetime` (requerido) — ISO 8601: `YYYY-MM-DDTHH:MM:SS`
  - `summary` — título del evento
  - `timezone` — si no se especifica, usar `Europe/Madrid`
  - `end_datetime` o `event_duration_hour` + `event_duration_minutes`
  - `eventType`: `default` | `birthday` | `focusTime` | `outOfOffice`
  - `calendar_id`: `primary` por defecto
  - `create_meeting_room`: `true` por defecto (crea Meet link)
  - `transparency`: `opaque` (ocupado) por defecto
- **Feriados disponibles:** `es.spain#holiday@group.v.calendar.google.com` (Festivos España)
- **Nota:** Para cumpleaños usar `eventType: "birthday"`, `transparency: "transparent"`, `exclude_organizer: true`

---

## 📧 Gmail

- **Cuenta conectada:** `huguitoalovera12@gmail.com`
- **Tool principal:** `GMAIL_SEND_EMAIL`
- **Notas:**
  - La conexión se hizo vía OAuth — no hay firma personalizada configurable
  - Los emails se envían desde la cuenta conectada automáticamente
- **Para leer:** `GMAIL_FETCH_MESSAGES` / `GMAIL_LIST_MESSAGES`

---

## 📁 Google Drive

- **Cuenta conectada:** `huguitoalovera12@gmail.com`
- **Tool principal:** `GOOGLEDRIVE_UPLOAD_FILE`
- **Carpeta default:** Raíz de Drive (a menos que se especifique `parent_folder_id`)
- **Para mover archivos:** `GOOGLEDRIVE_MOVE_FILE`
  - Requiere `file_id`, `add_parents` (destino), `remove_parents` (origen)

---

## ✅ Google Tasks

- **Cuenta conectada:** `huguitoalovera12@gmail.com`
- **Tool principal:** `GOOGLETASKS_CREATE_TASK`
- **Task list default:** `default` (lista por defecto)
- **Nota:** Si hay múltiples listas, preguntar cuál usar

---

## 🐙 GitHub

- **Usuario:** `Hugo-VC` (Hugo Villar)
- **Tool principal:** `GITHUB_CREATE_ISSUE`
- **Repos destacados:**
  - `Mi-empresa` — automatización con AI Engineering (⭐)
  - `expense-manager` — Angular + Spring Boot + PostgreSQL (⭐)
  - `Mi-TFG` — Trabajo de Fin de Grado (⭐)
- **Nota:** Usar API pública de GitHub (`api.github.com`) como alternativa ligera

---

## 🤖 Telegram

- **Canal:** Via OpenClaw (no Composio)
- **Uso:** `sessions_send` para enviar mensajes a sesiones de Telegram
- **No necesita conexión Composio** — configurado directo en OpenClaw

---

## ⚙️ Reglas generales

1. **Preguntar antes de actuar** si hay ambigüedad en datos, comandos o decisiones externas
2. Para acciones triviales y reversibles (leer, buscar), actuar por defecto
3. Siempre confirmar antes de enviar emails, crear eventos públicos o modificar datos reales
4. Usar `Europe/Madrid` como timezone por defecto para calendario
5. Si un servicio pide reconexión, avisar al usuario con el link de autorización