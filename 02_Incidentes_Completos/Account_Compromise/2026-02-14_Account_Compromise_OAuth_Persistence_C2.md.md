# INCIDENTE: Account Compromise con Persistencia OAuth y Beaconing C2

Fecha: 2026-02-14  
Analista: Nacho (SOC L1)  
Severidad: Crítico  
Estado: Confirmado  
Tipo de Incidente: Account Compromise / Endpoint Compromise / Persistence / C2 / Data Exfiltration Attempt

---

## 🎯 Resumen Ejecutivo

Se detecta actividad anómala asociada a un usuario corporativo tras alerta de Impossible Travel. Posteriormente se observa ejecución de PowerShell codificado desde teams.exe, consentimiento OAuth con permisos elevados, creación de regla de correo sospechosa y tráfico DNS periódico compatible con beaconing C2.

El análisis confirma compromiso híbrido (identidad + endpoint) con mecanismos de persistencia en entorno cloud y comunicación activa con infraestructura externa.

---

## 👤 Entidad Afectada

Usuario: user@empresa.com  
Host: DESKTOP-XXXX  
IP relevante: 185.XX.XX.XX  
Dispositivo: Unknown (First Seen)

---

## 🕒 Línea de Tiempo del Ataque

08:12 – Impossible Travel detectado  
08:15 – PowerShell encoded execution (parent: teams.exe)  
08:18 – OAuth App Consent (offline_access)  
08:20 – Creación de Mailbox Rule  
08:23 – DNS beaconing cada 30 segundos  
08:25 – Endpoint aislado  
08:27 – Sesiones revocadas

---

## 🔎 Evidencia Técnica

- Parent process: teams.exe
    
- PowerShell encoded en base64
    
- OAuth permisos: Mail.Read / Files.Read / offline_access
    
- Mailbox Rule redirigiendo correos a cuenta externa
    
- Tráfico DNS periódico cada 30s
    
- Dominio externo no categorizado
    

---

## 🧠 Análisis del Analista

Punto inicial probable: Phishing vía Teams o robo de token OAuth

Técnica principal: OAuth Abuse + Valid Account

Fases MITRE:

- Initial Access
    
- Execution
    
- Persistence
    
- Command & Control
    
- Exfiltration
    

Indicadores clave:

- Impossible Travel
    
- PowerShell ofuscado
    
- Consentimiento OAuth sospechoso
    
- Regla de correo maliciosa
    
- Beaconing DNS periódico
    

Impacto potencial:  
Acceso persistente a correo corporativo, posible exfiltración de información sensible y control remoto del endpoint.

---

## 🚨 Acciones Ejecutadas SOC L1

- Aislamiento inmediato del endpoint
    
- Revocación de sesiones activas
    
- Reset de credenciales
    
- Forzar re-registro MFA
    
- Eliminación de aplicación OAuth sospechosa
    
- Eliminación de Mailbox Rule
    
- Bloqueo de IOCs
    
- Monitoreo reforzado
    

---

## ⬆️ Escalamiento

Destino: SOC L2 / IR  
Prioridad: Urgente  
Motivo: Compromiso confirmado con persistencia y C2 activo

---

## ⚠️ Decisión Final

Incidente Confirmado – Account Compromise Crítico

---

## 📌 Lecciones / Observaciones

El abuso de OAuth permite persistencia incluso tras cambio de contraseña.  
Las reglas de correo continúan siendo técnica efectiva de exfiltración silenciosa.  
La correlación entre identidad y endpoint es clave para detección temprana.

---

## 🏷 Tags

#account_compromise  
#endpoint_compromise  
#oauth_abuse  
#powershell  
#c2  
#data_exfiltration  
#critical