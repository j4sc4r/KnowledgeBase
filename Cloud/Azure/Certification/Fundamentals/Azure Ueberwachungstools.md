# Azure Ueberwachungstools

## Azure Adivsor

- wertet Azure-Ressourcen aus und stellt Empfehlungen bereit, dabei zu unterstützen, die Zuverlässigkeit, Sicherheit und Leistung zu verbessern

Empfehlungskategorien:

- Zuverlaessigkeit
	- dient zum Sicherstellen und Verbessern der Kontinuität Ihrer unternehmenskritischer Anwendungen
- Sicherheit
	- dient zum Erkennen von Bedrohungen und Sicherheitsrisiken, die zu Sicherheitsverletzungen führen können
- Leistung
	- dient zum Verbessern der Geschwindigkeit Ihrer Anwendungen
- Optimaler Betrieb
	- dient zum Optimieren der Prozess- und Workfloweffizienz, Ressourcenverwaltbarkeit und bewährten Bereitstellungsmethoden
- Kosten
	- dient zum Optimieren und Reduzieren Ihrer Gesamtausgaben für Azure

## Azure Service Health

Mit Azure Service Health können Sie Azure-Ressourcen (Ihre speziell bereitgestellten Ressourcen und den Gesamtstatus von Azure) nachverfolgen.

- Azure Status 
	- bietet Bild vom globalen Status von Azure
	- informiert Sie über Dienstausfälle
- Service Health
	- bietet eine detailliertere Sicht auf Azure-Dienste und -Regionen
	- Informationen zu Ausfällen und geplanten Wartungen sowie andere Integritätsempfehlungen
- Ressource Health
	- maßgeschneiderte Ansicht Ihrer tatsächlichen Azure-Ressourcen
	- enthält Informationen zur Integrität von einzelnen Cloudressourcen

## Azure Monitor

- ist eine Plattform für das Sammeln von Daten der Ressourcen, die Analyse dieser Daten, die Visualisierung
- kann Azure-Ressourcen, lokale Ressourcen und sogar Multi-Cloud-Ressourcen wie virtuelle Computer überwachen

![[Azure_Monitor.png]]

### Azure Log Analytics

- Tool mit dem Protokollabfragen für die von Azure Monitor gesammelten Daten geschrieben und ausgeführt werden koennen
- unterstuetzt einfache Abfragen, komplexe Abfragen und Datenanalysen

### Azure Monitor-Warnungen

- automatische information, dass ein Schwellenwert ueberschritten wurde
- festlegung von Warnungsbedingungen und die Benachrichtigungsaktionen
- Kann auch korrekturmasnahmen versuchen
- verwenden Aktionsgruppen für die Konfiguration, wer benachrichtigt werden soll und welche Aktion ausgeführt werden soll
- Aktionsgruppe ist eine Sammlung von Benachrichtigungs- und Aktionseinstellungen, die Sie einer oder mehreren Warnungen zuordnen

### Application Insights

- Ueberwacht Webanwendungen
- Zum benutzen SDK in Anwendung installieren oder den Application Insights-Agent verwenden

Ueberwachte Informationen:

- Anforderungsraten, Antwortzeiten und Fehlerraten
- Abhängigkeitsraten, Antwortzeiten und Fehlerraten zum Ermitteln, ob die Leistung durch externe Dienste beeinträchtigt wird.
- Informationen zu Seitenansichten und Ladeleistung, die von den Browsern der Benutzer gemeldet werden
- AJAX-Aufrufe von Webseiten mit Informationen zu Raten, Antwortzeiten und Fehlerraten
- Anzahl von Benutzern und Sitzungen
- Leistungsindikatoren von Windows- oder Linux-Servercomputern, z. B. zu CPU, Arbeitsspeicher und Netzwerkauslastung