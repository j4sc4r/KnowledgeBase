# AZ - 104 - 1 - Prereqs for Azure Administrators

## Resource Groups 

Resource Groups are a logical collection of resources.
Resource groups store metadata of resources. 

- Resourcen koennen nur in einer resource group existieren
- Resource Groups koennen nicht umbenannt werden
- Resource Groups koennen viele verschiedene Services beinhalten
- Resource Groups koennen Resourcen von vielen verschiedenen Regionen beinhalten

- Resourcen mit dem selber Lebenszyklus sollten in einer resource group bereitgestellt, geupdated und geloescht werden.
- Wenn eine resource group geloescht wird werden alle resourcen darin geloescht

## ARM-Templates

ARM-Templates sind JSON Dateien.
Bicep ist eine Abstraktionsschicht von ARM-Templates, Synatx ist JSON simplified

Wenn du ein 2. mal ein ARM-Template bereitstellst werden die bereits erstellten Resourcen nicht veraendert.

Beispiele fuer ARM- und Bicep-Templates + die Bereitstellung von Ressourcen ueber die CLI:

[[Azure CLI Commands]]
[[Azure ARM-Templates]]
[[Azure Bicep-Templates]]