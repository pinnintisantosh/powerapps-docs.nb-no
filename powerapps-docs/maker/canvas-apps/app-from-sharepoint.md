---
title: Quickstart for å generere en app i PowerApps fra SharePoint | Microsoft Docs
description: Generer en app automatisk i PowerApps for å behandle data i en SharePoint-liste
services: powerapps
documentationcenter: na
author: AFTOwen
manager: kfile
ms.service: powerapps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/12/2018
ms.author: anneta
ms.openlocfilehash: 86e255f6c3fbb77b60820108c4a21dd8c0cba532
ms.sourcegitcommit: 59785e9e82da8f5bd459dcb5da3d5c18064b0899
ms.translationtype: HT
ms.contentlocale: nb-NO
ms.lasthandoff: 03/22/2018
ms.locfileid: "30996217"
---
# <a name="quickstart-for-generating-an-app-in-powerapps-from-sharepoint"></a>Hurtigstart for å generere en app i PowerApps fra SharePoint

I denne hurtigveiledningen skal du bruke PowerApps til å automatisk generere din første app basert på en liste du oppretter i SharePoint. I denne appen kan du bla gjennom alle elementene i listen, vise detaljer for et enkelt element og opprette, oppdatere eller slette et element.

Du kan lære konsepter og teknikker fra denne hurtigveiledningen hvis du har en liste i SharePoint. Hvis du vil følge denne hurtigveiledningen nøyaktig, kan du opprette en liste, kalt **SimpleApp**, som inneholder en kolonne med navnet **Tittel** i et SharePoint Online-område. I listen kan du opprette oppføringer for **Vanilla**, **Chocolate**, og **Strawberry**.

Du kan opprette en liste som er mye mer komplisert med mange kolonner av ulike typer, for eksempel tekst, datoer, tall og valuta. Prinsippene for generering av appen endres ikke. Du kan også generere en app fra en liste i et lokalt SharePoint-område hvis du [kobler deg til området](connect-to-sharepoint.md) gjennom en datagateway.

Hvis du ikke har en lisens for PowerApps, kan du [registrere deg gratis](../signup-for-powerapps.md).

## <a name="generate-an-app"></a>Generere en app
1. Logg deg på [PowerApps](https://web.powerapps.com).

    ![Hjemmesiden for PowerApps](./media/app-from-sharepoint/sign-in.png)

1. Under **Lag apper som disse**, holder du pekeren over **Begynn fra data**, og deretter velger du **Lag denne appen**.

    ![Alternativ for å opprette en app](./media/app-from-sharepoint/make-this-app.png)

1. Velg Telefonoppsett på **SharePoint**-flisen.

    ![Alternativ for å opprette en app](./media/app-from-sharepoint/sharepoint-tile.png)

1. Med alternativet **Koble til direkte** valgt velger du **Opprett**.

    ![Opprette tilkobling](./media/app-from-sharepoint/create-connection.png)

1. Under **Koble til et SharePoint-område** skriver du eller limer inn nettadressen for SharePoint Online-området, og deretter velger du **Gå**.

    Inkluder bare nettadressen (ikke navnet på listen), som i dette eksemplet:<br>`https://microsoft.sharepoint.com/teams/Contoso`

1. Under **Velg en liste** velger du **SimpleApp**, og deretter velger du **Koble**.

Etter noen minutter åpnes appen til Bla gjennom-skjermen, som viser elementene du opprettet i listen. Hvis listen har data i flere kolonner enn bare **Tittel**, viser appen disse dataene. Nær toppen av skjermen viser en tittellinje ikoner for å oppdatere listen, sortere listen og opprette et element i listen. Under tittellinjen inneholder en søkeboks muligheten til å filtrere listen basert på teksten du skriver eller limer inn. 

![Bla gjennom-skjermen](./media/app-from-sharepoint/browse-screen.png)

Du vil sannsynligvis gjøre flere endringer før du bruker denne appen eller deler den med andre. Som en anbefalt fremgangsmåte lagrer du arbeidet ditt så langt ved å trykke på Ctrl-S før du fortsetter. Gi appen et navn, og velg deretter **Lagre**.

## <a name="next-steps"></a>Neste trinn
I denne hurtigveiledningen opprettet du en app for å behandle data i en SharePoint-liste. Som et neste trinn kan du generere en app fra en mer komplisert liste og deretter tilpasse appen (fra skjermbildet Bla gjennom og videre) for å passe bedre til dine behov.

> [!div class="nextstepaction"]
> [Tilpasse et standard Bla gjennom-skjermbilde](customize-layout-sharepoint.md)