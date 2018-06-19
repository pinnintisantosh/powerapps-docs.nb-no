---
title: Reset-funksjonen | Microsoft Docs
description: Referanseinformasjon for Reset-funksjonen i PowerApps, inkludert syntaks og eksempel
documentationcenter: na
author: gregli-msft
manager: kfile
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: reference
ms.component: canvas
ms.date: 07/06/2017
ms.author: gregli
ms.openlocfilehash: bc87fd823b37869298b453aba439bda6aabbb112
ms.sourcegitcommit: 68fc13fdc2c991c499ad6fe9ae1e0f8dab597139
ms.translationtype: HT
ms.contentlocale: nb-NO
ms.lasthandoff: 06/04/2018
ms.locfileid: "31825836"
---
# <a name="reset-function-in-powerapps"></a>Reset-funksjonen i PowerApps
Tilbakestiller en kontroll til standardverdien, forkaster brukerendringer.  

## <a name="description"></a>Beskrivelse
**Reset**-funksjonen tilbakestiller en kontroll til **Standard**-egenskapsverdien.  Alle brukerendringer forkastes.

Du kan ikke tilbakestille kontroller som er innenfor en [**Galleri-**](../controls/control-gallery.md) eller [**Redigeringsskjema**](../controls/control-form-detail.md)-kontroll utenfor disse kontrollene.  Du kan tilbakestille kontroller fra formler i kontrollene innenfor det samme galleriet eller skjemaet.  Du kan også tilbakestille alle kontrollene i et skjema med [**ResetForm**](function-form.md)-funksjonen. 

Å bruke **Reset**-funksjonen er et alternativ til å veksle mellom **Tilbakestill**-egenskapen for inndatakontroller, og dette foretrekkes.  **Tilbakestill**-egenskapen kan være et bedre valg hvis mange kontroller må tilbakestilles sammen fra flere formler.  Å veksle mellom **Tilbakestill**-egenskapen kan gjøres fra en [**Knapp**](../controls/control-button.md)-kontroll med formelen **Reset = Button.Pressed** eller fra en variabel med **Reset = MyVar** og veksling mellom **MyVar** og formelen **Button.OnSelect = Set( MyVar, true ); Set( MyVar, false )**.    

Inndatakontroller er også tilbakestilt når **Standard**-egenskapen endres.

**Reset** har ingen returverdi, og du kan bare bruke den i [formler for virkemåter](../working-with-formulas-in-depth.md).

## <a name="syntax"></a>Syntaks
**Reset**( *Control* )

* *Control* – obligatorisk. Kontrollen som skal tilbakestilles.

## <a name="example"></a>Eksempel
1. Sett inn en **Tekstinndata**-kontroll på en skjerm.  Navnet blir som standard **TextInput1**, og **Standard**-egenskapen settes til **"Text input"**.
2. Skriv inn en ny verdi i tekstboksen.  
3. Sett inn en **Knapp**-kontroll på skjermen.
4. Sett knappens **OnSelect**-egenskap til **Reset( TextInput1 )**.
5. Velg knappen.  Dette kan gjøres selv når man redigerer, ved å velge mot slutten av kontrollen.
6. Innholdet i tekstboksen vil returnere verdien for **Standard**-egenskapen.
