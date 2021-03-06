---
title: Vanlige problemer og løsninger for Løsningskontroll | Microsoft Docs
description: ' En liste over vanlige problemer og løsninger i Løsningskontroll'
keywords: ''
ms.date: 02/11/2019
ms.service:
  - powerapps
ms.custom:
  - ''
ms.topic: article
ms.assetid: caa4e3f2-9700-49b8-87ed-8a68e8878b02
author: jowells1
ms.author: jowells
manager: austinj
ms.reviewer: null
robots: 'noindex,nofollow'
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# Vanlige problemer og løsninger for Løsningskontroll

Denne artikkelen inneholder en liste over enkelte vanlige problemer som kan oppstå når du bruker Løsningskontroll. Der det er nødvendig er løsninger tilgjengelig.

## Løsningskontroll-kjøring mislykkes på grunn av installert PowerApps-kontrollerversjon
Løsningskontroll en funksjon som er inkludert i PowerApps-kontrollversjonen.  Hvis du har en PowerApps-kontrollerversjon før 1.0.0.47, vil ikke Løsningskontroll-kjøring være vellykket. Du må oppgradere PowerApps-kontrollerversjonen fra [!INCLUDE [pn-dyn-365-admin-center](../../includes/pn-dyn-365-admin-center.md)]. 

Men hvis du har en PowerApps-kontrollerversjon før 1.0.0.45, bør du slette løsningen og installere den på nytt. På grunn av de siste skjemaendringene kan oppgradering av PowerApps-kontroller fra versjoner tidligere enn 1.0.0.45 mislykkes.

Hvis du vil beholde de siste resultatene fra Løsningskontroll, eksporterer du resultatene fra en tidligere kjøring eller eksporter alle Løsningskontroll-data ved hjelp av [Eksportere data til Excel](../../user/export-data-excel.md) for å eksportere data fra følgende enheter:

- Analysekomponent
- Analysejobb
- Analyseresultat
- Analyseresultatdetalj

### Slette PowerApps-kontroller

For å slette PowerApps-kontrollerløsningen:

1. Som systemansvarlig eller systemtilpasser kan du åpne PowerApps-portalen ved å gå til https://web.powerapps.com/environments.
2. Velg **Løsninger**.
3. Velg **PowerApps-kontroller**, og velg deretter på **Slett** på løsningsverktøytlinjen.

### Legge til PowerApps-kontroller

For å legge PowerApps-kontroller tilbake til CDS for Apps-miljøet:

1. Som systemansvarlig eller systemtilpasser kan du åpne PowerApps-portalen ved å gå til https://web.powerapps.com/environments.
2. Velg **Løsninger**.
3. På løsningsverktøylinjen velger du **Løsningskontroll**, og velg deretter **Installer**.

## Kjøring på store løsninger mislykkes

Løsningskontroll har 10-minutters tidsavbrudd for å eksportere en løsning fra Common Data Service (CDS) for Apps-miljøet. Store løsninger, som standardløsning, kan føre til at eksporten ikke kan utføres i dette tidsrommet, og kontrollen vil ikke fullføres. Løsningskontroll prøver tre ganger før den ikke lenger behandler jobben, slik at det kan ta over 30 minutter før du får et feilvarsel.

Hvis du vil løse dette problemet, kontroller eller opprett mindre løsninger som kan analyseres. For å redusere falske positive svar, sikre at du legger til avhengige tilpassinger. Når du oppretter en løsning og legger til disse komponentene, inkluder følgende:

- Når du legger til plugin-moduler, inkluder behandlingstrinn for SDK-melding for plugin-modulen.
- Når du legger til i enhetsskjemaer, kan du inkludere JavaScript-webressurser som er knyttet til skjemahendelsene.  
- Når du legger til JavaScript-webressurser, inkluder eventuelle avhengige JavaScript-webressurser.
- Når du legger til HTML-webressurser, inkluder eventuelle avhengige skript som er definert i HTML-webressursen.
- Når du legger til egendefinerte arbeidsflyter, kan du inkludere samlingen som brukes i arbeidsflyten.

## Løsningskontroll-kjøring eller -nedlastingsresultater fullføres ikke 
Kort tid etter kjøring av Løsningskontroll fullføres ikke operasjonen, og følgende melding vises:<br />
"Vi kan ikke kjøre kontrollen på *LØSNINGSNAVN*-løsningen. Prøv å kjøre den på nytt." <br />
![![Kan ikke kjøre](media/solution-checker-werent-able-to-run.png)](media/solution-checker-werent-able-to-run.png)

Dette problemet oppstår fordi organisasjonen er i **administrasjonsmodus**-tilstand, og Løsningskontroll klarer ikke å validere brukerens tillatelser til å kjøre forespørselen. Hvis du vil løse dette problemet, kan du deaktivere administrasjonsmodus. 

### Deaktivere administrasjonsmodus for en forekomst
1. Få tilgang til Dynamics 365 for Customer Engagement-forekomstvelgeren: https://port.crm.dynamics.com/G/Instances/InstancePicker.aspx.
2. Velg forekomsten som har problemer med å kjøre Løsningskontroll.
3. Velg **ADMIN**.<br />
![![Forekomstadmin](media/solution-checker-instance-admin.png)](media/solution-checker-instance-admin.png)

4. Fjern merket for **Aktiver administrasjonsmodus**. <br />
![![Deaktiver administratormodus](media/solution-checker-instance-disable-admin-mode.png)](media/solution-checker-instance-disable-admin-mode.png)

5. Kjør Løsningskontroll på nytt.

## Løsningskontroll behandler ikke oppdateringsløsninger

Hvis en løsning har en [oppdatering](https://docs.microsoft.com/powerapps/developer/common-data-service/create-patches-simplify-solution-updates), mislykkes Løsningskontroll i å eksportere løsningen for analysen. Når en løsning har brukt en oppdatering, låses den opprinnelige løsningen, og den kan ikke endres eller eksporteres så lenge det finnes avhengige oppdateringer i organisasjonen som identifiserer løsningen som den overordnede løsningen.

Hvis du vil løse dette problemet, kan du klone løsningen, slik at alle oppdateringer som gjelder løsningen, rulles inn i den nyopprettede løsningen. Dette låser opp løsningen og gjør at løsningen kan eksporteres fra systemet. Mer informasjon: [Klone en løsning](use-segmented-solutions-patches-simplify-updates.md#clone-a-solution)

## Linjenummerreferanser for problemer i HTML-ressursene med innebygd JavaScript er ikke riktig 

Når du skal behandles HTML-webressurser i Løsningskontroll, behandles HTML-webressursen separat fra JavaScript i HTML-webressursen. På grunn av dette vil linjenummeret inne i `<script>` i HTML-webressursen ikke bli riktig.

## Webstøttesyntaksproblem for webressurser

ECMAScript 6 (2015) eller senere versjoner støttes ikke for Løsningskontroll. Når Løsningskontroll analyserer JavaScript med ECMAScript 6 eller senere, rapporteres et webstøttesyntaksproblem for webressursen .  

## Se også
[[Gode fremgangsmåter og veiledning for Common Data Service for Apps](../../developer/common-data-service/best-practices/index.md)](../../developer/common-data-service/best-practices/index.md)<br />
[[Gode fremgangsmåter og veiledning for modelldrevne apper](../../developer/model-driven-apps/best-practices/index.md)](../../developer/model-driven-apps/best-practices/index.md)<br />
