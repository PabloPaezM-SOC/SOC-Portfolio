# Alerta: DNS Beaconing / C2
**Fecha:** 2026-02-02  
**Tipo de alerta:** Suspicious DNS Activity – Possible C2 Beaconing  
**Usuario / Host:** 10.0.5.23

## Descripción
Host interno hace consultas DNS a subdominios aleatorios en dominio .biz cada 30 seg; patrón automatizado.

## Evidencia
- 5 queries registradas entre 16:10 – 16:12  
- URLs: ajd92kqplx.biz, qow92mxkqp.biz, etc.

## Acciones L1
1. Registrar alerta  
2. Monitoreo de host  
3. Recopilar IP y timestamps

## Decisión
True Positive → Incidente

## Escalamiento
Escalar a L2 para análisis de host y verificación de C2

## Notas
Beaconing típico; posible malware; L1 documenta y escala

Tags: #dns_anomaly #c2 #media
