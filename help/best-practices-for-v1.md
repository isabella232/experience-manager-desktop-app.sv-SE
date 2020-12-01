---
title: AEM praxis för datorprogram version 1.x
description: Viktiga funktioner och rekommenderad användning av Adobe Experience Manager program version 1.x.
translation-type: tm+mt
source-git-commit: 200135fb96bbfcf9f72e857514bb9b71a88ed817
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# AEM praxis för datorprogram v1.x {#aem-desktop-app-best-practices}

## Översikt {#overview}

Adobe Experience Manager (AEM)-datorprogrammet länkar din DAM-lösning (Digital Asset Management) till skrivbordet så att du kan öppna de filer som finns i det AEM webbgränssnittet direkt på skrivbordet. Om du sparar en resurs från skrivbordet överförs den till AEM på lämplig plats.

AEM program eliminerar risken att du uppdaterar felaktiga lokala kopior eller uppdaterar fel resurs i AEM. datorappens lättanvända arbetsflöde aktiveras med hjälp av nätverksdelningsteknik som finns i operativsystemen.

Datorprogrammet monterar AEM Assets-databasen som en nätverksresurs på skrivbordet. Därför ser mapparna och filerna ut som om de var lokala. Vi rekommenderar dock inte att du utför digitala resurshanteringsåtgärder direkt från skrivbordet i den monterade nätverksresursen i Finder eller Utforskaren. I stället rekommenderar Adobe att du använder AEM Assets webbgränssnitt för att utföra åtgärder, som att kopiera eller flytta ett stort antal resurser.

>[!NOTE]
>
>Innan du läser det här dokumentet kan du läsa igenom den övergripande [AEM och bästa praxis för integrering med Creative Cloud](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/aem-cc-integration-best-practices.html) för en översikt över ämnet på högre nivå.

## Arkitektur för AEM{#aem-desktop-app-architecture}

AEM använder nätverksresurser för WebDAV (Windows) eller SMB (Mac) för att montera nätverksresurser. Den monterade nätverksresursen är endast lokal. AEM datorprogrammet fångar upp anropen (öppna, läsa, skriva) och erbjuder ytterligare lokal cachelagring. Det översätter fjärranrop till AEM Assets-servern för att optimera AEM HTTP-begäranden. I följande diagram visas arkitekturen för AEM datorprogram.

![AEM](assets/arch_v1.png)

*Bild: arkitektur för datorprogram*

Den extra cachelagringen vid skrivning när en fil sparas gör att filen sparas lokalt först (så att användaren inte väntar på nätverksöverföringen). Efter en fördefinierad fördröjning (30 sekunder) överförs filen till AEM i bakgrunden och resursen överförs sedan till AEM. AEM datorprogram har ett gränssnitt för övervakning av status för filöverföringar i bakgrunden.

## Rekommenderad användning AEM datorprogrammet {#recommended-use-of-aem-desktop-app}

Viktiga funktioner i AEM program:

* **Öppna filer från AEM Assets webbgränssnitt på datorn**. I webbgränssnittet kan du visa resurser på skrivbordet (i Finder, Utforskaren) eller öppna en resurs med ett skrivbordsprogram.

* **Checka ut och checka in**. Resurser kan checkas ut för redigering och markeras som låsta för användaren i AEM Assets. Efter redigeringen kan resursen checkas in för att låsa upp den.

* **Spara ändringar i filer**. Alla ändringar som du sparar i filen i nätverksresursen överförs automatiskt till AEM och en ny version skapas.

* **Montera länkade resurser i andra dokument**. I program som Creative Cloud ([!DNL Adobe Photoshop], [!DNL Adobe InDesign] och [!DNL Adobe Illustrator]) kan du placera en extern fil som en länk. Du kan till exempel montera en bild i ett InDesign-dokument. I det här fallet kan du med hjälp av nätverksresursen bläddra bland och välja resurser från AEM för placering. Det går också att placera länkade filer i vissa program som inte är Adobe, till exempel MS Office.

* **Referensupplösning i AEM**. Om både de monterade filerna och huvudfilerna med länkar lagras i AEM kan de automatiskt tillhandahålla information om resursreferenserna på serversidan.

* **Åtkomst till resursen från skrivbordet**. I den monterade nätverksresursen innehåller en snabbmeny en [!UICONTROL More Info]-dialogruta (större förhandsgranskning, nyckelmetadata) och möjlighet att öppna en resurs i AEM.

