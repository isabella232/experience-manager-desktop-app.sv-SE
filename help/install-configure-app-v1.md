---
title: Installera och konfigurera AEM-datorprogrammet version 1.x
description: Installera och konfigurera AEM-skrivbordsappversion 1.x så att den fungerar med AEM Assets-servrar och mappa resurserna som ska monteras som en enhet på skrivbordet.
uuid: 79bc9de9-5708-41f9-ac43-68c1fd2a2129
contentOwner: AG
products: SG_EXPERIENCEMANAGER/6.3/ASSETS
discoiquuid: f6365302-1690-4719-9b8c-035719422740
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 68cc5ee80aa12c08b48098ad666ca694b843405a

---


# Installera och konfigurera AEM-datorprogrammet v1.x {#install-and-configure-aem-desktop-app}

Med hjälp av AEM-skrivbordsappen är resurserna i AEM lättillgängliga på din lokala dator och kan användas i alla datorprogram. Resurser kan enkelt visas i Finder eller Utforskaren i Windows, öppnas i skrivbordsprogram och ändras lokalt. Ändringarna sparas sedan i AEM när du överför och en ny version skapas i databasen.

Tack vare en sådan integrering kan olika roller i organisationen hantera resurser centralt i AEM Assets och få tillgång till dem i Creative Cloud och andra program, samtidigt som det blir enkelt att följa de olika standarderna, inklusive branding.

Om du vill använda AEM-datorprogrammet

