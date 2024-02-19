# Vorteile von Clouddiensten

Die größten Herausforderungen bei der Erstellung oder Bereitstellung einer Cloudanwendung sind die Betriebszeit (oder Verfügbarkeit) und die Verarbeitung der Nachfrage (oder Skalierung).

## Hochverfuegbarkeit

Gewaehrleistung maximaler Verfuegbarkeit, unabhängig von Unterbrechungen oder möglichen Ereignissen. Diese garantierten Betriebszeiten werden in SLAs festgehalten und wenn diese gebrochen werden auch mit Verguenstigungen entschaedigt. 

Azure uebliche Downtimes sind laut Azure SLAs:
- 99%
- 99,9%
- 99,95%
- selten auch 99,99%

## Skalierbarkeit

Skalierbarkeit bietet die Möglichkeit, Ihre Ressourcen an den jeweiligen Bedarf anzupassen.

### Vertikale Skalierung

Bei mehr Auslastung koennen dem virtuellen Computer zusaetzliche CPUs oder RAM hinzufuegt werden koennen. Umgekehrt können Sie durch Verringern der CPU- oder RAM-Spezifikationen die Ressourcen auch vertikal herunterskalieren, wenn Sie feststellen, dass Sie weniger Leistung benoetigen.

TLDR: Bessere Componenten in einen bereits vorhandenen Computer hineinbauen.

### Horizontale Skalierung

Bei der horizontalen Skalierung können Sie bei plötzlich steigender Nachfrage Ihre bereitgestellten Ressourcen hochskalieren (automatisch oder manuell). Das bedeutet, dass Sie z. B. weitere VMs oder Container hinzufügen können bzw. bei sinkender Nachfrage wieder (automatisch oder manuell) entfernen können.

TLDR: Neue Computer/Container zum bereits vorhandenen Computer dazustellen.

## Zuverlaessigkeit

Ist die Faehigkeit eines Systems, nach Ausfällen eine Wiederherstellung durchzuführen und die Betriebsbereitschaft sicherzustellen.

Durch ihr dezentrales Design unterstützt die Cloud eine zuverlässige und resiliente Infrastruktur. Dieses dezentrale Design der Cloud ermöglicht es Ihnen, Ressourcen in Regionen auf der ganzen Welt bereitzustellen. Wenn in einer Region ein Notfall vorliegt, sind die anderen Regionen dank des globalen Maßstabs weiterhin in Betrieb.

## Vorhersagbarkeit

Durch Kosten und Leistungsrechner koennen in der Cloud viele Loesungen schon vorher gut kalkuliert werden und spart zeit in der Planung von Ressourcen.

## Governance und Compliance

Mithilfe von Vorlagen wird sichergestellt, dass alle bereitgestellten Ressourcen unternehmensinternen Standards und gesetzlichen Vorschriften entsprechen.

Im Rahmen der cloudbasierten Überwachung werden alle Ressourcen gekennzeichnet, die nicht den unternehmensinternen Standards entsprechen.

Je nach Betriebsmodell können Softwarepatches und -updates auch automatisch angewendet werden, was sowohl der Governance als auch der Sicherheit zugute kommt.

## Verwaltung

### Verwaltung der Cloud

Cloudverwaltung bedeutet Verwalten Ihrer Cloudressourcen. In der Cloud ist Folgendes möglich:

- Automatisches Skalieren der Ressourcenbereitstellung nach Bedarf
- Bereitstellen von Ressourcen basierend auf einer vorkonfigurierten Vorlage, wodurch eine manuelle Konfiguration nicht mehr notwendig ist
- Überwachen der Integrität von Ressourcen und automatisches Ersetzen fehlerhafter Ressourcen
- Erhalten automatischer Warnungen basierend auf konfigurierten Metriken, sodass Sie in Echtzeit über die Leistung informiert sind

### Verwaltung in der Cloud

Bei der Verwaltung in der Cloud geht es darum, wie Sie Ihre Cloudumgebung und -ressourcen verwalten können. Sie können sie folgendermaßen verwalten:

- Über ein Webportal
- Mithilfe einer Befehlszeilenschnittstelle
- Mithilfe von APIs
- Mithilfe von PowerShell.


