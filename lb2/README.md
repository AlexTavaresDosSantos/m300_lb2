# Alex Tavares Dos Santos Lb2
Dies ist eine Lerndokumentation einer Projektarbeit im ramen des Modules 300. 
Wir werden für die LB2 ein Webserver aufstellen.
## Inhaltsverzeichniss
* Grafische Übersicht
* Befehle und Erklärungen
    * Vagrant
    * Linux
    * Git
* Bereitstellung des Nginx Service
* Testfälle
* Quellenverzeichniss
## **Grafische Übersicht**
Hier 
## **Bereitstellung des Nginx Service**
Mit folgender Anleitung kann man ein Service Names Nginx bereitstellen.
Diese Anleitung dient auch zur erläuterung was ich für Sachen gemacht habe um dies Bereitstellen zu können. 

### **Box**

Als erstes müssen wir eine Box heraussuchen die uns für das wir machen möchten passt.
In meinem Fall war es der Service Nginx der nur auf Linux läuft also habe ich mich für folgende Box entschieden. 

**ubuntu/trusty64**

Leider ist bei dieser Box beim starten notwendig die Taste **S** zu drücken damit es in das System booted. Dies konnte ich leider nicht 
automatisieren.

Wen man nun sich für eine Box entschieden hat kann man dan loslegen mit dem initialiesern der Box. 
```
vagrant init ubuntu/trusty64
```
Anschliessend nach ausführen des Befehles wird im lokalen Repository einen so genannten Vagrantfile erstellt. 
Wen man nun die Box straten möchte kann man dies mit folgenden Befehl
```
vagrant up
```
### **Nginx**

Um Nginx zu installieren um die Website bereit zu stellen müssen folgende commands abgedrückt werden. 
Man kann dies direkt auf der Maschine machen aber für dieses Modul habe ich extra nur mit der Git Bash Konsole gearbeitet.
Man kann sich auf die Box mit SSH verbinden in dem man folgendes eingibt. 
```
vagrant SSH 
```
Wen man sich nun erfolgreich verbunden hat kann man wie man sich einem gewöhnlichen Terminal gewohnt ist die commands abdrücken. 
```
apt-get update
apt install -y nginx 
service nginx start
service nginx status (Falls man sehen möchte ob der Service läuft)
```
Die ganzen Befehle die man eingibt um den Service **Nginx** zu installieren kann man auch direkt beim starten der Box mitgeben. 
Das heisst wen man **Vagrant UP** macht dan wird der Service direkt installiert. Das ganze kann man mit der Vagrant Funktion
**config.vm.provision**. Alles was zwischen SHELL steht wird vereinzelt im Terminal beim starten der Box ausgeführt.
```
 config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get install -y nginx
    service nginx start
  SHELL
```
Da ich meinem Webserver einbisschen mer Ressourcen geben wollte habe ich dies mit der Funktion config.vm.provision gemacht. 
```
  config.vm.provider "virtualbox" do |vb|
     vb.gui = true
     vb.memory = "2024"
      vb.cpus = "2"
```
## **Befehle**
### **Git**
Anzeigen von aktuellen File-Status.
```
git status
```
Datei die ge-staged wurde, aus dem Index entfernen.
```
git reset HEAD {file}
```
Zeigt alles was im Workplace geändert wurde aber noch nicht im Index ist.
```
git diff
```
Zeigt was bereits zum Commit vorgemerkt wurde.
```
git diff --cached
```
Commit History ansehen.
```
git log
```
Remote Repository anzeigen
```
git remote -v
```
### **Vagrant** 
Mit folgendem Befehl initialisiert man eine gewünschte Box
```
vagrant init Beispiel/Box
```
Starten der Vagrant Box
```
vagrant up
```
### **Vagrantfile**
Definition der Box
```
config.vm.box "Windows" oder "Ubuntu" ...
```
Welcher Anbieter die Maschine Hostet
```
config.vm.provider "Virtualbox" oder "VMware" ...
```
Netzwerk konfiguration der VM
```
config.vm.network "forwarded_port" 
config.vm.network "private_network"
config.vm.network "public_network"
```
Mit folgender Funktion kann man Befehle im Terminal beim starten der Box eingeben lassen.
```
config.vm.provision "shell", inline <<-SHELL
SHELL
```
### **Linux** 
Hier ist eine Tabelle mit ein paar Linux Grundbefehlen 

