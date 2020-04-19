---
title: Bästa tillvägagångssätt för och felsökning av Adobe Experience Manager-datorprogrammet
description: Följ bästa praxis och felsök för att lösa tillfälliga problem som rör installation, uppgradering, konfiguration och så vidare.
uuid: ce98a3e7-5454-41be-aaaa-4252b3e0f8dd
contentOwner: AG
products: SG_EXPERIENCEMANAGER/6.3/ASSETS
discoiquuid: f5eb222a-6cdf-4ae3-9cf2-755c873f397c
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 9ae1580475569538838c58f642a7df43f2526d16

---


# Felsöka Adobe Experience Manager-datorprogrammet {#troubleshoot-v2}

Adobe Experience Manager-datorprogrammet (AEM) ansluter till en fjärransluten Experience Manager-distributionsdatabas för digital resurshantering (DAM). Appen hämtar databasinformation och sökresultat på din dator, hämtar och överför filer och mappar och innehåller funktioner för att hantera konflikter med användargränssnittet i AEM Assets.

Läs vidare för att felsöka appen, lära dig de bästa metoderna och ta reda på begränsningarna.

## God praxis {#best-practices-to-prevent-troubles}

Följ följande metodtips för att förebygga vissa vanliga problem och felsökning.

* **Lär dig hur datorprogrammet fungerar**: Innan du börjar använda programmet bör du ägna några minuter åt att veta hur programmet fungerar. Lär dig hur du länkar mellan webbgränssnitt och datorer, databasmappning, resurscachning, sparar lokalt och överför i bakgrunden. Se [hur det fungerar](release-notes.md#how-app-works).

* **Undvik tecken som inte stöds i mappnamn**: Använd inte blanksteg och ogiltiga tecken när du skapar eller överför mappar. Se en lista med tecken på [Skapa mappar i Experience Manager Assets](https://helpx.adobe.com/experience-manager/6-5/assets/using/managing-assets-touch-ui.html#Creatingfolders). Vissa användningsfall i Adobe Experience Manager kan påverkas av tecken i mappnamnet som inte stöds.

* **Bästa tillvägagångssätt för att undvika konflikter**: Information om hur du undviker potentiella konflikter när du samarbetar med flera resurser finns i [Undvik redigeringskonflikter](using.md#adv-workflow-collaborate-avoid-conflicts).

* **Använd mappöverföring för stora, hierarkiska mappar**: Använd Experience Manager-skrivbordsappen för att överföra stora mappar i stället för att använda Assets-webbgränssnittet eller andra metoder. Programmet överför resurserna i bakgrunden med loggning och övervakning. Se [Massöverföring av resurser](using.md#bulk-upload-assets).

* **Använd den senaste versionen**: Använd den senaste programversionen och kontrollera alltid om den är kompatibel innan du installerar en ny programversion eller innan du uppgraderar till en nyare version av Adobe Experience Manager. Se [versionsinformation](release-notes.md).

* **Använd samma enhetsbeteckning**: Använd samma enhetsbeteckning i hela organisationen för att mappa till Adobe Experience Manager DAM. Om du vill visa resurser som placerats av andra användare måste sökvägarna vara desamma. Om du använder samma enhetsbeteckning säkerställs en konstant sökväg till DAM-resurser. Resurserna förblir placerade och tas inte bort även om olika enhetsbeteckningar används av olika användare.

* **Lägg märke till nätverket**: Nätverksprestanda är avgörande för prestandan i datorprogrammet Experience Manager. Om du får ett långsammare svar på filöverföringar eller större åtgärder inaktiverar du de funktioner eller program som kan orsaka mycket nätverkstrafik.

* **Användningsexempel som inte stöds för datorprogrammet**: Använd inte appen för Assets&#39; migrering (den kräver planering och andra verktyg). för krävande DAM-åtgärder (som att flytta stora mappar, stora överföringar, hitta filer med avancerade metadatasökningar), och som en synkroniseringsklient (designprinciper och användningsmönster skiljer sig från synkroniserade klienter som Microsoft OneDrive eller Adobe Creative Cloud-synkronisering).

* **Timeout**: För närvarande har skrivbordsappen inte ett konfigurerbart timeout-värde som kopplar från anslutningen mellan Experience Manager-servern och skrivbordsappen efter ett fast tidsintervall. När du överför stora resurser, och anslutningen får timeout efter en stund, försöker programmet överföra resursen några gånger genom att öka tidsgränsen för överföring. Det finns inget rekommenderat sätt att ändra standardinställningarna för timeout.

## Felsöka {#troubleshooting-prep}

Om du vill felsöka problem med skrivbordsprogram bör du känna till följande information. Där kan du också bättre förmedla problemen till Adobes kundtjänst om du väljer att söka support.

### Aktivera felsökningsläge {#enable-debug-mode}

Om du vill felsöka kan du aktivera felsökningsläget och få mer information i loggarna. Om du vill använda programmet i felsökningsläge på Mac använder du följande kommandoradsalternativ i en terminal eller i kommandotolken: `AEM_DESKTOP_LOG_LEVEL=DEBUG open /Applications/Adobe\ Experience\ Manager\ Desktop.app`.

Så här aktiverar du felsökningsläget i Windows:

1. Leta reda på `Adobe Experience Manager Desktop.exe.config` filen i installationsmappen för skrivbordsappen. By default, the folder is `C:\Program Files\Adobe\Adobe Experience Manager Desktop`. Spara och stäng filen.

1. Leta `<level value="INFO"/>` mot slutet av filen. Ändra värdet till `DEBUG`, det vill säga, `<level value="DEBUG"/>`.

1. Leta reda på `logging.json` filen i installationsmappen för skrivbordsappen. By default, the folder is `C:\Program Files\Adobe\Adobe Experience Manager Desktop\javascript\`.

1. Leta reda på alla instanser av `logging.json` parametern i `level` filen. Ändra värdena från `info` till `debug`. Spara och stäng filen.

1. Rensa de cachelagrade kataloger som finns på den plats som anges i programinställningarna.

1. Starta om datorprogrammet.

<!-- The Windows command doesn't work for now.
* On Windows: `SET AEM_DESKTOP_LOG_LEVEL=DEBUG & "C:\Program Files\Adobe\Adobe Experience Manager Desktop\Adobe Experience Manager Desktop.exe"`
-->

### Plats för loggfiler {#check-log-files-v2}

Du hittar loggfilerna för AEM-skrivbordsappen på följande platser. När du överför många resurser, och vissa filer inte kan överföras, ska du läsa filen för att identifiera de misslyckade överföringarna `backend.log` .

* Sökväg i Windows: `%LocalAppData%\Adobe\AssetsCompanion\Logs`

* Bana i Mac: `~/Library/Logs/Adobe\ Experience\ Manager\ Desktop`

>[!NOTE]
>
>När du arbetar med Adobes kundtjänst på en supportförfrågan/anmälan kan du bli ombedd att dela loggfilerna för att hjälpa kundtjänstteamet att förstå problemet. Arkivera hela `Logs` mappen och dela den med kundtjänst.

### Rensa cache {#clear-cache-v2}

Att rensa cacheminnet för AEM-skrivbordsappen är en preliminär felsökningsuppgift som kan lösa flera problem. Rensa cacheminnet från appinställningarna. Se [Ange inställningar](install-upgrade.md#set-preferences). Standardplatsen för cachemappen är:

* I Windows: `%LocalAppData%\Adobe\AssetsCompanion\Cache\`

* Mac: `~/Library/Group/Containers/group.com.adobe.aem.desktop/cache/`

Platsen kan dock ändras beroende på AEM-datorns konfigurerade AEM-slutpunkt. Värdet är en kodad version av mål-URL:en. Om programmet till exempel har som mål `http://localhost:4502`är katalognamnet `http%3A%2F%2Flocalhost%3A4502%2F`. Ta bort lämplig mapp för att rensa cachen. Ett annat skäl till att rensa cacheminnet är att frigöra diskutrymme när diskutrymmet börjar ta slut.

>[!CAUTION]
>
>Om du rensar bort AEM-skrivbordscachen går ändringar av lokala resurser som inte synkroniseras till AEM-servern oåterkalleligen förlorade.

### Känn till AEM-versionen {#know-app-version-v2}

Klicka på ![App-menyn](assets/do-not-localize/more_options_da2.png) för att öppna appens meny och klicka på **[!UICONTROL Help]** > **[!UICONTROL About]**.

## Kan inte se placerade resurser {#placed-assets-missing}

Om du inte kan se de resurser som du eller andra kreatörer har placerat i supportfilerna (till exempel INDD-filer) ska du kontrollera följande:

* Anslutning till servern. Smidig nätverksanslutning kan stoppa hämtningar av resurser.
* Filstorlek. Stora resurser tar längre tid att hämta och visa.
* Enhetliga brev. Om du eller någon annan medarbetare placerade resurserna när du mappade AEM DAM till en annan enhetsbeteckning visas inte de placerade resurserna.
* Behörigheter. Kontakta AEM-administratören om du har behörighet att hämta de placerade resurserna.

## Problem vid uppgradering på macOS {#issues-when-upgrading-on-macos}

Ibland kan problem uppstå när du uppgraderar AEM-datorprogrammet på macOS. Detta orsakas av att det inte går att läsa in nya versioner av AEM-skrivbordsappen korrekt i en äldre systemmapp för AEM-skrivbordsappen. Följande mappar och filer kan tas bort manuellt för att åtgärda problemet.

Innan du utför följande steg drar du programmet `Adobe Experience Manager Desktop` från mappen macOS-program till papperskorgen. Öppna sedan terminalen, kör följande kommando och ange ditt lösenord när du uppmanas till det.

```shell
sudo rm -rf ~/Library/Application\ Support/com.adobe.aem.desktop
sudo rm -rf ~/Library/Preferences/com.adobe.aem.desktop.plist
sudo rm -rf ~/Library/Logs/Adobe\ Experience\ Manager\ Desktop

sudo find /var/folders -type d -name "com.adobe.aem.desktop" | xargs rm -rf
sudo find /var/folders -type d -name "com.adobe.aem.desktop.finderintegration-plugin" | xargs rm -rf
```

## Kan inte överföra filer {#upload-fails}

Om du använder datorprogrammet med AEM 6.5.1 eller senare uppgraderar du S3- eller Azure-anslutningen till version 1.10.4 eller senare. Det åtgärdar ett filöverföringsfel relaterat till [OAK-8599](https://issues.apache.org/jira/browse/OAK-8599). Se [installationsanvisningar](install-upgrade.md#install-v2).

## SSL-konfigurationsproblem {#ssl-config-v2}

Biblioteken som används av AEM-datorprogrammet för HTTP-kommunikation utnyttjar strikt SSL-tillämpning. Ibland kan en anslutning fungera med en webbläsare, men misslyckas med att använda AEM-skrivbordsappen. Installera det saknade mellanliggande certifikatet i Apache om du vill konfigurera SSL korrekt. Se [Så här installerar du ett mellanliggande CA-certifikat i Apache](https://access.redhat.com/solutions/43575).

## Appen svarar inte {#unresponsive}

I vissa fall kan programmet inte svara, bara visa en vit skärm eller visa ett fel längst ned i gränssnittet utan några alternativ i gränssnittet. Prova följande i den ordning du vill:

1. Högerklicka på programgränssnittet och klicka **[!UICONTROL Refresh]**.
1. Avsluta programmet och starta om det.

I båda metoderna startar programmet i rotmappen DAM.

>[!MORELIKETHIS]
>
>* [Kända fel](release-notes.md#known-issues-v2)
>* [Undvik redigeringskonflikter](using.md#adv-workflow-collaborate-avoid-conflicts)