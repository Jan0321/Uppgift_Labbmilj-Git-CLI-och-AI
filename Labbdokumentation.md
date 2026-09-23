**Namn** Jan Haddad
**Datum** 15-09 2026
**Kurs** Introduktion till yrkesrollen och grunderna i IT-infrastruktur



## Git - Versionshantering och skapa Projektmapp

För att verionshantera mitt arbete använde jag Git bash och Github.


cd ~\dokuments          "för att navigera till dokuments mappen"
mkdir Systementor-Labb  "för att skapa mappen som heter Systementor-Labb"
cd Systementor-Labb     "för att navigera till mappen systementor-Labb"
pwd                     "för att kontrollera att jag är i rätt map (/c/Users/janha/documents/systementor-labb)"  

### initiera Git repository samt skapa dokumentationsfilen

git init                 "För att göra den aktuella mappen till ett git repository"
git branch -M main       "för att döpa den nuvarande branhen till main"

touch Labbdokumentation.md "här skapade vi en markdown fil som heter Labbdokumentation för att kunna dokumetnera senare i uppgiften med hjälp av Visual Studio Code"

git status                    "Som visade att labbdokumentet är ospårade av git "

git add Labbdokumentation.md  ""

### Commits

git commit -m "grundstruktur" 

git log --oneline  "för att kontrollera commit historiken som visade resultat (5368645 (HEAD -> main) grundstruktur)"


### Github

Jag skapade en repositroy på Github för att kunna lagra projektet externt.

git remote add origin https://github.com/Jan0321/Uppgift_Labbmilj-Git-CLI-och-AI.git "för att koppla mitt lokala git repository till github"

git remote -v        "för att kontrollera att koppligen var ok"

git push -u orgin main  "då skickade jag mitt lokala main branch till github"

git status              "då visade det att koppligen lyckades och är synkroiserat med repositoryt på github(On branch main
Your branch is up to date with 'origin/main'.

nothing to commit, working tree clean
)"

git log --oneline   "5368645 (HEAD -> main) grundstruktur"


## Labbmiljö och nätverk

Jag använder mig utav VirtualBox och har skapat två virtualla maskiner: 

- Windows 11
- Unbunto Server

Jag bröjade med att konfigurera nätverket i båda virtuella maskinerna "VirtualBox-->Settings-->Network." Sedan ändra jag från NAT till Internal Network så att båda maskinerna kan komun lagt till namnen "Labb". Detta gjorde jag på båda maskinerna.

SKA LÄGGA IN BILD HÄR



### Ubunto Server

ip addr show        "kontrollerade nätverkskortet. Den heter enp0s3"

mcli device status  "då fick jag upp att nätverkskortet enp0s3 var frånkopplad (Disconnected)"


sudo nmcli connection add type ethernet ifname enp0s3 con-name Labb ipv4.method manual ipv4.addresses 192.168.10.50/24     "Då skapade jag en ny nätversanslutning som heter Labb och gav servern en statisk IP-adress 192.168.10.50/24"

sudo nmcli connection up Labb   "för att aktiverade jag anslutningen"

ip addr show enp0s3       "då kontrollerade jag den var aktiv (UP) och har fått rätt ip adress 192.168.10.50/24"

Lägger till bilden senare den heter liux ip 1


### Windows 11

Använder PowerShell

ipconfig /all    "kontrollerade ip adressen. den hade en automatisk ip-adress"

Network & internet --> Ethernet  Edit på IPv4 adress, Manual IP-adress: 192.168.10.51 Subnet mask: 255.255.255.0
"Jag fick ändra manuellt i windows 11 inställningar till en statisk ip adress 192.168.10.51, subnätmask 255.255.255.0 och ingen gateway på grund av ingen router."
Lägger bild sen den heter windows manual 1


ipconfig /all  "kontrollerade om maskinen fick ip adressen 192.168.10.51 samt att subnätmask 255.255.255.0"



### Nätverkstabell
| Hostname | Operativsystem | IP-adress | Subnätmask | Standard Gateway |
|---|---|---|---|---|
| Server | Ubuntu Server | 192.168.10.50 | 255.255.255.0 (/24) | Ingen |
| Jano | Windows 11 | 192.168.10.51 | 255.255.255.0 (/24) | Ingen |



### Nätvrksanslutning

ping 192.168.10.50  "Testade att pinga från windows 11 till Ubunto server, det gick att pinga lyckades.
Lägger till bilden sen "ping från win11 till linux "



ping 192.168.10.51       "inget hände
ping -c 4 192.168.10.51  testade att pinga från Ubunto server till windows 11, Det lyckades inte. då skickade jag 4 packet till windows 11 men fick 100% packet loss

lägger bilden senare den heter "ping linux till windows packet loss "


### Felsökning

Eftersom ping fungerade från Windows till ubunto börjar jag felsöka Windows


Get-NetConnectionProfile  "för att kontrollera vilken nätverksprofil windows anväde, och det visade att Ethernet anslutningen använde profilen Public, vilket var relevant när jag felsökte brandväggen.
lägger till bilden sedan bilden heter nätverksprofile


Jag kontrollerade därefter reglerna för inkommande trafik i Windows Defender Firewall. Reglerna för inkommande ICMPv4 Echo Request var inte aktiverade för den aktuella Public-profilen. Det gjorde så att brandväggen blockerade inkommande ping från ubunto servern

lägger till bilden "inbound rules

New-NetFirewallRule -DisplayName "Tillat Ping fran Labbnat" -Direction Inbound -Protocol ICMPv4 -IcmpType 8 -Action Allow -Profile Public
här skapade jag en specifik regel för ICMPv4 istället för att stänga av brandväggen. den tillåter inkommande ping förfrågan från ubunto servern.

## Test

ping -c 4 192.168.10.51  "skickade 4packet till windows 11 då fick 0% packet loss det gick att pinga

lägger till bilden senare. "Ping från ubunto till win






### Katalog & fil

sudo mkdir -p /var/systementor/kosultdata      "för att skapa första katalogen"

ls -ld '/var/systementor/konsultdata           "för att kontrollera katalogen"


sudo touch /var/ststenentor/konsultdata/anteckningar.txt "skapar filen"

ls -ld '/var/systementor/konsultdata           "för att kontrollera katalogens innehåll"

lägger till bilden senare namn; Skapar map samt txt


sudo groupadd konsulter         "för att skapa grouppen konsulter"


getent group konsulter                "för att kontrollera grouppen (konsulter:x:1001)"

sudo chgrp -R konsulter /var/systementor/konsultdata "ändrade gruppägaren och innehåll till konsulter"

lägger till bilden sernare i uppgiften namn_ katalogen samt filen tillhör konsulter






