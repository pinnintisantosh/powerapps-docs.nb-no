---
title: Å opprette en Common Data Service for apper-database | Microsoft Docs
description: Gjennomgang av hvordan du oppretter en Common Data Service (CDS) for apper-database.
services: powerapps
author: manasmams
manager: kfile
ms.service: powerapps
ms.component: pa-admin
ms.topic: conceptual
ms.date: 03/21/2018
ms.author: manasma
ms.openlocfilehash: 3343e8cd81e23d4938466d12ddca2e0a85dc12c8
ms.sourcegitcommit: 68fc13fdc2c991c499ad6fe9ae1e0f8dab597139
ms.translationtype: HT
ms.contentlocale: nb-NO
ms.lasthandoff: 06/04/2018
ms.locfileid: "34168485"
---
# <a name="create-a-common-data-service-for-apps-database"></a>Å opprette en Common Data Service for apper-database
Du kan opprette en database og utvikle apper ved hjelp av Common Data Service for apper som et datalager. Du kan enten opprette dine egne egendefinerte enheter, eller du kan bruke de forhåndsdefinerte enhetene. Hvis du vil opprette en database, må du først opprette et miljø, eller tilordnes til en eksisterende miljø som **miljøadministrator**. Du må dessuten være tilordnet den riktige lisensen. Hvis du vil ha informasjon om kjøp av et abonnement for å bruke CDS for apper, kan du se [Prisinformasjon](pricing-billing-skus.md).

Det finnes mange måter å opprette en database på:

* Fra administrasjonssenteret for PowerApps
* I **Enheter**-ruten på powerapps.com

## <a name="create-a-database-in-the-admin-center"></a>Å opprette en database i administrasjonssenteret
1. Klikk på **Miljøer** i [administrasjonssenteret](https://admin.powerapps.com) i venstre navigasjonsrute.
    
2. Velg miljøet der du ønsker å opprette en database.
    
    ![](./media/create-database/environment-list-new.png)

3. Klikk på **Opprett en database** på **Detaljer**-fanen. 
    
    ![](./media/create-database/Create-DB-From-Details.png)

4. Velg valuta og språk for å fortsette med opprettelsen av databasen. 
    
    ![](./media/create-database/DB-Choose-options.png)



## <a name="create-a-database-in-the-entities-pane-of-powerapps"></a>Å opprette en database i Enheter-ruten i PowerApps
1. Utvid **Data**-delen på [powerapps.com](https://web.powerapps.com), og trykk eller klikk på **Enheter** i venstre navigasjonsrute.

2. Klikk på **Opprett database** for å opprette databasen.

    ![](./media/create-database/Create-DB-From-Entities.png)

> [!NOTE]
> Det er for øyeblikket ikke mulig å opprette en database utenfor Azure AD-området. Det vil snart være mulig å opprette en database i et annet område enn hjemmeområdet for din Azure AD, men for øyeblikket må du kontrollere at du oppretter en database i et miljø som har samme område som hjemmeområdet som din Azure AD.

## <a name="security-model-for-the-databases"></a>Sikkerhetsmodell for databasene
Når databasen er opprettet, fortsetter brukerne som har tilordnet miljøroller å opprettholde disse tillatelsene.  
    Brukere med **Miljøadministrator**-rollen tilordnes nå **Systemadministrator**-rollen. Brukere med **Miljøoppretter** fortsetter med samme rolle.

Du kan tilordne flere brukere til forhåndsangitte roller, eller du kan til og med opprette [egendefinerte roller][1]. Se [Databasesikkerhet](database-security.md) for flere detaljer.

> [!NOTE]
> Når databasen er opprettet, innehar ikke sikkerhetsgruppene rollen som Miljøadministrator eller Miljøoppretter for en sikkerhetsgruppe. Tilordning av tillatelser i en database støtter for øyeblikket ikke ADD-sikkerhetsgruppe.


## <a name="license-and-security-permissions"></a>Tillatelser for lisenser og sikkerhet
Hvis du vil opprette en database, må du være administrator i det valgte miljøet, og den riktige lisensen må tilordnes til deg. Fra miljøet kan du konfigurere sikkerhetstillatelser ytterligere for andre brukere ved å velge **Sikkerhet**-fanen. Hvis du vil ha mer informasjon, kan du se [Konfigurer databasesikkerhet](database-security.md) og [Sikkerhetsmodell](https://docs.microsoft.c../maker/common-data-service/entity-reference/security-model).

## <a name="privacy-notice"></a>Erklæring om personvern
Med den vanlige datamodellen i Microsoft PowerApps samler vi inn og lagrer egendefinerte enhets- og feltnavn i diagnostiseringssystemene.  Vi bruker denne kunnskapen til å forbedre den vanlige datamodellen for kundene våre. Enhets- og feltnavnene som skapere oppretter, hjelper oss med å forstå scenarioene som er typiske i Microsoft PowerApps-fellesskapet og få rede på hull i tjenestens standarddekning for enheter, som eksempelvis skjemaer knyttet til organisasjoner. Dataene i databasetabeller som er knyttet til disse enhetene, blir ikke åpnet eller brukt av Microsoft eller replisert utenfor området hvor databasen er klargjort. Merk deg imidlertid at den egendefinerte enheten og feltnavnene kan repliseres på tvers av områder og blir slettet i henhold til retningslinjene våre for dataoppbevaring. Microsoft tar vare på personvernet ditt, som ytterligere beskrevet i [Klareringssenteret](https://www.microsoft.com/trustcenter/Privacy/default.aspx).


<!--Reference links in article-->
[1]: https://technet.microsoft.com/library/dn531130.aspx