# Memoria

**Decisiones de configuración:** Se conectó Composio a Google Docs y Google
Calendar mediante OAuth desde el panel de Composio, autorizando las
integraciones a través de enlaces de verificación.

**Problemas encontrados:** (1) El CLI de Composio (actions, apps) no
respondía, así que se usaron las herramientas internas de OpenClaw (Composio
Search/Execute). (2) Cada integración requirió autorización por separado,
aunque ya hubiera sesión en Composio. (3) El evento no se visualizaba
inicialmente en el calendario, pero se verificó que sí estaba creado
correctamente en la API.
