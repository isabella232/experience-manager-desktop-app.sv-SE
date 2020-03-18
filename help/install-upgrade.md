---
title: Installera och konfigurera datorprogrammet Adobe Experience Manager
description: Installera och konfigurera Adobe Experience Manager-skrivbordsappen så att den fungerar med Adobe Experience Manager Assets-servrar och hämta resurserna på det lokala filsystemet.
uuid: 79bc9de9-5708-41f9-ac43-68c1fd2a2129
contentOwner: AG
products: SG_EXPERIENCEMANAGER/6.3/ASSETS
discoiquuid: f6365302-1690-4719-9b8c-035719422740
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: ac4be2cb69a112f393ec76d5d95987634d0c9c46

---


# Installera Adobe Experience Manager-datorprogrammet {#install-app-v2}

Med Adobe Experience Managers skrivbordsapp är resurserna i Experience Manager lättillgängliga på din lokala dator och kan användas i alla datorprogram. Resurser kan enkelt visas i Finder eller Utforskaren i Windows, öppnas i skrivbordsprogram och ändras lokalt. Ändringarna sparas sedan i Experience Manager när du överför och en ny version skapas i databasen.

Tack vare en sådan integrering kan olika roller i organisationen hantera resurser centralt i Adobe Experience Manager Assets och få tillgång till dem i Creative Cloud och andra program, samtidigt som det är enkelt att följa de olika standarderna, inklusive branding.

Om du vill använda datorprogrammet Experience Manager

