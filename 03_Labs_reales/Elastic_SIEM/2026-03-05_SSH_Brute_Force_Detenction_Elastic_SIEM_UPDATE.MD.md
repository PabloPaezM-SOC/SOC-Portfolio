**Date:** 2026-03-13 **Tool:** Atomic Red Team + Elastic SIEM (Auditd Manager) **Status:** Detected ✅
##### **Descripción:**

Laboratorio donde implementé una regla de detección personalizada en Elastic SIEM para identificar intentos de autenticación fallida en SSH. El objetivo fue simular un ataque de fuerza bruta y validar la capacidad de detección y alerta del sistema.

#### **Technologies Used:**

- Elastic Stack 8.11
- Auditbeat / Auditd for process monitoring (Arch Linux)
- Elastic Agent with auditd input
- Fleet Server for centralized management
- Kibana for visualization and alerting



 # **Regla de detección:**
 

kql

event.dataset: "system.auth" 
AND message: (*Failed password* OR *Invalid user*)
AND process.name: sshd

**Configuración:**

- **Threshold:** 5 intentos en 5 minutos
- **Group by:** source.ip
- **Severidad:** High (70)
- **Índice:** logs-system.auth-*

#### **Evento detectado:**

json

{
  "message": "Failed password for invalid user falso from ::1 port 52800 ssh2",
  "source.ip": "::1",
  "user.name": "falso",
  "process.name": "sshd"
}

#### **MITRE ATT&CK:**

- **Técnica:** T1110 – Brute Force
- **Sub-técnica:** T1110.001 – Password Guessing

### **Investigación realizada:**

- ✅ Verificación de que los logs correspondían a intentos reales (no falsos positivos)
- ✅ Identificación de IP atacante (::1, localhost, por ser laboratorio
- ✅ Correlación con otros intentos en el mismo rango de tiempo
- ✅ Documentación del caso en el sistema de casos de Elastic

### **Resultado:**

La regla generó alertas exitosamente, permitiendo simular el flujo completo de detección, investigación y documentación de un incidente de seguridad.

### **Enlaces relacionados:**

- [[MITRE T1110]]
- [[Caso SSH Brute Force]]
- [[Arquitectura Elastic en Arch Linux]]