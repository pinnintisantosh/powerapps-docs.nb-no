---
title: Svar på DSR-forespørsler om sletting av kundedata | Microsoft Docs
description: Svar på DSR-forespørsler om sletting av kundedata
services: powerapps
suite: powerapps
documentationcenter: na
author: jamesol-msft
manager: kfile
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/17/2018
ms.author: jamesol
ms.openlocfilehash: 67e1ad0056f80b892343506ec9a89845e0bca05e
ms.sourcegitcommit: e3a2819c14ad67cc4ca6640b9064550d0f553d8f
ms.translationtype: HT
ms.contentlocale: nb-NO
ms.lasthandoff: 04/20/2018
---
# <a name="responding-to-delete-data-subject-rights-dsr-requests-for-customer-data-in-powerapps"></a>Svar på DSR-forespørsler om sletting av kundedata i PowerApps

«Retten til sletting» ved å fjerne personopplysninger fra en organisasjons kundedata er en viktig beskyttelse i EUs personvernforordning (GDPR). Fjerning av personopplysninger omfatter fjerning av systemgenererte logger, men ikke informasjon for revisjonslogger.

PowerApps gir brukere mulighet til å utvikle bransjespesifikke apper som er en viktig del av organisasjonens daglige drift. Når en bruker forlater organisasjonen, må du manuelt se gjennom data og ressurser brukeren har opprettet, og avgjøre om du vil slette det. Andre personopplysninger blir automatisk slettet når brukerens konto blir slettet fra Azure Active Directory.

Her er en oversikt over hvilke personopplysninger som automatisk blir slettet, og hvilke som krever at du går gjennom dem og sletter dem manuelt:

Krever manuell gjennomgang og sletting |   Slettes automatisk når brukeren slettes fra Azure Active Directory.
--- | ---
Miljø\** | Gateway
Miljøtillatelser\*** | Gatewaytillatelser
Lerretsapp\** | PowerApps-varslinger
Lerretsapptillatelser | PowerApps-brukerinnstillinger
Tilkobling\** | Brukerappinnstillinger for PowerApps
Tilkoblingstillatelser |
Egendefinert kobling\** |
Tillatelser for egendefinerte koblinger |  

\** Hver av disse ressursene inneholder oppføringer av typen «Opprettet av» og «Endret av» som inneholder personopplysninger. Av sikkerhetsgrunner beholdes disse oppføringene til ressursen er slettet.

