---
title: Bästa tillvägagångssätt för och felsökning [!DNL Adobe Experience Manager] datorprogram
description: Följ bästa praxis och felsök för att lösa tillfälliga problem som rör installation, uppgradering, konfiguration och så vidare.
exl-id: f388e4ac-907d-4093-ba6f-86ecdafeb015
source-git-commit: 2c846fb9cd82691f6439e93429dffcca8127ba68
workflow-type: tm+mt
source-wordcount: '2260'
ht-degree: 0%

---

# Felsökning [!DNL Adobe Experience Manager] datorprogram {#troubleshoot-v2}

[!DNL Adobe Experience Manager] datorprogrammet ansluter till en [!DNL Experience Manager] DAM-databasen (Digital Asset Management). Appen hämtar databasinformation och sökresultat på din dator, hämtar och överför filer och mappar och innehåller funktioner för att hantera konflikter med Assets-användargränssnittet.

Läs vidare för att felsöka appen, lära dig de bästa metoderna och ta reda på begränsningarna.

## God praxis {#best-practices-to-prevent-troubles}

Följ följande metodtips för att förebygga vissa vanliga problem och felsökning.

* **Förstå hur datorprogrammet fungerar**: Innan du börjar använda programmet bör du ägna en stund åt att veta hur programmet fungerar. Lär dig mer om länkar mellan [!DNL Experience Manager] webbgränssnitt och datorer, databasmappning, resurscachning, spara lokalt och ladda upp i bakgrunden. Se [hur det fungerar](release-notes.md#how-app-works).

* **Undvik tecken som inte stöds i mappnamn**: Använd inte blanksteg eller ogiltiga tecken när du skapar eller överför mappar. Se en lista med tecken på [Skapa mappar i [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/manage-assets.html#creating-folders). Några [!DNL Experience Manager] fall kan påverkas av tecken som inte stöds i mappnamnet.

* **Bästa tillvägagångssätt för att undvika konflikter**: Information om hur du undviker potentiella konflikter när du samarbetar med flera resurser finns i [undvika redigeringskonflikter](using.md#adv-workflow-collaborate-avoid-conflicts).

* **Använd mappöverföring för stora, hierarkiska mappar**: I stället för att använda webbgränssnittet Resurser eller andra metoder använder du [!DNL Experience Manager] för att överföra stora mappar. Programmet överför resurserna i bakgrunden med loggning och övervakning. Se [massöverföring av resurser](using.md#bulk-upload-assets).

* **Använd den senaste versionen**: Använd den senaste programversionen och kontrollera alltid om den är kompatibel innan du installerar en ny programversion eller innan du uppgraderar till en nyare [!DNL Experience Manager] version. Se [versionsinformation](release-notes.md).

* **Använd samma enhetsbeteckning**: Använd samma enhetsbeteckning i en organisation för att mappa till [!DNL Experience Manager] DAM. Om du vill visa resurser som placerats av andra användare måste sökvägarna vara desamma. Om du använder samma enhetsbeteckning säkerställs en konstant sökväg till DAM-resurser. Resurserna förblir placerade och tas inte bort även om olika enhetsbeteckningar används av olika användare.

* **Lägg märke till nätverket**: Nätverksprestanda är avgörande för [!DNL Experience Manager] datorprogrammets prestanda. Om du får ett långsammare svar på filöverföringar eller större åtgärder inaktiverar du de funktioner eller program som kan orsaka mycket nätverkstrafik.

* **Användningsexempel som inte stöds för datorprogrammet**: Använd inte appen för Assets&#39; migrering (den kräver planering och andra verktyg). för krävande DAM-åtgärder (som att flytta stora mappar, stora överföringar, hitta filer med avancerade metadatasökningar), och som en synkroniseringsklient (designprinciper och användningsmönster skiljer sig från synkroniserade klienter som Microsoft OneDrive eller Adobe Creative Cloud desktop sync).

* **Timeout**: För närvarande har skrivbordsprogrammet inte något konfigurerbart timeout-värde som kopplar från anslutningen mellan [!DNL Experience Manager] efter ett fast tidsintervall. När du överför stora resurser, och anslutningen får timeout efter en stund, försöker programmet överföra resursen några gånger genom att öka tidsgränsen för överföring. Det finns inget rekommenderat sätt att ändra standardinställningarna för timeout.

## Felsöka {#troubleshooting-prep}

Om du vill felsöka problem med skrivbordsprogram bör du känna till följande information. Ni kan också bättre informera Adobe kundsupport om ni väljer att söka support.

### Plats för loggfiler {#check-log-files-v2}

[!DNL Experience Manager] loggfilerna sparas på följande platser beroende på operativsystemet:

I Windows: `%LocalAppData%\Adobe\AssetsCompanion\Logs`

På Mac: `~/Library/Logs/Adobe\ Experience\ Manager\ Desktop`

Om det inte går att överföra vissa filer när du överför många resurser finns mer information i `backend.log` för att identifiera misslyckade överföringar.

>[!NOTE]
>
>När du arbetar med Adobe kundsupport på en supportförfrågan eller ett supportärende kan du bli ombedd att dela loggfilerna för att hjälpa kundsupportteamet att förstå problemet. Arkivera hela `Logs` och dela den med kundsupporten.

### Ändra detaljnivå i loggfiler {#level-of-details-in-log}

Så här ändrar du detaljnivån i loggfiler:

1. Kontrollera att programmet inte körs.

1. I Windows:

   1. Öppna ett kommandofönster.

   1. Starta [!DNL Adobe Experience Manager] genom att köra kommandot:

   ```shell
   set AEM_DESKTOP_LOG_LEVEL=DEBUG&"C:\Program Files\Adobe\Adobe Experience Manager Desktop.exe
   ```

   På Mac:

   1. Öppna ett terminalfönster.

   1. Starta [!DNL Adobe Experience Manager] genom att köra kommandot:

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

1. Starta [!DNL Experience Manager] genom att köra följande kommando:

   `AEM_DESKTOP_LOG_LEVEL=DEBUG open /Applications/Adobe\ Experience\ Manager\ Desktop.app`.

Så här aktiverar du felsökningsläge i Windows:

1. Öppna ett kommandofönster.

1. Starta [!DNL Experience Manager] genom att köra följande kommando:

`AEM_DESKTOP_LOG_LEVEL=DEBUG&"C:\Program Files\Adobe\Adobe Experience Manager Desktop.exe`.

### Lär känna [!DNL Adobe Experience Manager] datorprogramversion {#know-app-version-v2}

Så här ser du versionsnumret:

1. Starta programmet.

1. Klicka på ellipserna i det övre högra hörnet och hovra över [!UICONTROL Help]och sedan klicka [!UICONTROL About].

   Versionsnumret visas på den här skärmen.

### Rensa cache {#clear-cache-v2}

Utför följande steg:

1. Starta programmet och anslut [!DNL Experience Manager] -instans.

1. Öppna programmets inställningar genom att klicka på ellipserna i det övre högra hörnet och välja [!UICONTROL Preferences].

1. Leta reda på posten som visar [!UICONTROL Current Cache Size]. Klicka på papperskorgsikonen bredvid det här elementet.

Om du vill rensa cachen manuellt fortsätter du med stegen nedan.

>[!CAUTION]
>
>Detta kan vara en destruktiv åtgärd. Om det finns lokala filändringar som inte har överförts till [!DNL Adobe Experience Manager]kommer dessa ändringar att gå förlorade om du fortsätter.

Cacheminnet rensas genom att programmets cachekatalog, som finns i programmets inställningar, tas bort.

1. Starta programmet.

1. Öppna programmets inställningar genom att markera ellipserna i det övre högra hörnet och välja [!UICONTROL Preferences].

1. Anteckna [!UICONTROL Cache Directory] värde.

   I den här katalogen finns det underkataloger namngivna efter den kodade [!DNL Adobe Experience Manager] Slutpunkter. Namnen är en kodad version av målversionen [!DNL Adobe Experience Manager] URL. Om programmet till exempel har som mål `localhost:4502` så blir katalognamnet `localhost_4502`.

Om du vill rensa cachen tar du bort den kodade [!DNL Adobe Experience Manager] Slutpunktskatalog. Om du tar bort hela katalogen som anges i inställningarna rensas cachen för alla instanser som har använts av programmet.

Rensar [!DNL Adobe Experience Manager] datorprogrammets cache är en preliminär felsökningsåtgärd som kan lösa flera problem. Rensa cacheminnet från appinställningarna. Se [ange inställningar](install-upgrade.md#set-preferences). Standardplatsen för cachemappen är:

## Kan inte se placerade resurser {#placed-assets-missing}

Om du inte kan se de resurser som du eller andra kreatörer har placerat i supportfilerna (till exempel INDD-filer) ska du kontrollera följande:

* Anslutning till servern. Smidig nätverksanslutning kan stoppa hämtningar av resurser.

* Filstorlek. Stora resurser tar längre tid att hämta och visa.

* Enhetliga brev. Om du eller någon annan medarbetare placerade resurserna när de mappade [!DNL Experience Manager] DAM till en annan enhetsbeteckning visas inte de placerade resurserna.

* Behörigheter. Om du vill kontrollera om du har behörighet att hämta de placerade resurserna kontaktar du [!DNL Experience Manager] administratör.

### Redigeringar av filer i datorprogrammets användargränssnitt återspeglas inte i [!DNL Adobe Experience Manager] omedelbart {#changes-on-da-not-visible-on-aem}

[!DNL Adobe Experience Manager] när alla redigeringar av en fil är slutförda. Beroende på filens storlek och komplexitet tar det lång tid att överföra den nya versionen av filen tillbaka till [!DNL Adobe Experience Manager]. Programdesignen kräver att så många gånger som en fil överförs fram och tillbaka ska minimeras, i stället för att gissa när redigeringarna är klara och överförs automatiskt. Vi rekommenderar att användaren initierar överföringen av filen tillbaka till [!DNL Adobe Experience Manager] genom att välja att överföra en fils ändringar.

### Problem vid uppgradering till macOS {#issues-when-upgrading-on-macos}

Ibland kan problem uppstå vid uppgradering [!DNL Experience Manager] datorprogram på macOS. Detta orsakas av en äldre systemmapp för [!DNL Experience Manager] datorprogram förhindrar nya versioner av [!DNL Experience Manager] för att läsas in korrekt. Följande mappar och filer kan tas bort manuellt för att åtgärda problemet.

Innan du utför följande steg drar du `Adobe Experience Manager Desktop` från macOS-programmappen till papperskorgen. Öppna sedan terminalen, kör följande kommando och ange ditt lösenord när du uppmanas till det.

```shell
sudo rm -rf ~/Library/Application\ Support/com.adobe.aem.desktop
sudo rm -rf ~/Library/Preferences/com.adobe.aem.desktop.plist
sudo rm -rf ~/Library/Logs/Adobe\ Experience\ Manager\ Desktop

sudo find /var/folders -type d -name "com.adobe.aem.desktop" | xargs rm -rf
sudo find /var/folders -type d -name "com.adobe.aem.desktop.finderintegration-plugin" | xargs rm -rf
```

## Kan inte överföra filer {#upload-fails}

Om du använder datorprogrammet med [!DNL Experience Manager] 6.5.1 eller senare, uppgradera S3- eller Azure-anslutning till version 1.10.4 eller senare. Det åtgärdar ett problem med filöverföringsfel relaterat till [OAK-8599](https://issues.apache.org/jira/browse/OAK-8599). Se [installationsanvisningar](install-upgrade.md#install-v2).

## [!DNL Experience Manager] anslutningsproblem för skrivbordsprogram {#connection-issues}

Om du har problem med allmänna anslutningsmöjligheter kan du få mer information om vad [!DNL Experience Manager] det går för skrivbordsappen.

**Kontrollera begärandeloggen**

[!DNL Experience Manager] skrivbordsappen loggar alla begäranden som skickas, tillsammans med varje begärandes svarskod, i en dedikerad loggfil.

1. Öppna `request.log` i programmets loggkatalog för att se dessa begäranden.

1. Varje rad i loggen representerar antingen en begäran eller ett svar. Begäranden har `>` följt av den URL som begärdes. Svaren har en `<` följt av svarskoden och den URL som begärdes. Begäranden och svar kan matchas med varje rads GUID.

**Kontrollera förfrågningar som lästs in av programmets inbäddade webbläsare**

En majoritet av programmets begäranden finns i begärandeloggen. Men om det inte finns någon användbar information där kan det vara användbart att undersöka de förfrågningar som skickas av programmets inbäddade webbläsare.
Se [SAML-avsnitt](#da-connection-issue-with-saml-aem) om du vill ha anvisningar om hur du visar dessa förfrågningar.

### SAML-inloggningsautentisering fungerar inte {#da-connection-issue-with-saml-aem}

[!DNL Experience Manager] skrivbordsappen kan inte ansluta till din SSO-aktiverade (SAML) [!DNL Adobe Experience Manager] distribution. Programmets design används för att anpassa variationerna och komplexiteten i SSO-anslutningar och processer. En installation kan dock kräva ytterligare felsökning.

Ibland dirigeras SAML-processen inte tillbaka till den ursprungligen begärda sökvägen eller så är den slutliga omdirigeringen till en annan värd än den som konfigurerats i [!DNL Adobe Experience Manager] datorprogram. Så här kontrollerar du att så inte är fallet:

1. Öppna en webbläsare. Åtkomst `https://[aem_server]:[port]/content/dam.json` URL.

1. Logga in på [!DNL Adobe Experience Manager] distribution.

1. När inloggningen är klar tittar du på webbläsarens aktuella adress i adressfältet. Den ska exakt matcha den URL som ursprungligen angavs.

1. Verifiera också att allt förut `/content/dam.json` matchar målet [!DNL Adobe Experience Manager] värde konfigurerat i [!DNL Adobe Experience Manager] datorprogrammets inställningar.

**SAML-inloggningsprocessen fungerar korrekt enligt ovanstående steg, men användarna kan fortfarande inte logga in**

Fönstret inuti [!DNL Adobe Experience Manager] datorprogrammet som visar inloggningsprocessen är helt enkelt en webbläsare som visar målet [!DNL Adobe Experience Manager] instansens webbanvändargränssnitt:

* I Mac-versionen används en [WebView](https://developer.apple.com/documentation/webkit/webview).

* Windows-versionen använder Chromium-baserad [CefSharp](https://cefsharp.github.io/).

Kontrollera att SAML-processen har stöd för dessa webbläsare.

Om du vill felsöka ytterligare kan du visa de exakta URL:er som webbläsaren försöker läsa in. Om du vill se den här informationen:

1. Följ instruktionerna för att starta programmet i [felsökningsläge](#enable-debug-mode).

1. Återskapa inloggningsförsöket.

1. Navigera till [loggkatalog](#check-log-files-v2) av programmet

1. För Windows:

   1. Öppna&quot;aemcompanionlog.txt&quot;.

   1. Sök efter meddelanden som börjar med &quot;Inloggningsläsarens adress ändrad till&quot;. Dessa poster innehåller även den URL som programmet har läst in.

   För Mac:

   1. `com.adobe.aem.desktop-nnnnnnnn-nnnnnn.log`, där **n** ersätts med de tal som finns i det senaste filnamnet.

   1. Sök efter meddelanden som börjar med&quot;inläst bildruta&quot;. Dessa poster innehåller även den URL som programmet har läst in.


Om du tittar på den URL-sekvens som läses in kan det hjälpa till att felsöka i SAML:s slut för att avgöra vad som är fel.

### SSL-konfigurationsproblem {#ssl-config-v2}

Biblioteken som [!DNL Experience Manager] datorprogram som använder för HTTP-kommunikation använder strikt SSL-kontroll. Ibland kan en anslutning fungera med en webbläsare, men misslyckas med att använda [!DNL Experience Manager] datorprogram. Installera det saknade mellanliggande certifikatet i Apache om du vill konfigurera SSL korrekt. Se [Installera ett mellanliggande CA-certifikat i Apache](https://access.redhat.com/solutions/43575).

Biblioteken som [!DNL Experience Manager] datorprogrammet använder för HTTP-kommunikation med strikt SSL-kontroll. Det kan därför finnas tillfällen då SSL-anslutningar som lyckas via en webbläsare misslyckas med [!DNL Adobe Experience Manager] datorprogram. Detta är bra eftersom det uppmuntrar till korrekt konfigurering av SSL och ökar säkerheten, men det kan vara frustrerande när programmet inte kan ansluta.

I det här fallet rekommenderar vi att du använder ett verktyg för att analysera serverns SSL-certifikat och identifiera problem så att de kan korrigeras. Det finns webbplatser som inspekterar serverns certifikat när de tillhandahåller URL:en.

Som en tillfällig åtgärd är det möjligt att inaktivera strikta SSL-kontroller i [!DNL Adobe Experience Manager] datorprogram. Detta är inte en rekommenderad långsiktig lösning eftersom den minskar säkerheten genom att dölja grundorsaken till felaktigt konfigurerad SSL. Så här inaktiverar du strikt tvingande:

1. Använd valfri redigerare för att redigera programmets JavaScript-konfigurationsfil, som finns (som standard) på följande platser (beroende på operativsystem):

   På Mac: `/Applications/Adobe Experience Manager Desktop.app/Contents/Resources/javascript/lib-smb/config.json`

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

1. Spara filen och starta om [!DNL Adobe Experience Manager] datorprogram.

### Inloggningsproblem vid växling till en annan server {#cannot-login-cookies-issue}

Efter användning av [!DNL Experience Manager] när du försöker ändra anslutningen till en annan server kan du råka ut för inloggningsproblem. Det beror på att gamla cookies stör den nya autentiseringen. Ett alternativ på huvudmenyn för att [!UICONTROL Clear Cookies] hjälper. Logga ut från den aktuella sessionen i appen och välj [!UICONTROL Clear Cookies] innan du fortsätter att ansluta.

![Rensa cookies när du byter server](assets/main_menu_logout_da2.png)

## Appen svarar inte {#unresponsive}

I vissa fall kan programmet inte svara, bara visa en vit skärm eller visa ett fel längst ned i gränssnittet utan några alternativ i gränssnittet. Prova följande i den ordning du vill:

* Högerklicka på programgränssnittet och klicka **[!UICONTROL Refresh]**.
* Avsluta programmet och öppna det igen.

I båda metoderna startar programmet i rotmappen DAM.

## Dölj utgångna resurser {#hide-expired-assets}

När du bläddrar bland resurser inifrån [!DNL Experience Manager] de utgångna resurserna visas inte i användargränssnittet. Administratörer kan göra följande konfiguration för att förhindra att resurser som har gått ut visas, söks och hämtas när de bläddrar bland resurser från skrivbordsappen och Asset Link. Konfigurationen fungerar för alla användare, oavsett administratörsbehörighet.

* [Konfiguration i Experience Manager 6.5 för att dölja förfallna resurser](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/manage-assets.html#hide-expired-assets-via-acp-api).
* [Konfiguration i Experience Manager as a Cloud Service för att dölja utgångna resurser](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/manage/manage-digital-assets.html#hide-expired-assets-via-acp-api).

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

