---
title: Å la kunder testkjøre appene dine på AppSource | Microsoft Docs
description: Å bruk AppSource til å dele apper med kunder, og generere kundeemner for virksomheten din.
documentationcenter: na
author: linhtranms
manager: kfile
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: conceptual
ms.component: canvas
ms.date: 05/08/2017
ms.author: litran
ms.openlocfilehash: 11f0e0b8a0aa0dce59588c2e1eea21885f19b741
ms.sourcegitcommit: 68fc13fdc2c991c499ad6fe9ae1e0f8dab597139
ms.translationtype: HT
ms.contentlocale: nb-NO
ms.lasthandoff: 06/04/2018
ms.locfileid: "31836383"
---
# <a name="let-customers-test-drive-your-apps-on-appsource"></a>Å la kunder testkjøre appene dine på AppSource
Har du en lidenskap for å bygge apper i PowerApps? Har du en app du vil dele med kunder? Vi støtter nå en løsning for PowerApps-testversjon på [AppSource.com](https://appsource.microsoft.com), som en måte å dele apper med kunder samt generere kundeemner for bedriften din.

## <a name="what-is-a-test-drive-solution"></a>Hva er en testversjon?
Med en testversjon kan kundene prøve en ekte app uten å måtte registrere seg for et PowerApps-abonnement eller installere programmer. Kundene logger seg bare på AppSource.com ved bruk av Azure Active Directory (AAD)-kontoen sin, og kjører appen i nettleseren. Uten en testversjon kan kundene bare lese om appen eller se en video som beskriver den. Med testversjon får kundene en bedre forståelse av hva løsningen er og hvilke funksjoner appen har. Og de kan faktisk prøve appen også. Kundene har ingen mulighet til å se hvordan appen er bygget, noe som beskytter åndsverket. Vi samler inn og deler kundeemneinformasjon for brukere som starter testversjonsappen, for å hjelpe deg med vekst i virksomheten din.

Her kan du se et eksempel på en [appoppføring](https://go.microsoft.com/fwlink/?linkid=848867) på AppSource.com:

![Eksempel på AppSource-oppføring ](./media/dev-appsource-test-drive/sample-app-source-listing.png)

Hvis du velger koblingen **Gratis prøveversjon** fra appoppføringen ovenfor, starter den tilknyttede PowerApps-testversjonen direkte i brukerens nettleser:

![Eksempel på nettspiller for app](./media/dev-appsource-test-drive/sample-app-web-player.png)

## <a name="how-do-i-build-a-test-drive-solution"></a>Hvordan bygger jeg en testversjon?
Det å bygge en app for en testversjon er akkurat som å bygge en app i PowerApps, men du bruker innebygd data i stedet for eksterne datatilkoblinger. Ved å bruke innebygd data blir det enklere å bruke appen for kundene dine, så terskelen er veldig lav for å prøve den. Den fullstendige løsningen som du til syvende og sist distribuerer til kundene inkluderer som regel datatilkoblinger, men innebygd data fungerer bra for testversjoner.

PowerApps støtter bygging av apper med innebygd data, så du trenger bare eksempeldata for at appen skal fungere. Disse dataene skal registreres i en Excel-fil som én eller flere tabeller. I PowerApps henter du deretter data fra Excel-tabeller inn i appen og bruker de der, i stedet for gjennom en ekstern tilkobling. Prosessen nedenfor har tre trinn og den viser deg hvordan du henter data og bruker den i appen.

### <a name="step-1-import-data-into-the-app"></a>Trinn 1: Å importere data inn i appen
La oss si at du har en Excel-fil med to tabeller: **SiteInspector** og **SitePhotos**.

![Excel-tabeller som skal importeres](./media/dev-appsource-test-drive/excel-file.png)

Importer disse to tabellene i PowerApps ved bruk av alternativet **Legg til statiske data i appen**.

![Slik legger du til statiske data i appen](./media/dev-appsource-test-drive/static-data.png)

Du har nå tabellene som datakilder i appen.

![Excel-tabeller som importerte datakilder](./media/dev-appsource-test-drive/data-sources.png)

### <a name="step-2-handling-read-only-and-read-write-scenarios"></a>Trinn 2: Håndtering av scenarioer med skrivebeskyttet tilgang og lese/skrivetilgang
Dataene du importerte er *statisk*, noe som betyr skrivebeskyttet. Hvis appen er skrivebeskyttet (det vil si at den bare viser data til brukeren), kan du henvise til tabellene direkte i appen. Hvis du for eksempel ønsker tilgang til **Tittel**-feltet i **SiteInspector**-tabellen, bruker du **SiteInspector.Title** i formelen din.

Hvis appen er skrivebeskyttet, henter du først dataene fra hver tabell inn i en *samling*, som har en tabellstruktur i PowerApps. Deretter arbeider du med samlingen i stedet for tabellen. Hvis du vil hente data fra **SiteInspector**- og **SitePhotos**-tabellene inn i **SiteInspectorCollect**- og **SitePhotosCollect**-samlingene:

```
ClearCollect(SiteInspectorCollect,SiteInspector); ClearCollect(SitePhotosCollect,SitePhotos)
```

Formelen fjerner begge samlingene, deretter henter den dataene fra hver tabell inn i riktig samling:

* Påkall denne formelen et sted i appen for å laste dataene.
* Vis alle samlingene i appen ved å navigere til **Fil** > **Samlinger**.
* Hvis du vil ha mer informasjon, kan du se [Å opprette og oppdatere en samling i appen](../canvas-apps/create-update-collection.md).

Hvis du ønsker tilgang til **Tittel**-feltet, bruker du **SiteInspectorCollect.Title** i formelen.

### <a name="step-3-add-update-and-delete-data-in-your-app"></a>Trinn 3: Legg til, oppdater og slett data i appen
Du har nå sett hvordan du leser data direkte og fra en samling. Nå skal vi vise deg hvordan du kan legge til, oppdatere og slette data i en samling:

**Hvis du vil legge til en rad i en samling**, bruker du [Collect( DataSource, Item, ... )](../canvas-apps/functions/function-clear-collect-clearcollect.md):

```
Collect(SiteInspectorCollect,{ID:Value(Max(SiteInspectorCollect, ID)+1),
    Title:TitleText.Text,SubTitle:SubTitleText.Text,Description:DescriptionText.Text)
```

**Hvis du vil oppdatere en rad i en samling**, bruker du [UpdateIf( DataSource, Condition1, ChangeRecord1 [, Condition2, ChangeRecord2, ...] )](../canvas-apps/functions/function-update-updateif.md):

```
UpdateIf(SiteInspectorCollect,ID=record.ID,
    {Title:TitleEditText.Text,SubTitle:SubTitleEditText.Text,Description:DescriptionEditText.Text)
```

**Hvis du vil slette en rad fra en samling**, bruker du [RemoveIf( DataSource, Condition [, ...] )](../canvas-apps/functions/function-remove-removeif.md):

```
RemoveIf(SiteInspectorCollect,ID=record.ID)
```

> [!NOTE]
> Samlinger holder dataene kun mens appen kjører, eventuelle endinger fjernes når appen lukkes.

Kort fortalt så kan du opprette en versjon av appen med innebygde data, som simulerer at appen kobler seg til eksterne data. Etter at dataene er innebygget, er du klar for å publisere appen som en testversjon på AppSource.com.

## <a name="how-do-i-list-my-test-drive-solution-on-appsourcecom"></a>Hvordan registrerer jeg testversjonen min på AppSource.com?
Nå som appen er klar, kan du publisere den på AppSource.com. Du må fylle ut [søknadsskjemaet](https://powerapps.microsoft.com/partners/get-listed/) på PowerApps.com for å starte prosessen.

Når du har registrert appen, mottar du instruksjoner via e-post om hvordan du sender appen for publisering på AppSource.com. Pålastingsdokumentasjonen som omfatter den fullstendige prosessen kan også lastes ned [her](https://go.microsoft.com/fwlink/?linkid=851031).