| Befehl                             | Beschreibung                                         |
|:----------------------------------:|:----------------------------------------------------:|
| sudo apt-get install «Paket»       | Dieser Befehl dient um etwas zu installieren         |
| sudo cp «Dateiname» «Ziel»         | Kopiert ein gewünschtes File an einem bestimmten Ziel|
| ls                                 | Kann man sehen was in einem Ordnervorhanden ist      |
| sudo rm «Dateiname»                | Mann kann ein File löschen mit diesem Befehl         |
| sudo apt-get update                | Aktualisiert man das OS                              |
### **Testfälle**

#### Testfall 1

#### Durchführung
| Tester/in          |  Alex Santos                                                                                                              |
|:------------------:|:-------------------------------------------------------------------------------------------------------------------------:|
| Datum              | 17.03.2021                                                                                                                |
| Testergebnis       | erfolgreich                                                                                                               |
| Fehlerbeschreibung | Keine Fehler                                                                                                              |

| ID                 |                                                             1                                                             |
|:------------------:|:-------------------------------------------------------------------------------------------------------------------------:|
| Beschreibung       | Im Vagrantfile mit folgender Funktion "config.vm.provison" SHELL Befehle durchführen.                                     |
| Erwatetes Ergebnis | Der Service Nginx beim vagrant up installieren.                                                                           |
| Ergebnis           | Der Service Nginx wurde erfolgreich installiert und gestartet                                                             |

#### Testfall 2

#### Durchführung
| Tester/in          |  Alex Santos                                                                                                              |
|:------------------:|:-------------------------------------------------------------------------------------------------------------------------:|
| Datum              | 18.03.2021                                                                                                                |
| Testergebnis       | fehlgeschlagen                                                                                                            |
| Fehlerbeschreibung |"VM cant start a fatal error occured while the network configuration"                                                      |

| ID                 |                                                             2                                                             |
|:------------------:|:-------------------------------------------------------------------------------------------------------------------------:|
| Beschreibung       | Die Static IP Einstellung zu DHCP ändern im Vagrantfile mit der Funktion "config.vm.network"                              |
| Erwatetes Ergebnis | Die VM bezieht eine IP Adresse in meinem Netzwerk über DHCP beim straten                                                  |
| Ergebnis           | Die VM konnte man nicht mehr starten. Ich musste die Konfiguration die ich im Vagrantfile getätigt habe aus Kommentieren  |

#### Testfall 3

#### Durchführung
| Tester/in          |  Alex Santos                                                                                                              |
|:------------------:|:-------------------------------------------------------------------------------------------------------------------------:|
| Datum              | 18.03.2021                                                                                                                |
| Testergebnis       | erfolgreich                                                                                                               |
| Fehlerbeschreibung | Keine Fehler                                                                                                              |

| ID                 |                                                             3                                                             |
|:------------------:|:-------------------------------------------------------------------------------------------------------------------------:|
| Beschreibung       | Im Vagrantfile die Box Settings apassen mit der funktion "config.vm.provider"                                             |
| Erwatetes Ergebnis | Die CPU und die RAM im Vagrantfile angeben. CPU = 2 und RAM = 2                                                           |
| Ergebnis           | Ich konnte erfolgreich die Anpassung durchführen                                                                          |

### **Reflexion**

Im grossen und ganzen bin ich zufrieden mit meinem Projekt da es mir gefallen hat etwas neues aus zu probieren. 
Ich habe zwar ein kleines Projekt gemacht aber aus dem Grund, das man so einen guten Überblick hatte und trotzdem mit vielen Befehlen arbeiten konnte.  
Am anfang muss ich ehrlich sagen war es sehr schwierig einzusteigen und zum teil auch sehr frustrierend wen etwas nicht ging. 
Nachdem ich aber den dreh raus hatte, versuchte ich jegliste Sachen und fand sogar spass dran. 
Ich hoffe das wir in Zukunft wieder mit Git Hub arbeiten können und ich so noch mehr Erfahrung sammeln kann um besser darin zu werden.