# Alerta: Lateral Movement / Credential Stuffing Interno
**Fecha:** 2026-02-02  
**Tipo de alerta:** Multiple Internal Login Failures – Possible Lateral Movement  
**Usuario:** user4@company.com  
**Host Origen / Destino:** WS-10 → FS-02, FS-03, FS-04 → login exitoso en FS-02

## Descripción
Usuario realiza intentos fallidos en 3 hosts distintos en menos de 1 minuto, seguido de login exitoso; posible compromiso o malware.

## Evidencia
- Timestamps 19:05:01 – 19:06:05  
- Logs AD / Linux

## Acciones L1
1. Bloqueo temporal sesión/IP  
2. Contactar usuario  
3. Monitoreo de hosts

## Decisión
Incidente

## Escalamiento
Escalar urgente a L2/L3, prioridad alta

## Notas
Patrón típico de movimiento lateral / credential stuffing interno; L1 detecta y escala

Tags: #credential_stuffing #interno #alta

Relacionadas: [[2026-02-02_Credential_Stuffing_Externo]]
