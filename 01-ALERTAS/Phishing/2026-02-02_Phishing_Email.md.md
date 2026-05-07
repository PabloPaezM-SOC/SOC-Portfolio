# Alerta: Phishing Email / Credential Harvesting
**Fecha:** 2026-02-02  
**Tipo de alerta:** Email Click / Credential Harvesting  
**Usuario:** user3@company.com

## Descripción
Usuario hace click en link de phishing micros0ft-secure.com; intento de login posterior desde IP externa.

## Evidencia
- Timestamp click 18:21:10  
- Proxy logs; Auth log con intento fallido desde IP 185.71.66.90

## Acciones L1
1. Monitoreo de actividad  
2. Reset de credenciales  
3. Revisar si otros usuarios afectados

## Decisión
Incidente

## Escalamiento
Escalar a L2/L3 con prioridad media-alta

## Notas
Typosquatting; riesgo de credential compromise; L1 documenta y escalamiento

Tags: #phishing #credential_harvesting #media

Relacionadas: [[2026-02-02_OAuth_Phishing]]
