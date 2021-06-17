---
title: '[!DNL Adobe Experience Manager] versionsinformation för skrivbordsapp'
description: Versionsinformation, förbättringar, nya funktioner, kompatibilitet och hämtningslänkar för [!DNL Adobe Experience Manager] datorprogrammet.
mini-toc-levels: 1
feature: datorprogram,versionsinformation
exl-id: e058e7a2-fcc8-4ad1-899e-20695db6bc72
source-git-commit: d642a33c8e8c2f771a6f996a76167b7f6e42c1ce
workflow-type: tm+mt
source-wordcount: '1649'
ht-degree: 0%

---

# [!DNL Adobe Experience Manager] versionsinformation för skrivbordsapp  {#release-notes-v2}

Versionsinformationen för den senaste versionen av datorprogrammet 2.1 (2.1.3.1) visas nedan. Releasedatum är 8 juni 2021.

**Versionerna [!DNL Experience Manager] som stöds** är:

* [!DNL Experience Manager] som en  [!DNL Cloud Service]. Se [versionsinformation](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/home.html).
* [!DNL Experience Manager] 6.5.0 eller senare, på Adobe Managed Services (AMS) eller On-Premise. Se [Versionsinformation för Service Pack](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/service-pack/sp-release-notes.html).
* [!DNL Experience Manager] 6.4.4 eller senare, på Adobe Managed Services (AMS) eller On-Premise. Se [Versionsinformation för Service Pack](https://experienceleague.adobe.com/docs/experience-manager-64/release-notes/sp-release-notes.html).
* [!DNL Experience Manager] 6.4.0-6.4.3 med  [kompatibilitetspaketet ](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/featurepack/adobe-asset-link-support) installerat på Adobe Managed Services (AMS) eller On-Premise.
* [!DNL Experience Manager] 6.3 (med kompatibilitetspaket)
* [!DNL Experience Manager] 6.3.3.1 eller senare med  [kompatibilitetspaketet ](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/featurepack/adobe-asset-link-support) installerat. Datorprogrammet stöds inte för [!DNL Experience Manager] 6.3.3.0 eller tidigare versioner.

[!DNL Adobe Experience Manager] datorprogrammet är tillgängligt för följande  **operativsystem**:

* macOS X 10.14 eller senare, med de senaste felkorrigeringarna. [Mac-datorer med Apple ](https://support.apple.com/en-us/HT211814) siliconare stöds inte ännu.
* Windows 10 med de senaste servicepaketen och felkorrigeringarna.

Hämtnings-URL:erna **för operativsystem som stöds är:**

| Operativsystem | [!DNL Experience Manager] som  [!DNL Cloud Service] | [!DNL Experience Manager] 6.x |
|---|---|---|
| macOS 64-bitars | [Hämta länk](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-desktop-app/aem-desktop-osx-2.1.3.1.dmg) | [Hämta länk](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/adobe/aem-desktop-app/aem-desktop-osx-2.1.3.1.dmg) |
| Windows 64-bitars | [Hämta länk](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-desktop-app/aem-desktop-win64-2.1.3.1.exe) | [Hämta länk](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/adobe/aem-desktop-app/aem-desktop-win64-2.1.3.1.exe) |
| Windows 32-bitars | [Hämta länk](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-desktop-app/aem-desktop-win32-2.1.3.1.exe) | [Hämta länk](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/adobe/aem-desktop-app/aem-desktop-win32-2.1.3.1.exe) |

>[!NOTE]
>
>Windows 7 stöds inte längre. Se [artikeln om EOL i Windows 7](https://support.microsoft.com/en-us/help/4057281/windows-7-support-ended-on-january-14-2020).

<!-- The version of the app you plan to install on your local machine requires a specific [!DNL Adobe Experience Manager] server version/additional server-side components (service packs, hot fixes, or feature packs). Contact your [!DNL Experience Manager] administrator for help.
-->

## Stöd för olika resurser och filtyper {#support-for-file-types}

Programmet stöder resurser som lagras i [!DNL Experience Manager] som representerar binära filer för de grundläggande åtgärderna. När du öppnar filer i det inbyggda skrivbordsprogrammet måste operativsystemet associera specifika filtyper som PNG eller JPG med specifika program som Mac Preview eller Adobe Photoshop.

Några filtyper har stöd för att placera länkade resurser i binärfilen. Programmet hämtar de länkade resurserna i förväg om resursen finns i [!DNL Experience Manager]-databasen när sådana binära filer öppnas med skrivbordsappen. Filtyper som stöds för närvarande är:

* [!DNL Adobe InDesign] filer (INDD-format)
* [!DNL Adobe Illustrator] filer (AI-format)
* [!DNL Adobe Photoshop] filer (PS-format)

Funktionen stöds i versionerna [!DNL Adobe Creative Cloud] 2018 och [!DNL Adobe Creative Cloud] 2019 av ovanstående program. Appen använder en heuristisk, bäst matchande metod för att mappa de lokala skrivbordssökvägarna för länkade resurser till URL:er på [!DNL Experience Manager]-servern. Den bygger på några antaganden:

* Sökvägar till monterade filer i det ursprungliga programmet använder en global skrivbordssökväg (placerad från den lokala nätverksresursen som visas med alternativet [!UICONTROL Reveal]).

* Sökvägar lagras i filens XMP-post av det ursprungliga programmet.

* [!DNL Experience Manager] har extraherat XMP med sökvägarna till resursens metadatapost.

* Sökvägarna kan matchas mot resurser i [!DNL Experience Manager], d.v.s. de monterade filerna finns också i [!DNL Experience Manager] under en matchande sökväg.

## Nya funktioner, förbättringar och felkorrigeringar {#what-is-new}

Mer information finns i [Nyheter i v2.0](introduction.md#whats-new-v2).

**Uppdateringar i app v2.1.3.1**

Felet som har åtgärdats i den aktuella versionen är:

* Överförings- och nedladdningshastigheterna för mediefiler har förbättrats, även med stora mediefiler. Korrigerade ett problem där resursöverföringar med [!DNL desktop app] misslyckades i allt större utsträckning när stora filer överfördes.

**Uppdatering i app v2.1.2.0**

* Ett nytt alternativ för [!UICONTROL Clear Cookies] läggs till på programmets huvudmeny. Det hjälper vid potentiella inloggningsproblem, t.ex. vid byte av anslutning från en server till en annan. Se [rensa cookies innan du ansluter](/help/troubleshoot.md#cannot-login-cookies-issue).

* Ett alternativ läggs till som (om det här alternativet är markerat) gör att programmet kan överföra mappar och filer så att deras nodnamn som skapats i [!DNL Adobe Experience Manager] är desamma som de lokala fil- och mappnamnen.

   Det här beteendet liknar standardbeteendet i version 1 av datorprogrammet. Om alternativet inte är aktiverat i den aktuella versionen ersätts blanksteg och tecknen `% ; # , + ? ^ { } "` i mappnamn med bindestreck i mappsökvägar. Versaler konverteras också till gemener i mappsökvägar. I filnamn ersätts dock tecknen `# % { } ? &` med bindestreck; men blanksteg och hölje behålls. Mer information finns i [appinställningar](/help/install-upgrade.md#set-preferences) och [Överför och lägg till nya resurser](/help/using.md#upload-and-add-new-assets-to-aem).

**Uppdatering i app v2.1.1.0**

* Med en avancerad inställning kan appen emulera beteendet v1.10 när mappar överförs. I v1.10 gäller de nodnamn som skapas i databasen mellanslag och skiftlägen för de mappnamn som användaren anger. Standardbeteendet för v2.1 fortsätter att vara detsamma, d.v.s. ersätter flera mellanslag i mappnamn med ett bindestreck i databasens nodnamn och konverterar till gemena nodnamn. Se [appinställningarna](/help/install-upgrade.md#set-preferences).

**Uppdatering i app v2.1.0.0**

* Om du vill överföra resurser kan användare nu dra filer eller mappar i programmets gränssnitt, direkt från Utforskaren i Windows eller Finder i Mac. Detta fungerar utöver det överföringsalternativ som är tillgängligt i programmet. Se [ladda upp resurser](/help/using.md#upload-and-add-new-assets-to-aem) <!-- CQ-4309527 -->

**Uppdatering i app v2.0.3**

Felet som åtgärdas i den här versionen är:

* Korrigerade inloggningsproblemet för appanvändare i Windows som försöker få åtkomst till DAM-databasen på [!DNL Adobe Experience Manager] 6.5.5.0.

**Uppdateringar i app v2.0.2**

Felkorrigeringarna och uppdateringarna är:

* Uppladdningsaccelerationsinställningen är nu tillgänglig för att öka uppladdningsprestanda. När den här inställningen är aktiverad laddas programmet upp snabbare med fler lokala CPU-trådar och är mer resurskrävande.

* Resursuppladdning när filnamn eller sökvägar som innehåller vissa GB18030-tecken är fasta. <!-- CQ-4283494 -->

* Alternativet Sortera efter relevans är tillgängligt efter byte till en annan sorteringstyp i sökresultaten. <!-- CQ-4286874 -->

* Datorprogrammet listar nu undermappar utan att behöva uppdatera explicit. <!-- CQ-4285711 -->

* (Windows) Korrigerade ett sällsynt problem med oanvändbart appgränssnitt på vissa Windows-datorer. Användarna kan inte klicka på appgränssnittet eftersom det ser ut att vara förvrängt av klickområdet för gränssnittselementen &quot;shifts&quot;. <!-- CQ-4280785 -->

**Uppdateringar i app v2.0.1**

Felkorrigeringarna och uppdateringarna är:

* Tillåt alternativet att konfigurera katalogen `%Temp%` så att den matchar sökvägen `%APPDATA%`. <!-- CQ-4282665 -->

* Tillåt användare att logga in på [!DNL Experience Manager] Author via Okta SAML-autentisering. <!-- CQ-4278134 -->

## Installationsanvisningar {#installation-instructions-v2}

Mer information om hur du installerar och konfigurerar programmet finns i [Installera [!DNL Experience Manager] datorprogrammet](install-upgrade.md).

Om du uppgraderar från ett tidigare [!DNL Experience Manager]-skrivbordsprogram måste du följa de bästa metoderna för övergångar som listas i [uppgraderingen från en tidigare version](install-upgrade.md#upgrade-from-previous-version).

## Viktiga anteckningar om hur appen fungerar {#how-app-works}

Det är viktigt att du förstår följande om programmet och hur det fungerar.

* Programmet ger fullständig kontroll över åtgärder som kräver fullständig överföring av resurbinärfiler från och till [!DNL Experience Manager] (öppna, redigera, överföra ändringar och överföra resurser).

   * Om du vill arbeta med resursen på skrivbordet måste du uttryckligen öppna, redigera eller hämta till skrivbordet, antingen individuellt, i en mapp eller genom att markera flera.

   * Om du vill få lokala ändringar av resurser överförda till [!DNL Experience Manager] måste du välja [!UICONTROL Upload Changes], antingen individuellt eller via flerval.

   * Programmet är inte en synkroniseringsklient som synkroniserar resurser på skrivbordet och [!DNL Experience Manager].

   * Programmet tillhandahåller inte någon nätverksresurs som mappar databasen [!DNL Experience Manager] som en virtuell mappstruktur.

* Den lista över resurser som visas av programmet baseras på statusen för resurskatalogen. Filer som laddas ned lokalt och som sedan byter namn i de lokala filerna eller cachemappen visas eller hanteras inte av programmet.

* Om programmet inte visar det förväntade resultatet klickar du på ikonen Uppdatera i det övre fältet.

* Den lokala nätverksresursen, som visas när du använder åtgärden [!UICONTROL Reveal File], visar bara filer (och mappar) som är tillgängliga lokalt. [!UICONTROL Reveal File] och  [!UICONTROL Reveal Folder] hämtar resurser i förväg för att få rätt resurser att visas i den lokala nätverksresursen.

* Den lokala nätverksresursen SMB (Mac) /WebDAV (Win) används när en Adobe Creative Cloud-app läser resursfilerna som är länkade/placerade i en systemspecifik fil i appen Creative Cloud.

I följande diagram visas flödet av resurser och filer från molnet till det lokala filsystemet och tvärtom, vilket initierats av användaråtgärder.

![Flöde för resurser från  [!DNL Experience Manager] server till datorprogram via skrivbordsapp](assets/da20_flow_diagram.png)

## Kända fel {#known-issues-v2}

**Problem med användargränssnittet:**

* Ibland blir gränssnittet i skrivbordsappen tomt. Högerklicka och klicka på [!UICONTROL Refresh] för att läsa in programmet igen. Efter en sådan uppdatering börjar du i DAM-databasens rot. Uppdateringar eller status för dina resurser behålls. <!-- CQ-4270267 -->

* Det är svårt att navigera i mappar/sökresultat utan en styrplatta eller muspekare. Rullningslisten kanske inte visas med musenheter utan mushjul. <!-- CQ-4269947 -->

* I vissa fall visas inte förloppsindikatorn korrekt när den överförda resursen ändras.

* När du har tillämpat och tagit bort filtret för att hitta alla lokalt redigerade resurser tar programmet inte användarna till sökresultaten eller mappvyn som användarna började med. Appen visar rotmappen för DAM-databasen.

* När du ansluter till en URL som inte har [!DNL Experience Manager]-server igång, svarar inte anslutningsskärmen. Avsluta programmet och starta det igen.

**CRUD-problem (Skapa, Läs, Uppdatera och Ta bort):**

* När du överför ändringar till en resurs med kommentarer lagras kommentarerna med resursen i [!DNL Experience Manager], men de visas inte som versionskommentarer. Problemet åtgärdas i [!DNL Experience Manager] 6.4.5 och [!DNL Experience Manager] 6.5.1. Adobe rekommenderar att du installerar de senaste Service Pack-uppdateringarna. <!-- CQ-4268990 -->

* Resursöverföringar kan inte avbrytas av användaren. Om du utlöste en oavsiktlig stor överföring avslutar du programmet och startar det igen. <!-- CQ-4278940 -->

**Plattformsproblem:**

* I Windows kan en medias status ändras direkt till [!UICONTROL Edited Locally] efter att den har öppnats, även om du inte har redigerat den. Klicka på [!UICONTROL Refresh] för att uppdatera.

>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] as a [!DNL Cloud Service] dokumentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/landing/home.html)
>* [[!DNL Experience Manager] as a [!DNL Cloud Service] [!DNL Assets] dokumentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/home.html)
>* [Använda [!DNL Experience Manager] datorprogrammet](using.md)
* [Installera och uppgradera datorprogrammet](install-upgrade.md)
* [Bästa praxis och felsökningstips](troubleshoot.md)

