# Alerta: OAuth Phishing / Token Theft
**Fecha:** 2026-02-02  
**Tipo de alerta:** Suspicious OAuth Application Consent  
**Usuario:** user2@company.com

## Descripción
Usuario otorga consentimiento a app no aprobada con permisos Mail.Read, User.Read y offline_access; riesgo de token persistente.

## Evidencia
- Timestamp 17:02:11  
- AppDisplayName: Microsoft Secure Mail  
- IP: 179.23.88.14

## Acciones L1
1. Registrar alerta  
2. Recomendar reseteo de tokens  
3. Monitorear usuario y app

## Decisión
Incidente

## Escalamiento
Escalar urgente a L2/L3, prioridad media-alta

## Notas
OAuth phishing bypassa MFA; L1 no investiga tokens, solo detecta y escala

Tags: #phishing #oauth #alta

Relacionadas: [[2026-02-02_Phishing_Email]]
