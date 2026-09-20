# Daily Reports — VidaSalud QA | Módulo Registro de Pacientes y Turnos Online

> Formato SCRUM: ¿qué hice ayer? · ¿qué voy a hacer hoy? · ¿tengo algún bloqueo?
> QA Tester: Jeisson Marín Uribe Luis — Reporta a: QA Lead del equipo de producto

---

## Sprint 1 — Análisis y Planificación

### Día 1 / Sprint 1 — 23/06/2026
**¿Qué hice ayer?** → Leí la documentación del módulo dos veces: la primera como paciente que quiere registrarse y pedir un turno, la segunda como tester buscando puntos de falla. Dibujé los dos flujos (registro en 7 pasos, reserva de turno en 5 pasos).
**¿Qué voy a hacer hoy?** → Relevar los requerimientos funcionales RF-01 a RF-07 (área de registro) en la planilla de análisis.
**¿Tengo algún bloqueo?** → No.

### Día 2 / Sprint 1 — 24/06/2026
**¿Qué hice ayer?** → Completé el relevamiento de RF-01 a RF-07 y anoté 12 preguntas abiertas sobre el módulo.
**¿Qué voy a hacer hoy?** → Documentar RF-08 a RF-13 (área de turnos) y los no funcionales RNF-01 a RNF-05.
**¿Tengo algún bloqueo?** → Sí: no tengo claro el criterio de "cancelación tardía" para RF-12. Asumo que no se puede cancelar dentro de las 2 horas previas al turno y lo consulto con la QA Lead.

### Día 3 / Sprint 1 — 25/06/2026
**¿Qué hice ayer?** → Cerré los 18 requerimientos (13 RF + 5 RNF) con ID, descripción, prioridad, criterio de aceptación y riesgo. La QA Lead confirmó el criterio de RF-12.
**¿Qué voy a hacer hoy?** → Configurar el proyecto en Jira (Epic, Stories del Sprint 1, labels de severidad) y armar la primera versión de la matriz de trazabilidad.
**¿Tengo algún bloqueo?** → No.

### Día 4 / Sprint 1 — 26/06/2026
**¿Qué hice ayer?** → Dejé el Sprint 1 activo en Jira con sus Stories y criterios de aceptación.
**¿Qué voy a hacer hoy?** → Revisar la matriz de trazabilidad buscando requerimientos sin casos asociados antes de pasar a la Fase 2.
**¿Tengo algún bloqueo?** → No, pero detecté un riesgo: RF-13 (recordatorio de 24 hs), RNF-01 (tiempo de respuesta) y RNF-05 (privacidad de datos de salud) no tienen casos previstos en el diseño base. Lo llevo a la planificación de la Fase 2.

---

## Sprint 2 — Diseño de Casos de Prueba

### Día 1 / Sprint 2 — 29/06/2026
**¿Qué hice ayer?** → Cerré la Fase 1 con los 18 requerimientos documentados y Jira configurado.
**¿Qué voy a hacer hoy?** → Diseñar los casos de los flujos 1 a 3 (DNI, email y contraseña) aplicando partición de equivalencias y valores límite.
**¿Tengo algún bloqueo?** → No.

### Día 2 / Sprint 2 — 01/07/2026
**¿Qué hice ayer?** → Escribí CP-001 a CP-017 (validaciones del formulario de registro).
**¿Qué voy a hacer hoy?** → Diseñar CP-018 a CP-035 (obra social, consentimientos, reserva y cancelación de turnos).
**¿Tengo algún bloqueo?** → Sí, uno de diseño: para probar el recordatorio de 24 hs necesito reservar turnos al inicio del sprint de ejecución, porque si los reservo el mismo día la franja de 24 hs nunca cae dentro de la ventana de prueba. Lo dejo previsto en el plan.

### Día 3 / Sprint 2 — 03/07/2026
**¿Qué hice ayer?** → Completé los 39 casos del diseño base y los cargué en Jira como subtareas del sprint.
**¿Qué voy a hacer hoy?** → Cerrar la brecha detectada en la Fase 1: diseñar CP-040 a CP-043 para cubrir RF-13, RNF-01, RNF-05 y el filtro por cobertura de RF-08, y actualizar la matriz de trazabilidad.
**¿Tengo algún bloqueo?** → No. Con los 4 casos adicionales la cobertura de requerimientos llega al 100 %.

