# Alex Tavares Dos Santos Lb2
Dies ist eine Lerndokumentation einer Projektarbeit im ramen des Modules 300. 
Wir werden für die LB2 ein Webserver aufstellen.
## Inhaltsverzeichniss
* Grafische Übersicht
* Befehle und Erklärungen
    * Vagrant
    * Linux
    * Git
* Testfälle
* Quellenverzeichniss
## **Grafische Übersicht**
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
Folgendes Beispiel Zeigt auf wie man direkt beim starten der VM das Betriebsystem
mit dem Service apache2 vorinstalliert startet.
```
config.vm.provision "shell", inline <<-SHELL
    apt-get update
    apt-get install -y apache2
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

