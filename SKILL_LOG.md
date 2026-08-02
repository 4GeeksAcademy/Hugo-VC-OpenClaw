# SKILL_LOG — Conexión API 4Geeks

**Fecha:** 2026-08-02
**Autor:** Hugo Villar (vía OpenClaw)
**Estado:** ✅ 7 skills operativas

---

## 💬 Skill 1 — Autenticar en 4Geeks

**Prompt original:** *"Ayúdame a conectarme a la API de 4Geeks usando mi token del archivo .env"*

**¿Qué hace?** Verifica que el token de 4Geeks es válido, que la sesión está activa y que OpenClaw puede hablar con la API de BreatheCode (backend de 4Geeks Academy).

**Endpoint utilizado:** `GET /v1/auth/user/me` → `Authorization: Token`

**Prueba real:**
```bash
curl -sL "https://breathecode.herokuapp.com/v1/auth/user/me" \
  -H "Authorization: Token $TOKEN_4GEEKS" -H "Accept: application/json"
```
✅ **HTTP 200** — Respuesta:
```json
{"id":21236,"email":"hvillarc04@gmail.com","first_name":"Hugo",
 "last_name":"Villar Calvo","roles":[{"academy":{"name":"4Geeks Madrid",
 "slug":"madrid-spain"}}]}
```
**Conclusión:** Token válido. Sesión activa. Usuario identificado como estudiante de 4Geeks Madrid.

**Archivo:** `plugin-skills/4geeks-auth/SKILL.md`
**Config:** `openclaw.json` → `skills.entries.4geeks-auth.env.TOKEN_4GEEKS`

---

## 💬 Skill 2 — Obtener mis proyectos

**Prompt original:** *"Necesito consultar ejercicios y ver mi progreso"*

**¿Qué hace?** Lee el historial de actividad del usuario, extrae todos los proyectos y ejercicios asignados y los muestra con su estado actual (DONE/PENDING) y tipo (PROJECT/EXERCISE/LESSON).

**Endpoint utilizado:** `GET /v2/activity/me/activity?limit=300`

**Prueba real:**
```bash
curl -sL "https://breathecode.herokuapp.com/v2/activity/me/activity?limit=300" \
  -H "Authorization: Token $TOKEN_4GEEKS" -H "Accept: application/json"
```
✅ **HTTP 200** — **64 tareas únicas detectadas** de 300 entries de actividad.
```
🏁 DONE    | PROJECT  | Milestone 4 — AI-driven Engineering
🏁 DONE    | PROJECT  | Connect Your Agent: Telegram, Google Drive & Calendar
🏁 DONE    | PROJECT  | Applying Spec Driven Development — Financial dashboard
🏁 DONE    | PROJECT  | Building context from an existing project — Financial dashboard
🏁 DONE    | PROJECT  | Setting Up Your Personal AI Agent with OpenClaw
🏁 DONE    | PROJECT  | Talk to the Machine — Building a Chat Interface with a Real AI API
🏁 DONE    | PROJECT  | AgentHub Admin Panel Specs and Prompt-Driven Prototype
🏁 DONE    | PROJECT  | Cinema Seat Manager in TypeScript
🏁 DONE    | PROJECT  | My first collaborative professional project
🏁 DONE    | PROJECT  | A simple Dashboard with Tailwind CSS
🏁 DONE    | PROJECT  | Milestone 1 — Your Company's Public Website
🏁 DONE    | EXERCISE | Managing a VPS from VS Code
🏁 DONE    | LESSON   | Logical conditions in Python explained
🏁 DONE    | LESSON   | Learning to program with Python
📌 PENDING | ...      | 50 tareas pendientes
```
**Conclusión:** 14 completadas (11 proyectos, 1 ejercicio, 2 lecciones) + 50 pendientes.

**Archivo:** `plugin-skills/4geeks-proyectos/SKILL.md`

---

## 💬 Skill 3 — Obtener trabajo pendiente

**Prompt original:** *"Muéstrame qué ejercicios tengo pendientes"*

**¿Qué hace?** Filtra del historial solo las tareas con estado PENDING y las agrupa por tipo (PROJECT, EXERCISE, LESSON) para tener visibilidad clara de lo que falta.

**Endpoint utilizado:** `GET /v2/activity/me/activity?limit=300`

