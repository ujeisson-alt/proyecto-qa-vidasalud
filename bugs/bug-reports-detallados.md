# Bug Reports — VidaSalud S.A. | Módulo Registro de Pacientes y Turnos Online

> 9 defectos documentados en Jira (proyecto *VidaSalud QA - Registro y Turnos*) con formato estándar de industria.
> Reportados por: Jeisson Marín Uribe Luis — QA Tester Junior · Sprint 4 · Entorno: staging (simulado, proyecto educativo).


## Índice

| ID | Título | Severidad | Prioridad | Estado | Caso vinculado |
|---|---|---|---|---|---|
| **BUG-001** | [Registro] El campo contraseña muestra el texto en claro sin interacción del usuario | S2 - Mayor | P2 - Alta | Closed | CP-013 |
| **BUG-002** | [Registro] En Firefox el botón 'Registrarme' no responde al clic | S1 - Crítico | P1 - Crítica | Closed | CP-036 |
| **BUG-003** | [Registro] El email con el código de verificación llega a los 20 minutos | S2 - Mayor | P2 - Alta | Fixed | CP-023 (bloquea CP-024) |
| **BUG-004** | [Turnos] En mobile 375 px el botón 'Confirmar turno' queda fuera del viewport | S2 - Mayor | P1 - Crítica | Reopened | CP-038 |
| **BUG-005** | [Registro] El mensaje de error por DNI duplicado dice 'Error inesperado' | S3 - Menor | P3 - Media | Closed | CP-006 |
| **BUG-006** | [Turnos] El campo motivo de consulta acepta 300 caracteres | S3 - Menor | P3 - Media | In Progress | CP-030 |
| **BUG-007** | [Turnos] El historial no distingue visualmente los turnos activos de los cancelados | S3 - Menor | P3 - Media | Won't Fix | CP-035 |
| **BUG-008** | [Registro] El placeholder del campo DNI dice 'Ingrese su DU' | S4 - Trivial | P4 - Baja | Open | CP-001 |
| **BUG-009** | [Turnos] El sistema no envía el recordatorio 24 horas antes del turno | S2 - Mayor | P2 - Alta | In Progress | CP-040 |


---

## BUG-001 — [Registro] El campo contraseña muestra el texto en claro sin interacción del usuario

| Campo | Valor |
|---|---|
| **ID del Bug** | BUG-001 |
| **Entorno** | Staging | Chrome 120 | Windows 11 | Desktop 1920x1080 |
| **Severidad** | S2 - Mayor |
| **Prioridad** | P2 - Alta |
| **Estado actual** | Closed |
| **Requerimiento afectado** | RNF-04 |
| **Caso de prueba vinculado** | CP-013 |
| **Evidencia** | `evidencias/BUG-001-contrasena-visible-chrome.png` |
| **Reportado por** | Jeisson Marín Uribe Luis — 14/07/2026 |

**Precondiciones**

- El paciente no está logueado
- Navegador sin caché (modo incógnito)

**Pasos para reproducir**

1. Ingresar a https://staging.vidasalud.com.ar/registro
2. Hacer clic en el campo 'Contraseña'
3. Escribir cualquier contraseña

**Resultado obtenido**

El texto de la contraseña se muestra en claro desde el primer carácter, sin necesidad de hacer clic en el ícono del ojo. RNF-04 violado.

**Resultado esperado**

Los caracteres deben mostrarse como '••••••' por defecto. Solo al hacer clic en el ícono del ojo deben mostrarse en claro.

**Impacto en el negocio**

Exposición visual de credenciales de una cuenta que da acceso a datos de salud. Riesgo de privacidad y de cumplimiento para una plataforma con 180.000 pacientes.

**Ciclo de vida del defecto**

```
New
-> Open
-> In Progress
-> Fixed (comentario: 'Fix en build 2.1')
-> In Review (CP-013 reejecutado)
-> Closed (comentario: 'Verificado en build 2.1')
```

---

## BUG-002 — [Registro] En Firefox el botón 'Registrarme' no responde al clic

| Campo | Valor |
|---|---|
| **ID del Bug** | BUG-002 |
| **Entorno** | Staging | Firefox 121 | Windows 11 | Desktop 1920x1080 |
| **Severidad** | S1 - Crítico |
| **Prioridad** | P1 - Crítica |
| **Estado actual** | Closed |
| **Requerimiento afectado** | RNF-02 |
| **Caso de prueba vinculado** | CP-036 |
| **Evidencia** | `evidencias/BUG-002-boton-registrarme-firefox.png` |
| **Reportado por** | Jeisson Marín Uribe Luis — 14/07/2026 |

