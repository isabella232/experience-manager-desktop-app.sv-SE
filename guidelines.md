---
source-git-commit: a25c1fa13895ae9eb7268e3e01c83a5f0b9d7d1d
workflow-type: tm+mt
translation-type: tm+mt
source-wordcount: '721'
ht-degree: 5%

---
# Riktlinjer för att bidra till [!DNL Adobe Experience Manager]-dokumentation

## Dokumentationsfilosofi

Vi vet att [!DNL Adobe Experience Manager]-användare arbetar i mycket konkurrensutsatta miljöer och strävar efter att skapa digitala upplevelser som skiljer dem från deras konkurrenter. Därför är det viktigt att när Adobe levererar avancerade nya verktyg i [!DNL Experience Manager], dessa verktyg kompletteras med korrekt och tydlig dokumentation som gör det möjligt för kunden att omedelbart utnyttja sin [!DNL Experience Manager]-investering och maximera avkastningen.

Målet med [!DNL Experience Manager]-dokumentationen är att skicka dokumentation till [!DNL Experience Manager]-användare så snart som möjligt. Därför prioriterar vi korrekt, användbar dokumentation och strävar efter att kontinuerligt uppdatera och förbättra den.

## Dokumentationsbidrag

För att kontinuerligt förbättra [!DNL Experience Manager]-dokumentationen är det välkommet att alla [!DNL Experience Manager]-användare bidrar till dokumentationen. Vare sig det gäller förfrågningar eller frågor kan förbättringar av dokumentationen vara korrigeringar, förtydliganden, tillägg och ytterligare exempel.

## Dokumentationsstandarder

Vi välkomnar bidrag till vår dokumentation, men alla bidrag till [!DNL Experience Manager]-dokumentationen, antingen i form av en pull-begäran eller ett problem, bör överensstämma med våra bidrag- och dokumentationsstandarder.

Bidrag som inte uppfyller dessa standarder kan avvisas.

### Standardanvändningsfall för dokument

[!DNL Experience Manager] dokumentationen täcker standardanvändningsfall. Användningsfall som inte omfattas av standardinstallation och standardanvändning av produkten ingår inte i [!DNL Experience Manager]-dokumentationen.

### Vi dokumenterar vanligtvis inte buggar eller deras tillfälliga lösningar

[!DNL Experience Manager] dokumentationen täcker standardanvändningsfall. Av den anledningen är buggar, effekter orsakade av buggar och tillfälliga lösningar för buggar i allmänhet inte dokumenterade.

Undantag från den här regeln gäller versionsinformationen där kända problem kan listas med möjliga lösningar som har godkänts av [!DNL Experience Manager] Product Management.

### Dokumentationsbidragen är inte till för att besvara tekniska frågor

Alla idéer du kan behöva förbättra [!DNL Experience Manager]-dokumentationen är välkomna som bidrag. Kommentarer, utgåvor och pull-begäranden är dock endast avsedda för *bidrag*. De är inte avsedda att användas för att besvara dina frågor om hur du använder [!DNL Experience Manager], implementerar ditt [!DNL Experience Manager]-projekt eller löser tekniska problem.

Frågor om hur du använder [!DNL Experience Manager] eller tekniska fel som du kan ha gjort ska rapporteras via den normala supportprocessen via [Experience Cloud Enterprise Support-portalen](https://helpx.adobe.com/se/contact/enterprise-support.ec.html) eller diskuteras i [Experience Manager-communityn](https://forums.adobe.com/community/experience-cloud/marketing-cloud/experience-manager).

***[!DNL Experience Manager]Dokumentationsbidragen ersätter inte Adobe Customer*** Careoch eventuella bidrag som söker svar på supportrelaterade frågor kommer att refuseras.

### Bidragen ska tydligt hänvisa till berörda dokumentationssidor.

Om du skapar ett problem som kan föreslå förbättringar av dokumentationen måste du inkludera länkar till de sidor som påverkas. Om du skapar ett ärende genom att använda länken **Redigera den här sidan** på en dokumentationssida skapas ärendet automatiskt med en länk till sidan.

Detta gäller inte för pull-begäranden eftersom pull-begäranden till sin natur refererar till den eller de berörda sidorna.

## Riktlinjer för dokumentation

Vi ber att eventuella bidrag till vår dokumentation följer vissa riktlinjer för format.

Genom att följa dessa riktlinjer blir det enklare att granska ditt bidrag och det går därför snabbare att integrera det i vår dokumentation.

### Språk och format

#### Språk:

* [!DNL Experience Manager] Dokumentationen skrivs och underhålls på amerikansk engelska.
* Håll meningar så enkla som möjligt.
* Se till att språket är klart och koncist.

Kom ihåg att läsare av [!DNL Experience Manager]-dokumentation finns i hela världen och inte kan förväntas vara inbyggda eller flytande engelska högtalare. Undvik kollokvialism och håll språket så tydligt och enkelt som möjligt.

#### Följ Microsoft-formathandboken

[Microsoft Manual of ](https://docs.microsoft.com/en-us/style-guide/welcome/) Style är en kostnadsfri handbok för dokumentationsformat som fokuserar på programvarudokumentation och - [!DNL Experience Manager] dokumentation. Handboken följer den när det är möjligt.

### Formatering

| Objekt | Format |
|---|---|
| Element eller alternativ i användargränssnittet | **fet** |
| Filnamn, sökväg, användarindata, parametervärden | `monospaced` |
| Kod, kommandorad | ```Code Block``` |

### Skärmbilder

Skärmbilder ska användas med omdöme och endast när en textbeskrivning är otillräcklig.

Markörer eller andra anteckningar i skärmbilder (som röda ramar, pilar eller text) bör inte användas. På så sätt är skärmbilderna enklare att återanvända eller att replikera i lokaliserade versioner av dokumentationen.

### Versionsspecifika referenser

Undvik om möjligt direkta referenser till en viss version i dokumentationsinnehållet. Detta gör dokumentationen mer flexibel och utbyggbar för framtida versioner.

### Användning av dag, [!DNL Experience Manager], CQ, CRX

Använd det fullständiga namnet **Adobe Experience Manager** för att få information om hur produkten används första gången i en artikel och referera sedan till den som **Experience Manager**.

Använd inte termerna Day, Day Software, CQ och CRX, utom när det är oundvikligt, t.ex. i klassnamn eller som hänvisar till historiken för [!DNL Experience Manager].
