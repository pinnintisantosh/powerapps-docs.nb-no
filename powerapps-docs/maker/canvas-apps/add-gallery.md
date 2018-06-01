---
title: Vis en liste over elementer | Microsoft Docs
description: Bruk et galleri for å vise en liste over elementer i appen, og filtrer listen ved å angi et vilkår.
services: ''
suite: powerapps
documentationcenter: na
author: karthik-1
manager: anneta
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/28/2017
ms.author: sharik
ms.openlocfilehash: 04499f276e179fe6b57103a3d28a68ba6fe6b7bb
ms.sourcegitcommit: 59785e9e82da8f5bd459dcb5da3d5c18064b0899
ms.translationtype: HT
ms.contentlocale: nb-NO
ms.lasthandoff: 03/22/2018
ms.locfileid: "30996037"
---
# <a name="show-a-list-of-items-in-powerapps"></a>Vis en liste over elementer i PowerApps
Vis en liste over elementer fra en datakilde ved å legge til en **[galleri](controls/control-gallery.md)**-kontroll til appen. Dette emnet bruker Excel som datakilde. Filtrer listen ved å konfigurere **galleri**-kontrollen, for å vise bare elementene som samsvarer med filterkriteriet i en **[tekstinndata](controls/control-text-input.md)**-kontroll.

## <a name="prerequisites"></a>Forutsetninger
* Finn ut hvordan du [legger til og konfigurerer en kontroll](add-configure-controls.md) i PowerApps.

