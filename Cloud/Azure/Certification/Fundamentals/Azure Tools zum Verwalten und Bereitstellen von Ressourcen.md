# Azure Tools zum Verwalten und Bereitstellen von Ressourcen

## Azure Portal

- webbasierte, zentrale Konsole, die eine Alternative zu Befehlszeilentools darstellt

## Azure Cloud Shell

- browserbasiertes Shelltool, mit dem Sie Azure-Ressourcen verwalten koennen

## Azure Powershell/CLI

- eine Shell, mit der Azure Befehle ausgeführt werden können
- Ruft die Azure-REST-API auf

## Azure Arc

Mithilfe von Azure Resource Manager (ARM) und Arc können Sie Ihre Azure-Compliance und -Überwachung auf Ihre Hybrid- und Multi-Cloud-Konfigurationen ausdehnen.

- verwalten die gesamte  Multi-Cloud/Hybrid Cloud Umgebung zusammen
- verwalten Multi-Cloud- und Hybrid-VMs, Kubernetes-Cluster und Datenbanken so, als würden sie in Azure ausgeführt
- können ortsunabhängig vertraute Azure-Dienste und Verwaltungsfunktionen verwenden
- können ITOps-Methoden weiterverwenden und gleichzeitig DevOps-Methoden einführen
- konfigurierung von benutzerdefinierte Speicherorten als Abstraktionsschicht auf der Grundlage von Kubernetes-Clustern mit Azure Arc-Unterstützung und Clustererweiterungen

## Azure Resource Manager (ARM) und ARM-Vorlagen

- bietet Verwaltungsebene, die das Erstellen, Aktualisieren und Löschen von Ressourcen in Ihrem Azure-Konto ermöglicht
- Infrastruktur wird ueber deklarative Vorlagen mithilfe einer JSON verwaltet
- können Lösung während des Entwicklungszyklus erneut bereitstellen und sicher sein, dass Ressourcen in einem konsistenten Zustand bereitgestellt werden
- Abhängigkeiten zwischen Ressourcen definieren
- Anwendn von Zugriffssteuerung auf alle Dienste, da RBAC nativ in die Verwaltungsplattform integriert ist
- Anwenden von Tags auf Ressourcen
- genauere Informationen zur Abrechnung Ihrer Organisation erhalten

### Infrastructure-as-Code (IaC)

- Verwaltung der Infrastruktur mit Codezeilen
- Azure CLI zum Verwalten und Konfigurieren Ihrer Ressourcen

### ARM-Vorlagen

- können die Ressourcen, die verwendet werden, in einem deklarativen JSON-Format beschrieben
- wird der Bereitstellungscode überprüft, bevor Code ausgeführt wird

Vorteile:

- Deklarative Syntax
	- kann eine gesamte Azure-Infrastruktur deklarativ erstellen und bereitstellen
	- Sie deklarieren, was Sie bereitstellen möchten, aber nicht die tatsächlichen Programmierbefehle
- Wiederholbare Ergebisse
	- Wiederholtes Bereitstellen Ihrer Infrastruktur während des gesamten Entwicklungslebenszyklus
	- Gewährleistung, dass Ressourcen einheitlich bereitgestellt werden
- Orchestrierung
	- orchestriert die Bereitstellung unabhängiger Ressourcen, sodass sie in der richtigen Reihenfolge erstellt werden
	- stellt parallel bereit, sodass Ihre Bereitstellungen schneller abgeschlossen werden
- Modulare Dateien
	- können Vorlagen in kleinere, wiederverwendbare Komponenten unterteilen und sie zum Zeitpunkt der Bereitstellung miteinander verknüpfen
	- können eine Vorlage auch in anderen Vorlagen schachteln
- Erweiterbarkeit
	- Koennen mit zusaetzlichen Scripts Vorlagen PowerShell- oder Bash-Skripts hinzufügen
	- erweitern die Möglichkeiten zum Einrichten von Ressourcen während der Bereitstellung
	- kann in die Vorlage eingeschlossen werden oder in einer externen Quelle gespeichert werden

### Bicep

- ist eine Sprache, die eine deklarative Syntax zur Bereitstellung von Azure-Ressourcen verwendet
- Bicep-Datei definiert die Infrastruktur und Konfiguration
- stellt ARM diese Umgebung basierend auf Ihrer Bicep-Datei bereit

Vorteile: 

- Unterstuetzung fuer alle Ressourcentypen und API-Versionen
	- werden alle Vorschau- und allgemein verfügbaren Versionen für Azure-Dienste direkt unterstützt
- EInfache Syntax
	- sind präziser und einfacher zu lesen
	- sind keine Vorkenntnisse über Programmiersprachen erforderlich
	- deklarativ und gibt an, welche Ressourcen und Ressourceneigenschaften Sie bereitstellen möchten
- Wiederholbare Ergebisse
	- Wiederholtes Bereitstellen Ihrer Infrastruktur während des gesamten Entwicklungslebenszyklus
	- Gewährleistung, dass Ressourcen einheitlich bereitgestellt werden
- Orchestrierung
	- orchestriert die Bereitstellung unabhängiger Ressourcen, sodass sie in der richtigen Reihenfolge erstellt werden
	- stellt parallel bereit, sodass Ihre Bereitstellungen schneller abgeschlossen werden
- Modulare Dateien
	- können Bicep-Code mithilfe von Modulen in verwaltbare Teile unterteilen
	- Über ein Modul werden zugehörige Ressourcen bereitgestellt
	- Mit Modulen lässt sich Code wiederverwenden und die Entwicklung vereinfachen
	- können ein Modul jederzeit in einer Bicep-Datei hinzufügen, wenn Sie die entsprechenden Ressourcen bereitstellen möchten

