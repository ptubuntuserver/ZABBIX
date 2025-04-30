# ZABBIX
SCRIPT-WEB-WINBOX
###################################################
Archivo html +++ winbox_redirect.html  ++++
###################################################
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Abrir Winbox</title>
</head>
<body>
    <h2>Abrir MikroTik en Winbox</h2>
    <p>Haga clic en el siguiente enlace para abrir Winbox:</p>
    <a href="winbox://{HOST.IP}">Abrir Winbox para {$HOST_IP}</a>
</body>
</html>
##############################################################
Archivo .reg  +++ winbox_protocol.reg +++
##############################################################
Windows Registry Editor Version 5.00

[HKEY_CLASSES_ROOT\winbox]
@="URL:Winbox Protocol"
"URL Protocol"=""

[HKEY_CLASSES_ROOT\winbox\DefaultIcon]
@="\"C:\\Program Files (x86)\\Winbox\\winbox.exe\",1"

[HKEY_CLASSES_ROOT\winbox\shell]

[HKEY_CLASSES_ROOT\winbox\shell\open]

[HKEY_CLASSES_ROOT\winbox\shell\open\command]
@="\"C:\\Program Files (x86)\\Winbox\\winbox.exe\" \"%1\""