* **Överför stora, hierarkiska mappar i grupp**. Om du använder alternativet Skapa > Mappöverföring i AEM gränssnitt för att överföra resurser, överför AEM datorprogrammet den valda mapphierarkin till AEM i bakgrunden. Överföringsförloppet kan övervakas med ett dedikerat användargränssnitt i skrivbordsappen.

## Felaktig användning AEM datorprogrammet {#inappropriate-use-of-aem-desktop-app}

* Använd inte AEM datorprogram för att hantera resurser från skrivbordet. AEM skrivbordsapp skapades inte som ersättning för nätverksenheter. Använd följande funktioner i stället:

   * AEM Assets webbgränssnitt för hantering av digitala resurser (söka efter eller dela resurser, metadata samt kopiera eller flytta).

   * AEM datorprogrammet [!UICONTROL Folder Upload] för att överföra stora, hierarkiska mappar.

* Behandla inte AEM datorprogram som en&quot;datorsynkroniseringsklient&quot; för AEM Assets. Den största fördelen med AEM datorprogram här är att det ger&quot;virtuell&quot; åtkomst till hela databasen, och program för datorsynkronisering synkroniserar vanligtvis bara resurser som tillhör en användare. AEM datorprogram erbjuder viss nivå av cachelagring och bakgrundsuppladdning. fungerar det fortfarande på ett helt annat sätt än vanliga&quot;Synkroniseringsprogram&quot;, till exempel Adobe Creative Cloud-datorprogram eller Microsoft OneDrive.

* Använd inte AEM nätverksenheter för skrivbordsappar för att spara resurser ofta. Alla sparåtgärder överförs till AEM Assets. Därför är det opraktiskt att utföra intensiva redigeringsåtgärder direkt i den monterade AEM Assets-databasen. När du redigerar en resurs direkt i den monterade databasen krymper resursens tidslinje med irrelevanta versioner och lägger till ytterligare omkostnader på servern.