---

## Sprint 3 — Ejecución de Pruebas

### Día 1 / Sprint 3 — 06/07/2026
**¿Qué hice ayer?** → Cerré el diseño con 43 casos y la matriz de trazabilidad al 100 %.
**¿Qué voy a hacer hoy?** → Reservar los tres turnos de prueba para CP-040 (recordatorio) y ejecutar CP-001 a CP-022 en Chrome, capturando evidencia de cada caso.
**¿Tengo algún bloqueo?** → No.

### Día 2 / Sprint 3 — 08/07/2026
**¿Qué hice ayer?** → Ejecuté CP-001 a CP-022. Encontré dos fallas: mensaje genérico en DNI duplicado (CP-006) y contraseña visible en claro (CP-013).
**¿Qué voy a hacer hoy?** → Ejecutar CP-023 a CP-039: verificación por email, turnos, cancelación, compatibilidad y responsive.
**¿Tengo algún bloqueo?** → Sí: CP-024 queda bloqueado porque el email con el código de verificación no llega dentro de la ventana de ejecución (causa: la demora detectada en CP-023).

### Día 3 / Sprint 3 — 10/07/2026
**¿Qué hice ayer?** → Ejecuté CP-023 a CP-039. Encontré una falla crítica: en Firefox el botón "Registrarme" no responde y la consola muestra `Uncaught TypeError: e.submitForm is not a function`.
**¿Qué voy a hacer hoy?** → Ejecutar CP-040 a CP-043 (los cuatro casos adicionales) y repetir la falla de Firefox en una segunda máquina para confirmar que es reproducible.
**¿Tengo algún bloqueo?** → Sí: CP-037 (Safari mobile) queda bloqueado por no disponer de dispositivo iOS. Escalado a la QA Lead.

### Día 4 / Sprint 3 — 12/07/2026
**¿Qué hice ayer?** → Ejecuté los cuatro casos adicionales. CP-040 falló: no llegó ningún recordatorio en los tres turnos de prueba.
**¿Qué voy a hacer hoy?** → Cerrar la matriz con los resultados reales y ordenar las evidencias antes de empezar la Fase 4.
**¿Tengo algún bloqueo?** → No. Confirmé la falla de Firefox en una segunda máquina: es reproducible al 100 %.

---

## Sprint 4 — Reporte, Cierre y Portafolio

### Día 1 / Sprint 4 — 14/07/2026
**¿Qué hice ayer?** → Cerré la ejecución: 33 Passed, 8 Failed y 2 Blocked sobre 43 casos.
**¿Qué voy a hacer hoy?** → Documentar los 9 bugs en Jira con plantilla completa, evidencia, caso vinculado e impacto en el negocio.
**¿Tengo algún bloqueo?** → No.

### Día 2 / Sprint 4 — 15/07/2026
**¿Qué hice ayer?** → Documenté BUG-001 a BUG-009 con severidad y prioridad.
**¿Qué voy a hacer hoy?** → Simular el ciclo de vida completo en BUG-001, BUG-002 y BUG-005, y retestear BUG-004 sobre el build 2.1.
**¿Tengo algún bloqueo?** → No.

### Día 3 / Sprint 4 — 16/07/2026
**¿Qué hice ayer?** → Cerré BUG-001, BUG-002 y BUG-005 verificados en el build 2.1. Reabrí BUG-004: el botón sigue recortado en 375×667. El PO marcó BUG-007 como Won't Fix porque el rediseño del historial está planificado para el Sprint 6.
**¿Qué voy a hacer hoy?** → Redactar el informe final con las métricas reales y la recomendación GO / NO-GO.
**¿Tengo algún bloqueo?** → No.

### Día 4 / Sprint 4 — 17/07/2026
**¿Qué hice ayer?** → Emití el informe final con recomendación **NO-GO**, justificada en 1 bug S1 y 4 bugs S2.
**¿Qué voy a hacer hoy?** → Publicar el repositorio en GitHub con todos los artefactos organizados.
**¿Tengo algún bloqueo?** → No.
