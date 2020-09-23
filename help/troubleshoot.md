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
source-git-commit: 6a8a49865d2707f5d60fbd6d5e99b597c333d3d5
workflow-type: tm+mt
source-wordcount: '1242'
ht-degree: 0%

---


# Felsöka Adobe Experience Manager-datorprogrammet {#troubleshoot-v2}

Adobe Experience Manager (AEM) datorprogram ansluter till en fjärransluten Experience Manager-driftsättnings DAM-databas (Digital Asset Management). Appen hämtar databasinformation och sökresultat på din dator, hämtar och överför filer och mappar samt innehåller funktioner för att hantera konflikter med AEM Assets användargränssnitt.

Läs vidare för att felsöka appen, lära dig de bästa metoderna och ta reda på begränsningarna.

## Best practices {#best-practices-to-prevent-troubles}

Följ följande metodtips för att förebygga vissa vanliga problem och felsökning.

* **Lär dig hur datorprogrammet fungerar**: Innan du börjar använda programmet bör du ägna en stund åt att veta hur programmet fungerar. Lär dig mer om att länka mellan Experience Manager webbgränssnitt och stationära datorer, mappning av databaser, cachelagring av resurser, spara lokalt och ladda upp i bakgrunden. Se [hur det fungerar](release-notes.md#how-app-works).

* **Undvik tecken som inte stöds i mappnamn**: Använd inte blanksteg eller ogiltiga tecken när du skapar eller överför mappar. Se en lista med tecken på [Skapa mappar i Experience Manager Resurser](https://docs.adobe.com/content/help/en/experience-manager-65/assets/managing/managing-assets-touch-ui.html#Creatingfolders). Vissa Adobe Experience Manager-exempel kan påverkas av tecken i mappnamnet som inte stöds.

* **Bästa tillvägagångssätt för att undvika konflikter**: Information om hur du undviker potentiella konflikter när du samarbetar med flera resurser finns i [Undvik redigeringskonflikter](using.md#adv-workflow-collaborate-avoid-conflicts).

* **Använd mappöverföring för stora, hierarkiska mappar**: I stället för att använda webbgränssnittet Resurser eller andra metoder kan du överföra stora mappar med datorprogrammet Experience Manager. Programmet överför resurserna i bakgrunden med loggning och övervakning. Se [Massöverföring av resurser](using.md#bulk-upload-assets).

* **Använd den senaste versionen**: Använd den senaste programversionen och kontrollera alltid om den är kompatibel innan du installerar en ny programversion eller innan du uppgraderar till en nyare Adobe Experience Manager-version. Se [versionsinformation](release-notes.md).

* **Använd samma enhetsbeteckning**: Använd samma enhetsbeteckning i en hel organisation för att mappa till Adobe Experience Manager DAM. Om du vill visa resurser som placerats av andra användare måste sökvägarna vara desamma. Om du använder samma enhetsbeteckning säkerställs en konstant sökväg till DAM-resurser. Resurserna förblir placerade och tas inte bort även om olika enhetsbeteckningar används av olika användare.

* **Lägg märke till nätverket**: Nätverksprestanda är avgörande för prestandan i Experience Manager-datorprogrammet. Om du får ett långsammare svar på filöverföringar eller större åtgärder inaktiverar du de funktioner eller program som kan orsaka mycket nätverkstrafik.

* **Användningsexempel som inte stöds för datorprogrammet**: Använd inte appen för Assets&#39; migrering (den kräver planering och andra verktyg). för krävande DAM-åtgärder (som att flytta stora mappar, stora överföringar, hitta filer med avancerade metadatasökningar), och som en synkroniseringsklient (designprinciper och användningsmönster skiljer sig från synkroniserade klienter som Microsoft OneDrive eller Adobe Creative Cloud desktop sync).

* **Timeout**: För närvarande har skrivbordsprogrammet inte något konfigurerbart timeout-värde som kopplar från anslutningen mellan Experience Manager-servern och skrivbordsappen efter ett fast tidsintervall. När du överför stora resurser, och anslutningen får timeout efter en stund, försöker programmet överföra resursen några gånger genom att öka tidsgränsen för överföring. Det finns inget rekommenderat sätt att ändra standardinställningarna för timeout.

## Felsöka {#troubleshooting-prep}

Om du vill felsöka problem med skrivbordsprogram bör du känna till följande information. Dessutom får du hjälp att förmedla problemen bättre till Adobe kundtjänst om du väljer att söka support.

### Aktivera felsökningsläge {#enable-debug-mode}

Om du vill felsöka kan du aktivera felsökningsläget och få mer information i loggarna. Om du vill använda programmet i felsökningsläge på Mac använder du följande kommandoradsalternativ i en terminal eller i kommandotolken: `AEM_DESKTOP_LOG_LEVEL=DEBUG open /Applications/Adobe\ Experience\ Manager\ Desktop.app`.

Så här aktiverar du felsökningsläget i Windows:

1. Leta reda på `Adobe Experience Manager Desktop.exe.config` filen i installationsmappen för skrivbordsappen. By default, the folder is `C:\Program Files\Adobe\Adobe Experience Manager Desktop`.

1. Leta `<level value="INFO"/>` mot slutet av filen. Ändra värdet från `INFO` till `DEBUG`, vilket är `<level value="DEBUG"/>`. Spara och stäng filen.

1. Leta reda på `logging.json` filen i installationsmappen för skrivbordsappen. By default, the folder is `C:\Program Files\Adobe\Adobe Experience Manager Desktop\javascript\`.

1. Leta reda på alla förekomster av `logging.json` filen `"level": "info"`. Ändra värdena från `info` till `debug`, vilket är `"level": "debug"`. Spara och stäng filen.

1. Rensa de cachelagrade kataloger som finns på den plats som anges i [programinställningarna](/help/install-upgrade.md#set-preferences).

1. Starta om datorprogrammet.

<!-- The Windows command doesn't work for now.
* On Windows: `SET AEM_DESKTOP_LOG_LEVEL=DEBUG & "C:\Program Files\Adobe\Adobe Experience Manager Desktop\Adobe Experience Manager Desktop.exe"`
-->

### Plats för loggfiler {#check-log-files-v2}

Loggfilerna för AEM skrivbordsappen finns på följande platser. När du överför många resurser, och vissa filer inte kan överföras, ska du läsa filen för att identifiera de misslyckade överföringarna `backend.log` .

* Sökväg i Windows: `%LocalAppData%\Adobe\AssetsCompanion\Logs`

* Bana i Mac: `~/Library/Logs/Adobe\ Experience\ Manager\ Desktop`

>[!NOTE]
>
>När du arbetar med kundtjänst på Adobe på en supportförfrågan/anmälan kan du bli ombedd att dela loggfilerna för att hjälpa kundtjänstteamet att förstå problemet. Arkivera hela `Logs` mappen och dela den med kundtjänst.

### Rensa cache {#clear-cache-v2}

Att radera AEM cacheminne är en preliminär felsökningsåtgärd som kan lösa flera problem. Rensa cacheminnet från appinställningarna. Se [Ange inställningar](install-upgrade.md#set-preferences). Standardplatsen för cachemappen är:

* I Windows: `%LocalAppData%\Adobe\AssetsCompanion\Cache\`

* Mac: `~/Library/Group/Containers/group.com.adobe.aem.desktop/cache/`

Platsen kan dock ändras beroende på AEM datorns konfigurerade AEM. Värdet är en kodad version av mål-URL:en. Om programmet till exempel har som mål `http://localhost:4502`är katalognamnet `http%3A%2F%2Flocalhost%3A4502%2F`. Ta bort lämplig mapp för att rensa cachen. Ett annat skäl till att rensa cacheminnet är att frigöra diskutrymme när diskutrymmet börjar ta slut.

>[!CAUTION]
>
>Om du rensar AEM skrivbordscachen försvinner oåterkalleligt ändringar av lokala resurser som inte synkroniseras med AEM.

### Lär känna AEM version {#know-app-version-v2}

Klicka på ![App-menyn](assets/do-not-localize/more_options_da2.png) för att öppna appens meny och klicka på **[!UICONTROL Help]** > **[!UICONTROL About]**.

## Kan inte se placerade resurser {#placed-assets-missing}

Om du inte kan se de resurser som du eller andra kreatörer har placerat i supportfilerna (till exempel INDD-filer) ska du kontrollera följande:

* Anslutning till servern. Smidig nätverksanslutning kan stoppa hämtningar av resurser.
* Filstorlek. Stora resurser tar längre tid att hämta och visa.
* Enhetliga brev. Om du eller någon annan medarbetare placerade resurserna när du mappade AEM DAM till en annan enhetsbeteckning visas inte de placerade resurserna.
* Behörigheter. Kontakta AEM om du har behörighet att hämta de placerade resurserna.

## Problem vid uppgradering på macOS {#issues-when-upgrading-on-macos}

Ibland kan problem uppstå när du uppgraderar AEM datorprogram på macOS. Detta beror på att det inte går att läsa in nya versioner av AEM datorprogram korrekt i en äldre systemmapp AEM datorprogrammet. Följande mappar och filer kan tas bort manuellt för att åtgärda problemet.

Innan du utför följande steg drar du programmet `Adobe Experience Manager Desktop` från mappen macOS-program till papperskorgen. Öppna sedan terminalen, kör följande kommando och ange ditt lösenord när du uppmanas till det.

```shell
sudo rm -rf ~/Library/Application\ Support/com.adobe.aem.desktop
sudo rm -rf ~/Library/Preferences/com.adobe.aem.desktop.plist
sudo rm -rf ~/Library/Logs/Adobe\ Experience\ Manager\ Desktop

sudo find /var/folders -type d -name "com.adobe.aem.desktop" | xargs rm -rf
sudo find /var/folders -type d -name "com.adobe.aem.desktop.finderintegration-plugin" | xargs rm -rf
```

## Kan inte överföra filer {#upload-fails}

Om du använder skrivbordsappen med AEM 6.5.1 eller senare uppgraderar du S3- eller Azure-kopplingen till version 1.10.4 eller senare. Det åtgärdar ett filöverföringsfel relaterat till [OAK-8599](https://issues.apache.org/jira/browse/OAK-8599). Se [installationsanvisningar](install-upgrade.md#install-v2).

## SSL-konfigurationsproblem {#ssl-config-v2}

De bibliotek som AEM datorprogrammet använder för HTTP-kommunikation använder strikt SSL-kontroll. Ibland kan en anslutning fungera med en webbläsare, men misslyckas AEM skrivbordsappen. Installera det saknade mellanliggande certifikatet i Apache om du vill konfigurera SSL korrekt. Se [Så här installerar du ett mellanliggande CA-certifikat i Apache](https://access.redhat.com/solutions/43575).

## Appen svarar inte {#unresponsive}

I vissa fall kan programmet inte svara, bara visa en vit skärm eller visa ett fel längst ned i gränssnittet utan några alternativ i gränssnittet. Prova följande i den ordning du vill:

* Högerklicka på programgränssnittet och klicka **[!UICONTROL Refresh]**.
* Avsluta programmet och öppna det igen.

I båda metoderna startar programmet i rotmappen DAM.

>[!MORELIKETHIS]
>
>* [Kända fel](release-notes.md#known-issues-v2)
>* [Undvik redigeringskonflikter](using.md#adv-workflow-collaborate-avoid-conflicts)

