
# Azure Features und Tools fuer Governance und Compliance

## Microsoft Purview

- sind Datengovernance-, Risiko- und Compliancelösungen, mit denen ein zentraler, einheitlicher Überblick über Daten erhalten wird
- lokalen Daten, Multi-Cloud- und Software-as-a-Service-Daten
- Automatisierte Datenermittlung
- Klassifizierung vertraulicher Daten
- Vollständige Datenherkunft

![[Azure_Purview.png]]

### Risiko- und Complianceloesungen

- Microsoft 365 ist eine Kernkomponente
- Schützen von vertraulichen Daten in Clouds, Apps und auf Geräten
- Identifizieren von Datenrisiken und Verwalten gesetzlicher Complianceanforderungen
- Erste Schritte mit der Einhaltung gesetzlicher Bestimmungen

### Datagovernance

- Erstellen einer aktuellen Übersicht Ihres gesamten Datenbestands, einschließlich Datenklassifizierung und End-to-End-Herkunft
- Ermitteln, wo vertrauliche Daten in Ihrem Datenbestand gespeichert sind
- Erstellen einer sicheren Umgebung für Datenconsumer, um wertvolle Daten zu finden
- Generieren von Erkenntnissen darüber, wie Ihre Daten gespeichert und verwendet werden
- Sicheres Verwalten des Zugriffs auf die Daten in Ihrem Datenbestand im benötigten Umfang

## Azure Policy

- können einzelne Richtlinien als auch Gruppen verwandter Richtlinien definiert werden
- kann verhindern, dass nicht konforme Ressourcen erstellt werden
- können auf jeder Ebene festgelegt werden (Abonnement, Ressourcen, usw.)
- werden vereerbt
- enthält integrierte Richtlinien- und Initiativendefinitionen für Speicher, Netzwerk, Compute, Security Center und Überwachung

### Azure Policy-Initiativen

- ist eine Möglichkeit, verwandte Richtlinien zu gruppieren


## Ressourcensperren

- verhindert, dass Ressourcen versehentlich gelöscht oder geändert werden
- zwei Arten: eine verhindert das loeschen von ressourcen, die andere das veraendern von ressourcen

**Typen:**
- Loeschen:
	- autorisierte Benutzer koennen eine Ressource weiterhin lesen und ändern, jedoch nicht löschen können
- ReadOnly:
	- autorisierte Benutzer eine Ressource zwar lesen, aber nicht löschen oder aktualisieren können

### Verwaltung von Ressourcensperren

- Azure-Portal, Azure CLI und Azure Resource Manager-Vorlage
- selbst als Besitzer muessen sperren aufgehoben werden --> sonst kein aenderungsrecht

## Azure Service Trust Portal

- Zugriff auf weitere Tools zum Thema Sicherheit, Datenschutz und Compliance