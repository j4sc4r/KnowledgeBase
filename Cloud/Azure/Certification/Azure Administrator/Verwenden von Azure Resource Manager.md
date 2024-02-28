# Verwenden von Azure Resource Manager

![[Azure_ARM.png]]

## Vorteile

- Ressourcen als Gruppe bereitstellen, verwalten und überwachen, anstatt diese Ressourcen einzeln zu verarbeiten
- koennen ueber gesamten Entwicklungslebenszyklus wiederholt bereitgestellt werden, so dass Ressourcen einheitlich bleiben
- Verwaltung der Infrastruktur anstelle von Skripts auch mit deklarativen Vorlagen
- Abhängigkeiten zwischen Ressourcen definieren, sodass diese in der richtigen Reihenfolge bereitgestellt werden
- koennen Zugriffssteuerung auf alle Dienste in der Ressourcengruppe anwenden, da die rollenbasierte Zugriffssteuerung (Role-Based Access Control, RBAC) standardmäßig in die Verwaltungsplattform integriert ist
- können Tags auf Ressourcen anwenden, um alle Ressourcen im Abonnement logisch zu organisieren


## Resource-Anbieter

- folgendes Format: **{Ressourcenanbieter}/{Ressourcentyp}**. Der Schlüsseltresortyp lautet beispielsweise **Microsoft.KeyVault\vaults**


## Best-Practice zum erstellen von resource groups

- Alle Ressourcen einer Gruppe sollten über den gleichen Lebenszyklus verfügen
- Jede Ressource kann nur in einer Ressourcengruppe vorhanden sein
- können eine Ressource einer Ressourcengruppe jederzeit hinzufügen bzw. die Ressource daraus entfernen
- können eine Ressource aus einer Ressourcengruppe in eine andere Gruppe verschieben (hier gibt es einschraenkungen)
- kann Ressourcen enthalten, die sich in unterschiedlichen Regionen befinden
- kann zum Festlegen der Zugriffssteuerung für administrative Aktionen verwendet werden
- kann mit Ressourcen in anderen Ressourcengruppen interagieren


## Resource-Locks

- Nur die Rollen "Benutzer" und "Benutzerzugriffsadministrator" koennen Resource-Locks erstellen oder loeschen

## Neuorganisation von Azure-Resources

- Bei Verschiebungsvorgang werden Quell- und Zielgruppe fuer die dauer gesperrt
- Bei Virtuellen Netzwerken muessen auch die abhaenigkeiten verschoben werden

## Loeschen von Resources oder Resource groups in PowerShell

```powershell
Remove-AzResourceGroup -Name "<Name>"
```

## Resourcelimits

- Zu sehen bei seinem Abonnement unter Nutzung + Kontigente

- Azure-Grenzwerte:
https://learn.microsoft.com/de-de/azure/azure-resource-manager/management/azure-subscription-service-limits?toc=%2Fazure%2Fnetworking%2Ftoc.json