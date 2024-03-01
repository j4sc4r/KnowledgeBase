# Azure Kostenverwaltung

## Faktoren die sich auf Azure Kosten auswirken

Azure Betriebskosten werden beeinflusst von: 

- Ressourcentyp
- Nutzung
- Wartung
- Gebiet
- Abonnementtyp
- Azure Marketplace

## Vergleich Preis- und Gesamtkostenrechner

### Preisrechner

- dafür vorgesehen, Ihnen die geschätzten Kosten für die Bereitstellung von Ressourcen in Azure zu liefern
- Fokus liegt auf den Kosten für bereitgestellte Ressourcen in Azure

### Gesamtkostenrechner

- soll dabei helfen, die Kosten für die Ausführung einer lokalen Infrastruktur mit denen für eine Azure Cloud-Infrastruktur zu vergleichen

## Cost Management-Tool 

- Möglichkeit die Kosten für Azure-Ressourcen schnell zu überprüfen
- Warnungen basierend auf Ressourcenausgaben zu erstellen
- Budgets zu erstellen

### Kostenwarnungen

- bieten einen zentralen Ort, an dem Sie schnell alle unterschiedlichen Warnungstypen überprüfen können

Folgende Warnungstypen koennen aufkommen:

- Budgetwarnungen
	- benachrichtigt wenn Ausgaben basierend auf Verbrauch oder Kosten den in der Warnungsbedingung für das Budget definierten Betrag erreichen oder überschreiten
- Guthabenwarnungen
	- erhalten Warnungen wenn Ihr Azure-Guthaben aufgebraucht ist
	- betrifft nur Organisationen mit Enterprise Agreement (EA)
- Warnungen bei Ausgabenkontingenten für Abteilungen
	- benachrichtigung sobald die Ausgaben einer Abteilung einen bestimmten Schwellenwert eines Kontingents erreichen

### Budgets

- Ausgabenlimit für Azure
- basierend auf einem Abonnement, einer Ressourcengruppe, einem Diensttyp oder anderen Kriterien
- erstellt automatisch Budget warnung

## Tags

- moeglichkeit verwandte ressourcen zu organisieren
- Tags stellen zusätzliche Informationen oder Metadaten zu Ihren Ressourcen bereit

Metadaten/Tags eignen sich fuer:

- Ressourcenverwaltung
	- Mithilfe von Tags können Ressourcen, Umgebungen, Geschäftsbereichen und Besitzern die verknüpft sind gemeinsam ausführen
- Kostenverwaltung- und optimierung
	- können Ressourcen gruppieren
	- berichten ueber Kosten
	- koennen interne Kostenstellen zuweisen
	- Budgets nachverfolgen und geschätzte Kosten prognostizieren 
- Vorgangsverwaltung
	- koennen ressourcen entsprechend der Wichtigkeit gruppieren
	- unterstützt beim Formulieren von Vereinbarungen zum Servicelevel (SLAs)
- Sicherheit
	- können Daten nach Sicherheitsstufe klassifizieren
- Governance und Einhaltung gesetzlicher Bestimmungen
	- können Ressourcen identifizieren werden die Anforderungen an Governance oder Einhaltung gesetzlicher Vorschriften entsprechen
	- können auch Teil Ihrer Standarddurchsetzungsmaßnahmen sein
- Optimierung und Automatisierung von Workloads
	- können alle Ressourcen visualisieren die Teil komplexer Bereitstellungen sind
	- können eine Ressource mit der zugehörigen Workload oder dem Anwendungsnamen markieren --> automatische ausfuehrung von tasks die diese ressourcen verwenden

### Verwaltung von Ressourcentags

- Koennen mit allen Azure Zugriffen (Portal, API, CLI) hinzugefuegt, geaender oder geloescht werden
- Azure Policy fuer Taggingregeln und Taggingkonventionen