# ZABBIX
SCRIPT-WEB-WINBOX
Indicaciones:
1. Tener instalado winbox
2. Mover el archivo ejecutable a la ruta Windows C:\Program Files (x86)\Winbox
3. Crear el script en zabbix con url apuntando a la ubicacion del php usando en macro. Example: http://zabbix.panama.com/zabbix/winbox/winbox.php?ip={HOST.IP}
4. Crear el archivo php y subirlo en el servidor zabbix
5. Crear el archivo winbox_protocol.reg y ejecutarlo (Esperar que se agregue el registro de forma satisfactoria)
6. Crear el archivo  C:\scripts\launch_winbox.vbs en la ubicacion descripta ( hay que crear la ubiación)
7. Ir a mapa y validar funcionamiento
8. Darle permiso a firewall o antivirus para ejecutar sripts desde web
9. Listo
###################################################
Archivo php +++ winbox.php  ++++ Para el servidor ubicarlo en Raiz del zabbix default /usr/share/zabbix/winbox
###################################################
<?php
if (!isset($_GET['ip'])) {
    http_response_code(400);
    die("Falta el parámetro 'ip'");
}

$ip = $_GET['ip'];

if (!filter_var($ip, FILTER_VALIDATE_IP)) {
    http_response_code(400);
    die("IP no válida");
}

header("Location: winbox://$ip");
exit;
?>
##############################################################
Archivo .reg  +++ winbox_protocol.reg +++
##############################################################
Windows Registry Editor Version 5.00

[HKEY_CLASSES_ROOT\winbox]
@="URL:Winbox Protocol"
"URL Protocol"=""

[HKEY_CLASSES_ROOT\winbox\DefaultIcon]
@="\"C:\\Program Files (x86)\\Winbox\\Winbox.exe\",1"

[HKEY_CLASSES_ROOT\winbox\shell]

[HKEY_CLASSES_ROOT\winbox\shell\open]

[HKEY_CLASSES_ROOT\winbox\shell\open\command]
@="wscript.exe \"C:\\scripts\\launch_winbox.vbs\" \"%1\""

###############################################################3
1. Crear el archivo launch_winbox.vbs:

Guarda esto como C:\scripts\launch_winbox.vbs
###############################################################3
' launch_winbox.vbs
Dim ip, raw
Set args = WScript.Arguments
raw = args(0)

' Quitar el prefijo winbox://
ip = Replace(raw, "winbox://", "", 1, -1, vbTextCompare)

' Ejecutar Winbox con solo la IP
Set shell = CreateObject("WScript.Shell")
shell.Run Chr(34) & "C:\Program Files (x86)\Winbox\Winbox.exe" & Chr(34) & " " & Chr(34) & ip & Chr(34), 1, False