**Precondiciones**

- El paciente no está logueado
- Formulario completo y válido
- Ambos checkboxes marcados

**Pasos para reproducir**

1. Ingresar a https://staging.vidasalud.com.ar/registro en Firefox
2. Completar todos los campos con datos válidos
3. Marcar T&C y el consentimiento de datos de salud
4. Hacer clic en 'Registrarme'
5. Abrir DevTools (F12) > Console y Network

**Resultado obtenido**

El botón no ejecuta ninguna acción. No se genera petición de alta en la pestaña Network y la consola muestra 'Uncaught TypeError: e.submitForm is not a function'. Ningún paciente puede registrarse desde Firefox.

**Resultado esperado**

La cuenta debe crearse igual que en Chrome y redirigir a la pantalla de verificación del código.

**Impacto en el negocio**

Bloqueo total del alta de pacientes en Firefox. Un paciente que no puede registrarse tampoco puede pedir un turno médico: el impacto no es solo comercial, es de acceso a la atención.

**Ciclo de vida del defecto**

```
New
-> Open
-> In Progress
-> Fixed (comentario: 'Fix en build 2.1')
-> In Review (CP-036 reejecutado en Firefox 121)
-> Closed (comentario: 'Verificado en build 2.1')
```

---

## BUG-003 — [Registro] El email con el código de verificación llega a los 20 minutos

| Campo | Valor |
|---|---|
| **ID del Bug** | BUG-003 |
| **Entorno** | Staging | Chrome 120 | Windows 11 | Desktop 1920x1080 |
| **Severidad** | S2 - Mayor |
| **Prioridad** | P2 - Alta |
| **Estado actual** | Fixed |
| **Requerimiento afectado** | RF-07 |
| **Caso de prueba vinculado** | CP-023 (bloquea CP-024) |
| **Evidencia** | `evidencias/BUG-003-email-verificacion-demora.png` |
| **Reportado por** | Jeisson Marín Uribe Luis — 14/07/2026 |

**Precondiciones**

- Registro completado con éxito
- Casilla de correo accesible

**Pasos para reproducir**

1. Completar el registro con datos válidos
2. Abrir la casilla del email registrado
3. Cronometrar el tiempo hasta la recepción
4. Repetir 3 veces

**Resultado obtenido**

El email con el código de verificación llega a los 20 minutos aproximadamente (19:40, 20:15 y 21:02 en las tres mediciones), frente a los 5 minutos comprometidos en RF-07.

**Resultado esperado**

El email con el código de 6 dígitos debe llegar en menos de 5 minutos desde el alta.

**Impacto en el negocio**

El paciente nuevo no puede verificar su cuenta ni pedir un turno en su primera sesión. Aumenta el abandono en el alta y genera llamados al call center.

**Ciclo de vida del defecto**

```
New
-> Open
-> In Progress
-> Fixed (comentario: 'Cola de envío reconfigurada en build 2.2 - pendiente de retest')
```

---

## BUG-004 — [Turnos] En mobile 375 px el botón 'Confirmar turno' queda fuera del viewport

| Campo | Valor |
|---|---|
| **ID del Bug** | BUG-004 |
| **Entorno** | Staging | Chrome 120 (modo responsive 375x667) | Windows 11 |
| **Severidad** | S2 - Mayor |
| **Prioridad** | P1 - Crítica |
| **Estado actual** | Reopened |
| **Requerimiento afectado** | RNF-03 |
| **Caso de prueba vinculado** | CP-038 |
| **Evidencia** | `evidencias/BUG-004-confirmar-turno-fuera-viewport-mobile.png` |
| **Reportado por** | Jeisson Marín Uribe Luis — 14/07/2026 |

**Precondiciones**

- Paciente logueado
- DevTools en modo responsive 375 px
- Turno seleccionado

**Pasos para reproducir**

1. Abrir https://staging.vidasalud.com.ar/turnos con DevTools en 375 px
2. Seleccionar profesional, fecha y horario
3. Completar el motivo de consulta
4. Intentar presionar 'Confirmar turno'

**Resultado obtenido**

El botón queda por debajo del área visible y no se alcanza con scroll vertical; el contenedor tiene overflow oculto. El paciente no puede confirmar el turno desde mobile.

**Resultado esperado**

Todos los controles deben ser visibles y operables en 375 px, sin scroll horizontal ni recorte del contenedor.

