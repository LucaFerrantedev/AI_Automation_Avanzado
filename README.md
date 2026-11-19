# AI_Automation_Avanzado

Acá voy a subir mis trabajos del curso AI Automation Avanzado de Coderhouse

# Checkpoint 4 — Sincronización del Cerebro Agéntico con Ecosistemas de Negocio

**Alumno:** Luca Ferrante  
**Workflow:** `checkpoint4_luca_ferrante.json`

## Integraciones conectadas (OAuth2)
1. **Gmail (Casilla de correo):** Recepción de consultas vía Trigger y generación de borradores de respuesta.
2. **HubSpot (CRM):** Búsqueda, actualización y alta de contactos para mantener una fuente única de verdad.
3. **Slack (Canal del equipo):** Notificación liviana al canal `#soporte-it` una vez generado el borrador.

## Controles preventivos (Guardrails) implementados
1. **IF anti auto-reply (`IF - Es auto-reply?`):** Filtra correos automáticos (`Auto-reply`, `Out of office`, `Undeliverable`, `no-reply@`) con lógica `OR` inmediatamente después del trigger para cortar bucles infinitos.
2. **Limpieza de payload (`Set - Limpieza de Payload`):** Mapeo manual que conserva únicamente campos limpios (`email_usuario`, `asunto`, `mensaje_limpio`, `categoria`, `respuesta_ia`), descartando adjuntos y binarios pesados antes de impactar el CRM y Slack.
3. **Look up previo en CRM (`Search contacts` + `IF - Existe en CRM?`):** Verifica si el contacto ya existe por email en HubSpot antes de decidir entre `Update contacto` o `Create contacto`, evitando errores `409` por duplicados.
4. **Barrera Human-in-the-loop (`Create a draft`):** Guarda la respuesta redactada por el sistema multi-agente como borrador en Gmail para revisión y aprobación humana previa al envío.

## Evidencia de credenciales activas en n8n
![Credenciales activas en n8n]
<img width="1545" height="596" alt="image" src="https://github.com/user-attachments/assets/48acc037-794b-43b3-a892-136239b92434" />