* Kontrollera att din AEM-serverversion stöds av AEM-datorprogrammet. Se [kompatibilitetsmatrisen](release-notes-of-v1.md#compatibilitymatrix).
* Hämta och installera programmet.
* Testa anslutningen med några resurser. Se [Åtkomst och öppna resurser på skrivbordet](use-app-v1.md#openondesktop).

## Systemkrav, krav och nedladdningslänkar {#system-requirements-prerequisites-and-download-links}

Mer information finns i versionsinformationen för [AEM-skrivbordsappen](release-notes-of-v1.md).

## Installera och ansluta AEM-datorprogrammet till AEM-servern {#install-and-connect-aem-desktop-app-to-aem-server}

Mer information finns i [Installera och ansluta AEM-datorprogrammet till AEM-servern](use-app-v1.md#installandconnect).

>[!NOTE]
>
>Endast en instans av AEM-datorprogrammet kan installeras och vara aktiv åt gången.

## Filhantering {#file-handling}

När du ändrar en fil från en nätverksresursplats som monterats av skrivbordsprogrammet, sparas filerna på den platsen i två faser. I den första fasen sparas en fil lokalt. Användaren kan spara filen och fortsätta arbeta med den utan att vänta på att överföringen ska slutföras.

I den andra fasen överför skrivbordsappen den uppdaterade filen till AEM-servern efter en fördefinierad fördröjning (till exempel 30-tal). Den här åtgärden utförs i bakgrunden. Använd alternativet Visa resursstatus för att visa överföringsåtgärdens status.

1. Överför en resurs till AEM Resurser.
1. Klicka på/tryck på ikonen för AEM-skrivbordsappen i verktygsfältet.
1. Välj alternativet Visa resursstatus på menyn.
1. Granska överföringsåtgärdens status i dialogrutan.

>[!NOTE]
>
>AEM-skrivbordsappen kan hantera resurser på upp till 40 GB.

## Anslut till en AEM-instans bakom en dispatcher {#connect-to-an-aem-instance-behind-a-dispatcher}

Metoderna copy och move i Assets API kräver att följande ytterligare rubriker skickas till AEM:

* X-Destination
* X-djup
* X-Overwrite

AEM-skrivbordet ansluter till AEM via en URL som innehåller standardporten. Inställningen i `virtualhosts` dispatcherns konfiguration bör därför innehålla standardportnumret. Mer information om `virtualhosts` konfiguration finns i [Identifiera virtuella värdar](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#identifying-virtual-hosts-virtualhosts).

Mer information om hur du konfigurerar dispatchern att skicka genom dessa ytterligare rubriker finns i [Ange HTTP-rubriker](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#specifying-the-http-headers-to-pass-through-clientheaders).

### Stöd för proxy {#proxy-support}

AEM-skrivbordsappen använder systemets fördefinierade proxy för att ansluta till Internet via HTTPS. Appen kan bara ansluta med en nätverksproxy som inte kräver extra autentisering.

Om du konfigurerar eller ändrar proxyserverinställningarna för Windows (Internetalternativ > LAN-inställningar) startar du om AEM-datorprogrammet så att ändringarna börjar gälla.

>[!NOTE]
>
>Proxykonfigurationen används bara när du startar skrivbordsprogrammet. Stäng och starta om programmet för att ändringarna ska börja gälla.

Om din proxy kräver autentisering kan IT-teamet vitlista URL:en för AEM-resurser i proxyserverinställningarna så att programtrafiken kan passera igenom.

## Anpassa dialogrutan Resursinformation {#customize-the-asset-info-dialog}

Du kan anpassa dialogrutan Resursinformation genom att täcka över en eller båda av dessa komponenter:

* Gränssnittssidan för Granite finns på `/libs/dam/gui/content/assets/moreinfo`
* HTL- `/css/javascript` komponenten vid `/libs/dam/gui/components/admin/moreinfo`

Vilken komponent som överlappas beror på typen av anpassning. Om du vill ändra vilka komponenter som visas som en del av dialogrutan Resursinformation ska du täcka över användargränssnittssidan för Granite. Om du vill ändra HTML-/CSS-/JavaScript-innehållet i dialogrutan ska du täcka över HTML-komponenten.

## Hantera cache {#manage-cache}

I Windows finns cacheminnet, `%LOCALAPPDATA%\Adobe\AssetsCompanion\Cache\`där är en kodad version av AEM-värden som konfigurerats i skrivbordsappen. Visas till exempel `http://localhost:4502` som `http%3A%2F%2Flocalhost%3A4502%2F`.

I Mac OS X finns en liknande katalog i `~/Library/Group Containers/group.com.adobe.aem.desktop/cache`.

### Alternativ i appen för att hantera cache {#in-app-option-to-manage-cache}

Du kan styra hur mycket diskutrymme som finns tillgängligt för lokal cachelagring. Artefakterna från AEM Resurser-servern cachas lokalt för en smidigare upplevelse. Du kan ändra standardinställningarna så att de passar dina behov. Du kan även rensa cachen för att hämta alla resurser på nytt. Om du vill ange önskade alternativ klickar du på programikonen och sedan på **[!UICONTROL Advanced]** > **[!UICONTROL Manage Cache]**. ****

>[!NOTE]
>
>När du rensar cachen bevaras ändringarna som inte sparats. Resurser som inte har checkats in på AEM-servern behålls och tas inte bort.

### Ändra platsen för cachen i Windows {#change-location-of-cache-on-windows}

Standardplatsen för cacheminnet för AEM-datorprogrammet är:

* Windows: `%LocalAppData%\Adobe\AssetsCompanion\Cache\EncodedAEMEndpoint`
* Mac: `~/Library/Group/Containers/group.com.adobe.aem.desktop/cache/EncodedAEMEndpoint`

`EncodedAEMEndpoint` är AEM-appens konfigurerade AEM-slutpunkts-URL. Värdet är en kodad version av mål-URL:en för AEM-servern. Om programmet till exempel har som mål `http://localhost:4502`är katalognamnet `http%3A%2F%2Flocalhost%3A4502`. Windows-sökvägen till cachekatalogen i det här exemplet är %LocalAppData%\Adobe\AssetsCompanion\Cache\http%3A%2F%2Flocalhost%3A4502.

Om du vill peka programmet mot en annan mapp eller enhet redigerar du programmets konfigurationsfil.

1. Navigera till programmets installationskatalog. Standardplatsen i Windows är `C:\Program Files (x86)\Adobe\Adobe Experience Manager Desktop`.
1. Redigera filen Adobe Experience Manager Desktop.exe.config med en textredigerare.

   Administratörsbehörighet krävs för att spara ändringar i den här filen.

1. Sök efter strängen ProxyCacheRoot. Du ser att dess värde är inställt på cacheplatsen &quot;%LocalAppData%\Adobe\AssetsCompanion\Cache&quot;. Ändra bara det här värdet till en giltig sökväg.

   >[!NOTE]
   >
   >Appen skapar automatiskt en *&lt;Encoded AEM Endpoint>* underkatalog; det här beteendet kan inte konfigureras.

>[!MORELIKETHIS]
* [Introduktion till AEM-datorprogrammet](https://helpx.adobe.com/customer-care-office-hours/aem/desktop-app.html)
* [Använd AEM-skrivbordsapp](use-app-v1.md)
* [Förstå in- och utcheckning med AEM-datorprogrammet](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/collaboration/checkin-checkout-technical-video-understand.html)
* [Använda datorprogrammet med AEM Assets](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/collaboration/checkin-checkout-technical-video-understand.html)
* [Felsökning av AEM-skrivbordsprogram](troubleshoot-app-v1.md)

