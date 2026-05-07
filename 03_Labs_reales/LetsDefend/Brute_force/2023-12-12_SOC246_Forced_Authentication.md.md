# Alerta: SOC246 – Forced Authentication Detected
**Plataforma:** LetsDefend.io  
**Fecha:** 2023-12-12  
**Nivel:** SOC L1  
**Tipo de alerta:** Brute Force / Forced Authentication  

## Contexto
Alerta generada por el SIEM al detectar múltiples solicitudes POST al endpoint de autenticación `/accounts/login` desde una misma IP en un corto periodo de tiempo.

## Evidencia Clave
- **Event ID:** 208  
- **Source IP:** 120.48.36.175  
- **Destination IP:** 104.26.15.61  
- **Host:** WebServer_Test  
- **Request URL:** `http://test-frontend.letsdefend.io/accounts/login`  
- **Request Method:** POST  
- **Device Action:** Permitted  
- **Ventana temporal:** 14:06 – 14:15  

## Análisis
Al revisar los **proxy logs**, se observa que la IP `120.48.36.175` realizó múltiples intentos de autenticación contra el endpoint de login durante varios minutos.  
Después de numerosos intentos fallidos, se identifica **un login exitoso**, lo que sugiere un posible ataque de **brute force**.

No se detecta actividad maliciosa posterior al login:
- No acceso a recursos sensibles
- No creación de tokens
- No cambios de configuración

## Clasificación
- **True Positive**
- **Incidente:** Sí  
- **Severidad:** Media  

## Hipótesis
- Ataque de fuerza bruta exitoso contra credenciales válidas
- Posible uso de VPN por parte del atacante (IP no confiable)
- No se descarta compromiso parcial de credenciales

## Acciones SOC L1
1. Documentar alerta y evidencias en SIEM  
2. Recomendar **reset de credenciales** del usuario afectado  
3. Monitorear actividad post-login del usuario  
4. Revisar si otros usuarios presentan intentos similares  
5. Recomendar bloqueo de IP a nivel firewall (evaluando posible uso de VPN)

## Escalamiento
- **Sí, se escala a L2**
- Motivo: Autenticación exitosa tras múltiples intentos fallidos (brute force confirmado)
- L2 deberá validar impacto, revisar autenticaciones relacionadas y decidir contención adicional

## Aprendizaje
- Un login exitoso tras múltiples intentos fallidos **no descarta incidente**
- La ausencia de actividad post-login reduce impacto, pero **no elimina riesgo**
- El análisis temporal de logs es clave para detectar brute force exitoso

Tags: #letsdefend #bruteforce #authentication #medium
