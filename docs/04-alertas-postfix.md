# ⚙️ Fase 4: Sistema de Alertas Críticas (Postfix + SASL/TLS)

Para mantener una monitorización proactiva del servidor sin depender exclusivamente de dashboards, se configuró Postfix para actuar como un SMTP Relay seguro. Utilizando los servidores de Google, el sistema envía reportes de auditoría generados por Logwatch directamente a un correo de Outlook.

## 4.1 Instalación de Dependencias

bash

apt-get update
apt-get install postfix mailutils libsasl2-modules logwatch -y
(Durante el asistente, se seleccionó "Internet con smarthost", el nombre localhost y el Relay Host [smtp.gmail.com]:587).

4.2 Redirección de Correos del Sistema
Se configuró el alias para que las alertas del usuario root lleguen al correo del administrador.

Bash
echo "root: <TU_CORREO_DESTINO>@outlook.com" > /etc/aliases
newaliases
4.3 Fortificación de Credenciales (Mapeo Hash)
Se generó una App Password (contraseña de aplicación) en Google para no exponer credenciales principales.

Bash
nano /etc/postfix/sasl_passwd
Contenido del archivo:

Plaintext
[smtp.gmail.com]:587 <TU_CORREO_ORIGEN>@gmail.com:<APP_PASSWORD_16_CARACTERES>
Protección del archivo y generación de la base de datos de Postfix:

Bash
chmod 600 /etc/postfix/sasl_passwd
postmap /etc/postfix/sasl_passwd
4.4 Hardening de Postfix (Cifrado TLS y Autenticación SASL)
Se forzó el cifrado de las comunicaciones para evitar intercepciones de credenciales en texto plano.

Bash
postconf -e "smtp_sasl_auth_enable = yes"
postconf -e "smtp_sasl_password_maps = hash:/etc/postfix/sasl_passwd"
postconf -e "smtp_sasl_security_options = noanonymous"
postconf -e "smtp_sasl_tls_security_options = noanonymous"
postconf -e "smtp_tls_security_level = encrypt"
postconf -e "smtp_tls_CAfile = /etc/ssl/certs/ca-certificates.crt"
postconf -e "smtp_use_tls = yes"
postconf -e "header_size_limit = 4096000"

systemctl restart postfix
4.5 Troubleshooting y Validación
Para verificar el cifrado y la correcta entrega de los paquetes al servidor de destino:

Bash
echo "Prueba de seguridad del servidor con módulos SASL" | mail -s "Alerta SOC HomeLab" <TU_CORREO_DESTINO>@outlook.com

# Auditoría de los logs de correo en tiempo real
journalctl -t postfix/smtp -n 10 --no-pager
