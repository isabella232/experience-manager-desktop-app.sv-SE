---
title: Installera och konfigurera Adobe Experience Manager datorprogram
description: Installera och konfigurera Adobe Experience Manager datorprogram så att det fungerar med Adobe Experience Manager Assets-servrar och hämta resurserna i det lokala filsystemet.
uuid: 79bc9de9-5708-41f9-ac43-68c1fd2a2129
contentOwner: AG
products: SG_EXPERIENCEMANAGER/6.5/ASSETS, SG_EXPERIENCEMANAGER/6.4/ASSETS, SG_EXPERIENCEMANAGER/6.3/ASSETS
discoiquuid: f6365302-1690-4719-9b8c-035719422740
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 2893fc1f8aad02e1436a1a281a320e6837487220
workflow-type: tm+mt
source-wordcount: '1222'
ht-degree: 0%

---


# Installera Adobe Experience Manager datorprogram {#install-app-v2}

Med Adobe Experience Manager-datorprogrammet är materialet i Experience Manager enkelt tillgängligt på din dator och kan användas i alla datorprogram. Resurser kan förhandsgranskas, öppnas i datorprogram, visas i Finder i Mac eller Utforskaren i Windows för montering i andra dokument och ändras lokalt. Ändringarna sparas sedan i Experience Manager när du överför och en ny version skapas i databasen.

Tack vare en sådan integrering kan olika roller i organisationen

* Hantera materialet centralt i Experience Manager Assets.

* Få tillgång till materialet i alla datorprogram, inklusive program från tredje part och i Adobe Creative Cloud. När man gör det kan man enkelt följa de olika standarderna, inklusive branding.

Om du vill använda datorprogrammet Experience Manager

