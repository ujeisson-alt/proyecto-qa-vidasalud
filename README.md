# Proyecto QA End-to-End — VidaSalud: Registro de Pacientes y Turnos Online

![Estado](https://img.shields.io/badge/estado-cerrado-success) ![Conclusión](https://img.shields.io/badge/recomendaci%C3%B3n-NO--GO-critical) ![Casos](https://img.shields.io/badge/casos%20de%20prueba-43-blue) ![Bugs](https://img.shields.io/badge/bugs-9-orange) ![Cobertura](https://img.shields.io/badge/cobertura%20de%20requerimientos-100%25-brightgreen)

## Descripción

Testing end-to-end del módulo de Registro de Pacientes y Turnos Online de **VidaSalud S.A.**, plataforma de salud digital argentina *(empresa ficticia — proyecto educativo)*. El módulo cubre el alta de pacientes (DNI, obra social, consentimiento de datos de salud, verificación por email) y la gestión de turnos médicos (búsqueda de especialidad, reserva, cancelación, historial y recordatorios).

A diferencia de un e-commerce, acá un defecto no cuesta una venta: cuesta una consulta médica a la que el paciente no llega. Esa fue la vara para priorizar severidad e impacto durante todo el proyecto.

## Mi Rol

**QA Tester Junior** — responsable del análisis de requerimientos, el diseño y la ejecución de pruebas funcionales, de compatibilidad, de interfaz y de validaciones de seguridad y privacidad, y de la elaboración del informe final con la recomendación de go-live.

## Stack de Herramientas

`Jira` · `Google Sheets / Excel` · `Chrome DevTools` · `GitHub` · `Lightshot` · `SCRUM`

## Métricas del Proyecto

| Indicador | Resultado |
|---|---|
| Casos diseñados | **43** (39 del diseño base + 4 adicionales para cerrar una brecha de cobertura) |
| Casos ejecutados | **41 (95,3 %)** — 2 bloqueados y documentados |
| Passed / Failed / Blocked | **33 / 8 / 2** |
| Tasa de éxito | **76,7 %** sobre el total · **80,5 %** sobre los ejecutados |
| Bugs encontrados | **9** — 1 crítico (S1), 4 mayores (S2), 3 menores (S3), 1 trivial (S4) |
| Cobertura de requerimientos | **100 %** (13 RF + 5 RNF) |
| Evidencias | 53 capturas nombradas por caso y por defecto |
| Técnicas aplicadas | Partición de equivalencias · Valores límite |

## Hallazgos destacados

| Bug | Severidad | Hallazgo | Impacto |
|---|---|---|---|
| **BUG-002** | S1 — Crítico | En Firefox el botón "Registrarme" no responde: no se dispara la petición de alta y la consola arroja `Uncaught TypeError: e.submitForm is not a function` | Ningún paciente puede crear su cuenta desde Firefox, y sin cuenta no hay turno |
| **BUG-004** | S2 — Mayor (P1) | En mobile 375 px el botón "Confirmar turno" queda fuera del viewport | Impide reservar turnos desde el canal principal de los pacientes. **Reabierto** tras el retest del build 2.1 |
| **BUG-009** | S2 — Mayor | El sistema no envía el recordatorio 24 hs antes del turno (RF-13) | Sin recordatorio aumenta el ausentismo: el turno perdido ocupa agenda médica que otro paciente podría usar |

## Conclusión

> **NO-GO recomendado.** Existe 1 defecto crítico (BUG-002) que bloquea el alta de pacientes en Firefox y 4 defectos mayores que afectan la reserva de turnos desde mobile, el recordatorio de 24 horas, la verificación de la cuenta y el enmascarado de la contraseña. El criterio de salida definido en el plan de testing exige cero defectos S1 abiertos para recomendar GO.

La justificación completa, con datos y condiciones para revertir la recomendación, está en el [informe final](informe-final/informe-final-qa-vidasalud.pdf).

## Estructura del repositorio

```
proyecto-qa-vidasalud/
├── README.md
├── docs/
│   ├── analisis-requerimientos.xlsx    ← 13 RF + 5 RNF con prioridad, criterio de aceptación y riesgo
│   ├── matriz-trazabilidad.xlsx        ← requerimiento ↔ casos ↔ resultado ↔ bugs
│   ├── plan-de-testing.md              ← alcance, estrategia, técnicas, criterios y cronograma
│   └── daily-reports.md                ← 15 daily reports de los 4 sprints
├── casos-de-prueba/
│   └── matriz-de-prueba.xlsx           ← 43 casos con pasos, datos y resultados reales + dashboard
├── evidencias/
│   ├── README.md
│   └── (53 capturas nombradas CP-XXX / BUG-XXX)
├── bugs/
│   ├── bug-reports-detallados.md       ← los 9 bugs con plantilla completa y ciclo de vida
│   └── reporte-bugs-resumen.xlsx       ← resumen por severidad y por estado en Jira
├── informe-final/
│   └── informe-final-qa-vidasalud.pdf  ← informe con las 6 secciones y el GO/NO-GO
└── presentacion/
    ├── sprint-review-qa-vidasalud.pdf  ← deck de 15 diapositivas del Sprint Review (12 min)
    └── guion-sprint-review.md          ← guion, tiempos y preguntas probables con su respuesta
```

## Cómo recorrer este portafolio

1. **`docs/plan-de-testing.md`** — qué se testeó, con qué estrategia y bajo qué criterios de entrada y salida.
2. **`docs/analisis-requerimientos.xlsx`** y **`docs/matriz-trazabilidad.xlsx`** — cómo se pasó de la documentación funcional a una cobertura verificable del 100 %.
3. **`casos-de-prueba/matriz-de-prueba.xlsx`** — los 43 casos con su resultado real; la hoja *Dashboard* calcula todas las métricas con fórmulas.
4. **`bugs/bug-reports-detallados.md`** — los 9 defectos con pasos de reproducción, evidencia, impacto y ciclo de vida en Jira (incluye un Reopened y un Won't Fix).
5. **`informe-final/informe-final-qa-vidasalud.pdf`** — el documento de cierre y la recomendación GO / NO-GO.
6. **`presentacion/sprint-review-qa-vidasalud.pdf`** — cómo se presentaron estos resultados al equipo en el Sprint Review.

## Decisiones de testing que vale la pena destacar

- **Brecha de cobertura detectada y cerrada:** el diseño base de 39 casos dejaba sin verificar RF-13 (recordatorio de 24 hs), RNF-01 (tiempo de respuesta) y RNF-05 (privacidad de los datos de salud). Se diseñaron CP-040 a CP-043 antes de ejecutar, y CP-040 terminó destapando BUG-009.
- **Un requerimiento con ventana de 24 horas exige planificar la ejecución:** los turnos de prueba se reservaron al inicio del sprint para que la franja del recordatorio cayera dentro de la ventana de testing. Sin esa previsión, RF-13 habría quedado sin verificar.
- **Bloqueos documentados, no ocultados:** CP-024 quedó bloqueado por BUG-003 y CP-037 por no disponer de un dispositivo iOS. Ambos están registrados como *Blocked* con su causa, y el riesgo de CP-037 fue escalado a la QA Lead.
- **Severidad y prioridad se gestionan por separado:** BUG-004 es S2 por impacto técnico, pero P1 por impacto en la atención, ya que mobile es el canal principal de los pacientes.
- **Un defecto puede cerrarse sin corregirse:** BUG-007 quedó en *Won't Fix* por decisión del Product Owner, con el riesgo documentado. BUG-004, en cambio, se **reabrió** tras fallar el retest del build 2.1 en lugar de cerrarse por confianza en el fix.

---

*Proyecto formativo de la Guía de proyectos para QA Tester (Talently Lab). VidaSalud S.A., su entorno de staging, su equipo, sus pacientes y los defectos descritos son ficticios y tienen fines exclusivamente educativos. No se utilizó ningún dato de salud real.*

**Autor:** Jeisson Marín Uribe Luis — QA Tester Junior · Bogotá, Colombia