**Impacto en el negocio**

Impide reservar turnos desde mobile, que es el canal principal de acceso de los pacientes a la plataforma.

**Ciclo de vida del defecto**

```
New
-> Open
-> In Progress
-> Fixed (comentario: 'Fix en build 2.1')
-> In Review (CP-038 reejecutado)
-> Reopened (comentario: 'El botón sigue recortado en 375x667; se adjunta evidencia nueva BUG-004-retest-build21.png')
```

---

## BUG-005 — [Registro] El mensaje de error por DNI duplicado dice 'Error inesperado'

| Campo | Valor |
|---|---|
| **ID del Bug** | BUG-005 |
| **Entorno** | Staging | Chrome 120 | Windows 11 | Desktop 1920x1080 |
| **Severidad** | S3 - Menor |
| **Prioridad** | P3 - Media |
| **Estado actual** | Closed |
| **Requerimiento afectado** | RF-01 |
| **Caso de prueba vinculado** | CP-006 |
| **Evidencia** | `evidencias/BUG-005-mensaje-dni-duplicado.png` |
| **Reportado por** | Jeisson Marín Uribe Luis — 14/07/2026 |

**Precondiciones**

- Existe un paciente previo registrado con el DNI de prueba

**Pasos para reproducir**

1. Ingresar a /registro
2. Completar el formulario con un DNI ya registrado
3. Marcar ambos checkboxes
4. Clic en 'Registrarme'

**Resultado obtenido**

Se muestra el mensaje genérico 'Error inesperado'. El paciente no sabe que ya tiene cuenta ni que puede recuperar su contraseña.

**Resultado esperado**

Mensaje específico: 'Paciente ya registrado. Inicie sesión o recupere su contraseña'.

**Impacto en el negocio**

Fricción en el alta y aumento de llamados al call center. El paciente puede intentar registrarse varias veces creyendo que el sitio falló.

**Ciclo de vida del defecto**

```
New
-> Open
-> In Progress
-> Fixed (comentario: 'Fix en build 2.1')
-> In Review (CP-006 reejecutado)
-> Closed (comentario: 'Verificado en build 2.1')
```

---

## BUG-006 — [Turnos] El campo motivo de consulta acepta 300 caracteres

| Campo | Valor |
|---|---|
| **ID del Bug** | BUG-006 |
| **Entorno** | Staging | Chrome 120 | Windows 11 | Desktop 1920x1080 |
| **Severidad** | S3 - Menor |
| **Prioridad** | P3 - Media |
| **Estado actual** | In Progress |
| **Requerimiento afectado** | RF-10 |
| **Caso de prueba vinculado** | CP-030 |
| **Evidencia** | `evidencias/BUG-006-motivo-300-caracteres.png` |
| **Reportado por** | Jeisson Marín Uribe Luis — 14/07/2026 |

**Precondiciones**

- Paciente logueado en el formulario de reserva de turno

**Pasos para reproducir**

1. Ingresar a /turnos y seleccionar un profesional y un horario
2. Pegar un texto de 300 caracteres en el motivo de consulta
3. Revisar el contador de caracteres
4. Confirmar el turno

**Resultado obtenido**

El campo acepta los 300 caracteres y el turno se guarda con el texto completo. No hay contador ni mensaje de límite. RF-10 incumplido.

**Resultado esperado**

El campo debe limitarse a 250 caracteres, con contador visible y el mensaje 'Máximo 250 caracteres'.

**Impacto en el negocio**

Textos más largos de lo previsto pueden cortarse en la ficha del profesional o romper el email de confirmación, haciendo que el médico reciba el motivo incompleto.

**Ciclo de vida del defecto**

```
New
-> Open
-> In Progress (asignado al equipo frontend, build 2.2)
```

---

## BUG-007 — [Turnos] El historial no distingue visualmente los turnos activos de los cancelados

| Campo | Valor |
|---|---|
| **ID del Bug** | BUG-007 |
| **Entorno** | Staging | Chrome 120 | Windows 11 | Desktop 1920x1080 |
| **Severidad** | S3 - Menor |
| **Prioridad** | P3 - Media |
| **Estado actual** | Won't Fix |
| **Requerimiento afectado** | RF-12 |
| **Caso de prueba vinculado** | CP-035 |
| **Evidencia** | `evidencias/BUG-007-historial-sin-estado.png` |
| **Reportado por** | Jeisson Marín Uribe Luis — 14/07/2026 |

