---
title: Versionsinformation för Adobe Experience Manager-datorprogram
description: Versionsinformation, förbättringar, nya funktioner, kompatibilitet och nedladdningslänkar för Adobe Experience Manager-datorprogrammet.
uuid: b783c3f8-aa1e-4c05-b687-5894909769f5
contentOwner: AG
products: SG_EXPERIENCEMANAGER/6.5/ASSETS, SG_EXPERIENCEMANAGER/6.4/ASSETS, SG_EXPERIENCEMANAGER/6.3/ASSETS
discoiquuid: 3052549b-fe75-44fb-a55e-5cc612868f54
index: y
internal: n
snippet: y
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 2893fc1f8aad02e1436a1a281a320e6837487220
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Versionsinformation för Adobe Experience Manager-datorprogrammet {#release-notes-v2}

| Produkter | Adobe Experience Manager-datorprogram |
|--- |--- |
| Programversion (revision) | 2.0 (2.0.3.2) |
| Experience Manager-versioner som stöds | Experience Manager som Cloud Service, Experience Manager 6.5, Experience Manager 6.4 Experience Manager 6.3 (med kompatibilitetspaket) |
| Typ | Mindre release |
| Releasedatum | 27 aug 2020 (Mac och Win) |
| Hämta URL:er | [macOS 64-bitars](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/adobe/aem-desktop-app/aem-desktop-osx-2.0.3.2.dmg);  [Windows 64-bitars](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/adobe/aem-desktop-app/aem-desktop-win64-2.0.3.2.exe);  [Windows 32-bitars](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/adobe/aem-desktop-app/aem-desktop-win32-2.0.3.2.exe) |

## Systemkrav och krav {#system-requirements-and-prerequisites-v2}

Adobe Experience Manager-datorprogrammet är kompatibelt med följande operativsystem:

* Mac OS X 10.14 eller senare, med de senaste felkorrigeringarna.

* Windows 10 med de senaste servicepaketen och felkorrigeringarna.

>[!NOTE]
>
>Windows 7 stöds inte längre av leverantören (https://support.microsoft.com/en-us/help/4057281/windows-7-support-ended-on-january-14-2020).

Appen fungerar med följande Experience Manager-versioner, oavsett om de distribueras som en Cloud Service, på Adobe Managed Services (AMS) eller på plats:

* [Experience Manager as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/home.html).

* [Experience Manager 6.5.0](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/service-pack/sp-release-notes.html) eller senare.

* [Experience Manager 6.4.4](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/sp-release-notes.html) eller senare.

* Experience Manager 6.4.0 - 6.4.3 med [kompatibilitetspaket](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/featurepack/adobe-asset-link-support).

>[!NOTE]
>
>Stöd för skrivbordsappar i Experience Manager 6.3 är föråldrat. Adobe rekommenderar att du uppgraderar till en nyare version av Adobe Experience Manager som stöds.
>Experience Manager 6.3.3.1 eller senare fungerar med skrivbordsappen efter installation av [kompatibilitetspaketet](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/featurepack/adobe-asset-link-support). Inget sådant paket är tillgängligt för Experience Manager 6.3 eftersom inga [servicepaket är planerade](https://helpx.adobe.com/experience-manager/maintenance-releases-roadmap.html).

Den version av programmet som du tänker installera på den lokala datorn kräver en specifik version av Adobe Experience Manager eller ytterligare komponenter på serversidan (Service Pack, hot fixes eller feature packs). Kontakta Adobe Experience Manager-administratören om du behöver hjälp.

### Stöd för olika resurser och filtyper {#support-for-file-types}

Programmet har stöd för resurser som lagras i Adobe Experience Manager och som representerar binära filer för de grundläggande åtgärderna. När du öppnar filer i det inbyggda skrivbordsprogrammet måste operativsystemet associera specifika filtyper som PNG eller JPG med specifika program som Mac Preview eller Adobe Photoshop.

Några filtyper har stöd för att placera länkade resurser i binärfilen. Programmet hämtar de länkade resurserna i förväg om resursen finns i Experience Manager-databasen när sådana binära filer öppnas med skrivbordsappen. Filtyper som stöds för närvarande är:

* [!DNL Adobe InDesign] filer (INDD-format)
* [!DNL Adobe Illustrator] filer (AI-format)
* [!DNL Adobe Photoshop] filer (PS-format)

Funktionen stöds i Adobe Creative Cloud 2018- och Adobe Creative Cloud 2019-versionerna av ovanstående program. Appen använder en heuristisk, bäst matchande metod för att mappa lokala skrivbordssökvägar för länkade resurser till URL:er på Experience Manager-servern. Den bygger på några antaganden:

* Sökvägar till monterade filer i det ursprungliga programmet använder en global skrivbordssökväg (placerad från den lokala nätverksresursen som visas med alternativet [!UICONTROL Reveal]).

* Sökvägar lagras i filens XMP-post av det ursprungliga programmet.

* Experience Manager har extraherat XMP med sökvägarna till resursens metadatapost.

* Sökvägarna kan matchas mot resurser i Experience Manager, det vill säga de monterade filerna finns också i Experience Manager under en matchande sökväg.

## Nya funktioner och förbättringar {#whats-new-added}

Mer information finns i [Nyheter i v2.0](introduction.md#whats-new-v2).

**Uppdateringar i app v2.0.3**

Felet som har åtgärdats i den aktuella versionen är:

* Ett inloggningsproblem som Windows-användare som försöker få åtkomst till DAM-databasen på instansen [!DNL Adobe Experience Manager] 6.5.5.0 har korrigerats med hjälp av programmet.

**Uppdateringar i app v2.0.2**

Felkorrigeringarna och uppdateringarna är:

* Öka uppladdningsaccelerationen i [!UICONTROL Preferences] för att förbättra uppladdningsprestanda. När den här inställningen är aktiverad används fler lokala CPU-trådar och programmet är mer resurskrävande.

* Korrigerat problem med överföringar av resurser när filnamn eller sökvägar innehåller vissa GB18030-tecken. <!-- CQ-4283494 -->

* Alternativet Sortera efter relevans är tillgängligt efter byte till en annan sorteringstyp i sökresultaten. <!-- CQ-4286874 -->

* Datorprogrammet listar nu undermappar utan att behöva uppdatera explicit. <!-- CQ-4285711 -->

* (Windows) Korrigerade ett sällsynt problem med oanvändbart appgränssnitt på vissa Windows-datorer. Användarna kan inte klicka på appgränssnittet eftersom det ser ut att vara förvrängt av klickområdet för gränssnittselementen &quot;shifts&quot;. <!-- CQ-4280785 -->

**Uppdateringar i app v2.0.1**

Felkorrigeringarna och uppdateringarna är:

* Tillåt alternativet att konfigurera katalogen `%Temp%` så att den matchar sökvägen `%APPDATA%`. <!-- CQ-4282665 -->

* Tillåt användare att logga in på Experience Manager Author via Okta SAML-autentisering. <!-- CQ-4278134 -->

## Installationsanvisningar {#installation-instructions-v2}

Mer information om hur du installerar och konfigurerar programmet finns i [Installera Experience Manager-datorprogrammet](install-upgrade.md).

Om du uppgraderar från ett tidigare Experience Manager-program måste du följa de bästa metoderna för övergångar som anges i [uppgraderingen från en tidigare version](install-upgrade.md#upgrade-from-previous-version).

## Viktiga anteckningar om hur appen fungerar {#how-app-works}

Det är viktigt att du förstår följande om programmet och hur det fungerar.

* Programmet ger fullständig kontroll över åtgärder som kräver fullständig överföring av resurbinärfiler från och till Experience Manager (öppna, redigera, överföra ändringar och överföra resurser).

   * Om du vill arbeta med resursen på skrivbordet måste du uttryckligen öppna, redigera eller hämta till skrivbordet, antingen individuellt, i en mapp eller genom att markera flera.

   * Om du vill få lokala ändringar av resurser överförda till Experience Manager måste du välja [!UICONTROL Upload Changes], antingen individuellt eller via flerval.

   * Programmet är inte en synkroniseringsklient som synkroniserar resurser på skrivbordet och Experience Manager.

   * Programmet tillhandahåller inte någon nätverksresurs som mappar Experience Manager-databasen som en virtuell mappstruktur.

* Den lista över resurser som visas av programmet baseras på statusen för resurskatalogen. Filer som laddas ned lokalt och som sedan byter namn i de lokala filerna eller cachemappen visas eller hanteras inte av programmet.

* Om programmet inte visar det förväntade resultatet klickar du på ikonen Uppdatera i det övre fältet.

* Den lokala nätverksresursen, som visas när du använder åtgärden [!UICONTROL Reveal File], visar bara filer (och mappar) som är tillgängliga lokalt. [!UICONTROL Reveal File] och  [!UICONTROL Reveal Folder] hämtar resurser i förväg för att få rätt resurser att visas i den lokala nätverksresursen.

* Den lokala nätverksresursen SMB (Mac) /WebDAV (Win) används när en Adobe Creative Cloud-app läser resursfilerna som är länkade/placerade i en systemspecifik fil i appen Creative Cloud.

I följande diagram visas flödet av resurser och filer från molnet till det lokala filsystemet och vice versa, vilket initierats av användaråtgärder.

![Flöde för resurser från Experience Manager-server till datorprogram via skrivbordsapp](assets/da20_flow_diagram.png)

## Kända fel {#known-issues-v2}

**Problem med användargränssnittet:**

* Ibland blir gränssnittet i skrivbordsappen tomt. Högerklicka och klicka på [!UICONTROL Refresh] för att läsa in programmet igen. Efter en sådan uppdatering börjar du i DAM-databasens rot. Uppdateringar eller status för dina resurser behålls. <!-- CQ-4270267 -->

* Det är svårt att navigera i mappar/sökresultat utan en styrplatta eller muspekare. Rullningslisten kanske inte visas med musenheter utan mushjul. <!-- CQ-4269947 -->

* I vissa fall visas inte förloppsindikatorn korrekt när den överförda resursen ändras.

* När du har tillämpat och tagit bort filtret för att hitta alla lokalt redigerade resurser tar programmet inte användarna till sökresultaten eller mappvyn som användarna började med. Appen visar rotmappen för DAM-databasen.

* Ibland slutar anslutningsskärmen att svara när du ansluter till en URL som inte har en Experience Manager-server igång. Avsluta programmet och starta det igen.

**CRUD-problem (Skapa, Läs, Uppdatera och Ta bort):**

* Programmet försöker ladda upp filer även med ogiltiga tecken, vilket kan orsaka överföringsfel på serversidan. <!-- CQ-4273652 -->

* När du överför ändringar till en resurs med kommentarer lagras kommentarerna tillsammans med resursen i Experience Manager, men de visas inte som versionskommentarer. Problemet är löst i Experience Manager 6.4.5 och Experience Manager 6.5.1. Adobe rekommenderar starkt att du installerar de senaste servicepaketen. <!-- CQ-4268990 -->

* Resursöverföringar kan inte avbrytas av användaren. Om du utlöste en oavsiktlig stor överföring avslutar du programmet och startar det igen. <!-- CQ-4278940 -->

**Plattformsproblem:**

* I Windows kan en medias status ändras direkt till [!UICONTROL Edited Locally] efter att den har öppnats, även om du inte har redigerat den. Klicka på [!UICONTROL Refresh] för att uppdatera.

>[!MORELIKETHIS]
>
>* [Experience Manager som Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/landing/home.html)
>* [Experience Manager som Cloud Service Assets-dokumentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/home.html)
>* [Så här använder du datorprogrammet Experience Manager](using.md)
>* [Installera och uppgradera datorprogrammet](install-upgrade.md)
>* [Bästa praxis och felsökningstips](troubleshoot.md)