* Använd inte AEM datorprogram för att migrera stora mängder data från en AEM till en annan. Se [Migreringshandboken](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/assets-migration-guide.html) för att planera och köra resursmigreringar. Datorprogrammet [stöder däremot massöverföring](use-app-v1.md#bulkupload) av ett stort antal resurser för första gången i [!DNL Adobe Experience Manager].

## Recommendations för utvalda användningsfall {#recommendations-for-selected-use-cases}

### Tillgång till resurser för kreativa användare {#access-to-assets-for-creative-users}

AEM datorprogram ger virtuell åtkomst till hela DAM-databasen - och det kan vara komplicerat för de kreativa användarna på skrivbordet att hitta och komma åt rätt resurser på skrivbordet. Använd de här bästa sätten för att förenkla för dem.

* Använd samarbetsfunktionerna i AEM Assets webbgränssnitt för att ge mer direkt åtkomst till rätt material för den kreativa användaren. Några av dem är att dela mappar eller samlingar, tillhandahålla smarta samlingar (sparade sökningar) eller skicka meddelanden med pekare till rätt resurser. Den kreativa användaren kan sedan använda skrivbordsåtgärder i webbgränssnittet för att snabbt få tillgång till dessa resurser på sin dator.

* Tänk på rätt behörigheter för materialet (åtkomstkontroll) för att förenkla visningen av DAM-databasen för de kreativa användarna, och begränsa i princip åtkomsten till endast de resurser de behöver eller är intresserade av:

   * Vissa områden som inte är relevanta för de kreativa användarna kan nekas användargrupperna att ta bort dem från sina vyer, även på skrivbordet.

   * De flesta resurser i DAM är slutgiltiga och är inte avsedda att ändras - de ska vara skrivskyddade för de kreativa användarna.

   * Endast resurser som kräver ändringar eller retuschering ska vara skrivaktiverade för de kreativa användarna. Vissa organisationer använder AEM projekt och de mappar de skapar för att lagra resurser som fortfarande kan ändras.

### Söker efter resurser {#searching-assets}

Så här söker du efter en fil som du vill öppna på skrivbordet:

* Använd AEM Assets webbgränssnitt för att hitta resursen. Det är inte bara sökning i AEM Assets kraftfulla funktioner (sökfaktorer, sparade sökningar), utan även andra funktioner för att hitta rätt resurs. Detta inkluderar ytterligare filter, som möjligheten att söka efter resurser baserat på status (godkännande, förfallodatum), samlingar, uppgifter, meddelanden och att dela mappar/samlingar med andra användare/grupper.

* När du har hittat resursen kan du använda Skrivbordsåtgärder i AEM för att komma åt resursen på skrivbordet.

### Uppdaterar resurser som har öppnats med AEM{#updating-assets-opened-using-aem-desktop-app}

Om du redigerar en resurs direkt på den plats som mappats från AEM Assets till en lokal nätverksresurs, överförs resursen till AEM varje gång du sparar den på skrivbordet. Dessutom skapar AEM en version och skapar återgivningar.

Om en resurs som lagras i AEM behöver uppdateras:

* För **mindre uppdateringar**, till exempel mindre retuscheringsbegäranden i godkännandeprocessen:

   * Checka ut filen och öppna den på skrivbordet.

   * Uppdatera filen.

   * Spara den uppdaterade versionen. Resursen uppdateras och tidslinjen visar den ursprungliga versionen för jämförelse.

* För **större uppdateringar**, till exempel en ändringsbegäran som kräver en liten kreativ PIA-cykel:

   * Använd alternativet Visa för att öppna rätt mapp på skrivbordet.

   * Kopiera filen till en WIP-mapp utanför den mappade AEM Assets-resursen (kopiera till exempel filen till en mapp som synkroniseras med Adobe Creative Cloud-datorprogrammet).

   * Arbeta med filen och spara den regelbundet. Ändringarna sparas inte i AEM Assets.

   * När redigeringarna är klara flyttar, kopierar eller sparar du filen som mappats från AEM för att överföra den som en ny version.

## Nätverksprestanda {#network-performance}

En bra upplevelse för användare som använder det AEM datorprogrammet beror i hög grad på en bra, stabil nätverksanslutning mellan datorn och den AEM servern, samt på servern som är anpassad för att ge goda prestanda, särskilt när det gäller att överföra och uppdatera resurser. Rekommendationerna är till för nätverks-/IT-team i organisationer.

### Nätverkshändelser {#network-considerations}

Information om de effektivaste strategierna för AEM Assets nätverkskonfiguration finns i dokumentet [AEM Assets Network Considerations](https://experienceleague.adobe.com/docs/experience-manager-64/assets/administer/assets-migration-guide.html). Några av de viktiga aspekter som hjälper användarna att optimera AEM appupplevelsen är:

* **Använd korrekt konfigurerad Dispatcher**. Använd AEM Dispatcher för ytterligare säkerhet och kontrollera att den är konfigurerad för [AEM anslutning till datorprogrammet så att den AEM bakom en dispatcher](install-configure-app-v1.md#connect-to-an-aem-instance-behind-a-dispatcher)

* **Spara bandbredd**. Överväg att inaktivera förhandsvisning av ikoner i Finder på Mac - när du bläddrar i den monterade databasen med Finder. Finder begär att varje fil ska generera en förhandsgranskning och gör att skrivbordsappen hämtar och cachelagrar resursen lokalt. Observera att när du sparar bandbredd försämras även användarupplevelsen för användarna på skrivbordet, så det bör göras när du arbetar med databaser med stora resurser och/eller begränsad bandbredd.

>[!NOTE]
>
>Om du vill inaktivera förhandsvisning av ikoner går du till Visa i Finder, väljer Visningsalternativ och avmarkerar sedan alternativet &quot;Förhandsvisa ikon&quot;. Det här fungerar bara för den aktuella mappen. Om du vill göra den till standard klickar du på knappen Använd som standard i samma fönster.

### Optimerar serverprestanda {#optimizing-server-performance}

Mer information om hur AEM Assets-servern ska optimeras för prestanda finns i [AEM Assets Performance Tuning Guide](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/performance-tuning-guidelines.html). Några av de viktiga aspekterna av serverprestanda för AEM datorprogram är att optimera arbetsflödeskonfigurationen så att den fungerar bra för överföringar av resurser:

* **Mer prestanda för överföring** av resurser. Konfigurera arbetsflödesmodellen [AEM Resursuppdatering så att den är övergående](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/performance-tuning-guidelines.html).

* **Begränsa serverns CPU för överföringar**. Se till att parametern för maximala parallella arbetsflödesjobb är korrekt inställd så att överföringar inte tar bort hela processorn.
