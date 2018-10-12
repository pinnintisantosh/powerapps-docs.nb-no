---
title: Definer overføringer av statusårsak med PowerApps | MicrosoftDocs
description: Finn ut hvordan du definerer overføringer av statusårsak
ms.custom: ''
ms.date: 05/25/2018
ms.reviewer: ''
ms.service: crm-online
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Dynamics 365 (online)
- Dynamics 365 Version 9.x
- powerapps
author: Mattp123
ms.assetid: dbc4f436-0b23-42f9-8079-b0de482aaebe
caps.latest.revision: 11
ms.author: matp
manager: kvivek
ms.openlocfilehash: e21069a86d2ef21e8209fea6ea4a4b05e604cda4
ms.sourcegitcommit: aba996b1773ecdf62758e06b34eaf57bede29e08
ms.translationtype: HT
ms.contentlocale: nb-NO
ms.lasthandoff: 08/08/2018
ms.locfileid: "39694731"
---
# <a name="define-status-reason-transitions-for-the-case-or-custom-entities"></a>Definere overganger for statusårsaker for saken eller egendefinerte enheter

Du kan angi overføringer for statusårsak for enheten Hendelse (**Sak**) eller en egendefinert enhet.

> [!NOTE]
> Selv om hendelsesenheten (tilfelle) ikke er inkludert i et standardmiljø for Common Data Service for apper, er den brukt av [Dynamics 365 for Customer Service](https://dynamics.microsoft.com/customer-service/) og angitt i [Common Data Model](https://github.com/Microsoft/CDM/blob/master/schemaDocuments/core/applicationCommon/foundationCommon/crmCommon/service/Incident.cdm.json)
  
Overføringer for statusårsak er et valgfritt tilleggsnivå for filtrering for å angi hva verdien for statusårsaken kan endres til for hver statusårsak. Hvis du angir en begrenset liste med gyldige alternativer, kan dette gjøre det enklere for brukere å velge riktig neste statusårsak for en oppføring når du har et stort antall kombinasjoner av gyldige verdier for statusårsak.  
  
<a name="BKMK_StatusAndStatusReasons"></a>

## <a name="what-is-the-connection-between-status-and-status-reason-fields"></a>Hva er sammenhengen mellom feltene Status og Statusårsak?  

Enheter som kan ha ulike statusverdier, har to felt som fanger opp disse dataene:  
  
|Visningsnavn|Beskrivelse|  
|------------------|-----------------|  
|**Status**|Representerer statusen for oppføringen. Vanligvis **Aktiv** eller **Inaktiv**. Du kan ikke legge til nye statusalternativer.|  
|**Statusårsak**|Representerer en årsak som er knyttet til en bestemt status. Hver status må ha minst én mulig statusårsak. Du kan legge til flere alternativer for statusårsak.|  
  
Metadataene for feltet angir hvilke statusverdier som er gyldige for en bestemt tilstand. Standardstatus og alternativer for statusårsak for Hendelse-enheten (**Sak**) er for eksempel:  
  
|Status|Statusårsak|  
|------------|-------------------|  
|**Aktiv**|<li>**Pågår**</li><li>**På vent**</li><li>**Venter på detaljer**</li><li>**Undersøker**</li>| 
|**Løst**|<li>**Problem løst**</li><li>**Angitt informasjon**</li>|
|**Annullert**|<li>**Annullert**</li><li>**Sammenslått**</li>|
  
  
<a name="BKMK_EditStatusReasonTransitions"></a>   

## <a name="edit-status-reason-transitions"></a>Rediger overføringer av statusårsak
 
Du kan endre feltalternativene for statusårsaken for Sak-enheten og egendefinerte enheter for å definere hvilke andre alternativer for statusårsak brukere kan velge. Den eneste begrensningen er at hvert alternativ for statusårsak for en aktiv status må ha minst én bane til en inaktiv status. Hvis ikke, kan du skape en situasjon der det ikke vil være mulig å løse eller avbryte saken.  

> [!NOTE]
> Hvis du vil redigere overføringer av statusårsaker, må du ta i bruk Løsningsutforsker. Se [Opprett og rediger felt for Common Data Service for apper ved bruk av løsningsutforsker for PowerApps](create-edit-field-solution-explorer.md) hvis du vil ha mer informasjon om hvordan du redigerer felt.
  
 Når du redigerer et statusårsaksfelt, vises knappen **Rediger overføringer av statusårsak** på menyen. 

![Kommandoen Rediger overføringer av statusårsak](media/status-reason-transitions-command.png)

Når du klikker denne knappen, gir dialogboksen **Overføringer av statusårsak** mulighet til å velge **Aktiver overføringer av statusårsak**. Når dette alternativet er valgt, må du angi *hvilke* verdier for statusårsak som er tillatt for hver statusårsak. Hvis du vil fjerne filtrering som brukes, fjerner du merkingen for **Aktiver overføringer av statusårsak**. Overføringene du har angitt vil bli beholdt, men ikke brukt.  
  
Skjermbildet nedenfor viser et eksempel som oppfyller følgende krav: 
 
- En sak kan slås sammen når som helst. Du kan ikke slå sammen saker hvis en overføring av statusårsak ikke tillater det.  
- En aktiv sak kan avsluttes når som helst.  
- En løst eller avsluttet sak kan ikke reaktiveres.  
- Alle saker som må gå gjennom følgende trinn: **Pågår** > **På vent** > **Venter på detaljer** > **Undersøker** før de kan løses. En sak kan ikke settes til en tidligere status med denne konfigurasjonen.  
  > [!NOTE]
  >  Dette er ikke et godt eksempel for faktisk arbeid, men det demonstrerer hvordan statustrinn kan håndheves gjennom overføringer av statusårsak.  
  
 ![Eksempel på overføringer av statusårsak for sak](media/status-reason-transitions-example.PNG)  
  
### <a name="see-also"></a>Se også  

[Opprett og rediger felt for Common Data Service for apper ved bruk av løsningsutforsker for PowerApps](create-edit-field-solution-explorer.md)<br />
[Enhetsmetadata > Enhetstrinn](/powerapps/developer/common-data-service/entity-metadata#entity-states)<br />
[Definer egendefinerte tilstandsmodelloverføringer](/dynamics365/customer-engagement/developer/define-custom-state-model-transitions)
