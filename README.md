# Sistema Inteligente de Automatización de Turnos

Proyecto final orientado a la automatización de turnos para un centro de estética utilizando Make, Airtable, Google Gemini y Gmail.

## Objetivo

Automatizar la recepción, interpretación, validación y confirmación de solicitudes de turnos realizadas en lenguaje natural.

El sistema contempla procesamiento automático, intervención humana para casos ambiguos, control de disponibilidad, manejo de errores y monitoreo mediante dashboard.

## Tecnologías utilizadas

- Make
- Airtable
- Google Gemini
- Gmail
- Webhooks
- JSON
- Human-in-the-loop

## Arquitectura

El sistema está dividido en dos escenarios principales.

### Escenario 1 – Recepción, Procesamiento y Disponibilidad

1. Recepción de la solicitud mediante Webhook.
2. Alta o actualización del cliente.
3. Creación del turno.
4. Interpretación del mensaje mediante Gemini.
5. Procesamiento de respuesta JSON.
6. Identificación del servicio.
7. Evaluación de necesidad de revisión humana.
8. Reserva automática o derivación a aprobación.
9. Confirmación por correo electrónico.

### Escenario 2 – Aprobación y Confirmación

Este escenario procesa los turnos que requieren intervención humana.

Cuando el responsable completa los datos necesarios y marca el turno como aprobado, Make:

1. Detecta la modificación.
2. Busca disponibilidad.
3. Reserva el horario.
4. Confirma el turno.
5. Envía la confirmación al cliente.

## Human-in-the-loop

Las solicitudes ambiguas no son confirmadas automáticamente.

Gemini puede devolver:

`requiere_revision_humana = true`

En estos casos, el turno queda en estado `Esperando aprobación` hasta que una persona revise y complete la información.

## Manejo de errores

Los módulos críticos poseen rutas de Error Handling.

Los errores son almacenados en la tabla `Logs` de Airtable junto con información sobre:

- escenario;
- módulo;
- tipo de error;
- mensaje;
- acción tomada.

## Base de datos

Airtable contiene las siguientes tablas:

- Clientes
- Servicios
- Turnos
- Disponibilidad
- Logs

## Dashboard

El dashboard permite monitorear:

- total de turnos;
- confirmados;
- esperando aprobación;
- cancelados;
- errores;
- tasa de error;
- turnos por estado;
- servicios más solicitados.

## Pruebas realizadas

Se realizaron pruebas de:

- reserva automática;
- cliente existente;
- cliente nuevo;
- intervención humana;
- error controlado.

## Archivos

Los blueprints de los escenarios se encuentran en `/blueprints`.

Las capturas de evidencia se encuentran en `/evidencias`.

La documentación completa se encuentra en `/docs`.

## Seguridad

No se incluyen credenciales, API Keys ni tokens dentro del repositorio.

Todos los datos utilizados para las pruebas son ficticios.
