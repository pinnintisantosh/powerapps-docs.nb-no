---
title: Funksjonene Replace og Substitute | Microsoft Docs
description: Referanseinformasjon for funksjonene Replace og Substitute i PowerApps, inkludert syntaks og eksempler
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
ms.openlocfilehash: d08cbb1ae487c7ae4423d67a499f5477a5ea263b
ms.sourcegitcommit: 68fc13fdc2c991c499ad6fe9ae1e0f8dab597139
ms.translationtype: HT
ms.contentlocale: nb-NO
ms.lasthandoff: 06/04/2018
ms.locfileid: "31830377"
---
# <a name="replace-and-substitute-functions-in-powerapps"></a>Funksjonene Replace og Substitute i PowerApps
Erstatt en del av en tekststreng med en annen streng.

## <a name="description"></a>Beskrivelse
**Replace**-funksjonen identifiserer teksten du vil erstatte basert på startposisjon og lengde.  

**Substitute**-funksjonen identifiserer teksten du vil erstatte ved å sammenligne en streng.  Hvis det blir funnet mer enn ett treff, kan du styre hvilken som erstattes.

Hvis du angir en enkelt streng, er returverdien den endrede strengen.  Hvis du angir en [enkeltkolonnetabell](../working-with-tables.md) som inneholder strenger, vil returverdien være en enkeltkolonnetabell med endrede strenger. Hvis du har en flerkolonnetabell, kan du gjøre den om til en enkeltkolonnetabell, som beskrevet i [arbeid med tabeller](../working-with-tables.md).

## <a name="syntax"></a>Syntaks
**Replace**( *String*, *StartingPosition*, *NumberOfCharacters*, *NewString* )

* *String* – obligatorisk. Strengen det skal arbeides i.
* *StartingPosition* – obligatorisk.  Tegnplassering hvor erstatningen skal begynne. Det første tegnet i *String* er i posisjon 1.
* *NumberOfCharacters* – obligatorisk.  Antallet tegn som skal erstattes i *String*.
* *NewString* – obligatorisk.  Erstatningsstrengen. Antall tegn i dette argumentet kan være forskjellig fra *NumberOfCharacters*-argumentet.

**Substitute**( *String*, *OldString*, *NewString* [, *InstanceNumber* ] )

* *String* – obligatorisk. Strengen det skal arbeides i.
* *OldString* – obligatorisk.  Strengen som skal erstattes.
* *NewString* – obligatorisk.  Erstatningsstrengen. *OldString* og *NewString* kan ha forskjellig lengde.
* *InstanceNumber* – valgfritt. Som standard erstattes den første forekomsten av *OldString*. Hvis *String* inneholder mer enn én forekomst, kan du angi hvilken forekomst som skal erstattes.

**Replace**( *SingleColumnTable*, *StartingPosition*, *NumberOfCharacters*, *NewString* )

* *SingleColumnTable* – obligatorisk. En enkeltkolonnetabell med strenger som det skal arbeides i.
* *StartingPosition* – obligatorisk.  Tegnplassering hvor erstatningen skal begynne.  Det første tegnet i hver streng i tabellen er i posisjon 1.
* *NumberOfCharacters* – obligatorisk.  Antall tegn som skal erstattes i hver streng.
* *NewString* – obligatorisk.  Erstatningsstrengen. Antall tegn i dette argumentet kan være forskjellig fra *NumberOfCharacters*-argumentet.

**Substitute**( *SingleColumnTable*, *OldString*, *NewString* [, *InstanceNumber* ] )

* *SingleColumnTable* – obligatorisk. En enkeltkolonnetabell med strenger som det skal arbeides i.
* *OldString* – obligatorisk.  Strengen som skal erstattes.
* *NewString* – obligatorisk.  Erstatningsstrengen. *OldString* og *NewString* kan ha forskjellig lengde.
* *InstanceNumber* – valgfritt. Som standard erstattes den første forekomsten av *OldString*. Hvis tabellen inneholder mer enn én forekomst, kan du angi hvilken forekomst som skal erstattes.
