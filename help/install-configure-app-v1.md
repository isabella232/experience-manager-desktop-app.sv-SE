---
title: Installera och konfigurera datorprogrammet v1.10
description: Installera och konfigurera [!DNL Experience Manager] desktop app version 1.10 to work with [!DNL Assets] servrar och mappa resurserna som ska monteras som en enhet på skrivbordet.
translation-type: tm+mt
source-git-commit: cc4ce762ad1d7f4c5a54ab6bac9d1a872e3d18c9
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 0%

---


# Installera och konfigurera [!DNL Experience Manager]-datorprogrammet v1.10 {#install-and-configure-aem-desktop-app}

Med [!DNL Experience Manager]-datorprogrammet är resurserna i [!DNL Experience Manager] enkelt tillgängliga på ditt lokala skrivbord och kan användas i alla skrivbordsprogram. Resurser kan enkelt visas i Finder eller Utforskaren i Windows, öppnas i skrivbordsprogram och ändras lokalt. Ändringarna sparas sedan i [!DNL Experience Manager] när du överför och en ny version skapas i databasen.

Tack vare en sådan integrering kan olika roller i organisationen hantera mediefilerna centralt i Assets och få tillgång till dem i Creative Cloud och andra program, samtidigt som det är enkelt att följa de olika standarderna, inklusive branding.

Om du vill använda [!DNL Experience Manager]-datorprogrammet

