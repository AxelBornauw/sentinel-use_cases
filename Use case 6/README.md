# Use case 6: Een gebruiker genereerde meer dan 2 incidenten in de laatste 7 dagen en krijgt de mogelijkheid om zijn Sentinel incident te snoozen.

## Prereq
- ['NegeerIncident' watchlist met alias 'NegeerIncident' en 3 kolommen](https://github.com/AxelBornauw/sentinel-use_cases/blob/main/Use%20case%206/NegeerIncident.csv):
    - Naam
    - ID
    - EindTijd
- [STAT modules](https://github.com/briandelmsft/SentinelAutomationModules)
- Entra ID & Teams connecties autorizeren
- Playbook 'Microsoft Sentinel Contributor' role geven

## Playbook
[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAxelBornauw%2Fsentinel-use_cases%2Fmain%2FUse%2520case%25206%2Fazuredeploy.json)