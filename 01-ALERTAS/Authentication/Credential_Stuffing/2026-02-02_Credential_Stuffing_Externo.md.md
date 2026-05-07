# Alerta: Credential Stuffing Externo
**Fecha:** 2026-02-02  
**Tipo de alerta:** Multiple Failed Logins → Successful Authentication  
**Usuario:** user1  
**Host / IP:** 185.221.88.77

## Descripción
Usuario con 3 logins fallidos seguidos por un login exitoso en menos de 1 minuto. Patrón sospechoso de brute force o credential stuffing.

## Evidencia
- Logs de Linux auth; timestamps 15:21:03 – 15:21:20  
- Número de intentos fallidos: 3

## Acciones L1
1. Registrar alerta  
2. Recomendar reset de credenciales  
3. Bloquear IP temporal

## Decisión
Incidente

## Escalamiento
Escalar a L2/L3 con prioridad alta

## Notas
Patrón típico de acceso comprometido; L1 no investiga origen, solo detecta y escala

Tags: #credential_stuffing #externo #alta

Relacionadas: [[2026-02-02_Lateral_Movement]]