* Kontrollera att din [!DNL Experience Manager]-serverversion stöds av [!DNL Experience Manager]-datorprogrammet. Se [kompatibilitetsmatrisen](release-notes-of-v1.md#compatibilitymatrix).

* Hämta och installera programmet.

* Testa anslutningen med några resurser. Se [Få åtkomst till och öppna resurser på skrivbordet](use-app-v1.md#openondesktop).

## Systemkrav, krav och nedladdningslänkar {#system-requirements-prerequisites-and-download-links}

Mer information finns i [[!DNL Experience Manager] versionsinformationen för skrivbordsappen](release-notes-of-v1.md).

## Installera och anslut appen till [!DNL Experience Manager]-servern {#install-and-connect-aem-desktop-app-to-aem-server}

Mer information finns i [Installera och ansluta [!DNL Experience Manager] desktop app to [!DNL Experience Manager] server](use-app-v1.md#installandconnect).

>[!NOTE]
>
>Endast en instans av [!DNL Experience Manager]-datorprogrammet kan installeras och vara aktiv åt gången.

## Filhantering {#file-handling}

När du ändrar en fil från en nätverksresursplats som monterats av skrivbordsprogrammet, sparas filerna på den platsen i två faser. I den första fasen sparas en fil lokalt. Användaren kan spara filen och fortsätta arbeta med den utan att vänta på att överföringen ska slutföras.

I den andra fasen överför skrivbordsprogrammet den uppdaterade filen till [!DNL Experience Manager]-servern efter en fördefinierad fördröjning (till exempel 30s). Den här åtgärden utförs i bakgrunden. Använd alternativet Visa resursstatus för att visa överföringsåtgärdens status.

1. Överför en resurs till Assets.

1. Klicka på ikonen [!DNL Experience Manager] för datorprogrammet i verktygsfältet.

1. Välj alternativet Visa resursstatus på menyn.

1. Granska överföringsåtgärdens status i dialogrutan.

>[!NOTE]
>
>[!DNL Experience Manager] skrivbordsappen kan hantera resurser som är upp till 40 GB stora.

## Anslut till en [!DNL Experience Manager]-instans bakom en dispatcher {#connect-to-an-aem-instance-behind-a-dispatcher}

Metoderna copy och move i Assets API kräver att följande ytterligare rubriker skickas till [!DNL Experience Manager]:

* X-Destination
* X-djup
* X-Overwrite

[!DNL Experience Manager] Skrivbordet ansluts till  [!DNL Experience Manager] med en URL som innehåller standardporten. Därför bör inställningen `virtualhosts` i dispatcherkonfigurationen innehålla standardportnumret. Mer information om konfigurationen av `virtualhosts` finns i [identifiera virtuella värdar](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#identifying-virtual-hosts-virtualhosts).

Mer information om hur du konfigurerar dispatchern att skicka genom dessa ytterligare rubriker finns i [Ange HTTP-rubriker](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#specifying-the-http-headers-to-pass-through-clientheaders).

### Proxystöd {#proxy-support}

[!DNL Experience Manager] datorprogrammet använder systemets fördefinierade proxy för att ansluta till Internet via HTTPS. Appen kan bara ansluta med en nätverksproxy som inte kräver extra autentisering.

Om du konfigurerar eller ändrar proxyserverinställningarna för Windows (Internetalternativ > LAN-inställningar) startar du om [!DNL Experience Manager]-datorprogrammet så att ändringarna börjar gälla.

>[!NOTE]
>
>Proxykonfigurationen används bara när du startar skrivbordsprogrammet. Stäng och starta om programmet för att ändringarna ska börja gälla.

Om din proxy kräver autentisering kan IT-teamet tillåta att Experience Manager Assets-URL:en i proxyserverinställningarna tillåter att programtrafiken passerar igenom.

## Anpassa dialogrutan Resursinformation {#customize-the-asset-info-dialog}

Du kan anpassa dialogrutan Resursinformation genom att täcka över en eller båda av dessa komponenter:

* Gränssnittssidan för Granite på `/libs/dam/gui/content/assets/moreinfo`.

* HTL-komponenten `/css/javascript` vid `/libs/dam/gui/components/admin/moreinfo`.

Vilken komponent som överlappas beror på typen av anpassning. Om du vill ändra vilka komponenter som visas som en del av dialogrutan Resursinformation ska du täcka över användargränssnittssidan för Granite. Om du vill ändra HTML-, CSS- eller JavaScript-innehållet i dialogrutan ska du täcka över HTML-komponenten.

## Hantera cache {#manage-cache}

I Windows är cachen `%LOCALAPPDATA%\Adobe\AssetsCompanion\Cache\`, där är en kodad version av värddatorn [!DNL Experience Manager] som konfigurerats i skrivbordsprogrammet. `http://localhost:4502` visas till exempel som `http%3A%2F%2Flocalhost%3A4502%2F`.

I Mac OS X är en liknande katalog `~/Library/Group Containers/group.com.adobe.aem.desktop/cache`.

### Alternativ i appen för att hantera cache {#in-app-option-to-manage-cache}

Du kan styra hur mycket diskutrymme som finns tillgängligt för lokal cachelagring. Artefakterna från Assets-servern cachelagras lokalt för en smidigare upplevelse. Du kan ändra standardinställningarna så att de passar dina behov. Du kan även rensa cachen för att hämta alla resurser på nytt. Om du vill ange önskade alternativ klickar du på programmets ikon och sedan på **[!UICONTROL Advanced]** > **[!UICONTROL Manage Cache]**. ****

>[!NOTE]
>
>När du rensar cachen bevaras ändringarna som inte sparats. Alla resurser som inte har checkats in på [!DNL Experience Manager]-servern behålls och tas inte bort.

### Ändra platsen för cachen i Windows {#change-location-of-cache-on-windows}

Standardplatsen för cacheminnet för [!DNL Experience Manager]-datorprogrammet är följande:

* I Windows `%LocalAppData%\Adobe\AssetsCompanion\Cache\EncodedAEMEndpoint`.

* I Mac `~/Library/Group/Containers/group.com.adobe.aem.desktop/cache/EncodedAEMEndpoint`.

`EncodedAEMEndpoint` är programmets konfigurerade  [!DNL Experience Manager] slutpunkts-URL. Värdet är en kodad version av mål-URL:en för [!DNL Experience Manager]-servern. Om programmet till exempel har `http://localhost:4502` som mål är katalognamnet `http%3A%2F%2Flocalhost%3A4502`. Windows-sökvägen till cachekatalogen i det här exemplet är `%LocalAppData%\Adobe\AssetsCompanion\Cache\http%3A%2F%2Flocalhost%3A4502`.

Om du vill peka programmet mot en annan mapp eller enhet redigerar du programmets konfigurationsfil.

1. Navigera till programmets installationskatalog. Standardplatsen i Windows är `C:\Program Files (x86)\Adobe\Adobe Experience Manager Desktop`.

1. Redigera filen Adobe Experience Manager Desktop.exe.config med en textredigerare.

   Administratörsbehörighet krävs för att spara ändringar i den här filen.

1. Sök efter strängen ProxyCacheRoot. Du ser att dess värde är inställt på cacheplatsen `%LocalAppData%\Adobe\AssetsCompanion\Cache`. Ändra bara det här värdet till en giltig sökväg.

   >[!NOTE]
   >
   >Programmet skapar automatiskt en *&lt;Encoded AEM Endpoint>*-underkatalog. Det går inte att konfigurera det här beteendet.

>[!MORELIKETHIS]
* [Introduktion  [!DNL Experience Manager] till datorprogrammet](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/creative-workflows/aem-desktop-app.html).
* [Använd  [!DNL Experience Manager] datorprogrammet](use-app-v1.md).
* [ [!DNL Experience Manager] Felsökning av skrivbordsprogram](troubleshoot-app-v1.md).

