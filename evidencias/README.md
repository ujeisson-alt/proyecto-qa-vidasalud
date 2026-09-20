# Evidencias de testing — VidaSalud S.A.

Capturas de la ejecución de cada caso de prueba y de cada defecto reportado.

> **Nota sobre el entorno.** `staging.vidasalud.com.ar` es un entorno **ficticio** creado con fines educativos (proyecto formativo *Guía de proyectos para QA Tester* — Talently Lab). Las capturas de esta carpeta son **evidencias simuladas** que reproducen el formato, la nomenclatura y el contenido que tendría una evidencia real. No se utilizó ningún dato de salud real: todos los pacientes, DNI y turnos son de prueba.

## Convención de nombres

```
CP-XXX-descripcion-navegador.png     → evidencia de un caso de prueba
BUG-XXX-descripcion-navegador.png    → evidencia de un defecto
```

Cada archivo se nombra en el momento de la captura, nunca al final del sprint.

## Evidencias de casos de prueba

| Caso | Estado | Archivo |
|---|---|---|
| CP-001 | Passed | `CP-001-dni-8-digitos-chrome.png` |
| CP-002 | Passed | `CP-002-dni-7-digitos-chrome.png` |
| CP-003 | Passed | `CP-003-dni-6-digitos-chrome.png` |
| CP-004 | Passed | `CP-004-dni-9-digitos-chrome.png` |
| CP-005 | Passed | `CP-005-dni-con-letras-chrome.png` |
| CP-006 | Failed | `CP-006-dni-duplicado-chrome.png` |
| CP-007 | Passed | `CP-007-email-valido-chrome.png` |
| CP-008 | Passed | `CP-008-email-sin-arroba-chrome.png` |
| CP-009 | Passed | `CP-009-email-sin-dominio-chrome.png` |
| CP-010 | Passed | `CP-010-email-duplicado-chrome.png` |
| CP-011 | Passed | `CP-011-email-vacio-chrome.png` |
| CP-012 | Passed | `CP-012-password-7-caracteres-chrome.png` |
| CP-013 | Failed | `CP-013-password-8-caracteres-chrome.png` |
| CP-014 | Passed | `CP-014-password-sin-mayuscula-chrome.png` |
| CP-015 | Passed | `CP-015-password-sin-numero-chrome.png` |
| CP-016 | Passed | `CP-016-confirmacion-distinta-chrome.png` |
| CP-017 | Passed | `CP-017-password-vacio-chrome.png` |
| CP-018 | Passed | `CP-018-obra-social-listado-chrome.png` |
| CP-019 | Passed | `CP-019-obra-social-particular-chrome.png` |
| CP-020 | Passed | `CP-020-tyc-sin-marcar-chrome.png` |
| CP-021 | Passed | `CP-021-consentimiento-sin-marcar-chrome.png` |
| CP-022 | Passed | `CP-022-registro-exitoso-chrome.png` |
| CP-023 | Failed | `CP-023-email-verificacion-demora-chrome.png` |
| CP-024 | Blocked | `CP-024-bloqueado-por-BUG-003.png` |
| CP-025 | Passed | `CP-025-busqueda-cardiologia-chrome.png` |
| CP-026 | Passed | `CP-026-reserva-horario-disponible-chrome.png` |
| CP-027 | Passed | `CP-027-horario-no-disponible-chrome.png` |
| CP-028 | Passed | `CP-028-fecha-pasada-chrome.png` |
| CP-029 | Passed | `CP-029-motivo-250-caracteres-chrome.png` |
| CP-030 | Failed | `CP-030-motivo-251-caracteres-chrome.png` |
| CP-031 | Passed | `CP-031-motivo-vacio-chrome.png` |
| CP-032 | Passed | `CP-032-email-confirmacion-turno-chrome.png` |
| CP-033 | Passed | `CP-033-cancelacion-anticipada-chrome.png` |
| CP-034 | Passed | `CP-034-cancelacion-tardia-chrome.png` |
| CP-035 | Failed | `CP-035-historial-turnos-chrome.png` |
| CP-036 | Failed | `CP-036-registro-firefox.png` |
| CP-037 | Blocked | `CP-037-bloqueado-sin-dispositivo-ios.png` |
| CP-038 | Failed | `CP-038-responsive-375px-chrome.png` |
| CP-039 | Passed | `CP-039-responsive-768px-chrome.png` |
| CP-040 | Failed | `CP-040-recordatorio-24hs-chrome.png` |
| CP-041 | Passed | `CP-041-tiempo-respuesta-chrome.png` |
| CP-042 | Passed | `CP-042-privacidad-datos-salud-chrome.png` |
| CP-043 | Passed | `CP-043-filtro-obra-social-chrome.png` |

## Evidencias de defectos

| Bug | Severidad | Archivo |
|---|---|---|
| BUG-001 | S2 - Mayor | `BUG-001-contrasena-visible-chrome.png` |
| BUG-002 | S1 - Crítico | `BUG-002-boton-registrarme-firefox.png` |
| BUG-003 | S2 - Mayor | `BUG-003-email-verificacion-demora.png` |
| BUG-004 | S2 - Mayor | `BUG-004-confirmar-turno-fuera-viewport-mobile.png` |
| BUG-005 | S3 - Menor | `BUG-005-mensaje-dni-duplicado.png` |
| BUG-006 | S3 - Menor | `BUG-006-motivo-300-caracteres.png` |
| BUG-007 | S3 - Menor | `BUG-007-historial-sin-estado.png` |
| BUG-008 | S4 - Trivial | `BUG-008-placeholder-dni.png` |
| BUG-009 | S2 - Mayor | `BUG-009-sin-recordatorio-24hs.png` |
| BUG-004 | S2 - Mayor | `BUG-004-retest-build21.png` (evidencia del retest que motivó la reapertura) |

**Total: 53 evidencias.**
