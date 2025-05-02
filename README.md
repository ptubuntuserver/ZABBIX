# ZABBIX
SCRIPT-WEB-WINBOX
###################################################
Archivo php +++ winbox.php  ++++
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
1. Crear el archivo launch_winbox.bat:

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

