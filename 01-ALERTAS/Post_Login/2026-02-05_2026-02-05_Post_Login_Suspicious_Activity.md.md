# Alerta: Actividad Sospechosa Post-Login
**Fecha:** 2026-02-05  
**Tipo de alerta:** Suspicious activity after successful login  
**Usuario / Host / IP:** a.morales / 190.110.44.12  

## Descripción
Alerta HIGH generada en SIEM: “Suspicious activity after successful login”.  
Se detecta login exitoso desde un dispositivo nuevo y una ubicación geográfica distinta a la HR del usuario.  
Acciones post-login incluyen acceso a archivos sensibles y creación de OAuth token.

## Evidencia
1. **Auth Log**:  
	2026-02-05 14:22:11 user=a.morales src_ip=190.110.44.12 result=SUCCESS
2. **Geo IP**: IP 190.110.44.12 → Peru (usuario HR: Chile, sin VPN corporativa)  
3. **User Info**: MFA ENABLED & APPROVED, nuevo dispositivo detectado  
4. **Activity Log** (post login):  
   - 14:23:02 Accessed `/admin/export_users.csv`  
   - 14:23:18 Accessed `/finance/payroll_2025.xlsx`  
   - 14:24:01 Created OAuth token  
5. **EDR**: No malware detectado

## Hipótesis de ataque
- Posible compromiso de credenciales o phishing multi-factor  
- Acceso no autorizado a datos sensibles  
- Creación de OAuth token sospechosa → riesgo de persistencia de acceso

## Clasificación
- **True Positive → Incidente**

## Comunicación con usuario
- **No contactar todavía**; primero escalar a L2/L3 para análisis del dispositivo y validación de riesgo

## Acciones inmediatas SOC L1
1. Registrar alerta en SIEM/portafolio  
2. Bloquear sesión o requerir logout forzado si es posible  
3. Monitoreo inmediato de actividad de usuario y host  
4. Documentar todas las evidencias y timestamps  
5. Notificar escalamiento urgente a L2/L3

## Escalamiento
- Escalar **urgentemente a L2/L3**  
- Prioridad: Alta  
- Motivo: Acceso desde ubicación inesperada, nuevo dispositivo, MFA aprobado, actividad post-login sospechosa en archivos críticos

## Notas
- Un MFA aprobado **no garantiza legitimidad**  
- Evidencia post-login es crítica para evaluar el impacto  
- L1 documenta y prepara información completa para L2/L3

Tags: #post_login_sospechoso #incident #high #mfa_bypass

Relacionadas: [[2026-02-02_Credential_Stuffing_Externo]], [[2026-02-02_Lateral_Movement]]
