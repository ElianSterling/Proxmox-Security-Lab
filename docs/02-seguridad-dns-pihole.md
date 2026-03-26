# ⚙️ Fase 2: Seguridad DNS con Pi-hole (Sinkhole)

Para proteger la red interna contra telemetría invasiva, rastreadores y dominios conocidos por distribuir malware o phishing, se desplegó Pi-hole como un DNS Sinkhole.

## 2.1 Instalación y Despliegue
Para optimizar recursos, Pi-hole se montó en un contenedor LXC dentro de Proxmox.

```bash
# Descarga e instalación automatizada de Pi-hole
curl -sSL [https://install.pi-hole.net](https://install.pi-hole.net) | bash
2.2 Configuración Post-Instalación
Durante el asistente de instalación:

Se asignó una IP estática local al contenedor.

Se configuraron los servidores DNS upstream (ej. Cloudflare 1.1.1.1 o Quad9 9.9.9.9 para mayor privacidad).

Para establecer la contraseña de administración del panel web:

Bash
pihole -a -p
Resultado: Pi-hole ahora procesa y filtra todas las peticiones DNS de la red. El panel de administración (http://localhost/admin) audita las consultas en tiempo real y bloquea activamente las conexiones hacia dominios maliciosos.
