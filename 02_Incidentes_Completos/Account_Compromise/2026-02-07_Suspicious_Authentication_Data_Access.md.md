# INCIDENTE: Account Compromise con Data Exfiltration y Posible C2

Fecha: 2026-02-07
Analista: Nacho (SOC L1)
Severidad: Crítico
Estado: Confirmado
Tipo de Incidente: Account Compromise / Data Exfiltration

---

## 🎯 Resumen Ejecutivo
Usuario del área financiera inicia sesión desde ubicación extranjera con MFA aprobado y dispositivo desconocido. Posteriormente realiza descarga masiva de archivos sensibles, accede a dominio phishing recién registrado y genera tráfico DNS periódico compatible con beaconing C2.

---

## 👤 Entidad Afectada
Usuario: finance.user
Host: WS-FIN-07
IP inicial: 45.83.122.91 (Romania)
Dispositivo: Unknown (First Seen)

---

## 🕒 Línea de Tiempo del Ataque
21:12:03 – Login exitoso desde Romania
21:13:xx – MFA aprobado
21:18:xx – Acceso dominio phishing
21:20–21:30 – Descarga 37 archivos SharePoint Payroll
21:xx:xx – DNS beaconing cada 25s

---

## 🔎 Evidencia Técnica
- IP: 45.83.122.91
- Dominio phishing: secure-microsoft-login[.]co
- DNS: k22x.biz, zz91.biz, pp09.biz
- Dispositivo desconocido
- 1.2GB descargados
- SharePoint /Finance/Payroll/

---

## 🧠 Análisis del Analista
Punto inicial probable: Phishing o Fatiga MFA
Técnica principal: Valid Credential Abuse
Fases MITRE:
- Initial Access
- Collection
- Exfiltration
- Command & Control

Indicadores:
- Ubicación anómala
- Descarga masiva
- Beaconing DNS
- Dominio recién registrado

Impacto potencial:
Exposición de información financiera y nóminas.

---

## 🚨 Acciones Ejecutadas SOC L1
- Forzar cierre de sesiones
- Reset credenciales
- Revocar tokens
- Solicitar aislamiento WS-FIN-07
- Bloqueo dominio phishing
- Monitoreo reforzado

---

## ⬆️ Escalamiento
Destino: SOC L2 / IR
Prioridad: Urgente
Motivo: Compromiso confirmado + posible C2

---

## ⚠️ Decisión Final
Incidente Confirmado – Account Compromise Crítico

---

## 📌 Lecciones / Observaciones
MFA aprobado no garantiza legitimidad.
Patrón DNS periódico sugiere comunicación C2 activa.
Necesidad de alertas tempranas en descarga masiva.
