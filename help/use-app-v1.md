---
title: Använd version 1.x av AEM-skrivbordsappen.
description: Lär dig hur du använder Adobe Experience Manager-datorprogrammet version 1.x och optimerar ditt arbete med resurser på datorn.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 68cc5ee80aa12c08b48098ad666ca694b843405a

---


# Använd AEM-datorprogrammet v1.x {#use-aem-desktop-app-v1x}

Med appen är resurserna i AEM lättillgängliga på din lokala dator och kan användas i alla datorprogram. Resurser kan enkelt visas i Finder eller Utforskaren i Windows, öppnas i skrivbordsprogram och ändras lokalt - ändringarna sparas i AEM med en ny version som skapas i databasen.

Tack vare en sådan integrering kan olika roller i organisationen hantera resurser centralt i AEM Assets och få tillgång till dem i Creative Cloud och andra program, samtidigt som det blir enkelt att följa de olika standarderna, inklusive branding.

De viktigaste uppgifterna du gör med AEM-datorprogrammet v1 är:

1. [Anslut till en AEM-server](#installandconnect)
1. [Öppna resurser direkt på skrivbordet](#openondesktop)
1. [Redigera och checka ut resurser från datorn](#workonassets)
1. [Överför resurser och mappar i grupp](#bulkupload)

Information om de olika rekommenderade åtgärderna och inte finns i [Bästa metoderna för att använda programmet](best-practices-for-v1.md). Om du har problem med appen kan du läsa om hur du [felsöker AEM-skrivbordet](troubleshoot-app-v1.md).

>[!NOTE]
>
>AEM-datorprogrammet introducerades i AEM 6.1-versionen och kallades AEM Assets Companion App.

## AEM-kontaktytor i det kreativa arbetsflödet {#aem-desktop-app-touch-points-in-the-creative-workflow}

AEM Desktop-appen, tillsammans med AEM Assets, kan integreras i ditt kreativa arbetsflöde och erbjuder följande kontaktytor.

![AEM-appens kontaktytor i det kreativa arbetsflödet](assets/aem_desktopapp_workflow.png)

AEM-appens kontaktytor i det kreativa arbetsflödet

## Installera och ansluta AEM-datorprogrammet till AEM-servern {#installandconnect}

Innan du kan börja skapa eller redigera de kreativa resurserna måste du ansluta datorprogrammet till AEM Assets-servern för att hämta och överföra resurser i databasen. Utför följande uppgifter:

1. [Installera programmet](#installapp).
1. [Ange inställningar](#inapppref) och anslutningsinformation.
1. [Anslut till en AEM-server](#connect) och montera resurskatalogen som en lokal enhet.
1. [Aktivera skrivbordsåtgärder](#desktopactions) på AEM-servern.

AEM-skrivbordsappen använder en HTTPS-anslutning för att ansluta till AEM-servern för att överföra dina resurser på ett säkert och robust sätt.

>[!NOTE]
>För en del av eller alla installations- och konfigurationssteg kan du behöva hjälp av AEM-administratören eller systemadministratören.

### Installera programmet {#installapp}

Om du vill använda AEM-datorprogrammet måste du se till att din AEM-serverversion stöds av AEM-datorprogrammet. Hämta lämplig installationsfil (binär) för operativsystemet (Mac eller Windows) och installera programmet.

Det kan vara nödvändigt att göra en detaljerad konfiguration beroende på ditt nätverk och dina systeminställningar. Mer information finns i [Installera och konfigurera AEM-skrivbordsappen](install-configure-app-v1.md) .

1. Gå till hämtningssidan [för](https://helpx.adobe.com/experience-manager/kb/download-companion-app.html) AEM-appen och hämta den binärfil som passar ditt operativsystem.
1. Starta den hämtade installationsfilen och följ instruktionerna på skärmen för att installera programmet.

   >[!NOTE]
   >Endast en instans av AEM-datorprogrammet kan installeras och vara aktiv åt gången.

### Förstå alternativen och inställningarna i appen {#inapppref}

Programmet tillåter inställningar för att ansluta och koppla från AEM-servrar, visa status för överföringar, hantera lokal cache och så vidare. Standardinställningarna fungerar för en typisk användare av programmet. Du kan ändra inställningarna för att få ut mer av programmet och av integrationen med AEM-servern. De olika inställningarna beskrivs nedan i detalj.

**Utforska resurser** Öppna den lokala enheten där AEM Resurser-databasen är monterad. Du kan med andra ord utforska de resurser som nu finns tillgängliga på din lokala dator.

**Visa resursstatus** När ändrade resurser överförs eller nya resurser läggs till i AEM Resurser-databasen, överförs resurserna i bakgrunden. Bakgrundsuppladdningen möjliggör smidiga åtgärder utan att du behöver vänta tills överföringen är klar, särskilt för stora resurser. Du kan spara ändringarna lokalt och glömma det. Det tar ett tag att skicka resurserna till servern, beroende på den tillgängliga bandbredden. Du kan kontrollera överföringsstatus tillsammans med mer grundläggande information.

**Alternativ** Klicka/tryck på Alternativ i AEM-appfältet för datorer för att komma åt inställningar för att starta programmet när datorn startas; ansluta till AEM-servern när appen startas, och ändra den lokala enhetsbokstaven där AEM Resurser är tillgängliga efter montering.

**Avancerat > Hantera cacheminne** Du kan styra hur mycket diskutrymme som är tillgängligt för lokal cachning. Artefakterna från AEM Resurser-servern cachas lokalt för en smidigare upplevelse. Du kan ändra standardinställningarna så att de passar dina behov. Du kan även rensa cachen för att hämta alla resurser på nytt. När du rensar cachen bevaras ändringarna som inte sparats. Resurser som inte har checkats in på AEM-servern behålls och tas inte bort.

### Ansluta till en AEM-server {#connect}

Programmet har stöd för proxykonfiguration i Mac och Windows. Konfigurationen läses när appen startas. Om du ändrar proxyinställningarna startar du om programmet så att ändringarna börjar gälla.

>[!NOTE]
>
>Om du ändrar proxyinställningarna startar du om programmet så att ändringarna börjar gälla. Annars fortsätter programmet att använda den tidigare konfigurerade proxyservern.

1. Starta AEM-datorprogrammet. Om du vill mappa din AEM-instans till appen anger du AEM-servern i formatet `https://[aem-server-url]:[port]`.

   ![Autentisera på Mac och ange AEM-server-URL](assets/aem_desktop_app_server_url.png)

1. Ange användarnamn och lösenord för instansen på inloggningsskärmen. Om du vill ange en alternativ AEM-instans väljer du **[!UICONTROL Alternate Login URL]** alternativet.

   ![Ange AEM-serverns autentiseringsuppgifter på inloggningsskärmen på AEM Desktop](assets/chlimage_1-2.png)

### Aktivera skrivbordsåtgärder i AEM-webbgränssnittet {#desktopactions}

I Assets-användargränssnittet kan du utforska resursplatserna eller checka ut och öppna resursen för redigering i ditt skrivbordsprogram. Dessa alternativ kallas skrivbordsåtgärder och är inte aktiverade som standard. Följ de här stegen för att aktivera den.

1. Klicka/tryck på ikonen Användare i det övre högra hörnet av verktygsfältet i gränssnittet Resurser.
1. Klicka **[!UICONTROL My Preferences]** för att visa **[!UICONTROL Preferences]** dialogrutan.

   ![AEM-gränssnitt med användarinställningar](assets/aem_ui_user_preferences.png)

1. I dialogrutan Användarinställningar väljer du **[!UICONTROL Show Desktop Actions For Assets]**. Klicka på **[!UICONTROL Accept]**.

   ![Markera Visa skrivbordsåtgärder för resurser för att aktivera skrivbordsåtgärder](assets/chlimage_1-3.png)

   *Bild: Markera Visa skrivbordsåtgärder för resurser om du vill aktivera skrivbordsåtgärder.*

## Få åtkomst till och öppna resurser på datorn {#openondesktop}

När du klickar på **Öppna** för att öppna en resurs på den lokala datorn hämtas resursen till dess interna cache. Programmet startar det inbyggda skrivbordsprogrammet som är associerat med filtypen för den hämtade resursen.

På Mac väljer du **Öppna** på snabbmenyn för att öppna en resurs via AEM-datorprogrammet. I Windows väljer du Öppna på webben på snabbmenyn för att öppna resursen. Öppna resursen genom att klicka/trycka på ikonen ![](assets/aemassets_icon_openondesktop.png) Öppna på skrivbordet i fönstret Resursstatus.

För Adobe InDesign-filer (INDD) väljer du **[!UICONTROL Open]** på snabbmenyn. När du klickar på det här alternativet hämtar appen de länkade resurserna till det lokala filsystemet och öppnar sedan INDD-filen i Adobe InDesign. Den här metoden ser till att nödvändiga resurser är lokalt tillgängliga när du redigerar INDD-filen.

![Alternativ på snabbmenyn för att komma åt och öppna resurser med hjälp av AEM-skrivbordsappen](assets/aem_desktopapp_mac_context_menu.png)

*Bild: Alternativ på snabbmenyn för att komma åt och öppna resurser med hjälp av AEM-skrivbordsappen.*

>[!NOTE]
>I Windows förhindrar [standardinställningen](https://support.microsoft.com/en-us/kb/2668751) för Windows 7 att AEM-skrivbordsappen hanterar resurser som är större än 50 MB.

>[!NOTE]
>
>Adobe rekommenderar att du går till Visningsalternativ i Finder på Mac och inaktiverar alternativen **Visa objektinformation**, **Visa objektförhandsgranskning** och **Visa förhandsgranskningskolumn** för den monterade AEM Resurser-mappen. Det förbättrar prestandan.

### Ytterligare alternativ i AEM-gränssnittet {#additional-options-in-aem-assets}

När du har mappat AEM Resurser-databasen till din lokala enhet kan du aktivera ytterligare ikoner och funktionen Mappöverföring visas för mappade resurser och mappar.

1. Öppna gränssnittet för AEM Resurser och för pekaren över en mapp eller en resurs för att visa skrivbordsåtgärderna som snabbåtgärder i kortvyn.

   ![I resursgränssnittet öppnar du snabbåtgärdsmenyn för att se skrivbordsåtgärder](assets/chlimage_1-4.png)

   *Bild: I resursgränssnittet öppnar du snabbåtgärdsmenyn för att se skrivbordsåtgärder.*

   Dessa skrivbordsåtgärder är också tillgängliga när du klickar på ikonen **Skrivbordsåtgärder** i verktygsfältet efter att du har valt resursen eller från verktygsfältet på resurssidan.

1. Om du vill öppna resursen i skrivbordsprogrammet som är associerat med det specifika filtillägget klickar/trycker du på snabbåtgärden **Öppna på skrivbordet** och ![Öppna på skrivbordet](assets/aemassets_icon_openondesktop.png).

   Du kan också välja **Öppna** på menyn **Skrivbordsåtgärder** i verktygsfältet.

Om du vill hitta en viss resurs i det lokala filsystemet klickar du på **Visa** snabbredigeringsikonen ![Visa](assets/aemassets_reveal_icon.png). Du kan också välja **Visa** på menyn **Skrivbordsåtgärder** i verktygsfältet.

## Förstå tillgångsstatusarna {#understand-the-asset-statuses}

| ![Ikon för Windows-standardprogram](assets/win_default.png) | Appen är ansluten till servern och alla resurser synkroniseras. |
|------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| ![Ikon för inaktiverad Windows](assets/win_disabled.png) | Appen startas men är inte ansluten till servern. Vissa resurser kanske väntar på synkronisering. |
| ![Synkroniseringsikon för Windows-fil](assets/win_sync.png) | Resurserna synkroniseras. Filerna överförs eller hämtas. Du kan se exakta statusvärden och pausa överföringar från fönstret Resursstatus. |
| ![Ikon för återanslutning av Windows](assets/win_refresh.png) | Appen försöker återansluta. Nätverksproblemen kan leda till att den kopplas från. |

## Arbeta med dina resurser {#workonassets}

### Ta en titt på resurser från AEM-webbgränssnittet {#check-out-assets-from-the-aem-web-interface}

Med AEM Resurser kan du checka ut resurser för redigering och checka in dem igen när du är klar med ändringarna. När du har checkat ut en resurs kan bara du redigera, kommentera, publicera, flytta eller ta bort resursen. När du checkar ut en resurs låses resursen och andra användare hindras från att utföra någon av dessa åtgärder. Om du vill kunna checka ut/in resurser måste du ha skrivbehörighet för dem.

Det finns två sätt att checka ut resurser från AEM-webbgränssnittet. Detaljerad information om den första metoden finns i [Checka in och checka ut filer från Assets-gränssnittet](https://docs.adobe.com/content/help/en/experience-manager-65/assets/managing/check-out-and-submit-assets.html). Följ de här stegen för de andra metoderna för att checka ut och öppna resursen när AEM-datorprogrammet är installerat.

1. Öppna gränssnittet för AEM Resurser och för pekaren över en mapp eller en resurs för att visa skrivbordsåtgärderna som snabbåtgärder i kortvyn.

   ![Alternativet Egenskaper i kortvyn](assets/chlimage_1-4.png)

   Dessa skrivbordsåtgärder är också tillgängliga när du klickar/trycker på ikonen Skrivbordsåtgärder i verktygsfältet efter att du har valt resursen eller i verktygsfältet på resurssidan.

1. Om du vill öppna resursen klickar du på/trycker på snabbåtgärden Öppna på skrivbordet ![på ikonen](assets/aemassets_icon_openondesktop.png).

   Du kan också välja Öppna på menyn Skrivbordsåtgärder i verktygsfältet.

   >[!NOTE]
   >När du redigerar en fil som just har öppnats och inte är utcheckad, kommer andra användare inte att veta att en resurs uppdateras av dig.

1. Om du vill öppna en resurs för redigering i ett Adobe Creative Cloud-program klickar/trycker du på ikonen Redigera skrivbord för snabbåtgärden ![Redigera skrivbord](assets/aemassets_icon_editdesktop.png). Då checkas även resursen ut för redigering. När du är klar med redigeringen checkar du in resursen för att uppdatera ändringarna i AEM Resurser.

   Du kan också välja Redigera på menyn Skrivbordsåtgärder i verktygsfältet.

1. Välj menyalternativet Öppna. De valda resurserna öppnas i förhandsgranskningsläge.
1. Om du vill redigera resurserna väljer du alternativet Redigera. Resurserna öppnas i redigeringsläge.

### Ta en titt på resurser från Finder i Mac OS {#check-out-assets-on-mac}

Med appen kan du checka ut resursfiler för att förhindra att andra användare ändrar de filer som du arbetar med.

1. På Mac-snabbmenyn väljer du Öppna AEM Resursmapp för att öppna Finder.

   ![Alternativ på snabbmenyn för att komma åt och öppna resurser med hjälp av AEM-skrivbordsappen](assets/aem_desktopapp_mac_context_menu.png)

   Alternativ på snabbmenyn för att komma åt och öppna resurser med hjälp av AEM-skrivbordsappen

1. Navigera till resursen som du vill checka ut.

   ![Öppna i snabbmenyn för AEM Resurser på Mac](assets/chlimage_1-5.png)

1. Högerklicka på resursen och välj Mer resursinformation på snabbmenyn.
1. I dialogrutan Resursinformation klickar/trycker du på ikonen Checka ut för att checka ut resursen. Ikonen Checka ut växlar till ikonen för incheckning när du har klickat/tryckt på den.

   ![Bläddra till resurs att checka ut](assets/chlimage_1-6.png)

1. Om du vill checka in resursen så att den är tillgänglig för andra användare klickar du på/trycker på incheckningsikonen i dialogrutan Resursinformation.

### Checka ut resurser i Windows {#check-out-assets-on-windows}

Med appen kan du checka ut resursfiler för att förhindra att andra användare ändrar de filer som du arbetar med.

1. Välj Utforska resurser på snabbmenyn för att öppna Utforskaren.
1. I Utforskaren navigerar du till platsen för resursen som du vill checka ut.

   ![Ikonen Checka ut växlar](assets/chlimage_1-7.png)

1. Högerklicka på resursen och välj Öppna på webben på snabbmenyn.
1. Klicka/tryck på ikonen Checka ut i dialogrutan Resursinformation. Ikonen Checka ut växlar till ikonen Checka in.

   ![Ikonen Checka ut växlar](assets/chlimage_1-8.png)

1. Granska resursen i Utforskaren. Låsikonen på ![tillgångslåsikonen](assets/aemassets_icon_lockcheckout.png) anger att du har checkat ut resursen.

   >[!NOTE]
   >Låsikonen kan visas efter en fördröjning. AEM-skrivbordsappen cachelagrar resurserna för snabb åtkomst så det kan ta en stund att uppdatera den låsta statusen.

1. Om du vill checka in resursen så att den är tillgänglig för andra användare klickar du på/trycker på ikonen för incheckning i dialogrutan **Resursinformation** .

### Checka in en resurs med Finder eller Utforskaren och med webbgränssnittet {#check-in-an-asset-using-finder-or-explorer-and-using-web-interface}

När du är klar med redigeringen av resurserna sparar du resurserna i skrivbordsprogrammet. På snabbmenyn väljer du **Mer resursinformation** och klickar på incheckning.

Resurserna överförs till AEM-servern. Du kan också kontrollera överföringsstatus genom att välja **Visa resursstatus** från systemfältsikonen. Du kan också checka in en resurs från AEM-webbgränssnittet. Klicka på de utcheckade resurserna eller markera dem. Klicka på ikonen för ![incheckning](assets/aemassets_icon_checkin.png)i verktygsfältet.

En resurs överförs automatiskt till AEM efter att eventuella ändringar har sparats lokalt. Incheckningen gör resursen tillgänglig för andra AEM-användare för redigering.

### Massöverföra resurser och mappar till AEM-servern {#bulkupload}

Med AEM Desktop kan du överföra en hel mapp med resurser från din lokala filkatalog till AEM Assets. På så sätt överförs alla resurser i mappen gruppvis i stället för att behöva överföra dem en åt gången.

1. I resursgränssnittet klickar/trycker du på **Skapa** i verktygsfältet och väljer **Överför mapp** på menyn.
1. Bläddra till mappen som du vill överföra och markera den.
1. Klicka/tryck på OK. I dialogrutan Resursstatus visas status för överföringen.

   ![Se status för överföringen i fönstret Resursstatus](assets/aem_desktopapp_bulkupload_status.png)

   Se status för överföringen i fönstret Resursstatus

   >[!NOTE]
   >Du kan pausa eller avbryta överföringen manuellt genom att klicka/trycka på lämplig ikon.

1. När mappen har överförts stänger du dialogrutan och navigerar till resursgränssnittet. Den överförda mappen visas i webbgränssnittet.

Adobe rekommenderar inte att du kopierar och klistrar in eller drar ett större antal filer eller kapslade mappar från det lokala filsystemet till nätverksresursområdet. Programmet kan inte styra överföringsprocessen på grund av tekniska begränsningar och prestandan är dålig.

Du kan också välja filer/mappar som du vill överföra till AEM i Finder eller Utforskaren, kopiera dem till systemets Urklipp, navigera till målmappen i nätverksresursområdet och välja **Klistra in resurser** på snabbmenyn för AEM-skrivbordsappen. På så sätt börjar AEM-skrivbordsappen överföra inklistrade resurser som liknar alternativet **Överför mapp** som finns i AEM-webbgränssnittet.

>[!MORELIKETHIS]
>
>* [Introduktion till AEM-datorprogrammet](https://helpx.adobe.com/customer-care-office-hours/aem/desktop-app.html)
>* [Förstå in- och utcheckning med AEM-datorprogrammet](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/collaboration/checkin-checkout-technical-video-understand.html)
>* [Felsöka AEM-skrivbordsprogram](troubleshoot-app-v1.md)