* Konfigurere eksempeldataene:
    1. Last ned [denne Excel-filen](https://az787822.vo.msecnd.net/documentation/get-started-from-data/FlooringEstimates.xlsx), som inneholder eksempeldata for denne opplæringen.

    2. Last opp Excel-filen til en [skylagringstjeneste](connections/cloud-storage-blob-connections.md), for eksempel OneDrive for Business.

## <a name="add-a-gallery-control"></a>Legg til en gallerikontroll
1. Åpne PowerApps og klikk eller trykk deretter på **Ny** nær venstre kant.

2. Klikk eller trykk på **Telefonoppsett** på **Tom app**-flisen.

3. I dialogboksen **Velkommen til PowerApps Studio** klikker eller trykker du på **Hopp over**.

4. [Legg til en tilkobling](add-data-connection.md) til **FlooringEstimates**-tabellen i Excel-filen.

5. (valgfritt) Legg til en **galleri**-kontroll til standard-skjermbildet ved å klikke eller trykke på **Sett inn**-fanen, klikke eller trykke på **Galleri**, og deretter klikke eller trykke på en **galleri**-kontroll som er uten innhold (tom), eller som inneholder et standardsett med kontroller.

    Disse alternativene inkluderer **galleri**-kontrollene som ruller vannrett eller loddrett. Du kan også legge til en **galleri**-kontroll som automatisk baserer størrelsen på mengden med innhold i hvert element.

    ![Legg til galleri](./media/add-gallery/gallery-dropdown.png)

6. Klikk eller trykk på **Nytt skjermbilde** på **Hjem**-fanen.

    Du kan legge til et skjermbilde som er tomt, et som ruller, som inneholder en **galleri**-kontroll, eller som inneholder et skjema.

7. Klikk eller trykk på **Listeskjerm** for å legge til en skjerm som inneholder en **galleri**-kontroll og andre kontroller, for eksempel et søkefelt.

    > [!NOTE]
> Om du legger til en **galleri**-kontroll til en ny eller eksisterende skjerm, kan du klikke eller trykke nær bunnen av **galleri**-kontrollen for å merke den, klikke eller trykke på **Estimater for gulvlegging**i den høyre ruten, og klikke eller trykke på et annet oppsett i **Data**-ruten. La standardoppsettet være aktivert for denne opplæringen.

    ![Velg gallerioppsett](./media/add-gallery/select-layout.png)

8. Klikk eller trykk på **galleri**-kontrollen i skjermbildet som du nettopp la til.

9. På **Egenskaper**-kategorien i den høyre ruten klikker eller trykker du på **CustomGallerySample**.

10. I **Data**-ruten klikker eller trykker du på **CustomGallerySample**, og deretter på **FlooringEstimates**.

    ![Velg datakilde](./media/add-gallery/choose-data.png)

    **Galleri**-kontrollen viser eksempeldataene.

    ![Vis data](./media/add-gallery/show-data-default.png)

    Du vil konfigurere sortering og søk senere i dette emnet.

## <a name="add-a-control-to-the-gallery-control"></a>Legg til en kontroll til gallerikontrollen
Før du gjør eventuelle tilpasninger, bestemmer du deg for et oppsett for **galleri**-kontrollen. Det første settet med kontroller i en **galleri**-kontroll er malen, som bestemmer hvordan alle dataene i **galleri**-kontrollen vises.

1. Velg malen ved å klikke eller trykke nær bunnen av **galleri**-kontrollen og deretter klikke eller trykke på blyantikonet øverst til venstre.

    ![Rediger galleri-mal](./media/add-gallery/edit-item.png)

2. Mens malen fortsatt er merket, kan du legge til en **[etikett](controls/control-text-box.md)**-kontroll, og deretter flytte og endre størrelsen på den slik at den ikke overlapper med andre kontroller i malen.

    ![Legg til en etikett](./media/add-gallery/add-text-box.png)
3. Åpne **Data**-ruten ved å velge malen og deretter klikke eller trykke på **Estimater for gulvlegging** i ruten til høyre.

4. Velg etiketten som du har lagt til tidligere i denne prosedyren, og åpne deretter listen som er uthevet i **Data**-ruten.

    ![Åpne rullegardinliste](./media/add-gallery/open-dropdown.png)

5. Klikk eller trykk på **Pris** i denne listen.

    ![Endre bindingene for etikett](./media/add-gallery/change-binding.png)

    **Galleri**-kontrollen viser de nye verdiene.

    ![Det endelige galleriet](./media/add-gallery/final-gallery.png)

## <a name="filter-the-gallery-control"></a>Filtrer gallerikontrollen
**[Elementer](controls/properties-core.md)** -egenskapen for en **galleri**-kontroll bestemmer hvilke elementer den viser. I denne prosedyren må du konfigurere denne egenskapen slik at **Galleri**-kontrollen viser kun elementer som inneholder navnet på produktet teksten i **TextSearchBox1**.

![Boks for tekstsøk](./media/add-gallery/text-search-box.png)

1. Velg **galleri**-kontrollen ved å klikke eller trykke nær bunnen av denne kontrollen.

2. Angi **[Elementer](controls/properties-core.md)**-egenskapen for **Galleri**-kontrollen på **Avansert**-fanen til denne formelen:

    **If(IsBlank(TextSearchBox1.Text), FlooringEstimates, Filter(FlooringEstimates, TextSearchBox1.Text in Text(Name)))**

    Hvis du vil ha mer informasjon om funksjonene i denne formelen, kan du se [formelreferansen](formula-reference.md).

3. Skriv inn hele eller deler av et produktnavn i søkeboksen.

    **Galleri**-kontrollen viser bare elementer som oppfyller filterkriteriet.

## <a name="sort-the-gallery-control"></a>Filtrer galleri-kontrollen
**[Elementer](controls/properties-core.md)** -egenskapen for en **galleri**-kontroll bestemmer rekkefølgen elementene vises i. I denne prosedyren må du konfigurere denne egenskapen slik at **galleri**-kontrollen viser rekkefølgen av elementer, som angitt av **ImageSortUpDown1**.

![Bilde for sortering](./media/add-gallery/image-sorting.png)

1. Angi **[Elementer](controls/properties-core.md)**-egenskapen for **Galleri**-kontrollen til denne formelen:

    **Sort(If(IsBlank(TextSearchBox1.Text), FlooringEstimates, Filter(FlooringEstimates, TextSearchBox1.Text in Text(Name))), Name, If(SortDescending1, SortOrder.Descending, SortOrder.Ascending))**

2. Velg Sorter-ikonet for å endre sorteringsrekkefølgen for **galleri**-kontrollen basert på navnene på produktene.

Hvis du vil sortere *og* filtrere **galleri**-kontrollen:

* Erstatt begge forekomstene av *DataSource* i denne formelen med navnet på datakilden.

* Erstatt begge forekomstene av *ColumnName* med navnet på kolonnen du vil sortere og filtrere etter.

**Sort(If(IsBlank(TextSearchBox1.Text),** *DataSource*, **Filter(** *DataSource*, **TextSearchBox1.Text in Text(** *ColumnName* **))),** *ColumnName*, **If(SortDescending1, SortOrder.Descending, SortOrder.Ascending))**

## <a name="highlight-the-selected-item"></a>Merk det valgte elementet
Angi **Galleri**-kontrollens **TemplateFill**-egenskap til en formel som ligner på dette eksemplet:

**If(ThisItem.IsSelected, LightCyan, White)**

## <a name="change-the-default-selection"></a>Endre standardutvalget
Angi **Galleri**-kontrollens **Standard**-egenskap til posten du vil merke som standard. Angi for eksempel at det femte elementet i datakilden **FlooringEstimates**:

**Last(FirstN(FlooringEstimates, 5))**

I dette eksemplet angir du det første elementet i **Hardwood**-kategorien for **FlooringEstimates**-datakilden:

**First(Filter(FlooringEstimates, Category = "Hardwood"))**

## <a name="next-steps"></a>Neste trinn
Finn ut hvordan du arbeider med [skjemaer](working-with-forms.md) og [formler](working-with-formulas.md).