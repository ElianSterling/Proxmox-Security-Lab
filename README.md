# 🛡️ HomeLab & Blue Team SOC Infrastructure

Este repositorio documenta la arquitectura, el despliegue y la fortificación de un servidor HomeLab basado en **Proxmox VE 8.x**. El objetivo de esta infraestructura es emular un entorno empresarial para prácticas de Blue Team, implementar herramientas de un Centro de Operaciones de Seguridad (SOC), garantizar el acceso remoto seguro y establecer un sistema de auditoría y alertas en tiempo real.

## 🏗️ Arquitectura del Laboratorio

La infraestructura está dividida en cuatro pilares de seguridad, documentados en su respectiva sección:

1. **Virtualización y Acceso Seguro:** Hardening de Proxmox VE y túnel Tailscale (Mesh VPN).
2. **Seguridad DNS (Sinkhole):** Filtrado de red y bloqueo de amenazas con Pi-hole.
3. **Monitorización de Seguridad (SIEM/XDR):** Detección de intrusiones con Wazuh.
4. **Sistema de Alertas Críticas:** Envío cifrado de logs a través de Postfix (SMTP Relay) y Logwatch.

## 📂 Estructura de la Documentación

La configuración detallada y los comandos de despliegue se encuentran en la carpeta `docs/`:

* [Fase 1: Virtualización, Firewall y Acceso Remoto](docs/01-virtualizacion-y-vpn.md)
* [Fase 2: Seguridad DNS con Pi-hole](docs/02-seguridad-dns-pihole.md)
* [Fase 3: Monitorización de Seguridad con Wazuh](docs/03-monitoreo-wazuh.md)
* [Fase 4: Sistema de Alertas Críticas (Postfix + SASL/TLS)](docs/04-alertas-postfix.md)

---
*Infraestructura diseñada para simulaciones de defensa y operaciones de Blue Team.*
