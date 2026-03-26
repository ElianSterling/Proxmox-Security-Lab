# ⚙️ Fase 3: Monitorización de Seguridad con Wazuh (SIEM/XDR)

Como núcleo del Centro de Operaciones de Seguridad (SOC) del laboratorio, se implementó Wazuh. Esta herramienta permite la recolección, indexación y correlación de eventos de seguridad en tiempo real.

## 3.1 Instalación del Servidor Wazuh (All-in-one)
Se utilizó el script de instalación desatendida para desplegar el Indexador, el Servidor Wazuh y el Dashboard en un solo nodo.

# Descarga del script de instalación
curl -sO [https://packages.wazuh.com/4.x/wazuh-install.sh](https://packages.wazuh.com/4.x/wazuh-install.sh)

# Ejecución de la instalación con el flag -a (All-in-one)
bash wazuh-install.sh -a
3.2 Extracción de Credenciales
Una vez finalizada la instalación, se extrajeron las contraseñas generadas automáticamente para acceder al Dashboard seguro.

Bash
# Extraer y visualizar contraseñas de administración
tar -O -xvf wazuh-install-files.tar wazuh-install-files/wazuh-passwords.txt
Resultado: El entorno SIEM/XDR está operativo en https://localhost. El sistema está preparado para recibir logs mediante el despliegue futuro de agentes HIDS en las máquinas virtuales (ej. análisis de logs, monitoreo de integridad de archivos y detección de rootkits).
