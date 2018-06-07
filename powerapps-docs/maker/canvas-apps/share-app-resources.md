---
title: Dele ressurser som brukes i appen | Microsoft Docs
description: Forstå hvordan ressursene som brukes i appen din deles når en app er delt
services: ''
suite: powerapps
documentationcenter: na
author: archnair
manager: anneta
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2016
ms.author: archanan
ms.openlocfilehash: 02df7f1df53842706bf6a41244f470f09de20c90
ms.sourcegitcommit: 59785e9e82da8f5bd459dcb5da3d5c18064b0899
ms.translationtype: HT
ms.contentlocale: nb-NO
ms.lasthandoff: 03/22/2018
ms.locfileid: "30997387"
---
# <a name="share-app-resources"></a>Dele app-ressurser
Før du [deler en app](share-app.md) bør du vurdere ressurstypene som den er avhengig av, for eksempel ett eller flere av følgende:

* en kobling til en datakilde
* en lokal datagateway
* en egendefinert kobling
* en Excel-arbeidsbok, eller en annen tjeneste
* en flyt

Noen av disse ressursene deles automatisk når du deler appen. Andre ressurser krever at du eller andre som du deler appen med, må utføre ytterligere trinn for at appen skal fungere slik du forventer.

Du kan også dele tilkoblinger, egendefinerte koblinger og lokale datagatewayer med hele organisasjonen.

## <a name="connections"></a>Tilkoblinger
Enkelte typer tilkoblinger, for eksempel SQL Server, deles automatisk, men krever at andre brukere oppretter sine egne tilkoblinger til datakilden eller kilder i appen.

På [powerapps.com](https://web.powerapps.com) kan du bestemme om en tilkobling skal deles automatisk, og du kan oppdatere delingstillatelser. Klikk eller trykk på **Behandle** i det venstre navigasjonsfeltet, klikk eller trykk på **Tilkoblinger** og klikk eller trykk deretter på en tilkobling. Hvis **Del**-fanen vises, deles tilkoblingen automatisk.

  ![Del-fanen i Detaljer-siden for tilkobling](./media/share-app-resources/shared-connections.png)

## <a name="on-premises-data-gateways"></a>Lokale datagatewayer
Hvis du oppretter og deler en app som inneholder data fra en lokal kilde, deles den [lokale datagatewayen](gateway-management.md) automatisk og visse typer tilkoblinger til gatewayen. For alle tilkoblinger som ikke er delt automatisk, kan du dele den manuelt (som vist i forrige inndeling), eller la appen be brukerne om å opprette sine egne tilkoblinger. Slik viser du tilkoblingene eller tilkoblinger som har blitt konfigurert med en gateway:

1. Åpne [powerapps.com](https://web.powerapps.com), klikk eller trykk på **Administrer** i venstre navigasjonsfelt, og klikk eller trykk på **gatewayer**.
2. Klikk eller trykk på en gateway, og klikk eller trykk deretter på **Connections**-fanen.

> [!NOTE]
> Hvis du deler en eller flere tilkoblinger manuelt, må du kanskje dele dem på nytt under disse forholdene:

* Du legger til en lokal datagateway til en app som du allerede har delt.
* Du endrer settet med personer eller grupper som du har delt en app med som har en lokal datagateway.

## <a name="custom-connectors"></a>Egendefinerte tilkoblinger
Når du deler en app som bruker en egendefinert tilkobling, deles den automatisk, men brukerne må opprette egne tilkoblinger til den.

Du kan vise eller oppdatere tillatelser for en egendefinert tilkobling på [powerapps.com](https://web.powerapps.com). Klikk eller trykk på **Behandle** i det venstre navigasjonsfeltet, klikk eller trykk på **Tilkoblinger** og dklikk eller trykk deretter på **Ny tilkobling** (i øvre høyre hjørne). Klikk eller trykk på **Egendefinert**, deretter klikker eller trykker du på en egendefinert kobling for å vise detaljer om den.

## <a name="excel-workbooks"></a>Excel-arbeidsbøker
Hvis en delt app bruker data som ikke alle brukere har tilgang til (for eksempel en Excel-arbeidsbok i en konto for lagring i skyen), må du [dele dataene](share-app-data.md).

## <a name="flows"></a>Flyter
Hvis du deler en app som inneholder en flyt, vil brukere som kjører appen bli bedt om å bekrefte eller oppdatere alle tilkoblinger som flyten er avhengig av. I tillegg kan bare personen som opprettet flyten tilpasse parameterne. For eksempel kan du opprette en flyt som sender e-post til en adresse du angir, men andre brukere kan ikke endre denne adressen.