**Prueba real:**
✅ **50 tareas pendientes identificadas:**
```
📌 PRIORIDAD 1 — Cohorts activas (1690, 1688, 1670, 1627 = ~10 tareas):
  [PROJECT]  My 4Geeks Assistant — Teaching OpenClaw to Track Your Progress
  [PROJECT]  My Agent, My Way: Teaching Your Personal Assistant New Skills
  [PROJECT]  Voice Command API — Talk to Your Task List
  [EXERCISE] Building a Python API to Serve the Frontend
  [EXERCISE] Teaching OpenClaw New Skills
  [EXERCISE] OpenClaw Advanced Concepts for Beginners
  [EXERCISE] How to Make Your Agent Interact with a System
  [EXERCISE] Connecting OpenClaw with 4Geeks Academy
  [EXERCISE] Common Backend Architectures
  [EXERCISE] Learn Python Interactively (beginner)
  [LESSON]   Working with Functions in Python

📌 PRIORIDAD 2 — Cohorts intermedias:
  [PROJECT]  Todo List CLI with Python
  [PROJECT]  Enhancing development with agent skills — Financial dashboard
  [PROJECT]  Milestone 3 — Talent Pipeline Tracker
  [EXERCISE] Prompting Engineering Fundamentals
  + varios ejercicios más

📌 PRIORIDAD 3 — Cohorts base:
  [PROJECT]  Wanderlust Explorer with React and Next.js
  [PROJECT]  Building an Airbnb UI Clone with Next.js and React
  [PROJECT]  Milestone 2 — Building Scripts to Automate Tasks
  [PROJECT]  Music playlist player modeling and class diagrams
  [PROJECT]  Data modeling and class diagrams
  [PROJECT]  Command Line Challenge
  [EXERCISE] ~15 ejercicios de TypeScript/JS
  [LESSON]   Context API
```
**Conclusión:** Visibilidad completa de la carga pendiente por cohort y tipo.

**Archivo:** `plugin-skills/4geeks-pendientes/SKILL.md`

---

## 💬 Skill 4 — Obtener resumen de progreso

**Prompt original:** *"Dame una visión general de cuánto he avanzado en el curso"*

**¿Qué hace?** Analiza todo el historial de actividad y genera un resumen ejecutivo: porcentaje completado, desglose por tipo de tarea, y recomendaciones.

**Endpoint utilizado:** `GET /v2/activity/me/activity?limit=300`

**Prueba real:**
```
==================================================
  📊 RESUMEN DE PROGRESO — 4GEEKS MADRID
==================================================
  🎯 Completadas:  14/64 (22%)
  📌 Pendientes:   50
  
  📁 Proyectos:   11 completados, ~17 pendientes
  📖 Lecciones:    2 completadas,  2 pendientes
  ⚡ Ejercicios:   1 completado,  ~31 pendientes
==================================================
```
**Conclusión:** 22% del curso completado. Buen avance en proyectos, mucho margen en ejercicios base.

**Archivo:** `plugin-skills/4geeks-progreso/SKILL.md`

---

## 💬 Skill 5 — Consejos de proyectos entregados

**Prompt original:** *"Consejos o sugerencias de los proyectos entregados"*

**¿Qué hace?** Analiza los proyectos que ya entregaste (DONE) y genera recomendaciones personalizadas basadas en tus repos reales de GitHub, tu perfil y tu progreso.

**Endpoint utilizado:** `GET /v2/activity/me/activity?limit=300`

**Prueba real:**
```
💡 CONSEJOS — PROYECTOS ENTREGADOS

📁 Mi-empresa (Milestone 1, 4 + PR)
   🔗 https://github.com/4GeeksAcademy/Mi-empresa
   💡 Añadir tests automatizados y documentar arquitectura.
   💡 Es tu proyecto estrella — mantenlo activo.

📁 OpenClaw connection
   🔗 https://github.com/4GeeksAcademy/Hugo-VC-OpenClaw
   💡 Añadir capturas de pantalla al README.
   💡 Enlazarlo desde LinkedIn como portfolio.

📁 Financial dashboard (Spec Driven Dev)
   🔗 https://github.com/4GeeksAcademy/Hugo-VC-ai-eng-financial-dashboard-context-project
   💡 Refactorizar siguiendo buenas prácticas de clean code.

🎯 RECOMENDACIÓN GENERAL:
   Todos tus proyectos están en revision_status: PENDING.
   → Pide feedback a tus mentores (Ehiber Graterol, Robert Tovar).
```
**Conclusión:** Consejos accionables y contextuales basados en datos reales.

**Archivo:** `plugin-skills/4geeks-consejos-entregados/SKILL.md`

---

## 💬 Skill 6 — Consejos de proyectos pendientes

**Prompt original:** *"Consejos o sugerencias de los proyectos pendientes"*

**¿Qué hace?** Prioriza tus 50 tareas pendientes en 3 niveles por cohort y genera un plan de acción concreto con estimaciones de tiempo.

**Endpoint utilizado:** `GET /v2/activity/me/activity?limit=300`

