---
title: Table-funksjonen | Microsoft Docs
description: Referanseinformasjon for Table-funksjonen i PowerApps, inkludert syntaks og eksempler
documentationcenter: na
author: gregli-msft
manager: kfile
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: reference
ms.component: canvas
ms.date: 11/07/2015
ms.author: gregli
ms.openlocfilehash: 28d393d9be240b3e9ba57d108761c7a38f013b24
ms.sourcegitcommit: 68fc13fdc2c991c499ad6fe9ae1e0f8dab597139
ms.translationtype: HT
ms.contentlocale: nb-NO
ms.lasthandoff: 06/04/2018
ms.locfileid: "31826871"
---
# <a name="table-function-in-powerapps"></a>Table-funksjonen i PowerApps
Oppretter en midlertidig [tabell](../working-with-tables.md).

## <a name="description"></a>Beskrivelse
**Table**-funksjonen oppretter en tabell fra en argumentliste av [poster](../working-with-tables.md#records).

Tabellens [kolonner](../working-with-tables.md#columns) blir unionen av alle egenskapene fra postene i argumentet. Når poster ikke inneholder noen verdi, legger funksjonen til en *tom* verdi i kolonnen.

En tabell er en verdi i PowerApps, akkurat som en streng eller et tall. Du kan angi en tabell som et argument for en funksjon, og funksjoner kan returnere en tabell som et resultat. **Table** oppretter ikke en permanent tabell. I stedet returneres en midlertidig tabell som er bygget opp av argumentene.  Du kan angi denne midlertidige tabellen som et argument til en annen funksjon, visualisere dataene i et galleri eller bygge det inn i en annen tabell.  Hvis du vil ha mer informasjon, kan du se [Å arbeide med tabeller](../working-with-tables.md).

Du kan også opprette en tabell med én kolonne med syntaksen **[ value1, value2, ... ]**.

## <a name="syntax"></a>Syntaks
**Table**( *Record1* [, *Record2*, ... ] )

* *Record(s)* – obligatorisk. Postene som legges til i tabellen.

## <a name="examples"></a>Eksempler
* Angi **[Elementer](../controls/properties-core.md)**-egenskapen til en liste som denne formelen:
  <br>**Table({Color:"red"}, {Color:"green"}, {Color:"blue"})**
  
    Listen viser hver farge som et alternativ.
* Legg til et tekstgalleri, og angi **[Elementer](../controls/properties-core.md)**-egenskapen som denne funksjonen:<br>
  **Table({Item:"Violin123", Location:"France", Owner:"Fabrikam"}, {Item:"Violin456", Location:"Chile"})**
  
    Galleriet viser to poster. Begge inneholder navnet og stedet til et element. Bare én post inneholder navnet på eieren.
