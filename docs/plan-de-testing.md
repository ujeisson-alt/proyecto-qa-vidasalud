# Plan de Testing — VidaSalud S.A. | Módulo de Registro de Pacientes y Turnos Online

| Campo | Detalle |
|---|---|
| **Proyecto** | VidaSalud QA — Registro y Turnos |
| **Módulo bajo prueba** | Registro de nuevo paciente y gestión de turnos online |
| **Entorno** | Staging — `https://staging.vidasalud.com.ar` |
| **Metodología** | SCRUM — sprints semanales |
| **QA Tester** | Jeisson Marín Uribe Luis (QA Tester Junior) |
| **Equipo** | Product Owner, Scrum Master, QA Lead y 4 desarrolladores del equipo de producto |
| **Período** | 22/06/2026 – 17/07/2026 (4 sprints) |
| **Versión del plan** | 1.2 (actualizada al cierre de la Fase 3) |

---

## 1. Objetivo

Verificar que el módulo de Registro de Pacientes y Turnos Online cumple los 13 requerimientos funcionales y los 5 no funcionales definidos para el MVP, antes de habilitar su paso a producción.

El módulo es el punto de entrada al ecosistema de atención de VidaSalud: si falla, un paciente no puede crear su cuenta, pedir un turno médico ni acceder a su historial. A diferencia de un e-commerce, acá el costo de un defecto no es solo una venta perdida — es un paciente que no llega a la consulta.

## 2. Alcance

### Incluido
- Registro de paciente: validaciones de DNI, email, contraseña, obra social y consentimientos.
- Email de verificación con código de 6 dígitos.
- Turnos: búsqueda de especialidad, reserva, motivo de consulta, confirmación por email.
- Cancelación de turnos e historial.
- Recordatorio automático 24 horas antes del turno.
- Compatibilidad en Chrome, Firefox y Safari mobile.
- Responsive en 375 px, 768 px y 1920 px.
- Validaciones básicas de seguridad y privacidad de datos de salud (RNF-04 y RNF-05).

### Fuera de alcance
- Automatización de pruebas (Cypress, Playwright).
- Testing avanzado de APIs con Postman.
- Pruebas de carga o estrés (JMeter, k6).
- Testing de seguridad avanzado / pentesting.
- Acceso al código fuente y gestión del backlog de producto.
- Módulo de teleconsulta (pertenece a otro sprint).

## 3. Estrategia de pruebas

| Tipo de prueba | Objetivo | Técnica aplicada |
|---|---|---|
| Funcional positiva | Confirmar que el alta y la reserva funcionan con datos válidos | Casos de flujo principal |
| Funcional negativa | Confirmar que el sistema rechaza datos inválidos con el mensaje correcto | Partición de equivalencias |
| Valores límite | Verificar el comportamiento en los bordes permitidos y fuera de ellos | Análisis de valores límite |
| Compatibilidad | Detectar diferencias entre navegadores | Ejecución cruzada Chrome / Firefox / Safari |
| Interfaz / responsive | Validar visibilidad y operabilidad de los controles | Inspección con DevTools en 375 px y 768 px |
| No funcional | Medir tiempos de respuesta y verificar el manejo de datos de salud | DevTools → Network y Application |

### Técnicas de diseño aplicadas

**Partición de equivalencias — campo DNI (RF-01: entre 7 y 8 dígitos numéricos, único)**

| Partición | Dato de ejemplo | Clase | Caso |
|---|---|---|---|
| Menos de 7 dígitos | `123456` | Inválida | CP-003 |
| 7 dígitos | `1234567` | Válida | CP-002 |
| 8 dígitos | `20123456` | Válida | CP-001 |
| 9 dígitos | `123456789` | Inválida | CP-004 |
| Con caracteres no numéricos | `1234AB78` | Inválida | CP-005 |
| DNI ya registrado | `20123456` | Inválida | CP-006 |

**Valores límite — motivo de consulta (RF-10: máximo 250 caracteres)**

| Valor | Resultado esperado | Caso |
|---|---|---|
| 250 caracteres | Válido | CP-029 |
| 251 caracteres | Inválido | CP-030 |
| Campo vacío | Inválido | CP-031 |

**Valores límite — contraseña (RF-03)**: 7 caracteres → inválida (CP-012) · 8 caracteres válidos → válida (CP-013) · sin mayúscula → inválida (CP-014) · sin número → inválida (CP-015).

**Valores límite — ventana de cancelación (RF-12: hasta 2 horas antes)**: turno a 48 h → cancelable (CP-033) · turno a 1 h 30 min → no cancelable (CP-034).

## 4. Entorno y datos de prueba

| Elemento | Configuración |
|---|---|
| URL | `https://staging.vidasalud.com.ar` |
| Navegadores | Chrome 120, Firefox 121, Safari mobile |
| Resoluciones | Desktop 1920×1080 · Tablet 768 px · Mobile 375 px |
| DNI de prueba | 20123456, 20123457, 20123458 (incrementales, para evitar duplicados) |
| Emails de prueba | `qa_test01@mail.com` … `qa_test07@mail.com` |
| Contraseña de prueba | `TestPass1234!` (cumple RF-03) |
| Usuario de test | `qa_tester@vidasalud.com.ar` / `VidaSalud2024!` |
| Herramientas | Jira · Google Sheets · Chrome DevTools · GitHub · Lightshot |

