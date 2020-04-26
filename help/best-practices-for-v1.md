---
title: Bästa praxis för AEM-datorprogram version 1.x
description: Viktiga funktioner och rekommenderad användning av Adobe Experience Manager-datorprogrammet version 1.x.
uuid: ba8fbc74-e1ad-4085-a031-ffd317628ba6
contentOwner: AG
products: SG_EXPERIENCEMANAGER/6.3/ASSETS
discoiquuid: 57d5cd78-abce-4ede-a50e-7c161ddb43ae
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: b92e47456f9e16c24eac43d1c5fef9a582f143b5

---


# Bästa praxis för AEM-datorprogram v1.x {#aem-desktop-app-best-practices}

## Översikt {#overview}

Adobe Experience Manager (AEM)-datorprogrammet länkar din DAM-lösning (Digital Asset Management) till din dator så att du kan öppna de filer som är tillgängliga i AEM-webbgränssnittet direkt på skrivbordet. Om du sparar en resurs från skrivbordet överförs den till AEM på lämplig plats.

Med AEM-skrivbordsappen slipper du chanser att uppdatera felaktiga lokala kopior eller uppdatera fel resurs i AEM. datorappens lättanvända arbetsflöde aktiveras med hjälp av nätverksdelningsteknik som finns i operativsystemen.

Datorprogrammet monterar AEM Assets-databasen som en nätverksresurs på datorn. Därför ser mapparna och filerna ut som om de var lokala. Vi rekommenderar dock inte att du utför digitala resurshanteringsåtgärder direkt från skrivbordet i den monterade nätverksresursen i Finder eller Utforskaren. Adobe rekommenderar i stället att du använder webbgränssnittet för AEM Resurser för att utföra åtgärder, som att kopiera eller flytta ett stort antal resurser.

