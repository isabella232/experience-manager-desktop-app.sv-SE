---
title: Adobe Experience Manager desktop app release notes
description: Release details, enhancements, new features, compatibility, and download links for Adobe Experience Manager desktop app.
uuid: b783c3f8-aa1e-4c05-b687-5894909769f5
contentOwner: AG
products: SG_EXPERIENCEMANAGER/6.3/ASSETS
discoiquuid: 3052549b-fe75-44fb-a55e-5cc612868f54
index: y
internal: n
snippet: y
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: ac4be2cb69a112f393ec76d5d95987634d0c9c46

---


# Adobe Experience Manager desktop app release notes {#release-notes-v2}

| Produkter | Adobe Experience Manager (AEM) desktop app |
|---------------|--------------------------------------------------------------------|
| App version (Revision) | 2.0 (2.0.1.1) |
| Supported AEM versions | AEM 6.5, AEM 6.4, AEM 6.3 (with compatibility package) |
| Typ | Mindre release |
| Releasedatum | Dec 12, 2019 (Mac and Win) |
| Download URLs | [MacOS 64-bitars](https://download.macromedia.com/aem-assets-companion-app/aem-desktop-osx-2.0.1.1.dmg); 64-bitars [Windows](https://download.macromedia.com/aem-assets-companion-app/aem-desktop-win64-2.0.1.1.exe); 32-bitars [Windows](https://download.macromedia.com/aem-assets-companion-app/aem-desktop-win32-2.0.1.1.exe) |

## Systemkrav och krav {#system-requirements-and-prerequisites-v2}

Adobe Experience Manager desktop app is compatible with the following operating systems:

* Mac OS X 10.10 or later, with latest bug fixes.
* Windows 7 och Windows 10 med de senaste Service Pack och felkorrigeringarna.

Appen fungerar med följande Experience Manager-versioner, oavsett om de körs lokalt eller på Adobe Managed Services (AMS):

* [Experience Manager 6.5.0](https://helpx.adobe.com/experience-manager/6-5/release-notes.html) eller senare
* [Experience Manager 6.4.4](https://helpx.adobe.com/experience-manager/6-4/release-notes/sp-release-notes.html) or later
* Experience Manager 6.4.0-6.4.3 med [kompatibilitetspaket](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/featurepack/adobe-asset-link-support)

>[!NOTE]
>
>Desktop app support for Experience Manager 6.3 is deprecated. Adobe rekommenderar att du uppgraderar till en nyare version av Adobe Experience Manager som stöds.
>Experience Manager 6.3.3.1 or later works with desktop app after installing the [compatibility package](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/featurepack/adobe-asset-link-support). No such package is available for Experience Manager 6.3 as no [service packs are planned](https://helpx.adobe.com/experience-manager/maintenance-releases-roadmap.html).

Den version av programmet som du tänker installera på den lokala datorn kräver en specifik version av Adobe Experience Manager-servern/ytterligare komponenter på serversidan (Service Pack, hot fixes eller funktionspaket). Kontakta Adobe Experience Manager-administratören om du behöver hjälp.

### Stöd för olika resurser och filtyper {#support-for-file-types}

Programmet har stöd för resurser som lagras i Adobe Experience Manager som representerar binära filer för de grundläggande åtgärderna. När du öppnar filer i det ursprungliga skrivbordsprogrammet måste operativsystemet koppla filtyperna PNG eller JPG till specifika program, som Mac Preview eller Adobe Photoshop, till operativsystemet.

Några filtyper har stöd för att placera länkade resurser i binärfilen. Programmet hämtar de länkade resurserna i förväg om resursen finns i Experience Manager-databasen när sådana binära filer öppnas med skrivbordsappen. Filtyper som stöds för närvarande är:

* Adobe InDesign-filer (INDD-format)
* Adobe Illustrator-filer (AI-format)
* Adobe Photoshop-filer (PS-format)

Funktionen stöds i Adobe Creative Cloud 2018- och Adobe Creative Cloud 2019-versionerna av ovanstående program. Appen använder en heuristisk, bäst matchande metod för att mappa lokala skrivbordssökvägar för länkade resurser till URL:er på Experience Manager-servern. Den bygger på några antaganden:

* Sökvägar till monterade filer i det ursprungliga programmet använder en global skrivbordssökväg (placerad från den lokala nätverksresursen som visas med [!UICONTROL Reveal] alternativet).
* Sökvägar lagras i filens XMP-post av det ursprungliga programmet.
* Experience Manager har extraherat XMP-posten med sökvägarna till resursens metadatapost.
* Sökvägarna kan matchas mot resurser i Experience Manager, det vill säga de monterade filerna finns även i Experience Manager under en matchande sökväg).

## Nya funktioner och förbättringar {#whats-new-added}

Mer information finns i [Nyheter i v2.0](introduction.md#whats-new-v2).

Felkorrigeringar och uppdateringar i version 2.0.1 är:

* Tillåt alternativet att konfigurera `%Temp%` katalogen så att den matchar `%APPDATA%` sökvägen. <!-- CQ-4282665 -->
* Tillåt användare att logga in på AEM Author via Okta SAML-autentisering. <!-- CQ-4278134 -->

## Installationsanvisningar {#installation-instructions-v2}

Mer information om hur du installerar och konfigurerar programmet finns i [Installera Experience Manager-datorprogrammet](install-upgrade.md).

Om du uppgraderar från ett tidigare Experience Manager-datorprogram måste du följa de bästa metoderna för övergångar som listas vid [uppgradering från en tidigare version](install-upgrade.md#upgrade-from-previous-version).

## Viktiga anteckningar om hur appen fungerar {#how-app-works}

Det är viktigt att du förstår följande om programmet och hur det fungerar.

* Programmet ger fullständig kontroll över åtgärder som kräver fullständig överföring av resurbinärfiler från och till AEM (öppna, redigera, överföra ändringar och överföra resurser).
   * Om du vill arbeta med resursen på skrivbordet måste du uttryckligen öppna, redigera eller hämta till skrivbordet, antingen individuellt, i en mapp eller genom att markera flera.
   * Om du vill få lokala ändringar av resurser överförda till AEM måste du välja [!UICONTROL Upload Changes], antingen individuellt eller via flerval.
   * Programmet är inte en synkroniseringsklient som synkroniserar resurser på skrivbordet och AEM.
   * Programmet tillhandahåller inte någon nätverksresurs som mappar AEM-databasen till en virtuell mappstruktur.
* Den lista över resurser som visas av programmet baseras på statusen för AEM Resurser-databasen. Filer som laddas ned lokalt och som sedan byter namn i de lokala filerna eller cachemappen visas eller hanteras inte av programmet.
* Om programmet inte visar det förväntade resultatet klickar du på ikonen Uppdatera i det övre fältet.
* Den lokala nätverksresursen, som visas när du använder [!UICONTROL Reveal File] åtgärden, visar bara filer (och mappar) som är tillgängliga lokalt. [!UICONTROL Reveal File] och [!UICONTROL Reveal Folder] hämtar resurser i förväg för att få rätt resurser att visas i den lokala nätverksresursen.
* Den lokala nätverksresursen SMB (Mac) /WebDAV (Win) används när en Adobe Creative Cloud-app läser resursfilerna som är länkade/placerade i en intern fil i Creative Cloud-programmet.

I följande diagram visas flödet av resurser och filer från molnet till det lokala filsystemet och vice versa, vilket initierats av användaråtgärder.

![Flöde av resurser från AEM-server till inbyggda datorprogram via skrivbordsapp](assets/da20_flow_diagram.png)

## Known issues {#known-issues-v2}

**Problem med användargränssnittet:**

* Ibland blir gränssnittet i skrivbordsappen tomt. Högerklicka och klicka [!UICONTROL Refresh] för att läsa in programmet igen. Efter en sådan uppdatering börjar du i DAM-databasens rot. Uppdateringar eller status för dina resurser behålls. <!-- CQ-4270267 -->
* Det är svårt att navigera i mappar/sökresultat utan en styrplatta eller muspekare. Rullningslisten kanske inte visas med musenheter utan mushjul. <!-- CQ-4269947 -->
* I vissa fall visas inte förloppsindikatorn korrekt när den överförda resursen ändras.
* När du har tillämpat och tagit bort filtret för att hitta alla lokalt redigerade resurser tar programmet inte användarna till sökresultaten eller mappvyn som användarna började med. Appen visar rotmappen för DAM-databasen.
* Ibland slutar anslutningsskärmen att svara när du ansluter till en URL som inte har en AEM-server igång. Avsluta programmet och starta det igen.

**CRUD-problem (Skapa, Läs, Uppdatera och Ta bort):**

* Programmet försöker ladda upp filer även med ogiltiga tecken, vilket kan orsaka överföringsfel på serversidan. <!-- CQ-4273652 -->
* När du överför ändringar till en resurs med kommentarer lagras kommentarerna tillsammans med resursen i AEM, men de visas inte som versionskommentarer. Problemet åtgärdas i AEM 6.4.5 och AEM 6.5.1. Adobe rekommenderar starkt att du installerar de senaste servicepaketen. <!-- CQ-4268990 -->
* Resursöverföringar kan inte avbrytas av användaren. Om du utlöste en oavsiktlig stor överföring avslutar du programmet och startar det igen. <!-- CQ-4278940 -->

**Plattformsproblem:**

* I Windows kan en medias status ändras direkt till [!UICONTROL Edited Locally] efter att den har öppnats, även om du inte har redigerat den. Klicka [!UICONTROL Refresh] för att uppdatera.

>[!MORELIKETHIS]
>
>* [AEM 6.5 - dokumentation](https://helpx.adobe.com/support/experience-manager/6-5.html)
>* [AEM Assets 6.5 - dokumentation](https://docs.adobe.com/content/help/en/experience-manager-65/assets/home.html)
>* [Så här använder du Experience Manager-datorprogrammet](using.md)
>* [Installera och uppgradera datorprogrammet](install-upgrade.md)
>* [Bästa praxis och felsökningstips](troubleshoot.md)

