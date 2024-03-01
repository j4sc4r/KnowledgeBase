# Cloud computing

Bereitstellung von IT-Diensten ueber das Internet. 
z.B.
- IT Infrastruktur
- virutelle Computer
- Speicher
- Datenbanken 
- Netzwerke

Clouddienste Erweitern um funktionen wie: 
- IoT 
- Machine Learning 
- KI

## Shared Responsibility Modell

Aufgaben des Cloud Anbieters: 
- physische Sicherheit 
- Das physische Rechenzentrum
- Strom
- Das physische Netzwerk

Aufgaben des Benutzers:
- Verwaltung Daten in der Cloud
- Verwaltung Geräte mit Cloudverbindung
- Verwaltung von Konten und Identitäten der Personen, Dienste und Geräte innerhalb der Organisation

Situationsbedingte Aufgaben:
- Wenn der Cloudanbieter die SQL Datenbank hostet ist er fuer die Verwaltung verantwortlich, aber der Benutzer ist immernoch fuer die Daten verantwortlich
- Wenn der Cloudanbieter eine VM hostet auf der eine SQL Datenbank laeuft, ist der Benutzer fuer das updaten der Datenbank und deren Daten verantwortlich

## Clouddiensttyp/Service Modelle

![[shared-responsibility-cloud-computing.svg]]

Das Servicemodell bestimmt die Verantwortung fuer Dinge wie:
- Betriebssysteme
- Netzwerksteuerungen
- Anwendungen
- Identitaet und Infrastruktur

## Cloudmodelle

Cloudmodelle definieren den Bereitstellungstyp von Cloudressourcen.

| Public Cloud                                                                           | Private Cloud                                                                    | Hybrid Cloud                                                                         |
| -------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------ |
| Keine hochzuskalierenden Investitionskosten                                            | Organisationen haben die vollstaendige Kontrolle ueber Ressourcen und Sicherheit | Bietet die groesste Flexibilitaet                                                    |
| Anwendungen koennen schnell bereitgestellt und ausser Betrieb genommen werden          | Daten werden nicht mit den Daten anderer Organisationen zusammengefuehrt         | Organisationen bestimmen, wo ihre Anwendungen ausgefuehrt werden                     |
| Organisationen zahlen nur das was sie nutzen                                           | Hardware muss fuer die Inbetriebnahme erworben und gewartet werden               | Organisationen kontrollieren Sicherheits-, Compliance- oder rechtliche Anforderungen |
| Organisationen haben nicht die vollstaendige Kontrolle ueber Ressourcen und Sicherheit | Organisationen sind fuer Hardwarewartung und -erneuerung verantwortlich          |                                                                                      |

### Multi-Cloud Modell

In Multi-Cloud-Szenarien werden mehrere öffentliche Cloudanbieter verwendet. In Multi-Cloud-Umgebung arbeitet man mit zwei (oder mehr) öffentlichen Cloudanbietern zusammen und verwalten Ressourcen und die Sicherheit in beiden Umgebungen.

## Azure Arc
- umfasst Technologien die helfen Cloudumgebungen zu Verwalten
- oeffentlich, private hybrid und multi-cloud wird unterstuetzt

## Verbrauchsbasiertes Modell

Beim Cloud Computing fallen für die physische Infrastruktur, Strom, Sicherheit oder andere Wartungsaspekte eines Rechenzentrums keine Kosten an. Stattdessen bezahlt man für die IT-Ressourcen, die verbraucht werden. Wenn Sie einen Monat lang keine IT-Ressourcen nutzen, bezahlen Sie auch nicht dafür.

Vorteile:
- Keine Vorlaufkosten
- Kostspielige Infrastruktur, die Benutzer moeglicherweise nicht voll nutzen, muss nicht erworben und verwaltet werden
- Bei hoeherem Bedarf koennen weitere Ressourcen dazugekauft werden
- Die Moeglichekeit, fuer weniger Ressourcen zu zahlen, wenn weniger benoetigt werden