>[!NOTE]
>
>Innan du läser det här dokumentet kan du läsa de övergripande [arbetssätten för integrering med](https://docs.adobe.com/content/help/en/experience-manager-64/assets/administer/aem-cc-integration-best-practices.html) AEM och Creative Cloud för att få en översikt över ämnet på en högre nivå.

## AEM-arkitektur för datorprogram {#aem-desktop-app-architecture}

AEM-skrivbordsappen använder nätverksresurser för WebDAV (Windows) eller SMB (Mac) för att montera nätverksresurser. Den monterade nätverksresursen är endast lokal. AEM-skrivbordsappen fångar upp samtalen (öppna, läsa, skriva) och erbjuder ytterligare lokal cachelagring. Det översätter fjärranrop till AEM Assets-servern till optimerade AEM HTTP-begäranden. I följande diagram visas arkitekturen för AEM-skrivbordsappen.

![AEM-arkitektur för datorprogram](assets/chlimage_1.png)

Den extra cachelagringen vid skrivning när en fil sparas gör att filen sparas lokalt först (så att användaren inte väntar på nätverksöverföringen). Efter en fördefinierad fördröjning (30 sekunder) överförs filen till AEM i bakgrunden och resursen överförs sedan till AEM. AEM-skrivbordsappen tillhandahåller ett gränssnitt för övervakning av status för filöverföringar i bakgrunden.

## Rekommenderad användning av AEM-datorprogrammet {#recommended-use-of-aem-desktop-app}

Bland huvudfunktionerna i AEM-datorprogrammet finns:

* Öppna filer från webbgränssnittet för AEM Assets på datorn: I webbgränssnittet kan du visa resurser på skrivbordet (i Finder, Utforskaren) eller öppna en resurs med ett skrivbordsprogram.
* Checka ut och checka in: Resurser kan checkas ut för redigering och markeras som låsta för användaren i AEM Resurser. Efter redigeringen kan resursen checkas in för att låsa upp den.
* Spara ändringar i filer: Alla ändringar som du sparar i filen i nätverksresursen överförs automatiskt till AEM och en ny version skapas.
* Placera länkade resurser i andra dokument: I program som Creative Cloud (PS, ID, AI osv.) kan du montera en extern fil som en länk (du kan till exempel montera en bild i ett InDesign-dokument). I det här fallet kan du med hjälp av nätverksresursen bläddra bland och välja resurser från AEM för placering. Det går även att placera länkade filer i vissa program som inte är från Adobe, till exempel MS Office.
* Referensupplösning i AEM: Om både den eller de monterade filerna och huvudfilen med länkar lagras i AEM kan den automatiskt tillhandahålla serverinformation om resursreferenserna.
* Åtkomst till resursen från skrivbordet: I den monterade nätverksresursen finns en sammanhangsbaserad meny med dialogrutan Mer information (större förhandsgranskning, viktiga metadata) och möjligheten att öppna en resurs i AEM UI.
* Överför stora hierarkiska mappar i grupp: Om du använder alternativet Skapa > Mappöverföring i AEM-gränssnittet för att överföra resurser, överför AEM-skrivbordsappen den valda mapphierarkin till AEM i bakgrunden. Överföringsförloppet kan övervakas med ett dedikerat användargränssnitt i skrivbordsappen.

## Felaktig användning av AEM-datorprogrammet {#inappropriate-use-of-aem-desktop-app}

* Använd inte AEM-datorprogrammet för att hantera resurser från skrivbordet. AEM-skrivbordsappen skapades inte som ersättning för nätverksenheter. Använd följande funktioner i stället:
   * Webbgränssnittet för AEM Resurser för hantering av digitala resurser (söka/dela resurser, metadata, kopiera/flytta osv.)
   * Mappöverföring för AEM-skrivbordsprogram för överföring av stora, hierarkiska mappar

* Behandla inte AEM-datorprogrammet som en&quot;datorsynkroniseringsklient&quot; för AEM Assets. Den största fördelen med AEM-datorprogrammet här är att det ger&quot;virtuell&quot; åtkomst till hela databasen, och program för datorsynkronisering synkroniserar vanligtvis bara resurser som tillhör en användare. AEM-skrivbordsappen erbjuder viss nivå av cachelagring och bakgrundsuppladdning; fungerar det fortfarande på ett helt annat sätt än vanliga synkroniseringsprogram, som Adobe Creative Cloud-datorprogrammet eller Microsoft OneDrive.
* Använd inte nätverksenheter för AEM-skrivbordsappar för att spara resurser ofta. Alla sparåtgärder överförs till AEM Resurser. Därför är det opraktiskt att utföra intensiva redigeringsåtgärder direkt i den monterade AEM Resurser-databasen. När du redigerar en resurs direkt i den monterade databasen krymper resursens tidslinje med irrelevanta versioner och lägger till ytterligare omkostnader på servern.
* Använd inte AEM-datorprogrammet för att migrera stora mängder data från en AEM-instans till en annan. Se [Migreringshandboken](https://docs.adobe.com/content/help/en/experience-manager-65/assets/administer/assets-migration-guide.html) för att planera och utföra resursmigreringar. Datorprogrammet [stöder däremot massöverföring](use-app-v1.md#bulkupload) av ett stort antal resurser för första gången i AEM.

## Rekommendationer för valda användningsfall {#recommendations-for-selected-use-cases}

### Tillgång till material för kreativa användare {#access-to-assets-for-creative-users}

AEM-skrivbordsappen ger virtuell åtkomst till hela DAM-databasen - och det kan vara komplicerat för de kreativa användarna på skrivbordet att hitta och komma åt rätt resurser på skrivbordet. Använd de här bästa sätten för att förenkla för dem.

* Använd samarbetsfunktionerna i webbgränssnittet för AEM Assets för att ge mer direkt åtkomst till rätt material för den kreativa användaren. Några av dem är att dela mappar eller samlingar, tillhandahålla smarta samlingar (sparade sökningar) eller skicka meddelanden med pekare till rätt resurser. Den kreativa användaren kan sedan använda skrivbordsåtgärder i webbgränssnittet för att snabbt få tillgång till dessa resurser på sin dator.
* Tänk på rätt behörigheter för resurserna (åtkomstkontroll) för att förenkla visningen av DAM-databasen för de kreativa användarna, och begränsa i princip åtkomsten till endast de resurser de behöver/är intresserade av:

   * Vissa områden som inte är relevanta för de kreativa användarna kan nekas för sina användargrupper, så att de kan tas bort från sina vyer, även på skrivbordet
   * De flesta resurser i DAM är slutgiltiga och är inte avsedda att ändras - de ska vara skrivskyddade för de kreativa användarna
   * Endast resurser som kräver ändringar/retuschering ska vara skrivaktiverade för de kreativa användarna. Vissa organisationer använder AEM Projects och de mappar de skapar för att lagra resurser som fortfarande kan ändras.

### Söka efter resurser {#searching-assets}

Så här söker du efter en fil som du vill öppna på skrivbordet:

* Använd webbgränssnittet för AEM Resurser för att hitta resursen. Det är inte bara att söka i AEM Resurser som är kraftfulla (sökfunktioner, sparade sökningar), det innehåller också ytterligare funktioner för att hitta rätt resurs. Detta inkluderar ytterligare filter, som möjligheten att söka efter resurser baserat på status (godkännande, förfallodatum), samlingar, uppgifter, meddelanden och att dela mappar/samlingar med andra användare/grupper.
* När du har hittat resursen använder du Skrivbordsåtgärder i AEM-gränssnittet för att komma åt resursen på skrivbordet.

### Uppdatera resurser som har öppnats med AEM-skrivbordsappen {#updating-assets-opened-using-aem-desktop-app}

Om du redigerar en resurs direkt på den plats som mappas från AEM Assets till en lokal nätverksresurs, överförs resursen till AEM varje gång du sparar den på skrivbordet. Dessutom skapar AEM en version och skapar renderingar.

Om en resurs som lagras i AEM behöver uppdateras:

* För **mindre uppdateringar**, som mindre retuscheringsbegäranden i godkännandeprocessen:

   * Checka ut filen och öppna den på skrivbordet
   * Uppdatera filen
   * Spara den uppdaterade versionen. Resursen uppdateras och tidslinjen visar den ursprungliga versionen för jämförelse

* För **större uppdateringar**, till exempel en ändringsbegäran som kräver en liten kreativ PIA-cykel:

   * Använd alternativet Visa för att öppna lämplig mapp på skrivbordet
   * Kopiera filen till en Pågående arbete-mapp utanför den mappade AEM Resurser-resursen (kopiera till exempel filen till en mapp som synkroniserats med Adobe Creative Cloud-datorprogrammet)
   * Arbeta med filen och spara den regelbundet. Ändringarna sparas inte i AEM Resurser
   * När redigeringarna är klara flyttar, kopierar eller sparar du filen som mappats från AEM för att överföra den som en ny version

## Nätverksprestanda {#network-performance}

En bra upplevelse för användare som använder AEM-skrivbordsappen är i hög grad beroende av en bra, stabil nätverksanslutning mellan sina datorer och AEM-servern, samt av den server som är anpassad för höga prestanda, särskilt när det gäller att överföra och uppdatera resurser. Rekommendationerna är till för nätverks-/IT-team i organisationer.

### Nätverkshändelser {#network-considerations}

Information om de effektivaste strategierna för AEM Assets-nätverkskonfiguration finns i dokumentet [AEM Assets Network Considerations](https://docs.adobe.com/content/help/en/experience-manager-64/assets/administer/assets-migration-guide.html) . Några av de viktiga aspekter som hjälper användarna att optimera upplevelsen av AEM-skrivbordsappen är:

* **Använd korrekt konfigurerad Dispatcher:** Använd AEM Dispatcher för ytterligare säkerhet och se till att den är konfigurerad för [AEM-skrivbordsappsanslutning till AEM bakom en dispatcher](using.md)

* **Spara bandbredd:** Överväg att inaktivera förhandsvisning av ikoner i Finder på Mac - när du bläddrar i den monterade databasen med Finder. Finder begär att varje fil ska generera en förhandsgranskning och gör att skrivbordsappen hämtar och cachelagrar resursen lokalt. Observera att när du sparar bandbredd försämras även användarupplevelsen för användarna på skrivbordet, så det bör göras när du arbetar med databaser med stora resurser och/eller begränsad bandbredd.

>[!NOTE]
>
>Om du vill inaktivera förhandsvisning av ikoner går du till Visa i Finder, väljer Visningsalternativ och avmarkerar sedan alternativet &quot;Förhandsvisa ikon&quot;. Det här fungerar bara för den aktuella mappen. Om du vill göra den till standard klickar du på knappen Använd som standard i samma fönster.

### Optimera serverprestanda {#optimizing-server-performance}

Mer information om hur AEM Assets-servern ska optimeras för prestanda finns i [Prestandajusteringsguiden](https://docs.adobe.com/content/help/en/experience-manager-65/assets/administer/performance-tuning-guidelines.html)för AEM Assets. Några av de viktiga aspekterna av serverprestanda för AEM-skrivbordsappen är att optimera arbetsflödeskonfigurationen så att den fungerar bra för överföringar av resurser:

* **Uppladdning av resurser med högre prestanda:** Konfigurera arbetsflödesmodellen [AEM Asset Update så att den blir tillfällig](https://docs.adobe.com/content/help/en/experience-manager-65/assets/administer/performance-tuning-guidelines.html#Workflows).

* **Begränsa serverprocessor för överföringar:** Se till att parametern för maximala parallella arbetsflödesjobb är korrekt inställd så att överföringar inte tar bort hela processorn.
