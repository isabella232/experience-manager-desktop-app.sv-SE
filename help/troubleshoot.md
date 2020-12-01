---
title: Bästa tillvägagångssätt för och felsökning av Adobe Experience Manager-datorprogram
description: Följ bästa praxis och felsök för att lösa tillfälliga problem som rör installation, uppgradering, konfiguration och så vidare.
uuid: ce98a3e7-5454-41be-aaaa-4252b3e0f8dd
contentOwner: AG
products: SG_EXPERIENCEMANAGER/6.5/ASSETS, SG_EXPERIENCEMANAGER/6.4/ASSETS, SG_EXPERIENCEMANAGER/6.3/ASSETS
discoiquuid: f5eb222a-6cdf-4ae3-9cf2-755c873f397c
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 2893fc1f8aad02e1436a1a281a320e6837487220
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Felsök Adobe Experience Manager-datorprogrammet {#troubleshoot-v2}

Adobe Experience Manager-datorprogrammet ansluter till en DAM-databas (Digital Asset Management) för en fjärrdistribution i Experience Manager. Appen hämtar databasinformation och sökresultat på din dator, hämtar och överför filer och mappar och innehåller funktioner för att hantera konflikter med Assets-användargränssnittet.

Läs vidare för att felsöka appen, lära dig de bästa metoderna och ta reda på begränsningarna.

## God praxis {#best-practices-to-prevent-troubles}

Följ följande metodtips för att förebygga vissa vanliga problem och felsökning.

* **Lär dig hur datorprogrammet fungerar**: Innan du börjar använda programmet bör du ägna en stund åt att veta hur programmet fungerar. Lär dig mer om att länka mellan Experience Manager webbgränssnitt och stationära datorer, mappning av databaser, cachelagring av resurser, spara lokalt och ladda upp i bakgrunden. Se [hur det fungerar](release-notes.md#how-app-works).

* **Undvik tecken som inte stöds i mappnamn**: Använd inte blanksteg eller ogiltiga tecken när du skapar eller överför mappar. Se en lista med tecken på [Skapa mappar i Experience Manager Resurser](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/manage-assets.html#creating-folders). Vissa Adobe Experience Manager-exempel kan påverkas av tecken i mappnamnet som inte stöds.

* **Bästa tillvägagångssätt för att undvika konflikter**: Information om hur du undviker potentiella konflikter när du samarbetar med flera resurser finns i  [Undvik redigeringskonflikter](using.md#adv-workflow-collaborate-avoid-conflicts).

* **Använd mappöverföring för stora, hierarkiska mappar**: I stället för att använda webbgränssnittet Resurser eller andra metoder kan du överföra stora mappar med datorprogrammet Experience Manager. Programmet överför resurserna i bakgrunden med loggning och övervakning. Se [massöverföring av resurser](using.md#bulk-upload-assets).

* **Använd den senaste versionen**: Använd den senaste programversionen och kontrollera alltid om den är kompatibel innan du installerar en ny programversion eller innan du uppgraderar till en nyare Adobe Experience Manager-version. Se [versionsinformation](release-notes.md).

* **Använd samma enhetsbeteckning**: Använd samma enhetsbeteckning i en hel organisation för att mappa till Adobe Experience Manager DAM. Om du vill visa resurser som placerats av andra användare måste sökvägarna vara desamma. Om du använder samma enhetsbeteckning säkerställs en konstant sökväg till DAM-resurser. Resurserna förblir placerade och tas inte bort även om olika enhetsbeteckningar används av olika användare.

* **Lägg märke till nätverket**: Nätverksprestanda är avgörande för prestandan i Experience Manager-datorprogrammet. Om du får ett långsammare svar på filöverföringar eller större åtgärder inaktiverar du de funktioner eller program som kan orsaka mycket nätverkstrafik.

* **Användningsexempel som inte stöds för datorprogrammet**: Använd inte appen för Assets&#39; migrering (den kräver planering och andra verktyg). för krävande DAM-åtgärder (som att flytta stora mappar, stora överföringar, hitta filer med avancerade metadatasökningar), och som en synkroniseringsklient (designprinciper och användningsmönster skiljer sig från synkroniserade klienter som Microsoft OneDrive eller Adobe Creative Cloud desktop sync).

* **Timeout**: För närvarande har skrivbordsprogrammet inte något konfigurerbart timeout-värde som kopplar från anslutningen mellan Experience Manager-servern och skrivbordsappen efter ett fast tidsintervall. När du överför stora resurser, och anslutningen får timeout efter en stund, försöker programmet överföra resursen några gånger genom att öka tidsgränsen för överföring. Det finns inget rekommenderat sätt att ändra standardinställningarna för timeout.

## Felsöka {#troubleshooting-prep}

Om du vill felsöka problem med skrivbordsprogram bör du känna till följande information. Dessutom får du hjälp att förmedla problemen bättre till Adobe kundtjänst om du väljer att söka support.

### Plats för loggfiler {#check-log-files-v2}

[!DNL Experience Manager] loggfilerna sparas på följande platser beroende på operativsystemet:

I Windows: `%LocalAppData%\Adobe\AssetsCompanion\Logs`

Mac: `~/Library/Logs/Adobe\ Experience\ Manager\ Desktop`

Om det inte går att överföra vissa filer läser du i `backend.log`-filen för att identifiera misslyckade överföringar när du överför många resurser.

>[!NOTE]
>
>När du arbetar med kundtjänst på Adobe på en supportförfrågan eller ett supportärende kan du bli ombedd att dela loggfilerna för att hjälpa kundtjänstteamet att förstå problemet. Arkivera hela `Logs`-mappen och dela den med kundtjänst.

### Ändra detaljnivå i loggfiler {#level-of-details-in-log}

Så här ändrar du detaljnivån i loggfiler:

1. Kontrollera att programmet inte körs.

1. I Windows:

   1. Öppna ett kommandofönster.

   1. Starta [!DNL Adobe Experience Manager]-datorprogrammet genom att köra kommandot:

   ```shell
   set AEM_DESKTOP_LOG_LEVEL=DEBUG&"C:\Program Files\Adobe\Adobe Experience Manager Desktop.exe
   ```

   På Mac:

   1. Öppna ett terminalfönster.

   1. Starta [!DNL Adobe Experience Manager]-datorprogrammet genom att köra kommandot:

   ```shell
   AEM_DESKTOP_LOG_LEVEL=DEBUG open /Applications/Adobe\ Experience\ Manager\ Desktop.app
   ```

Giltiga loggnivåer är DEBUG, INFO, WARN eller ERROR. Loggarnas utförlighet är högst i DEBUG och lägst i FEL.

### Aktivera felsökningsläge {#enable-debug-mode}

Om du vill felsöka kan du aktivera felsökningsläget och få mer information i loggarna.

>[!NOTE]
>
>Giltiga loggnivåer är DEBUG, INFO, WARN och ERROR. Loggarnas utförlighet är högst i DEBUG och lägst i FEL.

Så här använder du programmet i felsökningsläge på Mac:

1. Öppna ett terminalfönster eller en kommandotolk.

1. Starta [!DNL Experience Manager]-datorprogrammet genom att köra följande kommando:

   `AEM_DESKTOP_LOG_LEVEL=DEBUG open /Applications/Adobe\ Experience\ Manager\ Desktop.app`.

Så här aktiverar du felsökningsläge i Windows:

1. Öppna ett kommandofönster.

1. Starta [!DNL Experience Manager]-datorprogrammet genom att köra följande kommando:

`AEM_DESKTOP_LOG_LEVEL=DEBUG&"C:\Program Files\Adobe\Adobe Experience Manager Desktop.exe`.

### Rensa cache {#clear-cache-v2}

Utför följande steg:

1. Starta programmet och anslut en Experience Manager-instans.

1. Öppna programmets inställningar genom att klicka på ellipserna i det övre högra hörnet och välja [!UICONTROL Preferences].

1. Leta reda på posten som visar [!UICONTROL Current Cache Size]. Klicka på papperskorgsikonen bredvid det här elementet.

Om du vill rensa cachen manuellt fortsätter du med stegen nedan.

>[!CAUTION]
>
>Detta kan vara en destruktiv åtgärd. Om det finns lokala filändringar som inte har överförts till [!DNL Adobe Experience Manager], kommer dessa ändringar att gå förlorade om du fortsätter.

Cacheminnet rensas genom att programmets cachekatalog, som finns i programmets inställningar, tas bort.

1. Starta programmet.

1. Öppna programmets inställningar genom att markera ellipserna i det övre högra hörnet och välja [!UICONTROL Preferences].

1. Observera [!UICONTROL Cache Directory]-värdet.

   I den här katalogen finns det underkataloger som heter efter de kodade slutpunkterna [!DNL Adobe Experience Manager]. Namnen är en kodad version av målwebbadressen [!DNL Adobe Experience Manager]. Om programmet till exempel har `localhost:4502` som mål blir katalognamnet `localhost_4502`.

Om du vill rensa cachen tar du bort den kodade katalogen [!DNL Adobe Experience Manager] Endpoint. Om du tar bort hela katalogen som anges i inställningarna rensas cachen för alla instanser som har använts av programmet.

Att rensa cacheminnet för [!DNL Adobe Experience Manager]-skrivbordsappen är en preliminär felsökningsåtgärd som kan lösa flera problem. Rensa cacheminnet från appinställningarna. Se [ange inställningar](install-upgrade.md#set-preferences). Standardplatsen för cachemappen är:

### Lär dig [!DNL Adobe Experience Manager]-versionen av skrivbordsappen {#know-app-version-v2}

Så här ser du versionsnumret:

1. Starta programmet.

1. Klicka på ellipserna i det övre högra hörnet, hovra över [!UICONTROL Help] och klicka sedan på [!UICONTROL About].

   Versionsnumret visas på den här skärmen.

### Kan inte se placerade resurser {#placed-assets-missing}

Om du inte kan se de resurser som du eller andra kreatörer har placerat i supportfilerna (till exempel INDD-filer) ska du kontrollera följande:

* Anslutning till servern. Smidig nätverksanslutning kan stoppa hämtningar av resurser.

* Filstorlek. Stora resurser tar längre tid att hämta och visa.

* Enhetliga brev. Om du eller någon annan medarbetare placerade resurserna när du mappade Experience Manager DAM till en annan enhetsbeteckning visas inte de placerade resurserna.

* Behörigheter. Kontakta Experience Manager-administratören om du har behörighet att hämta de placerade resurserna.

### Redigeringar av filer i skrivbordsappens användargränssnitt återspeglas inte direkt i [!DNL Adobe Experience Manager] {#changes-on-da-not-visible-on-aem}

[!DNL Adobe Experience Manager] när alla redigeringar av en fil är slutförda. Beroende på storleken och komplexiteten hos en fil tar det lång tid att överföra den nya versionen av en fil tillbaka till [!DNL Adobe Experience Manager]. Programdesignen kräver att så många gånger som en fil överförs fram och tillbaka ska minimeras, i stället för att gissa när redigeringarna är klara och överförs automatiskt. Vi rekommenderar att användaren initierar överföringen av filen tillbaka till [!DNL Adobe Experience Manager] genom att välja att överföra en fils ändringar.

### Problem vid uppgradering på macOS {#issues-when-upgrading-on-macos}

Ibland kan problem uppstå när du uppgraderar datorprogrammet Experience Manager på macOS. Detta orsakas av att det inte går att läsa in nya versioner av datorprogrammet Experience Manager korrekt i en äldre systemmapp för Experience Manager. Följande mappar och filer kan tas bort manuellt för att åtgärda problemet.

Innan du utför följande steg drar du `Adobe Experience Manager Desktop`-programmet från mappen macOS-program till Papperskorgen. Öppna sedan terminalen, kör följande kommando och ange ditt lösenord när du uppmanas till det.

```shell
sudo rm -rf ~/Library/Application\ Support/com.adobe.aem.desktop
sudo rm -rf ~/Library/Preferences/com.adobe.aem.desktop.plist
sudo rm -rf ~/Library/Logs/Adobe\ Experience\ Manager\ Desktop

sudo find /var/folders -type d -name "com.adobe.aem.desktop" | xargs rm -rf
sudo find /var/folders -type d -name "com.adobe.aem.desktop.finderintegration-plugin" | xargs rm -rf
```

### Det går inte att överföra filer {#upload-fails}

Om du använder datorprogrammet med Experience Manager 6.5.1 eller senare, uppgraderar du S3- eller Azure-anslutningen till version 1.10.4 eller senare. Det åtgärdar ett filöverföringsfel relaterat till [OAK-8599](https://issues.apache.org/jira/browse/OAK-8599). Se [installationsanvisningar](install-upgrade.md#install-v2).

### [!DNL Experience Manager] anslutningsproblem för skrivbordsprogram  {#connection-issues}

Om du har allmänna anslutningsproblem kan du få mer information om vad [!DNL Experience Manager]-datorprogrammet gör.

**Kontrollera begärandeloggen**

[!DNL Experience Manager] skrivbordsappen loggar alla begäranden som skickas, tillsammans med varje begärandes svarskod, i en dedikerad loggfil.

1. Öppna `request.log` i programmets loggkatalog för att se dessa begäranden.

1. Varje rad i loggen representerar antingen en begäran eller ett svar. Förfrågningar kommer att ha ett `>`-tecken följt av den URL som begärdes. Svaren kommer att ha ett `<`-tecken följt av svarskoden och den URL som begärdes. Begäranden och svar kan matchas med varje rads GUID.

**Kontrollera förfrågningar som lästs in av programmets inbäddade webbläsare**

En majoritet av programmets begäranden finns i begärandeloggen. Men om det inte finns någon användbar information där kan det vara användbart att undersöka de förfrågningar som skickas av programmets inbäddade webbläsare.
Se [SAML-avsnittet](#da-connection-issue-with-saml-aem) för instruktioner om hur du visar dessa begäranden.

#### SAML-inloggningsautentiseringen fungerar inte {#da-connection-issue-with-saml-aem}

Om [!DNL Experience Manager]-datorprogrammet inte ansluter till din SAML-aktiverade (SSO-enabled) [!DNL Adobe Experience Manager]-instans kan du felsöka i det här avsnittet. SSO-processer är olika, ibland komplexa, och programmets design gör sitt bästa för att hantera den här typen av anslutningar. Vissa inställningar kräver dock ytterligare felsökning.

Ibland dirigeras SAML-processen inte tillbaka till den ursprungligen begärda sökvägen, eller så dirigeras den till en annan värd än den som är konfigurerad i [!DNL Adobe Experience Manager]-datorprogrammet. Så här kontrollerar du att så inte är fallet:

1. Öppna en webbläsare. Åtkomst till URL:en `https://[aem_server]:[port]/content/dam.json`.

1. Logga in på [!DNL Adobe Experience Manager]-distributionen.

1. När inloggningen är klar tittar du på webbläsarens aktuella adress i adressfältet. Den ska exakt matcha den URL som ursprungligen angavs.

1. Kontrollera också att allt före `/content/dam.json` matchar det målvärde som konfigurerats i [!DNL Adobe Experience Manager]-inställningarna för skrivbordsappen.[!DNL Adobe Experience Manager]

**SAML-inloggningsprocessen fungerar korrekt enligt ovanstående steg, men användarna kan fortfarande inte logga in**

Fönstret i [!DNL Adobe Experience Manager]-datorprogrammet som visar inloggningsprocessen är bara en webbläsare som visar målinstansens webbanvändargränssnitt:[!DNL Adobe Experience Manager]

* Mac-versionen använder en [WebView](https://developer.apple.com/documentation/webkit/webview).

* I Windows-versionen används Chromium-baserad [CefSharp](https://cefsharp.github.io/).

Kontrollera att SAML-processen har stöd för dessa webbläsare.

Om du vill felsöka ytterligare kan du visa de exakta URL:er som webbläsaren försöker läsa in. Om du vill se den här informationen:

1. Följ instruktionerna för att starta programmet i [felsökningsläge](#enable-debug-mode).

1. Återskapa inloggningsförsöket.

1. Navigera till [loggkatalogen](#check-log-files-v2) för programmet

1. För Windows:

   1. Öppna&quot;aemcompanionlog.txt&quot;.

   1. Sök efter meddelanden som börjar med &quot;Inloggningsläsarens adress ändrad till&quot;. Dessa poster innehåller även den URL som programmet har läst in.

   För Mac:

   1. `com.adobe.aem.desktop-nnnnnnnn-nnnnnn.log`, där den  **** ersätts med det nummer som finns i det senaste filnamnet.

   1. Sök efter meddelanden som börjar med&quot;inläst bildruta&quot;. Dessa poster innehåller även den URL som programmet har läst in.


Om du tittar på den URL-sekvens som läses in kan det hjälpa till att felsöka i SAML:s slut för att avgöra vad som är fel.

#### SSL-konfigurationsproblem {#ssl-config-v2}

Biblioteken som Experience Manager datorprogram använder för HTTP-kommunikation använder strikt SSL-kontroll. Ibland kan en anslutning fungera med en webbläsare, men misslyckas med att använda datorprogrammet Experience Manager. Installera det saknade mellanliggande certifikatet i Apache om du vill konfigurera SSL korrekt. Se [Installera ett mellanliggande CA-certifikat i Apache](https://access.redhat.com/solutions/43575).

De bibliotek som används för HTTP-kommunikation i Experience Manager Desktop använder strikt SSL-tillämpning. Det kan alltså finnas instanser där SSL-anslutningar som lyckas via en webbläsare misslyckas med [!DNL Adobe Experience Manager]-skrivbordsappen. Detta är bra eftersom det uppmuntrar till korrekt konfigurering av SSL och ökar säkerheten, men det kan vara frustrerande när programmet inte kan ansluta.

I det här fallet rekommenderar vi att du använder ett verktyg för att analysera serverns SSL-certifikat och identifiera problem så att de kan korrigeras. Det finns webbplatser som inspekterar serverns certifikat när de tillhandahåller URL:en.

Som en tillfällig åtgärd är det möjligt att inaktivera strikt SSL-tvång i [!DNL Adobe Experience Manager]-datorprogrammet. Detta är inte en rekommenderad långsiktig lösning eftersom den minskar säkerheten genom att dölja grundorsaken till felaktigt konfigurerad SSL. Så här inaktiverar du strikt tvingande:

1. Använd valfri redigerare för att redigera programmets JavaScript-konfigurationsfil, som finns (som standard) på följande platser (beroende på operativsystem):

   Mac: `/Applications/Adobe Experience Manager Desktop.app/Contents/Resources/javascript/lib-smb/config.json`

   I Windows: `C:\Program Files (x86)\Adobe\Adobe Experience Manager Desktop\javascript\config.json`

1. Leta reda på följande avsnitt i filen:

   ```shell
   ...
   "assetRepository": {
       "options": {
   ...
   ```

1. Ändra avsnittet genom att lägga till `"strictSSL": false` enligt följande:

   ```shell
   ...
   "assetRepository": {
       "options": {
           "strictSSL": false,
   ...
   ```

1. Spara filen och starta om [!DNL Adobe Experience Manager]-datorprogrammet.

### Appen svarar inte {#unresponsive}

I vissa fall kan programmet inte svara, bara visa en vit skärm eller visa ett fel längst ned i gränssnittet utan några alternativ i gränssnittet. Prova följande i den ordning du vill:

* Högerklicka på programgränssnittet och klicka på **[!UICONTROL Refresh]**.
* Avsluta programmet och öppna det igen.

I båda metoderna startar programmet i rotmappen DAM.

<!--
### Need additional help with [!DNL Experience Manager] desktop app {#additional-help}

Create Jira ticket with the following information:

* Use `DAM - Companion App` as the [!UICONTROL Component].

* Detailed steps to reproduce the issue in [!UICONTROL Description].

* DEBUG level logs that were captured while reproducing the issue.

* Target Experience Manager version.

* Operating system version.

* [!DNL Adobe Experience Manager] desktop app version. To know your app version, see [finding the desktop app version](#know-app-version-v2).
-->

>[!MORELIKETHIS]
>
>* [Kända fel](release-notes.md#known-issues-v2)
>* [Undvik redigeringskonflikter](using.md#adv-workflow-collaborate-avoid-conflicts)

