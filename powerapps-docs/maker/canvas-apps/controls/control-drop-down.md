---
title: 'Rullegardinkontroll: referanse | Microsoft Docs'
description: Informasjon om Rullegardin-kontrollen, inkludert egenskaper og eksempler
services: ''
suite: powerapps
documentationcenter: na
author: fikaradz
manager: anneta
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/25/2016
ms.author: fikaradz
ms.openlocfilehash: 828292cc888d26f2060260826296960f1bd4f98f
ms.sourcegitcommit: 59785e9e82da8f5bd459dcb5da3d5c18064b0899
ms.translationtype: HT
ms.contentlocale: nb-NO
ms.lasthandoff: 03/22/2018
ms.locfileid: "30996177"
---
# <a name="drop-down-control-in-powerapps"></a>Rullegardin-kontrollen i PowerApps
En liste som viser bare det første elementet, med mindre brukeren åpner det.

## <a name="description"></a>Beskrivelse
En **rullegardin**-kontroll sparer skjermplass, spesielt når listen inneholder mange valg. Kontrollen tar opp bare én linje med mindre brukeren velger vinkeltegnet for å vise flere valg.

## <a name="key-properties"></a>Nøkkelegenskaper
**[Standard](properties-core.md)** – startverdien for en kontroll før den er endret av brukeren.

**[Elementer](properties-core.md)** – kilden til dataene som vises i en kontroll, for eksempel et galleri, en liste eller et diagram.

[!INCLUDE [long-items](../../../includes/long-items.md)]

**Valgt** – det valgte elementet.

## <a name="additional-properties"></a>Tilleggsegenskaper
**[BorderColor](properties-color-border.md)** – fargen på kontrollens kantlinje.

**[BorderStyle](properties-color-border.md)** – om kontrollens kantlinje er satt til **Heltrukket**, **Stiplet**, **Prikket** eller **Ingen**.

**[BorderThickness](properties-color-border.md)** – tykkelsen til kontrollens kantlinje.

**[FocusedBorderThickness](properties-color-border.md)**  – tykkelsen på kontrollens kantlinje når den har tastaturfokus.

**ChevronBackground** – fargen bak den nedovervendte pilen i en rullegardinliste.

**ChevronFill** – fargen på den nedovervendte pilen i en rullegardinliste.

**[Farge](properties-color-border.md)** – fargen på teksten i kontrollen.

**[DisplayMode](properties-core.md)** – om kontrollen tillater brukerinndata (**Rediger**), bare viser data (**Vis**) eller er deaktivert (**Deaktivert**).

**[DisabledBorderColor](properties-color-border.md)** – fargen på kontrollens kantlinje hvis kontrollens **[DisplayMode](properties-core.md)**-egenskap er angitt som **Deaktivert**.

**[DisabledColor](properties-color-border.md)** – fargen på kontrollens tekst hvis kontrollens **[DisplayMode](properties-core.md)**-egenskap er angitt som **Deaktivert**.

**[DisabledFill](properties-color-border.md)** – bakgrunnsfargen på en kontroll hvis **[DisplayMode](properties-core.md)**-egenskapen er angitt som **Deaktivert**.

**[Fyll](properties-color-border.md)** – bakgrunnsfargen på kontrollen.

**[Skrift](properties-text.md)** – navnet på skriftserien som teksten vises i.

**[Skrifttykkelse](properties-text.md)** – tykkelsen på teksten i en kontroll: **Fet**, **Halvfet**, **Normal** eller **Smalere**.

**[Høyde](properties-size-location.md)** – avstanden mellom kontrollens øvre og nedre kant.

**[HoverBorderColor](properties-color-border.md)** – fargen på kontrollens kantlinje når brukeren holder musepekeren på denne kontrollen.

**[HoverColor](properties-color-border.md)** – Fargen på teksten i en kontroll når brukeren holder musepekeren over den.

**[HoverFill](properties-color-border.md)**  – bakgrunnsfargen for en kontroll når brukeren holder musepekeren over den.

**[Kursiv](properties-text.md)** – om teksten i en kontroll er i kursiv.

**[OnChange](properties-core.md)** – hvordan appen reagerer når brukeren endrer verdien på en kontroll (ved å for eksempel justere en glidebryter).

**[OnSelect](properties-core.md)** – hvordan appen responderer når brukeren klikker eller trykker på en kontroll.

**[PaddingBottom](properties-size-location.md)** – avstanden mellom teksten i en kontroll og den nederste kanten av kontrollen.

**[PaddingLeft](properties-size-location.md)** – avstanden mellom teksten i en kontroll og den venstre kanten av kontrollen.

**[PaddingRight](properties-size-location.md)** – avstanden mellom teksten i en kontroll og den høyre kanten av kontrollen.