* Kontrollera att din version av Experience Manager stöds av Experience Manager-datorprogrammet. Se [systemkraven](release-notes.md#system-requirements-and-prerequisites-v2) nedan.

* Hämta och installera programmet. Se [Installera skrivbordsappen](#install-v2) nedan.

* Testa anslutningen med några resurser. Se [hur du söker efter resurser](using.md#browse-search-preview-assets).

## Systemkrav, krav och nedladdningslänkar {#tech-specs-v2}

Mer information finns i versionsinformationen för [Experience Manager-datorprogrammet](release-notes.md).

## Uppgradera från en tidigare version {#upgrade-from-previous-version}

Om du använder v1.x av skrivbordsappen måste du förstå skillnaderna och likheterna mellan den tidigare och den senaste versionen av appen. Se [vad som är nytt i datorprogrammet](introduction.md#whats-new-v2) och [hur appen fungerar](release-notes.md#how-app-works)

>[!NOTE]
>
>Två versioner av skrivbordsprogrammet kan inte finnas samtidigt på en dator. Avinstallera den andra versionen innan du installerar en version.

Följ dessa anvisningar om du vill uppgradera från en tidigare version av programmet:

1. Synkronisera alla resurser och överför ändringarna till Experience Manager innan du uppgraderar. Detta för att undvika att ändringar går förlorade när programmet avinstalleras.

1. Avinstallera den tidigare versionen av programmet. När du avinstallerar markerar du alternativet att rensa cachen.

1. Starta om datorn.

1. [Hämta](release-notes.md) och [installera](#install-v2) det senaste programmet. Följ instruktionerna nedan.

## Installera {#install-v2}

Följ de här stegen för att installera skrivbordsappen. Avinstallera alla befintliga Adobe Experience Manager-program v1.x innan du installerar den senaste appen. Mer information finns ovan.

1. Hämta det senaste installationsprogrammet från sidan [Versionsinformation](release-notes.md) .

1. Ha URL:en och autentiseringsuppgifterna för din distribution av Experience Manager till hands.

1. Om du uppgraderar från en annan version av programmet ska du läsa [Uppgradera datorprogrammet](#upgrade-from-previous-version).

1. Hoppa över det här steget om du använder Experience Manager som Cloud Service, Experience Manager 6.4.4 eller senare eller Experience Manager 6.5.0 eller senare. Kontrollera att Experience Manager-installationen uppfyller kompatibilitetskraven som anges i [versionsinformationen](release-notes.md). Hämta vid behov [kompatibilitetspaketet](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/featurepack/adobe-asset-link-support) och installera det med Experience Manager Package Manager som administratör för Experience Manager. Information om hur du installerar ett paket finns i [Så här arbetar du med paket](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html).

1. Kör installationsprogrammets binärfil och följ instruktionerna på skärmen.

1. I Windows kan installationsprogrammet uppmana dig att installera `Visual Studio C++ Redistributable 2015`. Installera den genom att följa instruktionerna på skärmen. Om installationen misslyckas installerar du den manuellt. Hämta installationsprogrammet [här](https://www.microsoft.com/en-us/download/details.aspx?id=52685) och installera både `vc_redist.x64.exe` och `vc_redist.x86.exe` filer. Kör installationsprogrammet för [!DNL Experience Manager] skrivbordsappen igen.

1. Starta om datorn enligt anvisningarna. Starta och konfigurera skrivbordsappen.

1. Om du vill ansluta programmet till en [!DNL Experience Manager] databas klickar du på programikonen i fältet och startar programmet. Ange adressen till [!DNL Experience Manager] servern i formatet `https://[aem_server]:[port]/`.

   Klicka på **[!UICONTROL Connect]** och ange autentiseringsuppgifterna.

   ![Anslutningsskärmen för skrivbordsprogrammet till serveradressen för indata](assets/connect_da2.png)

   *Bild: Anslutningsskärmen till inmatningsserveradressen.*

   >[!CAUTION]
   >
   >Kontrollera att det inte finns några inledande eller avslutande blanksteg före eller efter [!DNL Experience Manager] serveradressen. Annars kan programmet inte ansluta till [!DNL Experience Manager] servern.

1. När anslutningen lyckades kan du visa listan över mappar och resurser som är tillgängliga i rotmappen för [!DNL Experience Manager] DAM. Du kan bläddra bland mapparna inifrån programmet.

   ![När du loggar in visas DAM-innehållet](assets/firstview_da2.png)

   *Bild: Programmet visar DAM-innehållet efter inloggning*

1. (Experience Manager 6.5.1 eller senare) Om du använder datorprogrammet med Experience Manager 6.5.1 eller senare, uppgraderar du S3- eller Azure-anslutningen till version 1.10.4 eller senare. Se [Azure Connector](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/data-store-config.html#azure-data-store) eller [S3 Connector](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/data-store-config.html#amazon-s-data-store).

   Om du är Adobe Managed Services-kund (AMS) kontaktar du Adobe kundtjänst.

## Ange inställningar {#set-preferences}

Om du vill ändra inställningarna klickar du på ikonen ![](assets/do-not-localize/more_options_da2.png) Fler alternativ och **[!UICONTROL Preference]** ikonen ![](assets/do-not-localize/preferences_icon_da2.png)Inställningar. Justera värdena för följande i **[!UICONTROL Preferences]** fönstret:

* [!UICONTROL Launch application on login].

* [!UICONTROL Show window when application starts].

* **[!UICONTROL Cache Directory]**: Plats för appens lokala cache (den innehåller de lokalt hämtade resurserna).

* **[!UICONTROL Network Drive Letter]**: Enhetsbokstaven som används för att mappa till [!DNL Experience Manager] DAM. Ändra inte detta om du inte är säker. Appen kan mappas till valfri enhetsbeteckning i Windows. Om två användare placerar resurser från olika enhetsbokstäver kan de inte se de resurser som placerats ut av varandra. Resursernas sökväg ändras. Resurserna förblir placerade i den binära filen (till exempel INDD) och tas inte bort. Appen visar alla tillgängliga enhetsbokstäver och som standard använder den senast tillgängliga bokstaven som vanligtvis är `Z`.

* **[!UICONTROL Maximum Cache Size]**: Tillåten cache på hårddisken i GB som används för att lagra lokalt hämtade resurser.

* **[!UICONTROL Current cache size]**: Lagringsstorlek för lokalt hämtade resurser. Informationen visas först när resurserna har hämtats med appen.

* **[!UICONTROL Automatically download linked assets]**: Resurserna som placeras i de Creative Cloud-program som stöds hämtas automatiskt om du hämtar originalfilen.

* **[!UICONTROL Maximum number of downloads]**: När du hämtar resurser för första gången (via Visa, Öppna, Redigera, Hämta eller liknande) hämtas resurserna endast om gruppen innehåller mindre än det här antalet. Standardvärdet är 50. Ändra inte om du är osäker. Om du ökar värdet kan det leda till längre väntetider och om du minskar värdet kanske du inte kan hämta nödvändiga resurser eller mappar på en gång.

* **[!UICONTROL Upload Acceleration]**: När du överför resurser kan programmet använda samtidiga överföringar för att förbättra överföringshastigheten. Du kan öka samtidigheten för överföringen genom att flytta reglaget åt höger. Skjutreglaget längst till vänster betyder ingen samtidighet (enkeltrådad överföring), mittpositionen motsvarar 10 samtidiga trådar och maxgränsen längst till höger motsvarar 20 samtidiga trådar. En högre samtidighetsgräns kräver större resursförbrukning för den lokala datorns processor.

Om du vill uppdatera inställningarna som inte är tillgängliga loggar du ut från [!DNL Experience Manager] servern. När du har uppdaterat inställningarna klickar du på ![Spara inställningar](assets/do-not-localize/save_preferences_da2.png) för att spara ändringarna.

![Inställningar och inställningar för skrivbordsprogram](assets/preferences_da2.png)

*Bild: Inställningar för skrivbordsprogram.*

## Avinstallera appen {#uninstall-the-app}

Så här avinstallerar du programmet i Windows:

1. Överför alla ändringar för [!DNL Experience Manager] att undvika att förlora redigeringar. Se [Redigera resurser och överföra uppdaterade resurser till [!DNL Experience Manager]](using.md#edit-assets-upload-updated-assets). Logga ut och [!UICONTROL Exit] appen.

1. Ta bort appen när du tar bort andra operativsystemsprogram. Avinstallera det från Lägg till och ta bort program i Windows.

1. Markera kryssrutan om du vill ta bort cachen och loggarna.

   ![Avinstallera dialogrutan för att ta bort loggar och cacheminne](assets/uninstall_da2.png)

1. Följ instruktionerna på skärmen. Starta om datorn när du är klar.

Så här avinstallerar du programmet på Mac:

1. Överför alla ändringar för [!DNL Experience Manager] att undvika att förlora redigeringar. Se [Redigera resurser och överföra uppdaterade resurser till [!DNL Experience Manager]](using.md#edit-assets-upload-updated-assets). Logga ut och [!UICONTROL Exit] appen.

1. Ta bort `Adobe Experience Manager Desktop.app` från `/Applications`.

Du kan även rensa interna programcacheminnen på Mac och avinstallera programmet genom att köra följande kommando i terminalen:

```shell
/Applications/Adobe Experience Manager Desktop/Contents/Resources/uninstall-osx/uninstall.sh
```