* Kontrollera att Experience Manager-serverversionen stöds av Experience Manager-datorprogrammet. Se [kompatibilitetsmatrisen](release-notes-of-v1.md#compatibilitymatrix).
* Hämta och installera programmet.
* Testa anslutningen med några resurser. Se [Åtkomst och öppna resurser på skrivbordet](use-app-v1.md#openondesktop).

## Systemkrav, krav och nedladdningslänkar {#tech-specs-v2}

Mer information finns i versionsinformationen för [Experience Manager-datorprogrammet](release-notes.md).

## Uppgradera från app v1.x till app v2 {#upgrade-from-previous-version}

Om du är en befintlig användare av appen måste du förstå skillnaderna och likheterna mellan den tidigare och den senaste versionen av appen. Följ även riktlinjerna nedan för att gå över från v1.x till den senaste versionen.

>[!NOTE]
>
>Skrivbordsappen v1.x och v2 kan inte finnas samtidigt på en dator. Avinstallera den andra versionen innan du installerar en version.

Följ dessa anvisningar för att uppgradera från v1.x till den senaste versionen av programmet:

1. Synkronisera alla resurser innan du uppgraderar. Överför alla ändringar med appen v1.x. Detta för att undvika att ändringar går förlorade när appen v1.x avinstalleras.
1. Avinstallera app v1.x. Rensa cachen när v1.x avinstalleras.
1. Starta om datorn.
1. Hämta och installera den senaste appen. Följ instruktionerna nedan.

## Installera {#install-v2}

Följ de här stegen för att installera skrivbordsappen. Avinstallera alla befintliga Adobe Experience Manager-datorprogram v1.x innan du installerar den senaste appen. Mer information finns ovan.

1. Ha URL:en och autentiseringsuppgifterna för din AEM-distribution till hands.
1. Hoppa över det här steget om du använder AEM 6.4.4 och senare eller AEM 6.5.0 eller senare. Kontrollera att din AEM-konfiguration uppfyller kompatibilitetskraven som anges i versionsinformationen. Hämta vid behov [kompatibilitetspaketet](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/featurepack/adobe-asset-link-support) och installera det med AEM Package Manager som AEM-administratör. Information om hur du installerar ett paket finns i [Så här arbetar du med paket](https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/package-manager.html).
1. Kör installationsprogrammets binärfil och följ instruktionerna på skärmen.
1. I Windows kan installationsprogrammet uppmana dig att installera `Visual Studio C++ Redistributable 2015`. Installera den genom att följa instruktionerna på skärmen. Om installationen misslyckas installerar du den manuellt. Hämta installationsprogrammet [här](https://www.microsoft.com/en-us/download/details.aspx?id=52685) och installera både `vc_redist.x64.exe` och `vc_redist.x86.exe` filer. Kör installationsprogrammet för AEM-skrivbordsappen igen.
1. Starta om datorn enligt anvisningarna. Starta skrivbordsappen för att konfigurera den.
1. Om du vill ansluta programmet till en AEM-databas klickar du på programikonen i fältet för att starta programmet. Ange adressen till AEM-instansen. Klicka på **[!UICONTROL Connect]** och ange autentiseringsuppgifterna.

   ![Anslutningsskärmen för skrivbordsprogrammet till](assets/connect_da2.png "inmatningsserverns adressAnslutningsskärmen till inmatningsserveradressen")

   >[!Cauktion]
   >
   >Kontrollera att det inte finns några inledande eller avslutande blanksteg före eller efter adressen till AEM-servern. Annars kan programmet inte ansluta till AEM-servern.

1. När anslutningen lyckades kan du visa listan över mappar och resurser som är tillgängliga i rotmappen för AEM DAM. Du kan bläddra bland mapparna inifrån programmet.

   ![När du loggar in visas DAM-](assets/firstview_da2.png "innehållet i appen. När du loggar in visas DAM-innehållet i appen")

1. (AEM 6.5.1 eller senare) Om du använder datorprogrammet med AEM 6.5.1 eller senare, uppgraderar du S3- eller Azure-anslutningen till version 1.10.4 eller senare. Se [Azure Connector](https://helpx.adobe.com/experience-manager/6-5/sites/deploying/using/data-store-config.html#AzureDataStore) eller [S3 Connector](https://helpx.adobe.com/experience-manager/6-5/sites/deploying/using/data-store-config.html#AmazonS3DataStore).

   Om du är Adobe Managed Services-kund (AMS) kontaktar du Adobes kundtjänst.

## Ange inställningar {#set-preferences}

Om du vill ändra inställningarna klickar du på ikonen ![](assets/do-not-localize/more_options_da2.png) Fler alternativ och **[!UICONTROL Preference]** ikonen ![](assets/do-not-localize/preferences_icon_da2.png)Inställningar. Justera värdena för följande i **[!UICONTROL Preferences]** fönstret:

* [!UICONTROL Launch application on login].
* [!UICONTROL Show window when application starts].
* **[!UICONTROL Cache Directory]**: Plats för appens lokala cache (den innehåller de lokalt hämtade resurserna).
* **[!UICONTROL Network Drive Letter]**: Enhetsbokstaven som används för att mappa till AEM DAM. Ändra inte detta om du inte är säker. Appen kan mappas till valfri enhetsbeteckning i Windows. Om två användare placerar resurser från olika enhetsbokstäver kan de inte se de resurser som placerats ut av varandra. Resursernas sökväg ändras. Resurserna förblir placerade i den binära filen (till exempel INDD) och tas inte bort. Appen visar alla tillgängliga enhetsbokstäver och som standard använder den senast tillgängliga bokstaven som vanligtvis är `Z`.
* **[!UICONTROL Maximum Cache Size]**: Tillåten cache på hårddisken i GB som används för att lagra lokalt hämtade resurser.
* **[!UICONTROL Current cache size]**: Lagringsstorlek för lokalt hämtade resurser. Informationen visas först när resurserna har hämtats med appen.
* **[!UICONTROL Automatically download linked assets]**: Resurserna som placeras i de Creative Cloud-program som stöds hämtas automatiskt om du hämtar originalfilen.
* **[!UICONTROL Maximum number of downloads]**: När du hämtar resurser för första gången (via Visa, Öppna, Redigera, Hämta eller liknande) hämtas resurserna endast om gruppen innehåller mindre än det här antalet. Standardvärdet är 50. Ändra inte om du är osäker. Om du ökar värdet kan det leda till längre väntetider och om du minskar värdet kanske du inte kan hämta nödvändiga resurser eller mappar på en gång.

Logga ut från AEM-servern om du vill uppdatera inställningarna som inte är tillgängliga. När du har uppdaterat inställningarna klickar du på ![Spara inställningar](assets/do-not-localize/save_preferences_da2.png) för att spara ändringarna.

![Inställningar och](assets/preferences_da2.png "inställningar för AEM-skrivbordsprogramInställningar för skrivbordsprogram")

## Avinstallera appen {#uninstall-the-app}

Så här avinstallerar du programmet i Windows:

1. Överför alla ändringar till AEM för att undvika att förlora redigeringar. Se [Redigera resurser och överföra uppdaterade resurser till AEM](using.md#edit-assets-upload-updated-assets). Logga ut och [!UICONTROL Exit] appen.
1. Ta bort appen när du tar bort andra operativsystemsprogram. Avinstallera det från Lägg till och ta bort program i Windows.
1. Markera kryssrutan om du vill ta bort cachen och loggarna.
   ![Avinstallationsdialogrutan för att ta bort loggar och](assets/uninstall_da2.png "cacheAvinstallationsdialogrutan för att ta bort loggar och cacheminne")
1. Följ instruktionerna på skärmen. Starta om datorn när du är klar.

Så här avinstallerar du programmet på Mac:

1. Överför alla ändringar till AEM för att undvika att förlora redigeringar. Se [Redigera resurser och överföra uppdaterade resurser till AEM](using.md#edit-assets-upload-updated-assets). Logga ut och [!UICONTROL Exit] appen.
1. Ta bort `Adobe Experience Manager Desktop.app` från `/Applications`.

Du kan även rensa interna programcacheminnen på Mac och avinstallera programmet genom att köra följande kommando i terminalen:
`/Applications/Adobe Experience Manager Desktop/Contents/Resources/uninstall-osx/uninstall.sh`