**[PaddingTop](properties-size-location.md)** – avstanden mellom teksten i en kontroll og den øverste kanten av kontrollen.

**[PressedBorderColor](properties-color-border.md)**  – fargen på kontrollens kantlinje når brukeren trykker eller klikker på kontrollen.

**[PressedColor](properties-color-border.md)** – fargen på teksten i en kontroll når brukeren trykker eller klikker på kontrollen.

**[PressedFill](properties-color-border.md)** – bakgrunnsfargen på teksten i en kontroll når brukeren trykker eller klikker på kontrollen.

**[Tilbakestill](properties-core.md)** – om en kontroll tilbakestilles til standardverdien.

**[SelectionColor](properties-color-border.md)** – tekstfargen for et merket element, elementer i en liste eller fargen på markeringsverktøyet i en pennekontroll.

**[SelectionFill](properties-color-border.md)** – bakgrunnsfargen for et merket element eller merkede elementer i en liste eller et merket område for en pennekontroll.

**[Størrelse](properties-text.md)** – skriftstørrelsen på teksten som vises på en kontroll.

**[Gjennomstrekning](properties-text.md)** – om det vises en linje gjennom teksten som vises på en kontroll.

**[TabIndex](properties-accessibility.md)** – tilpasser fanerekkefølgen for kontroller ved kjøretid når de er angitt som en annen verdi enn null.

**[Verktøytips](properties-core.md)** – forklarende tekst som vises når brukeren holder pekeren over en kontroll.

**[Understreking](properties-text.md)** – om det vises en linje under teksten som vises på en kontroll.

**[Synlig](properties-core.md)** – om kontrollen vises eller skjules.

**[Bredde](properties-size-location.md)** – avstanden mellom kontrollens venstre og høyre kant.

**[X](properties-size-location.md)** – avstanden mellom kontrollens venstre kant og den venstre kanten til kontrollens overordnede beholder (eller skjermen, hvis det ikke finnes noen overordnet beholder).

**[Y](properties-size-location.md)** – avstanden mellom kontrollens øvre kant og den øvre kanten til kontrollens overordnede beholder (eller skjermen, hvis det ikke finnes noen overordnet beholder).

## <a name="example"></a>Eksempel
1. Legg til en **[Knapp](control-button.md)**-kontroll og angi knappens **[tekst](properties-core.md)**-egenskap til å vise **Samle inn**.
   
    Vet du ikke hvordan du [legger til, gir navn til og konfigurerer en kontroll](../add-configure-controls.md)?
2. Angi **[OnSelect](properties-core.md)**-egenskapen for **[knappen](control-button.md)** til denne formelen:
   <br>**ClearCollect(CityPopulations, {City:"London", Country:"United Kingdom", Population:8615000}, {City:"Berlin", Country:"Germany", Population:3562000}, {City:"Madrid", Country:"Spain", Population:3165000}, {City:"Rome", Country:"Italy", Population:2874000}, {City:"Paris", Country:"France", Population:2273000}, {City:"Hamburg", Country:"Germany", Population:1760000}, {City:"Barcelona", Country:"Spain", Population:1602000}, {City:"Munich", Country:"Germany", Population:1494000}, {City:"Milan", Country:"Italy", Population:1344000})**
   
    Vil du ha mer informasjon om **[ClearCollect](../functions/function-clear-collect-clearcollect.md)**-funksjonen eller [andre funksjoner](../formula-reference.md)?
3. Trykk på F5, klikk eller trykk på **[Knapp](control-button.md)**-kontrollen, og trykk deretter på ESC.
4. Legg til en **Rullegardin**-kontroll, gi den navnet **Land**, og angi **[Elementer](properties-core.md)**-egenskapen til denne formelen:
   <br>**Distinct(CityPopulations, Country)**
5. Legg til en **tekstgalleri**-kontroll i en loddrett/stående retning, og angi **[Elementer](properties-core.md)**-egenskapen til denne formelen:
   <br>**Filter(CityPopulations, Countries.Selected.Value in Country)**
6. Angi **[Tekst](properties-core.md)**-egenskapen for den øverste **[Etikett](control-text-box.md)**-kontrollen i det første elementet i **Tekstgalleri**-kontrollen til **ThisItem.City**, og slett den nederste **[Etikett](control-text-box.md)**-kontrollen.
7. Angi den **[TemplateSize](control-gallery.md)**-egenskapen for **Tekstgalleri**-kontrollen til **80**.
8. Trykk på F5, klikk eller trykk på vinkeltegnet i **Land**-listen, og velg deretter et alternativ i listen.
   
    **Tekstgalleri**-kontrollen viser bare disse byene i landet som du valgte.
