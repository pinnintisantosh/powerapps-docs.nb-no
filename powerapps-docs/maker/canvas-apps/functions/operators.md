---
title: Operatorer | Microsoft Docs
description: Referanseinformasjon for operatorene i PowerApps, inkludert syntaks og eksempler
documentationcenter: na
author: gregli-msft
manager: kfile
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: reference
ms.component: canvas
ms.date: 07/24/2017
ms.author: gregli
ms.openlocfilehash: 9dce0ac36cd16faaa9c8b9a0b34d15eff086ab2e
ms.sourcegitcommit: 68fc13fdc2c991c499ad6fe9ae1e0f8dab597139
ms.translationtype: HT
ms.contentlocale: nb-NO
ms.lasthandoff: 06/04/2018
ms.locfileid: "31838037"
---
# <a name="operators-and-data-types-in-powerapps"></a>Operatorer og datatyper i PowerApps
Noen av disse operatorene er avhengig av språket til forfatteren.  Se [Globale apper](../global-apps.md) for mer informasjon.

| Symbol | Type | Syntaks | Beskrivelse |
| --- | --- | --- | --- |
| **.** |Valg av egenskap |**Slider1.Value<br>Color.Red<br>Acceleration.X** |Henter en egenskap fra en [tabell](../working-with-tables.md), kontroll, et [signal](signals.md) eller en opplisting.  Hvis du ønsker bakoverkompatibilitet, kan også **!** brukes. |
| **.**<br>[eller **,** [avhengig av språk](../global-apps.md)] |Desimalskilletegn |**1.23**<br>[eller **1,23** avhengig av språk] |Skilletegn mellom hele tall og delvise tall.  Tegnet er avhengig av språket. |
| **( )** |Parenteser |**Filter(T, A &lt; 10)**<br><br>**(1 + 2) * 3** |Fremtvinger prioritert rekkefølge, og grupperer deluttrykk i et større uttrykk |
| **+** |Aritmetiske operatorer |**1 + 2** |Addisjon |
| **-** |&nbsp; |**2 - 1** |Subtraksjon og tegn |
| **\*** |&nbsp; |**2 * 3** |Multiplikasjon |
| **/** |&nbsp; |**2 / 3** |Divisjon (se også **[Mod](function-mod.md)**-funksjonen) |
| **^** |&nbsp; |**2 ^ 3** |Eksponentiering, tilsvarer **[Power](function-numericals.md)**-funksjonen |
| **%** |&nbsp; |**20 %** |Prosent (tilsvarer &quot;* 1/100&quot;) |
| **=** |Sammenligningsoperatorer |**Pris = 100** |Er lik |
| **&gt;** |&nbsp; |**Pris &gt; 100** |Mer enn |
| **&gt;=** |&nbsp; |**Pris &gt;= 100** |Større enn eller lik |
| **&lt;** |&nbsp; |**Pris &lt; 100** |Mindre enn |
| **&lt;=** |&nbsp; |**Pris &lt;= 100** |Mindre enn eller lik |
| **&lt;&gt;** |&nbsp; |**Pris &lt;&gt; 100** |Ikke lik |
| **&amp;** |Operator for sammenslåing av streng |**&quot;hello&quot; &amp; &quot; &quot; &amp; &quot;world&quot;** |Gjør at flere strenger vises kontinuerlig |
| **&amp;&amp;** eller **And** |Logiske operatorer |**Price &lt; 100 &amp;&amp; Slider1.Value = 20**<br>eller **Price &lt; 100 And Slider1.Value = 20** |Logisk forbindelse, tilsvarer **[And](function-logicals.md)**-funksjonen |
| **&#124;&#124;** eller **Or** |&nbsp; |**Price &lt; 100 &#124;&#124; Slider1.Value = 20** eller **Price &lt; 100 Or Slider1.Value = 20** |Logisk disjunksjon, tilsvarer **[Or](function-logicals.md)**-funksjonen |
| **!** eller **Not** |&nbsp; |**!(Price &lt; 100)** eller **Not (Price &lt; 100)** |Logisk negasjon, tilsvarer **[Not](function-logicals.md)**-funksjonen |
| **exactin** |[Medlemskapsoperatorer](#in-and-exactin-operators) |**Gallery1.Selected exactin SavedItems** |Tilhører en [samling](../working-with-data-sources.md#collections) eller en tabell |
| **exactin** |&nbsp; |**&quot;Windows&quot; exactin «For å vise vinduer i Windows-operativsystemet ...»** |Delstreng-test (skiller mellom små og store bokstaver) |
| **in** |&nbsp; |**Gallery1.Selected in SavedItems** |Tilhører en samling eller en tabell |
| **in** |&nbsp; |**&quot;Den&quot; in &quot;Tastaturet og skjermen...&quot;** |Delstreng-test (skiller ikke mellom små og store bokstaver) |
| **@** |[Tvetydighetsoperator](#disambiguation-operator) |**MyTable[@fieldname]** |Felttvetydighet |
| **@** |&nbsp; |**[@MyVariable]** |Global tvetydighet |
| **,**<br>[eller **;** [avhengig av språket](../global-apps.md)] |Listeskilletegn |**If( X < 10, "Low", "Good" )**<br>**{ X: 12, Y: 32 }**<br>**[ 1, 2, 3 ]**<br>[or **If( X < 10; "Low"; "Good" )<br>{ FirstName: "Jane"; LastName: "Doe" }<br>[ 1; 2; 3 ]** ] |Adskiller: <ul><li>argumenter i funksjonsoppkallinger</li><li>felter i en [post](../working-with-tables.md#elements-of-a-table)</li><li>poster i en [verditabell](../working-with-tables.md#inline-syntax)</li></ul>.  Tegnene er avhengig av språket. |
| **;**<br>[eller **;;** [avhengig av språket](../global-apps.md)] |Formelkjeding |**Collect(T, A); Navigate(S1, &quot;&quot;)**<br>[eller **Collect(T; A);; Navigate(S1; &quot;&quot;)**] |Separerer starten av funksjoner i egenskaper for virkemåte.  Kjedingoperatoren er avhengig av språket. |
| **Overordnet** |[Overordnet operator](#parent-operator) |**Parent.Fill** |Tilgang til egenskapene til en kontrollbeholder |
| **ThisItem** |[ThisItem-operatoren](#thisitem-operator) |**ThisItem.FirstName** |Tilgang til felt i en Galleri- eller Skjema-kontroll |

## <a name="in-and-exactin-operators"></a>in- og exactin-operatorer
Du kan bruke **[in](operators.md#in-and-exactin-operators)**- og **[exactin](operators.md#in-and-exactin-operators)**-operatorene for å finne en streng i en [datakilde](../working-with-data-sources.md), som en samling eller en importert tabell. **[in](operators.md#in-and-exactin-operators)**-operatoren identifiserer treff uavhengig av bokstavtype, og **[exactin](operators.md#in-and-exactin-operators)**-operatoren identifiserer treff bare hvis de samme store bokstavene er i bruk. Her kan du se et eksempel:

1. Opprett eller importer en samling kalt **Beholdning** og vis den i et galleri, som den første prosedyren i [Vis bilder og tekst i et galleri](../show-images-text-gallery-sort-filter.md) beskriver.
2. Angi **[Elementer](../controls/properties-core.md)**-egenskapen for galleriet til denne formelen:
   <br>**Filter(Inventory, "E" in ProductName)**
   
    Galleriet viser alle produktene bortsett fra Callisto. Det er fordi navnet er det eneste produktet som ikke inneholder bokstaven du oppgav.
3. Endre **[Elementer](../controls/properties-core.md)**-egenskapen for galleriet til denne formelen:
   <br>**Filter(Inventory, "E" exactin ProductName)**
   
    Galleriet viser bare Europa fordi navnet er det eneste som inneholder bokstaven du oppgav i det angitte tilfellet.

## <a name="thisitem-operator"></a>ThisItem-operator
Du kan vise data i kontrollene **[Galleri](../controls/control-gallery.md)**, **[Redigeringsskjema](../controls/control-form-detail.md)** eller **[Visningsskjema](../controls/control-form-detail.md)** ved å binde dem til en tabell eller samling.  Disse kontrollene er en beholder for andre kort og kontroller.  Hvert kort eller hver kontroll i beholderen får tilgang til de bundne dataene gjennom **[ThisItem](operators.md#thisitem-operator)**-operatoren.   

Du kan bruke **[ThisItem](operators.md#thisitem-operator)**-operatoren til å angi [kolonnen](../working-with-tables.md#columns) med data som hvert kort eller kontroll innehar i den ytre kontrollen. Operatoren i produktgalleriet for[Vis bilder og tekst i et galleri](../show-images-text-gallery-sort-filter.md) spesifiserte for eksempel at Bilde-kontrollen viste produktdesign, den øvre etiketten viste produktnavnet, og den bedre etiketten viste antall enheter på lager.

Når det gjelder nestede gallerier, så henviser **[ThisItem](operators.md#thisitem-operator)** til elementene til det innerste galleriet. Hvis vi antar at radfeltene i de indre og ytre galleriene ikke er i konflikt, kan du også bruke de ukvalifiserte feltnavnene (kolonne) direkte. Denne tilnærmingen gjør at regler i et indre galleri henviser til elementene i et ytre galleri.

## <a name="parent-operator"></a>Overordnet operator
Noen kontroller er vert for andre kontroller. Kontrollene **[Skjerm](../controls/control-screen.md)**, **[Galleri](../controls/control-gallery.md)**, **[Kort](../controls/control-card.md)**, **[Redigeringsskjema](../controls/control-form-detail.md)** og **[Visningsskjema](../controls/control-form-detail.md)** er alle beholdere for kontroller. Vertskontrollen blir da overordnet i forhold til kontrollene inni.

Alle kontroller i PowerApps kan henvises til ved navn fra hvor som helst i appen. Det kan hende at **Screen1** er navnet på en skjerm i appen din. Hvis du ønsker å hente bakgrunnsfargen til skjermen, kan du bruke **Screen1.Fill**.

Kontrollene på denne skjermen har et annet alternativ. De kan også bruke en relativ referanse: **Parent.Fill**. Den **[overordnede](operators.md#parent-operator)** operatoren henviser til kontrollen som er vert for denne kontrollen, noe som gjør at alle egenskapene blir tilgjengelige. Det er nyttig å bruke **[overordnet](operators.md#parent-operator)** fordi det ikke avhenger av navnet på kontrollen. Du kan kopiere og lime inn en beholderkontroll uten å måtte justere noen referanser i beholderen. Denne operatoren gjør også at forholdet mellom de underordnede og overordnede kontrollene er tydeligere når du leser formler.

## <a name="disambiguation-operator"></a>Tvetydighetsoperator
Noen funksjoner oppretter [postområder](../working-with-tables.md#record-scope) for å få tilgang til feltene i tabellen under behandling av hver post, som **Filter**, **AddColumns** og **Sum**.  Feltnavnene som ble lagt til ved bruk av postområdet overstyrer de samme navnene fra appen ellers.  Når dette skjer, får du fremdeles tilgang til verdiene som er utenfor postområdet ved bruk av **@** tvetydighetsoperatoren:

* Hvis du vil ha tilgang til verdiene fra nestede postområder, bruker du **@** operatoren med samme navn som tabellen der operatoren arbeider ved bruk av mønsteret ***Table *[@* FieldName*]**.  
* Hvis du vil ha tilgang til globale verdier, som datakilder, samlinger og kontekstvariabler, bruker du mønsteret **[@*ObjectName*]** (uten en tabellangivelse).

Hvis du vil ha mer informasjon og eksempler, kan du se diskusjonen om [postområder](../working-with-tables.md#record-scope).
