# ⚙️ Fase 1: Virtualización, Firewall y Acceso Remoto

Para garantizar que el servidor base esté protegido contra accesos no autorizados y sea administrable de forma segura desde ubicaciones remotas, aplicamos políticas de Hardening y desplegamos una VPN Zero-Trust.

## 1.1 Hardening del Firewall de Proxmox
Se activó el firewall integrado a nivel de Datacenter aplicando una política de denegación por defecto (Default Deny) y permitiendo solo el tráfico administrativo esencial.

```bash
# Habilitar el firewall a nivel de clúster/nodo (vía CLI)
pve-firewall enable
pve-firewall start

1.2 Implementación de Tailscale (Mesh VPN)
Se implementó Tailscale para crear un túnel cifrado (WireGuard) directo al servidor. Esto elimina por completo la necesidad de abrir puertos (Port Forwarding) en el router físico hacia internet.

Bash
# Instalación del cliente Tailscale
curl -fsSL [https://tailscale.com/install.sh](https://tailscale.com/install.sh) | sh

# Autenticación y levantamiento del túnel
tailscale up

