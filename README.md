# SM OS · SM Soluciones

SM OS es el CRM / gestor de proyectos de SM Soluciones (Pako Studio). Es una app web estática (HTML, CSS y JavaScript puro) con backend en Supabase (Postgres + REST) y funciones serverless en Vercel para alertas por correo vía Resend.

Incluye además un módulo de inventario para Prokicks.

## Stack

- Frontend: HTML/CSS/JS puro (`index.html`, `assets/js/app.js`, `assets/css/styles.css`), sin build ni framework.
- Backend de datos: Supabase (Postgres, autenticación por PIN con verificación vía RPC `sm_verify_pin`).
- Alertas: funciones serverless en `api/` (Vercel) + `server/alerts-lib.js`, envío de correo con Resend, cron diario configurado en `vercel.json`.
- Base de datos: scripts SQL en `supabase/` (`pako-crm-base.sql`, `security-hardening.sql`, `notifications.sql`, `prokicks-inventory.sql`).

## Roles

- `admin`: acceso total, crea/edita proyectos y usuarios.
- `responsable`: edita proyectos y tareas donde es responsable.
- `colaborador`: edita tareas donde participa.
- `lectura`: solo consulta, sin edición.

## Seguridad

Ver `docs/security-status.md`, `VERSION_NOTES_SM_OS_2_5.md` y `CHECKLIST_SM_OS_2_5.md` para el estado y los pendientes de seguridad (hardening de PIN, RLS y alertas).

## Módulo de inventario Prokicks

Ver `VERSION_NOTES_INVENTARIO_PROKICKS.md` y `CHECKLIST_INVENTARIO_PROKICKS.md`.

## Despliegue

El sitio se despliega en Vercel (ver `vercel.json` para headers de seguridad y el cron de alertas). La base de datos vive en Supabase; los scripts SQL deben ejecutarse manualmente en el SQL Editor de Supabase en el orden indicado en `CHECKLIST_SM_OS_2_5.md`.

## Variables de entorno (Vercel)

- `SUPABASE_URL`
- `SUPABASE_SERVICE_ROLE_KEY`
- `RESEND_API_KEY`
- `ALERT_FROM_EMAIL`
- `CRON_SECRET`