> Las credenciales y los datos de paciente listados son ficticios y pertenecen a un entorno educativo simulado. No se usó ningún dato real de salud.

## 5. Criterios de entrada y salida

**Criterios de entrada**
- Los 13 RF y 5 RNF están documentados y aprobados.
- La matriz de trazabilidad cubre el 100 % de los requerimientos.
- El entorno de staging está desplegado y accesible.
- El proyecto en Jira tiene el Epic, las Stories y el Sprint activo.

**Criterios de salida**
- El 100 % de los casos diseñados fue ejecutado o formalmente bloqueado y documentado.
- Todos los defectos encontrados están reportados en Jira con evidencia y caso vinculado.
- Cero defectos S1 (críticos) abiertos para recomendar GO.
- Ningún defecto abierto que comprometa la privacidad de datos de salud (RNF-05).
- El informe final está emitido con recomendación GO / NO-GO justificada con datos.

## 6. Criterios de severidad y prioridad

| Severidad | Definición | Prioridad | Definición |
|---|---|---|---|
| S1 — Crítico | Bloquea una funcionalidad esencial, sin workaround | P1 — Crítica | Debe corregirse antes del go-live |
| S2 — Mayor | Afecta gravemente una función importante; hay workaround parcial | P2 — Alta | Se corrige en el sprint actual |
| S3 — Menor | Falla de comportamiento o mensaje que no impide completar el flujo | P3 — Media | Se planifica para el siguiente sprint |
| S4 — Trivial | Defecto cosmético o de texto, sin impacto funcional | P4 — Baja | Se atiende cuando haya capacidad |

> La severidad la define QA según el impacto técnico; la prioridad la define el Product Owner según el impacto en el negocio y en la atención del paciente. Por eso BUG-004 es S2 pero P1: no es crítico técnicamente, pero impide reservar turnos desde mobile.

## 7. Ciclo de vida del defecto en Jira

```
New → Open → In Progress → Fixed → In Review → Closed
                                        ↓
                                    Reopened → In Progress → …

          Open → Won't Fix   (decisión del Product Owner)
```

| Estado | Responsable | Qué significa |
|---|---|---|
| New | QA | Bug recién reportado, esperando revisión |
| Open | QA Lead | Bug confirmado y aceptado por el equipo |
| In Progress | Dev Team | El desarrollador está trabajando en el fix |
| Fixed | Dev Team | El fix fue implementado y subido a staging |
| In Review | QA | QA reejecuta el caso vinculado para confirmar el fix |
| Closed | QA | El bug fue corregido y verificado |
| Reopened | QA | El fix no funcionó: el bug sigue existiendo |
| Won't Fix | Product Owner | El equipo decide no corregirlo en este sprint |

## 8. Entregables

| Entregable | Ubicación |
|---|---|
| Análisis de requerimientos | `docs/analisis-requerimientos.xlsx` |
| Matriz de trazabilidad | `docs/matriz-trazabilidad.xlsx` |
| Plan de testing | `docs/plan-de-testing.md` |
| Daily reports | `docs/daily-reports.md` |
| Matriz de casos de prueba con resultados | `casos-de-prueba/matriz-de-prueba.xlsx` |
| Bug reports detallados | `bugs/bug-reports-detallados.md` |
| Resumen de bugs | `bugs/reporte-bugs-resumen.xlsx` |
| Evidencias | `evidencias/` |
| Informe final | `informe-final/informe-final-qa-vidasalud.pdf` |

## 9. Cronograma

| Sprint | Semana | Foco | Horas |
|---|---|---|---|
| Sprint 1 | 22–28/06/2026 | Análisis de requerimientos, matriz de trazabilidad, setup de Jira | 8–10 h |
| Sprint 2 | 29/06–05/07/2026 | Diseño de los 43 casos de prueba | 10–12 h |
| Sprint 3 | 06–12/07/2026 | Ejecución, evidencias y actualización de la matriz | 12–15 h |
| Sprint 4 | 13–17/07/2026 | Reporte de defectos, informe final y portafolio | 12–14 h |

## 10. Riesgos del proyecto de testing

| Riesgo | Probabilidad | Impacto | Mitigación |
|---|---|---|---|
| No contar con dispositivo iOS para Safari mobile | Alta | Medio | Documentar el caso como *Blocked* y escalar a la QA Lead para gestionar un laboratorio de dispositivos |
| Requerimientos con ventanas de tiempo largas (recordatorio de 24 h) que no entran en la ventana de ejecución | Alta | Alto | Reservar turnos al inicio del sprint para que la franja de 24 h caiga dentro de la ejecución (aplicado en CP-040) |
| Demoras en el envío de emails que bloqueen la verificación | Media | Alto | Definir una ventana de espera máxima y documentar el bloqueo (ocurrió: BUG-003 bloqueó CP-024) |
| Brechas de cobertura en requerimientos sin casos | Media | Alto | Revisar la matriz de trazabilidad al cerrar cada fase (se detectó y corrigió: CP-040 a CP-043) |
| Uso accidental de datos de salud reales | Baja | Muy alto | Trabajar solo con los DNI y emails de prueba definidos en este plan |