\*** For miljøer som inkluderer en Common Data Service (CDS) for Apps-database, blir miljøtillatelser (det vil si hvilke brukere som er tilordnet miljøoppretter- og administratorroller), lagret som oppføringer i den databasen. Se [Executing DSRs against Common Data Service Customer Data](https://go.microsoft.com/fwlink/?linkid=872251) (Håndtering av DSR-forespørsler om kundedata for Common Data Service) for å få en veiledning i hvordan du svarer på DSR-forespørsler for brukere som bruker CDS for Apps.

For data og ressurser som krever manuell gjennomgang, kan du tilordne (om nødvendig) eller slette personopplysninger for en bestemt bruker i PowerApps på følgende steder:

- Nettstedstilgang: [PowerApps-området](https://web.powerapps.com), [PowerApps-administrasjonssenteret](https://admin.powerapps.com/) og [Office 365 Service Trust Portal](https://servicetrust.microsoft.com/)
- PowerShell-tilgang: PowerApps-cmdleter (for [apputviklere](https://go.microsoft.com/fwlink/?linkid=871448) og [administratorer](https://go.microsoft.com/fwlink/?linkid=871804)) og cmdleter for [lokale gatewayer](https://go.microsoft.com/fwlink/?linkid=872238)
Her er en oversikt over hvor du kan slette de ulike ressurstypene som kan inneholde personopplysninger:

Ressurser som inneholder personopplysninger | Nettstedstilgang | PowerShell-tilgang
--- | --- | ---
Miljø | Administrasjonssenteret for PowerApps |  PowerApps-cmdleter
Miljøtillatelser**   | Administrasjonssenteret for PowerApps | PowerApps-cmdleter
Lerretsapp  | Administrasjonssenteret for PowerApps <br> PowerApps-området| PowerApps-cmdleter
Lerretsapptillatelser  | Administrasjonssenteret for PowerApps | PowerApps-cmdleter
Tilkobling | | Apputvikler: tilgjengelig <br> Administrator: under utvikling
Tilkoblingstillatelser | | Apputvikler: tilgjengelig <br> Administrator: under utvikling
Egendefinert kobling | | Apputvikler: tilgjengelig <br> Administrator: under utvikling
Tillatelser for egendefinerte koblinger | | Apputvikler: tilgjengelig <br> Administrator: under utvikling

\** I CDS for Apps blir miljøtillatelser og tillatelser for modelldrevne apper lagret som oppføringer i instansen for den databasen hvis du har opprettet en database i miljøet. Se [Executing DSRs against Common Data Service Customer Data](https://go.microsoft.com/fwlink/?linkid=872251) (Håndtering av DSR-forespørsler om kundedata for Common Data Service) for å få en veiledning i hvordan du svarer på DSR-forespørsler for brukere som bruker CDS for Apps.

## <a name="prerequisites"></a>Forutsetninger

### <a name="for-users"></a>For brukere
Alle brukere som har en gyldig PowerApps-lisens, kan utføre brukeroperasjonene som beskrevet i dette dokumentet, ved hjelp av [PowerApps-området](https://web.powerapps.com) eller [PowerShell-cmdleter for apputviklere](https://go.microsoft.com/fwlink/?linkid=871448).

### <a name="for-administrators"></a>For administratorer
For at du skal kunne utføre de administrative operasjonene som er beskrevet i dette dokumentet, ved å bruke [administrasjonssenteret for PowerApps](https://admin.powerapps.com/), administrasjonssenteret for Microsoft Flow eller [PowerShell-cmdleter for PowerApps-administratorer](https://go.microsoft.com/fwlink/?linkid=871804), må du ha en konto som har følgende tillatelser:

- En betalt lisens eller prøvelisens på PowerApps Plan 2. Du kan [registrer deg for en prøvelisens](http://web.powerapps.com/trial) og fornye den etter 30 dager.
- I tillegg kreves det rettigheter for [global administrator for Office 365](https://support.office.com/article/assign-admin-roles-in-office-365-for-business-eac4d046-1afd-4f1a-85fc-8219c79e1504) eller [global administrator for Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal) hvis du har behov for å søke via ressursene til en annen bruker. Ellers har du bare tilgang til de miljøene og miljøressursene der du har miljøadministratorrettigheter.

## <a name="step-1-delete-or-reassign-all-environments-created-by-the-user"></a>Trinn 1: Slett eller tilordne på nytt alle miljøer som er opprettet av brukeren
Som administrator må du under behandlingen av en DSR-forespørsel om sletting ta to beslutninger for hvert miljø som brukeren har opprettet:

1.  Hvis du finner ut at miljøet ikke brukes av andre i organisasjonen, kan du velge å slette miljøet.

2.  Hvis du finner ut at miljøet er fremdeles nødvendig, kan du velge ikke å slette miljøet og legge til deg selv (eller en annen bruker i organisasjonen) som miljøadministrator.

> [!IMPORTANT]
> Hvis du sletter et miljø, slettes alle ressurser i miljøet permanent, inkludert alle apper, flyter, tilkoblinger og så videre. Du bør derfor se gjennom innholdet i et miljø før du sletter det.

### <a name="give-access-to-a-users-environments-from-the-powerapps-admin-center"></a>Gi tilgang til en brukers miljøer fra administrasjonssenteret for PowerApps
En administrator kan gi administrativ tilgang til et miljø som er opprettet av en bestemt bruker, ved å følge disse trinnene fra [administrasjonssenteret for PowerApps](https://admin.powerapps.com/):

1. Fra [administrasjonssenteret for PowerApps](https://admin.powerapps.com/) velger du hvert miljø i organisasjonen.

    ![Målside for administrasjonssenteret](./media/powerapps-gdpr-delete-dsr/admin-center-landing.png)

2. Hvis miljøet ble opprettet av brukeren fra DSR-forespørselen, velger du **Security** (Sikkerhet) og fortsetter med trinnene som er beskrevet i [Administer environments](environments-administration.md) (Administrer miljøer) for å gi administratorrettigheter til deg selv eller en annen bruker i organisasjonen.

    ![Miljøsikkerhet](./media/powerapps-gdpr-delete-dsr/share-environment.png)

### <a name="delete-environments-created-by-a-user-from-the-powerapps-admin-center"></a>Slett miljøer som er opprettet av en bruker, fra administrasjonssenteret for PowerApps
En administrator kan gå gjennom og slette miljøer som er opprettet av en bestemt bruker, ved å følge disse trinnene fra [administrasjonssenteret for PowerApps](https://admin.powerapps.com/):

1. Fra [administrasjonssenteret for PowerApps](https://admin.powerapps.com/) velger du hvert miljø i organisasjonen.

    ![Målside for administrasjonssenteret](./media/powerapps-gdpr-delete-dsr/admin-center-landing.png)

2. Hvis miljøet ble opprettet av brukeren fra DSR-forespørselen, velger du **Delete** (Slett) og fortsetter deretter med trinnene for å slette miljøet:

    ![Miljøsletting](./media/powerapps-gdpr-delete-dsr/delete-environment.png)

### <a name="give-access-to-a-users-environments-using-powershell"></a>Gi tilgang til en brukers miljøer ved hjelp av PowerShell
En administrator kan gi seg selv (eller en annen bruker i organisasjonen) tilgang til alle miljøer som er opprettet av en bruker, via funksjonen **Set-AdminEnvironmentRoleAssignment** i [PowerShell-cmdleter for PowerApps-administratorer](https://go.microsoft.com/fwlink/?linkid=871804):

```
Add-PowerAppsAccount
$deleteDsrUserId = "0ecb1fcc-6782-4e46-a4c4-738c1d3accea"
$myUserId = $global:currentSession.UserId

#Assign yourself as an admin to each environment created by the user
Get-AdminEnvironment -CreatedBy $deleteDsrUserId | Set-AdminEnvironmentRoleAssignment -RoleName EnvironmentAdmin -PrincipalType User -PrincipalObjectId $myUserId

#Retrieve the environment role assignments to confirm
Get-AdminEnvironment -CreatedBy $deleteDsrUserId | Get-AdminEnvironmentRoleAssignment
```

> [!IMPORTANT]
> Denne funksjonen fungerer bare i miljøer som ikke har en instans av en database i CDS for Apps.

### <a name="delete-environments-created-by-a-user-using-powershell"></a>Slett miljøer som er opprettet av en bruker, ved hjelp av PowerShell
 En administrator kan slette alle miljøer som er opprettet av en bruker, via funksjonen **Remove-AdminEnvironment** i [PowerShell-cmdleter for PowerApps administratorer](https://go.microsoft.com/fwlink/?linkid=871804):

```
Add-PowerAppsAccount
$deleteDsrUserId = "0ecb1fcc-6782-4e46-a4c4-738c1d3accea"

# Retrieve all environments created by the user and then delete them
Get-AdminEnvironment -CreatedBy $deleteDsrUserId | Remove-AdminEnvironment
```

## <a name="step-2-delete-the-users-permissions-to-all-other-environments"></a>Trinn 2: Slett brukerens tillatelser til alle andre miljøer
Brukere kan gis tillatelser (for eksempel miljøadministrator og miljøoppretter) i et miljø, og disse lagres i PowerApps-tjenesten som en «rolletildeling».
I CDS for Apps blir disse rolletildelingene lagret som oppføringer i instansen for den databasen hvis du har opprettet en database i miljøet.
Du finner mer informasjon i [Administer environments](environments-administration.md) (Administrer miljøer).

### <a name="for-environments-without-a-cds-for-apps-database"></a>For miljøer uten en CDS for Apps-database

#### <a name="powerapps-admin-center"></a>Administrasjonssenteret for PowerApps
En administrator kan slette en brukers miljøtillatelser fra [administrasjonssenteret for PowerApps](https://admin.powerapps.com/) ved å følge disse trinnene:

1.  Fra [administrasjonssenteret for PowerApps](https://admin.powerapps.com/) velger du hvert miljø i organisasjonen.

    Du må være [global administrator for Office 365](https://support.office.com/article/assign-admin-roles-in-office-365-for-business-eac4d046-1afd-4f1a-85fc-8219c79e1504) eller [global administrator for Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal) for å kunne gjennomgå alle miljøer som har blitt opprettet i organisasjonen.

    ![Målside for administrasjonssenteret](./media/powerapps-gdpr-delete-dsr/admin-center-landing.png)

2.  Velg **Security** (Sikkerhet).

    Hvis miljøet ditt ikke har en CDS for Apps-database, ser du en del med **Environment Roles** (Miljøroller).

4.  I **Environment Roles** (Miljøroller) velger du både **Environment Admin** (Miljøadministrator) og **Environment Maker** (Miljøoppretter), og søker deretter etter brukerens navn ved å bruke søkefeltet.

    ![Miljørollesiden](./media/powerapps-gdpr-delete-dsr/admin-environment-role-share-page.png)

5.  Hvis brukeren har tilgang til en av rollene, fjerner du tillatelsen i skjermbildet **Users** (Brukere) og velger **Save** (Lagre).

#### <a name="powershell"></a>PowerShell
Administratorer kan slette alle miljørolletildelinger for en bruker i alle miljøer uten en CDS for Apps-database ved hjelp av funksjonen **Remove-AdminEnvironmentRoleAssignment** i [PowerShell-cmdleter for PowerApps-administratorer](https://go.microsoft.com/fwlink/?linkid=871804):

```
Add-PowerAppsAccount
$deleteDsrUserId = "0ecb1fcc-6782-4e46-a4c4-738c1d3accea"

#find all environment role assignments for the user for environments without a CDS for Apps instance and delete them
Get-AdminEnvironmentRoleAssignment -UserId $deleteDsrUserId | Remove-AdminEnvironmentRoleAssignment
```

> [!IMPORTANT]
> Denne funksjonen fungerer bare for miljøer som ikke har en instans av en CDS for Apps-database.

### <a name="for-environments-with-a-cds-for-apps-database"></a>For miljøer MED en CDS for Apps-database
I CDS for Apps blir disse rolletildelingene lagret som oppføringer i instansen for den databasen hvis du har opprettet en database i miljøet. Du finner informasjon om hvordan du fjerner personopplysninger fra en databaseinstans for CDS for Apps, i dokumentasjonen nedenfor.

## <a name="step-3-delete-or-reassign-all-canvas-apps-owned-by-a-user"></a>Trinn 3: Slett eller tilordne på nytt alle lerretsapper som eies av en bruker

### <a name="reassign-a-users-canvas-apps-using-the-powerapps-admin-powershell-cmdlets"></a>Tilordne en brukers lerretsapper på nytt ved hjelp av PowerShell-cmdleter for PowerApps-administratorer
Hvis en administrator bestemmer seg for ikke å slette en brukers lerretsapper, kan appene som eies av en bruker, tilordnes på nytt via funksjonen **Set-AdminAppOwner** i [PowerShell-cmdleter for PowerApps-administratorer](https://go.microsoft.com/fwlink/?linkid=871804):

```
Add-PowerAppsAccount
$deleteDsrUserId = "0ecb1fcc-6782-4e46-a4c4-738c1d3accea"
$newAppOwnerUserId = "72c272b8-14c3-4f7a-95f7-a76f65c9ccd8"

#find all apps owned by the DSR user and assigns them a new owner
Get-AdminApp -Owner $deleteDsrUserId | Set-AdminAppOwner -AppOwner $newAppOwnerUserId
```

### <a name="delete-a-users-canvas-app-using-the-powerapps-site"></a>Slett en brukers lerretsapp ved hjelp av PowerApps-området
En bruker kan slette en app fra [PowerApps-området](https://web.powerapps.com). Du finner den fullstendige fremgangsmåten om hvordan du sletter en app, i delen om appsletting.

### <a name="delete-a-users-canvas-app-using-the-powerapps-admin-center"></a>Slett en brukers lerretsapp ved hjelp av administrasjonssenteret for PowerApps
Administratorer kan slette apper som er opprettet av en bruker, fra [administrasjonssenteret for PowerApps](https://admin.powerapps.com/) ved å følge disse trinnene:

1.  Fra [administrasjonssenteret for PowerApps](https://admin.powerapps.com/) velger du hvert miljø i organisasjonen.

    Du må være [global administrator for Office 365](https://support.office.com/article/assign-admin-roles-in-office-365-for-business-eac4d046-1afd-4f1a-85fc-8219c79e1504) eller [global administrator for Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal) for å kunne gjennomgå alle miljøer som har blitt opprettet i organisasjonen.

    ![Målside for administrasjonssenteret](./media/powerapps-gdpr-delete-dsr/admin-center-landing.png)

2.  Velg **Resources** (Ressurser)  >  **Apps** (Apper).

3.  Bruk søkefeltet til å søke etter navnet til brukeren. Dette viser alle apper som brukeren har opprettet i dette miljøet:

    ![Søk etter apper](./media/powerapps-gdpr-delete-dsr/search-apps.png)

4.  Velg **Details** (Detaljer) for hver av appene som eies av brukeren:

    ![Velg appdetaljer](./media/powerapps-gdpr-delete-dsr/select-app-details.png)

5.  Velg **Delete** (Slett) for å slette hver app:

### <a name="delete-a-users-canvas-app-using-the-powerapps-admin-powershell-cmdlets"></a>Slett en brukers lerretsapp ved hjelp av PowerShell-cmdleter for PowerApps-administratorer
Hvis en administrator bestemmer seg for å slette alle lerretsapper som eies av en bruker, kan dette gjøres ved hjelp av funksjonen **Remove-AdminApp** i [PowerShell-cmdleter for PowerApps-administratorer](https://go.microsoft.com/fwlink/?linkid=871804):

```
Add-PowerAppsAccount
$deleteDsrUserId = "0ecb1fcc-6782-4e46-a4c4-738c1d3accea"

#find all apps owned by the DSR user and deletes them
Get-AdminApp -Owner "0ecb1fcc-6782-4e46-a4c4-738c1d3accea" | Remove-AdminApp
```

## <a name="step-4-delete-the-users-permissions-to-canvas-apps"></a>Trinn 4: Slett brukerens tillatelser til lerretsapper
Når en app blir delt med en bruker, lagrer PowerApps lagrer en oppføring kalt en «rolletildeling», som beskriver brukerens tillatelser (CanEdit eller CanUse), i programmet. Du finner mer informasjon i artikkelen om appdeling.

> [!NOTE]
> Rolletildelingene for en app blir slettet når appen slettes.

> [!NOTE]
> Rolletildelingen for en appeier kan bare slettes ved å tilordne en ny eier for appen.

### <a name="powerapps-admin-center"></a>Administrasjonssenteret for PowerApps
Administratorer kan slette approlletildelinger for en bruker fra [administrasjonssenteret for PowerApps](https://admin.powerapps.com/) ved å følge disse trinnene:

1.  Fra [administrasjonssenteret for PowerApps](https://admin.powerapps.com/) velger du hvert miljø i organisasjonen.

    Du må være [global administrator for Office 365](https://support.office.com/article/assign-admin-roles-in-office-365-for-business-eac4d046-1afd-4f1a-85fc-8219c79e1504) eller [global administrator for Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal) for å kunne gjennomgå alle miljøer som har blitt opprettet i organisasjonen.

    ![Målside for administrasjonssenteret](./media/powerapps-gdpr-delete-dsr/admin-center-landing.png)

2.  Velg **Resources** (Ressurser)  >  **Apps** (Apper) for hvert miljø.

3.  Velg **Share** (Del) for hver av appene i miljøet:

    ![Velg appdeling](./media/powerapps-gdpr-delete-dsr/select-admin-share-nofilter.png)

6.  Hvis brukeren har tilgang til appen, fjerner du tillatelsen i skjermbildet **Share** (Del) og velger **Save** (Lagre).

    ![Appdelingssiden for administratorer](./media/powerapps-gdpr-delete-dsr/admin-share-page.png)

### <a name="powerapps-admin-powershell-cmdlets"></a>PowerShell-cmdleter for PowerApps-administratorer
En administrator kan slette alle rolletildelinger for lerretsapper for en bruker ved hjelp av funksjonen **Remove-AdminAppRoleAssignmnet** i [PowerShell-cmdleter for PowerApps-administratorer](https://go.microsoft.com/fwlink/?linkid=871804):

```
Add-PowerAppsAccount
$deleteDsrUserId = "0ecb1fcc-6782-4e46-a4c4-738c1d3accea"

#find all app role assignments for the DSR user and deletes them
Get-AdminAppRoleAssignment -UserId $deleteDsrUserId | Remove-AdminAppRoleAssignment
```

## <a name="step-5-delete-connections-created-by-a-user"></a>Trinn 5: Slett tilkoblinger som er opprettet av en bruker
Tilkoblinger brukes sammen med koblinger ved oppretting av tilkoblingsmuligheter med andre API-er og SaaS-systemer.  Tilkoblinger inneholder blant annet referanser til brukeren som opprettet dem, og kan derfor slettes for å fjerne alle referanser til brukeren.

### <a name="powershell-cmdlets-for-app-creators"></a>PowerShell-cmdleter for apputviklere
En bruker kan slette alle tilkoblingene sine ved hjelp av funksjonen Remove-Connection i [PowerShell-cmdleter for apputviklere](https://go.microsoft.com/fwlink/?linkid=871448):

```
Add-PowerAppsAccount

#Retrieves all connections for the calling user and deletes them
Get-Connection | Remove-Connection
```

### <a name="powershell-cmdlets-for-powerapps-administrators"></a>PowerShell-cmdleter for PowerApps-administratorer
Funksjonen som tillater en administrator å finne og slette en brukers tilkoblinger med [PowerShell-cmdleter](https://go.microsoft.com/fwlink/?linkid=871804), er under utvikling.

## <a name="step-6-delete-the-users-permissions-to-shared-connections"></a>Trinn 6: Slett brukerens tillatelser til delte tilkoblinger

### <a name="powershell-cmdlets-for-app-creators"></a>PowerShell-cmdleter for apputviklere
En bruker kan slette alle tilkoblingsrolletildelingene for delte tilkoblinger ved hjelp av funksjonen Remove-ConnectionRoleAssignment i [PowerShell-cmdleter for apputviklere](https://go.microsoft.com/fwlink/?linkid=871448):

```
Add-PowerAppsAccount

#Retrieves all connection role assignments for the calling users and deletes them
Get-ConnectionRoleAssignment | Remove-ConnectionRoleAssignment
```
> [!NOTE]
> Eierrolletildelinger kan ikke slettes uten å slette tilkoblingsressursen.

### <a name="powerapps-admin-powershell-cmdlets"></a>PowerShell-cmdleter for PowerApps-administratorer
Funksjonen som tillater en administrator å finne og slette en brukers tilkoblingsrolletildelinger med [PowerShell-cmdleter for PowerApps-administratorer](https://go.microsoft.com/fwlink/?linkid=871804), er under utvikling.

## <a name="step-7-delete-custom-connectors-created-by-the-user"></a>Trinn 7: Slett egendefinerte koblinger som er opprettet av brukeren
Egendefinerte koblinger er et supplement til eksisterende standardkoblinger og gir tilkoblingsmulighet til andre API-er, SaaS og spesialutviklede systemer. Du kan overføre eierskap for egendefinerte koblinger til andre brukere i organisasjonen eller slette den egendefinerte koblingen.

### <a name="powershell-cmdlets-for-app-creators"></a>PowerShell-cmdleter for apputviklere
En bruker kan slette alle de egendefinerte koblingene sine ved hjelp av funksjonen Remove-Connector i [PowerShell-cmdleter for apputviklere](https://go.microsoft.com/fwlink/?linkid=871448):

```
Add-PowerAppsAccount

#Retrieves all custom connectors for the calling user and deletes them
Get-Connector -FilterNonCustomConnectors | Remove-Connector
```

### <a name="powerapps-admin-powershell-cmdlets"></a>PowerShell-cmdleter for PowerApps-administratorer
Funksjonen som tillater en administrator å finne og slette en brukers egendefinerte koblinger med [PowerShell-cmdleter for PowerApps-administratorer](https://go.microsoft.com/fwlink/?linkid=871804), er under utvikling.

## <a name="step-8-delete-the-users-permissions-to-shared-custom-connectors"></a>Trinn 8: Slett brukerens tillatelser til delte egendefinerte koblinger

### <a name="powershell-cmdlets-for-app-creators"></a>PowerShell-cmdleter for apputviklere
En bruker kan slette alle koblingsrolletildelingene for delte egendefinerte koblinger ved hjelp av funksjonen Remove-ConnectorRoleAssignment i [PowerShell-cmdleter for apputviklere](https://go.microsoft.com/fwlink/?linkid=871448):

```
Add-PowerAppsAccount

#Retrieves all connector role assignments for the calling users and deletes them
Get-ConnectorRoleAssignment | Remove-ConnectorRoleAssignment
```

> [!NOTE]
> Eierrolletildelinger kan ikke slettes uten å slette tilkoblingsressursen.

### <a name="powerapps-admin-powershell-cmdlets"></a>PowerShell-cmdleter for PowerApps-administratorer
Funksjonen som tillater en administrator å finne og slette en brukers koblingsrolletildelinger med [PowerShell-cmdleter for PowerApps-administratorer](https://go.microsoft.com/fwlink/?linkid=871804), er under utvikling.

## <a name="step-9-delete-the-users-personal-data-in-microsoft-flow"></a>Trinn 9: Slett brukerens personopplysninger i Microsoft Flow
PowerApps-lisenser inkluderer alltid Microsoft Flow-funksjoner. I tillegg til å være inkludert i PowerApps-lisensene er Microsoft Flow også tilgjengelig som en frittstående tjeneste.
Du finner informasjon om hvordan du svarer på DSR-forespørsler for brukere som bruker Microsoft Flow-tjenesten, i [Executing DSRs against Microsoft Flow Customer Data](https://go.microsoft.com/fwlink/?linkid=872250) (Håndtering av DSR-forespørsler om kundedata for Microsoft Flow).

> [!IMPORTANT]
> Det anbefales at administratorer utfører dette trinnet for PowerApps-brukere.

## <a name="step-10-delete-the-users-personal-data-in-instances-of-cds-for-apps"></a>Trinn 10: Slett brukerens personopplysninger i CDS for Apps-instanser
Enkelte PowerApps-lisenser, deriblant PowerApps Community Plan, gir brukerne i organisasjonen muligheten til å opprette instanser av CDS for Apps samt til å opprette og utvikle apper på CDS for Apps. PowerApps Community Plan er en gratislisens som gir brukere muligheten til å prøve CDS for Apps i et enkeltmiljø. Se siden med PowerApps-priser for informasjon om hvilke funksjoner som er inkludert i de ulike PowerApps-lisensene.

Se [Executing DSRs against customer data in CDS for Apps](https://go.microsoft.com/fwlink/?linkid=872251) (Håndtering av DSR-forespørsler om kundedata i CDS for Apps) for å få en veiledning i hvordan du svarer på DSR-forespørsler for brukere som bruker CDS for Apps.

> [!IMPORTANT]
> Det anbefales at administratorer utfører dette trinnet for PowerApps-brukere.

## <a name="step-11-delete-the-user-from-azure-active-directory"></a>Trinn 11: Slett brukeren fra Azure Active Directory
Når trinnene ovenfor er fullført, er det siste trinnet å slette brukerens konto for Azure Active Directory ved å følge trinnene som er beskrevet i GDPR-dokumentasjonen om DSR-forespørsler for Azure, som finnes i [Office 365 Service Trust Portal](https://servicetrust.microsoft.com/ViewPage/GDPRDSR).