**Prueba real:**
```
🎯 PLAN DE ACCIÓN — PROYECTOS PENDIENTES

🥇 PRIORIDAD 1 (Cohorts activas: 1690, 1688, 1670, 1627)
  🏗️  My 4Geeks Assistant — Teaching OpenClaw to Track Your Progress
     💡 Ya tienes la skill authenticate-4geeks funcionando.
     💡 Este proyecto consiste justamente en lo que hemos hecho hoy.
     💡 ¡Marca como entregado!
  🏗️  Connecting OpenClaw with 4Geeks Academy
     💡 Ya tienes el TOKEN_4GEEKS configurado y la API conectada.
  🏗️  Building a Python API to Serve the Frontend
     💡 Combínalo con Voice Command API (misma cohort 1670).

🥈 PRIORIDAD 2 (Cohorts 1627, 1615)
  🏗️  Todo List CLI with Python, Enhancement financial dashboard, Milestone 3

🥉 PRIORIDAD 3 (Cohorts base 1614, 1613, 1612)
  🏗️  6 proyectos y ~15 ejercicios de TypeScript/JS/fundamentos

⏰ ESTIMACIÓN TOTAL: ~40-80h de trabajo
```
**Conclusión:** Plan claro y priorizado. Las skills de OpenClaw ya están casi listas para entregar.

**Archivo:** `plugin-skills/4geeks-consejos-pendientes/SKILL.md`

---

## 💬 Skill 7 — Autenticación base (authenticate-4geeks)

**Prompt original:** *"He modificado el apartado de skill del openclaw.json para ello"* (configuración inicial del skill con el token)

**¿Qué hace?** Skill base que expone la variable `TOKEN_4GEEKS` a todas las demás skills y sirve como dependencia de autenticación.

**Endpoint utilizado:** `GET /v1/auth/user/me`

**Prueba real:** ✅ Token configurado en `openclaw.json` y verificado con HTTP 200.

**Archivo:** `plugin-skills/authenticate-4geeks/SKILL.md`

---

## 🗺️ Mapa completo de skills

| Skill | Prompt inicial | Endpoint principal | Resultado |
|-------|---------------|-------------------|-----------|
| `authenticate-4geeks` | "modificado el apartado de skill del openclaw.json" | `GET /v1/auth/user/me` | ✅ Token operativo |
| `4geeks-auth` | "conectarme usando mi token del .env" | `GET /v1/auth/user/me` | ✅ Sesión verificada |
| `4geeks-proyectos` | "consultar ejercicios y ver mi progreso" | `GET /v2/activity/me/activity` | ✅ 64 tareas listadas |
| `4geeks-pendientes` | "qué ejercicios tengo pendientes" | `GET /v2/activity/me/activity` | ✅ 50 pendientes |
| `4geeks-progreso` | "visión general de cuánto he avanzado" | `GET /v2/activity/me/activity` | ✅ 22% completado |
| `4geeks-consejos-entregados` | "consejos de proyectos entregados" | `GET /v2/activity/me/activity` | ✅ Recomendaciones contextuales |
| `4geeks-consejos-pendientes` | "consejos de proyectos pendientes" | `GET /v2/activity/me/activity` | ✅ Plan de acción priorizado |

---

## 📡 Endpoints verificados

| Endpoint | Estado | Uso |
|----------|--------|-----|
| `GET /v1/auth/user/me` | ✅ 200 | Perfil del usuario — Skill 1 y 7 |
| `GET /v1/auth/profile/me` | ✅ 200 | Perfil extendido con avatar |
| `GET /v2/activity/me/activity` | ✅ 200 | Historial de actividad — Skills 2,3,4,5,6 |
| `GET /v1/registry/asset` | ✅ 200 | Assets/ejercicios disponibles |
| `POST /v1/auth/login/` | ✅ 400 (esperado) | Login con credenciales |
| `GET /v1/assignment/task` | ❌ 500 | Endpoint inestable |
| `POST /v1/payments/plan/{slug}` | ✅ 404 (esperado) | Plan no encontrado |
| `GET /v1/admissions/cohort` | ❌ 404 | No existe |
| `GET /v1/payments/subscription` | ❌ 404 | No existe |

## 👤 Datos del usuario

- **Nombre:** Hugo Villar Calvo
- **Email:** hvillarc04@gmail.com
- **Academia:** 4Geeks Madrid (slug: `madrid-spain`, timezone: `Europe/Madrid`)
- **Rol:** Student
- **GitHub vinculado:** Hugo-VC
- **Idioma:** Español
- **Fecha de registro:** 2026-03-30

## 📊 Estadísticas de progreso

| Métrica | Valor |
|---------|-------|
| Tareas totales detectadas | 64 |
| Completadas (DONE) | 14 (22%) |
| Pendientes (PENDING) | 50 (78%) |
| Proyectos completados | 11 |
| Lecciones completadas | 2 |
| Ejercicios completados | 1 |
| Cohorts activas | 8 |
| Mentorías registradas | 4 (con Ehiber Graterol) |
| NPS General | 9/10 |
| NPS Mentores | 10/10 |

## ⚙️ Configuración técnica

- **Token source:** `.env` → `4GEEKS_TOKEN`
- **openclaw.json:** `skills.entries.*.env.TOKEN_4GEEKS`
- **Skills path:** `~/.openclaw/plugin-skills/4geeks-*/SKILL.md`
- **API Host:** `https://breathecode.herokuapp.com`
- **Auth header:** `Authorization: Token`
- **Token expires:** Cada 24h (tokens de tipo `ExpiringTokenAuthentication`)