**Precondiciones**

- Paciente con al menos un turno activo y uno cancelado

**Pasos para reproducir**

1. Ingresar a 'Mis turnos'
2. Abrir la pestaña de historial
3. Comparar un turno activo con uno cancelado

**Resultado obtenido**

Ambos turnos se muestran con el mismo formato: no hay etiqueta de estado, color ni ícono que los diferencie.

**Resultado esperado**

El turno cancelado debe mostrar la etiqueta 'Cancelado' y diferenciarse visualmente del activo.

**Impacto en el negocio**

El paciente puede creer que un turno cancelado sigue vigente y no presentarse, o presentarse a uno inexistente. Impacto directo en el ausentismo de la agenda médica.

**Ciclo de vida del defecto**

```
New
-> Open
-> Won't Fix (decisión del Product Owner: el rediseño del historial está planificado para el Sprint 6; se acepta el riesgo y se documenta)
```

---

## BUG-008 — [Registro] El placeholder del campo DNI dice 'Ingrese su DU'

| Campo | Valor |
|---|---|
| **ID del Bug** | BUG-008 |
| **Entorno** | Staging | Chrome 120 | Windows 11 | Desktop 1920x1080 |
| **Severidad** | S4 - Trivial |
| **Prioridad** | P4 - Baja |
| **Estado actual** | Open |
| **Requerimiento afectado** | RF-01 |
| **Caso de prueba vinculado** | CP-001 |
| **Evidencia** | `evidencias/BUG-008-placeholder-dni.png` |
| **Reportado por** | Jeisson Marín Uribe Luis — 14/07/2026 |

**Precondiciones**

- El paciente no está logueado

**Pasos para reproducir**

1. Ingresar a https://staging.vidasalud.com.ar/registro
2. Observar el texto placeholder del campo DNI

**Resultado obtenido**

El placeholder del campo DNI muestra el texto 'Ingrese su DU'.

**Resultado esperado**

El placeholder debe decir 'Ingrese su DNI'.

**Impacto en el negocio**

Confusión menor en el formulario de alta. No bloquea el flujo pero afecta la percepción de calidad de una plataforma de salud.

**Ciclo de vida del defecto**

```
New
-> Open (aceptado y priorizado para el backlog del Sprint 6)
```

---

## BUG-009 — [Turnos] El sistema no envía el recordatorio 24 horas antes del turno

| Campo | Valor |
|---|---|
| **ID del Bug** | BUG-009 |
| **Entorno** | Staging | Chrome 120 | Windows 11 | Desktop 1920x1080 |
| **Severidad** | S2 - Mayor |
| **Prioridad** | P2 - Alta |
| **Estado actual** | In Progress |
| **Requerimiento afectado** | RF-13 |
| **Caso de prueba vinculado** | CP-040 |
| **Evidencia** | `evidencias/BUG-009-sin-recordatorio-24hs.png` |
| **Reportado por** | Jeisson Marín Uribe Luis — 14/07/2026 |

**Precondiciones**

- Paciente con turnos programados a más de 24 horas
- Casilla de correo accesible

**Pasos para reproducir**

1. Reservar tres turnos con más de 24 hs de anticipación
2. Esperar a la franja de 24 hs previas a cada turno
3. Revisar la casilla del paciente, incluida la carpeta de spam

**Resultado obtenido**

No llega ningún recordatorio en ninguno de los tres turnos probados. RF-13 no se cumple: la tarea programada no se ejecuta o no está implementada.

**Resultado esperado**

El sistema debe enviar un recordatorio por email dentro de las 24 horas previas al turno.

**Impacto en el negocio**

El recordatorio es la principal herramienta contra el ausentismo. Sin él, los turnos perdidos ocupan agenda médica que otro paciente podría usar.

**Ciclo de vida del defecto**

```
New
-> Open
-> In Progress (asignado al equipo backend, build 2.2)
```

---

## Resumen por severidad

| Severidad | Cantidad | Bugs |
|---|---|---|
| S1 — Crítico | 1 | BUG-002 |
| S2 — Mayor | 4 | BUG-001, BUG-003, BUG-004, BUG-009 |
| S3 — Menor | 3 | BUG-005, BUG-006, BUG-007 |
| S4 — Trivial | 1 | BUG-008 |

**Bloqueantes para producción:** BUG-002 (S1) y los tres S2 (BUG-001, BUG-003, BUG-004). Ver la justificación completa en `informe-final/informe-final-qa-shopnow.pdf`.
