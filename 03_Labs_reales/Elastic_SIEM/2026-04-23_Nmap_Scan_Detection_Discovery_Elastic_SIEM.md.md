
**Date:** 2026-03-13 **Tool:** Atomic Red Team - "Nmap Scan" + Elastic SIEM (Auditd Manager) **Status:** Detected ✅
### **Descripción:**

Laboratorio donde implementé una regla de detección personalizada en Elastic SIEM para identificar actividades de reconocimiento de red, específicamente escaneo de puertos utilizando la herramienta Nmap. El objetivo fue simular un adversario en su fase de descubrimiento y validar la capacidad de detección del sistema.

### **Tecnologías utilizadas:**

- Elastic Stack 8.11
    
- Auditbeat / Auditd para monitoreo de procesos (Arch Linux)
    
- Elastic Agent con input auditd
    
- Fleet Server para gestión centralizada
    
- Kibana para visualización y alertas
    

### **Regla de detección:**

kql

event.dataset: auditd_manager.auditd 
AND process.name: nmap 
AND process.args: (*-s* OR *-p* OR *-T*) 
AND process.args: (*localhost* OR *192.168.* OR *10.* OR *172.*)

**Configuración:**

- **Threshold:** >= 1 ejecución
    
- **Group by:** [host.name](https://host.name/), [user.name](https://user.name/)
    
- **Severidad:** Medium (47)
    
- **Índice:** auditbeat-_, logs-auditd_
    

### **Evento detectado:**

json

{
  "@timestamp": "2026-04-23T03:52:21.296Z",
  "process.name": "nmap",
  "process.args": ["nmap", "-sS", "-p-", "localhost"],
  "process.parent.pid": 281874,
  "user.name": "nacho",
  "host.name": "arclinuxlinux",
  "event.action": "executed",
  "event.outcome": "success"
}

### **MITRE ATT&CK:**

- **Técnica:** T1046 – Network Service Scanning
    
- **Táctica:** Discovery (TA0007)
    

### **Investigación realizada:**

- ✅ Verificación de la ejecución del binario `nmap` con argumentos de escaneo (`-sS -p- localhost`)
    
- ✅ Identificación del usuario que ejecutó el proceso (`nacho`, UID 1000)
    
- ✅ Correlación con el proceso padre (PID 281874) para determinar el origen del comando
    
- ✅ Confirmación de que la actividad no corresponde a tareas legítimas de administración
    
- ✅ Documentación del hallazgo en el sistema de casos de Elastic
    

### **Resultado:**

La regla generó una alerta exitosamente ante la ejecución de `nmap`, demostrando la capacidad de detectar actividades de reconocimiento de red en la fase temprana de un ataque (Discovery). Esto permite a un equipo SOC intervenir antes de que el adversario avance a etapas posteriores como la explotación o persistencia.

### **Enlaces relacionados:**

- [[MITRE T1046 - Network Service Scanning]]
    
- [[Caso Escaneo de Puertos con Nmap]]
    
- [[Arquitectura Elastic en Arch Linux]]