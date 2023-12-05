# Use case 5: SOC Automated Assistance

## Alle playbooks combined
[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAxelBornauw%2Fsentinel-use_cases%2Fmain%2FUse%2520case%25205%2FOwnerPrompt-Combined%2Fazuredeploy.json)

## Base playbook (OwnerPrompt-Base)
[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAxelBornauw%2Fsentinel-use_cases%2Fmain%2FUse%2520case%25205%2FOwnerPrompt-Base%2Fazuredeploy.json)

## Base playbook (OwnerPrompt-Teams)
[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAxelBornauw%2Fsentinel-use_cases%2Fmain%2FUse%2520case%25205%2FOwnerPrompt-Teams%2Fazuredeploy.json)

## Base playbook (OwnerPrompt-CustomTeams)
[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAxelBornauw%2Fsentinel-use_cases%2Fmain%2FUse%2520case%25205%2FOwnerPrompt-CustomTeams%2Fazuredeploy.json)

## Base playbook (OwnerPrompt-BlockUser)
[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAxelBornauw%2Fsentinel-use_cases%2Fmain%2FUse%2520case%25205%2FOwnerPrompt-BlockUser%2Fazuredeploy.json)

## Base playbook (OwnerPrompt-InvestigateEntity)
[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAxelBornauw%2Fsentinel-use_cases%2Fmain%2FUse%2520case%25205%2FOwnerPrompt-InvestigateEntity%2Fazuredeploy.json)

## Vereisten:
Allereerst zijn er eerst twee externe modules nodig om de Assistant te laten werken: de [STAT](https://github.com/briandelmsft/SentinelAutomationModules/tree/main/Deploy) en [AbuseIPDB](https://github.com/Azure/Azure-Sentinel/tree/master/Solutions/AbuseIPDB/Playbooks#custom-connectors--3-playbook-templates-deployment) modules. De STAT modules moeten ook de juiste rechten krijgen via het script op de GitHub. Het is ook vereist dat de namen van de API custom connectors en playbooks default blijven staan! De ARM templates rekenen hierop en anders gebeuren er errors.  <br/><br/>
Het script zorgt er wel niet voor dat alle STAT modules de juiste permissies hebben gekregen. De module Run-Playbook is cruciaal in de flow tussen alle verschillende playbooks, maar ontbreekt het recht om andere playbooks op te roepen. Geef het daarom in IAM de role “Microsoft Sentinel Playbook Operator”, waardoor alle permissies normaal juist staan.  <br/><br/>
De twee playbooks ‘OwnerPrompt-Teams’ en ‘OwnerPrompt-CustomTeams’ gebruiken beiden een Azure blob om data op te slaan (gekozen gebruikers). Hiervoor is eerst een Azure storage account nodig. In dat storage account moet er ook een container zitten. De naam van die container wordt dan later als parameter meegegeven bij het deployen van deze playbooks.  <br/><br/>
Bij zo goed als alle playbooks wordt ook de tenant-id van de omgeving gevraagd, om zo de juiste resources te kunnen locaten.  <br/><br/>
Bij het playbook ‘OwnerPrompt-BlockUser’ moet er eerst ook voordien een app registration gemaakt worden. Om een gebruiker zijn wachtwoord te laten resetten moet er een API call gemaakt worden via deze app. Maak dus een nieuwe app registration en geef deze een passende naam. Ga hierna naar Entra ID, ‘Roles and administrators’ en klik dan op ‘password administrator’. Voeg de net-gemaakte application toe als assignment.
Keer hierna terug naar de app registration, en kopieer bij ‘Overview’ de application (client) ID. Deze waarde moet ook als parameter meegegeven worden. Ga hierna bij ‘Certificates en secrets’ en kopieer de value van de secret en zet deze waarde op een veilige zoals een Azure Key Vault.  <br/><br/>
Na het implementeren van de playbooks moeten ook de connecties nog geauthorized worden. Deze connecties staan allemaal op het einde van de uitleg over elke playbook.