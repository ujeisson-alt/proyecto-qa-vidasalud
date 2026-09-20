# Guion del Sprint Review — VidaSalud QA

> Presentación de cierre del Sprint 4 ante el Product Owner, el Scrum Master, la QA Lead y el equipo de desarrollo.
> Duración prevista: 12 minutos de exposición + 3 minutos de preguntas.

| # | Diapositiva | Mensaje central | Tiempo |
|---|---|---|---|
| 1 | Portada | Vengo a contar en qué estado está el módulo y si podemos salir a producción | 0:30 |
| 2 | Lo que vamos a ver | Recorrido de la presentación; preguntas al final | 0:30 |
| 3 | Alcance | Qué se testeó y qué quedó explícitamente fuera | 1:00 |
| 4 | Cuatro sprints | El ciclo completo, y por qué los turnos de prueba se reservaron el primer día | 1:00 |
| 5 | Diseño de pruebas | Técnicas aplicadas y la brecha de cobertura cerrada antes de ejecutar | 1:30 |
| 6 | Métricas | 43 casos, 33 Passed, 8 Failed, 2 Blocked; 5 de las 8 fallas frenan una acción del paciente | 1:30 |
| 7 | Defectos por severidad | 9 defectos y su estado real en Jira, incluido el Won't Fix | 1:00 |
| 8 | BUG-002 | El defecto crítico: en Firefox ningún paciente puede registrarse | 1:30 |
| 9 | Los cuatro mayores | Mobile, recordatorio de 24 hs, verificación y contraseña visible | 1:30 |
| 10 | Cobertura | 100 % de requerimientos verificados; dos verificaciones parciales | 1:00 |
| 11 | NO-GO | La recomendación, dicha con calma | 0:20 |
| 12 | Cuatro datos | Por qué NO-GO, con evidencia y no con opinión | 2:00 |
| 13 | Condiciones para GO | La lista corta y concreta de lo que falta | 1:00 |
| 14 | Próximos pasos | Quién hace qué en el Sprint 6 | 1:30 |
| 15 | Cierre | Dónde está documentado todo + preguntas | 2:00 |

## Preguntas probables y cómo responderlas

**¿Cuándo podríamos salir a producción?**  
Un sprint de corrección para los cuatro bloqueantes, más dos días de regresión sobre los 43 casos. La fecha depende de cuándo lleguen los fixes, no del testing.

**¿Por qué BUG-007 quedó en Won't Fix? ¿No es un riesgo?**  
Lo es, y por eso está documentado con su impacto: el paciente puede creer que un turno cancelado sigue vigente. La decisión de diferirlo al Sprint 6 es del Product Owner, que ya tiene planificado el rediseño del historial. QA reporta el riesgo; priorizar es del PO.

**¿Por qué BUG-004 es S2 y no S1 si bloquea mobile?**  
La severidad mide el impacto técnico y existe un camino alternativo: el paciente puede reservar desde desktop. La prioridad, que la define el PO por impacto de negocio, sí es P1.

**¿Cómo sabemos que BUG-002 no es un problema de tu máquina?**  
Se reprodujo en dos equipos distintos, con perfil limpio de Firefox, y falla el 100 % de las veces. La evidencia incluye la consola y la pestaña Network sin petición de alta.

**¿Por qué el recordatorio de 24 horas se probó recién en el Sprint 3?**  
Se probó en el Sprint 3, pero los turnos se reservaron el primer día del sprint justamente para que la franja de 24 horas previas cayera dentro de la ventana de ejecución. Sin esa previsión, RF-13 habría quedado sin verificar y BUG-009 no se habría detectado.

**¿Los dos casos bloqueados no deberían contarse como fallidos?**  
No: un caso bloqueado no se ejecutó, no falló. Contarlo como fallido inventaría un defecto que no observamos. Por eso se reportan aparte y con su causa.

**¿Se usaron datos de pacientes reales?**  
No. Todo el testing se hizo con los DNI, emails y turnos de prueba definidos en el plan, sobre el entorno de staging. RNF-05 (privacidad de datos de salud) se verificó explícitamente en CP-042.

---

El deck completo está en `presentacion/sprint-review-qa-vidasalud.pdf`. Las notas del orador de cada diapositiva contienen estas mismas indicaciones.
