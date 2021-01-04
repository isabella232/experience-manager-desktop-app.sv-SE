---
title: Använd [!DNL Experience Manager] datorprogrammet version 1.x.
description: Lär dig hur du använder Adobe Experience Manager-datorprogram version 1.x och optimerar ditt arbete med resurser på datorn.
translation-type: tm+mt
source-git-commit: a25c1fa13895ae9eb7268e3e01c83a5f0b9d7d1d
workflow-type: tm+mt
source-wordcount: '2379'
ht-degree: 0%

---


# Använd [!DNL Experience Manager] skrivbordsapp v1.x {#use-aem-desktop-app-v1x}

Med appen är resurserna i [!DNL Experience Manager] enkelt tillgängliga på din lokala dator och kan användas i alla datorprogram. Resurser kan enkelt visas i Finder eller Utforskaren i Windows, öppnas i skrivbordsprogram och ändras lokalt - ändringarna sparas tillbaka till [!DNL Experience Manager] med en ny version som skapas i databasen.

Tack vare en sådan integrering kan olika roller i organisationen hantera mediefilerna centralt i Assets och få tillgång till dem i Creative Cloud och andra program, samtidigt som det är enkelt att följa de olika standarderna, inklusive branding.

De viktigaste uppgifterna du gör med [!DNL Experience Manager]-datorprogrammet v1 är:

1. [Anslut till  [!DNL Experience Manager] en server](#installandconnect)
1. [Öppna resurser direkt på skrivbordet](#openondesktop)
1. [Redigera och checka ut resurser från datorn](#workonassets)
1. [Överför resurser och mappar i grupp](#bulkupload)

Information om olika rekommenderade åtgärder och inte finns i [metodtips för att använda app](best-practices-for-v1.md). Om du har problem med appen kan du läsa om hur du [felsöker [!DNL Experience Manager] skrivbordet](troubleshoot-app-v1.md).

>[!NOTE]
>
>[!DNL Experience Manager] datorprogrammet introducerades i version  [!DNL Experience Manager] 6.1 och anropades  [!DNL Experience Manager Assets Companion App].

## [!DNL Experience Manager] pekpunkter i datorprogrammet i det kreativa arbetsflödet  {#aem-desktop-app-touch-points-in-the-creative-workflow}

[!DNL Experience Manager] skrivbordsappen, tillsammans med  [!DNL Assets], integreras i ditt kreativa arbetsflöde och erbjuder följande kontaktytor.

![[!DNL Experience Manager] pekpunkter i datorprogrammet i det kreativa arbetsflödet](assets/aem_desktopapp_workflow.png)

[!DNL Experience Manager] pekpunkter i datorprogrammet i det kreativa arbetsflödet

## Installera och anslut appen till [!DNL Experience Manager]-servern {#installandconnect}

Innan du kan börja skapa eller redigera de kreativa resurserna måste du ansluta datorprogrammet till [!DNL Assets]-servern för att hämta och överföra resurser i databasen. Utför följande uppgifter:

1. [Installera programmet](#installapp).
1. [Ange dina ](#inapppref) inställningar och anslutningsinformation.
1. [Anslut till  [!DNL Experience Manager] ](#connect) en server och montera resurskatalogen som lokal enhet.
1. [Aktivera skrivbordsåtgärd ](#desktopactions) på  [!DNL Experience Manager] servern.

[!DNL Experience Manager] skrivbordsappen använder en HTTPS-anslutning för att ansluta till  [!DNL Experience Manager] servern för att överföra dina resurser på ett säkert och robust sätt.

>[!NOTE]
>
>För en del av eller alla installations- och konfigurationssteg kan du behöva hjälp av [!DNL Experience Manager]-administratören eller systemadministratören.

### Installera programmet {#installapp}

Om du vill använda [!DNL Experience Manager]-datorprogrammet kontrollerar du att din [!DNL Experience Manager]-serverversion stöds av programmet. Hämta lämplig installationsfil (binär) för operativsystemet (Mac eller Windows) och installera programmet.

Det kan vara nödvändigt att göra en detaljerad konfiguration beroende på ditt nätverk och dina systeminställningar. Mer information finns i [Installera och konfigurera [!DNL Experience Manager] datorprogrammet](install-configure-app-v1.md).

1. Gå till [[!DNL Experience Manager] nedladdningssidan för skrivbordsappen](https://helpx.adobe.com/experience-manager/kb/download-companion-app.html) och hämta den binära filen för ditt operativsystem.
1. Starta den hämtade installationsfilen och följ instruktionerna på skärmen för att installera programmet.

   >[!NOTE]
   >
   >Endast en instans av [!DNL Experience Manager]-datorprogrammet kan installeras och vara aktiv åt gången.

### Förstå alternativen och inställningarna i appen {#inapppref}

Programmet tillåter inställningar för att ansluta och koppla från [!DNL Experience Manager]-servrar, visa status för överföringar, hantera lokal cache och så vidare. Standardinställningarna fungerar för en typisk användare av programmet. Du kan ändra inställningarna för att få ut mer av programmet och av integreringen med [!DNL Experience Manager]-servern. De olika inställningarna beskrivs nedan i detalj.

**Utforska** resurserÖppna den lokala enheten där  [!DNL Assets] databasen är monterad. Du kan med andra ord utforska de resurser som nu finns tillgängliga på din lokala dator.

**Visa** resursstatusNär ändrade resurser överförs eller nya resurser läggs till i  [!DNL Assets] databasen, överförs resurserna i bakgrunden. Bakgrundsuppladdningen möjliggör smidiga åtgärder utan att du behöver vänta tills överföringen är klar, särskilt för stora resurser. Du kan spara ändringarna lokalt och glömma det. Det tar ett tag att skicka resurserna till servern, beroende på den tillgängliga bandbredden. Du kan kontrollera överföringsstatus tillsammans med mer grundläggande information.

**** AlternativKlicka på alternativen i skrivbordsappen för att komma åt inställningarna för att starta programmet när datorn startas; ansluta till  [!DNL Experience Manager] servern när appen startas, och för att ändra den lokala enhetsbokstaven där  [!DNL Assets] är tillgänglig efter montering.

**Avancerat > Hantera** cacheDu kan styra hur mycket diskutrymme som är tillgängligt för lokal cachelagring. Artefakterna från [!DNL Assets]-servern cachelagras lokalt för en smidigare upplevelse. Du kan ändra standardinställningarna så att de passar dina behov. Du kan även rensa cachen för att hämta alla resurser på nytt. När du rensar cachen bevaras ändringarna som inte sparats. Alla resurser som inte har checkats in på [!DNL Experience Manager]-servern behålls och tas inte bort.

### Anslut till en [!DNL Experience Manager]-server {#connect}

Programmet har stöd för proxykonfiguration i Mac och Windows. Konfigurationen läses när appen startas. Om du ändrar proxyinställningarna startar du om programmet så att ändringarna börjar gälla.

>[!NOTE]
>
>Om du ändrar proxyinställningarna startar du om programmet så att ändringarna börjar gälla. Annars fortsätter programmet att använda den tidigare konfigurerade proxyservern.

1. Starta [!DNL Experience Manager]-datorprogrammet. Om du vill mappa din [!DNL Experience Manager]-instans med programmet anger du din [!DNL Experience Manager]-server i formatet `https://[aem-server-url]:[port]`.

   ![Autentisera på Mac och ange  [!DNL Experience Manager] server-URL](assets/aem_desktop_app_server_url.png)

1. Ange användarnamn och lösenord för instansen på inloggningsskärmen. Om du vill ange en alternativ [!DNL Experience Manager]-instans väljer du alternativet **[!UICONTROL Alternate Login URL]**.

   ![Ange  [!DNL Experience Manager] serverautentiseringsuppgifter på inloggningsskärmen i  [!DNL Experience Manager] skrivbordsappen](assets/login_screen_v1.png)

### Aktivera skrivbordsåtgärder i [!DNL Experience Manager]-webbgränssnittet {#desktopactions}

I Assets-användargränssnittet kan du utforska resursplatserna eller checka ut och öppna resursen för redigering i ditt skrivbordsprogram. Dessa alternativ kallas skrivbordsåtgärder och är inte aktiverade som standard. Följ de här stegen för att aktivera den.

1. Klicka/tryck på ikonen Användare i det övre högra hörnet av verktygsfältet i gränssnittet Resurser.
1. Klicka på **[!UICONTROL My Preferences]** för att visa dialogrutan **[!UICONTROL Preferences]**.

   ![[!DNL Experience Manager] gränssnitt med användarinställningar](assets/aem_ui_user_preferences.png)

1. Välj **[!UICONTROL Show Desktop Actions For Assets]** i dialogrutan Användarinställningar. Klicka på **[!UICONTROL Accept]**.

   ![Markera  [!UICONTROL Show Desktop Actions For Assets] för att aktivera skrivbordsåtgärder](assets/enable_desktop_actions.png)

   *Bild: Markera Visa skrivbordsåtgärder för resurser för att aktivera skrivbordsåtgärder.*

## Få åtkomst till och öppna resurser på skrivbordet {#openondesktop}

När du klickar på **Öppna** för att öppna en resurs på den lokala datorn hämtar programmet resursen till dess interna cache. Programmet startar det inbyggda skrivbordsprogrammet som är associerat med filtypen för den hämtade resursen.

På Mac väljer du **Öppna** på snabbmenyn för att öppna en resurs via [!DNL Experience Manager]-datorprogrammet. I Windows väljer du Öppna på webben på snabbmenyn för att öppna resursen. Öppna resursen genom att klicka/trycka på ![ikonen Öppna på skrivbordet](assets/do-not-localize/aemassets_icon_openondesktop.png) i fönstret Resursstatus.

För Adobe InDesign-filer (INDD) väljer du **[!UICONTROL Open]** på snabbmenyn. När du klickar på det här alternativet hämtar appen de länkade resurserna till ditt lokala filsystem och öppnar sedan INDD-filen i Adobe InDesign. Den här metoden ser till att nödvändiga resurser är lokalt tillgängliga när du redigerar INDD-filen.

![Alternativ på snabbmenyn för att komma åt och öppna resurser med  [!DNL Experience Manager] skrivbordsappen](assets/aem_desktopapp_mac_context_menu.png)

*Bild: Alternativ på snabbmenyn för att komma åt och öppna resurser med  [!DNL Experience Manager] skrivbordsappen.*

>[!NOTE]
>
>I Windows förhindrar [standardinställningen för Windows 7](https://support.microsoft.com/en-us/kb/2668751) att [!DNL Experience Manager]-datorprogrammet hanterar resurser som är större än 50 MB.

>[!NOTE]
>
>Adobe rekommenderar att du går till Visningsalternativ i Finder på Mac och avaktiverar alternativen **Visa objektinformation**, **Visa förhandsgranskning av objekt** och **Visa förhandsgranskningskolumn** för den monterade [!DNL Assets]-mappen. Det förbättrar prestandan.

### Ytterligare alternativ i [!DNL Experience Manager]-gränssnittet {#additional-options-in-aem-assets}

När du har mappat [!DNL Assets]-databasen till den lokala enheten kan du aktivera ytterligare ikoner och funktionen Mappöverföring visas för mappade resurser och mappar.

1. Öppna gränssnittet [!DNL Assets] och för pekaren över en mapp eller en resurs för att visa skrivbordsåtgärderna som snabbåtgärder i kortvyn.

   ![I resursgränssnittet öppnar du snabbåtgärdsmenyn för att se skrivbordsåtgärder](assets/desktop_actions_in_card_view.png)

   *Bild: I resursgränssnittet öppnar du snabbåtgärdsmenyn för att se skrivbordsåtgärder.*

   Dessa skrivbordsåtgärder är också tillgängliga när du klickar på alternativet **Skrivbordsåtgärder** i verktygsfältet efter att du har valt resursen eller från verktygsfältet på sidan med resursen.

1. Om du vill öppna resursen i skrivbordsprogrammet som är associerat med det specifika filtillägget klickar du på snabbåtgärden **Öppna på skrivbordet** ![Öppna på skrivbordet](assets/do-not-localize/aemassets_icon_openondesktop.png).

   Du kan också välja **Öppna** på menyn **Skrivbordsåtgärder** i verktygsfältet.

Om du vill hitta en viss resurs i det lokala filsystemet klickar du på **Visa** snabbåtgärd ![Visa ikon](assets/do-not-localize/aemassets_reveal_icon.png). Du kan också välja **Visa** på menyn **Skrivbordsåtgärder** i verktygsfältet.

## Förstå tillgångsstatusarna {#understand-the-asset-statuses}

| ![Ikon för Windows-standardprogram](assets/do-not-localize/win_default.png) | Appen är ansluten till servern och alla resurser synkroniseras. |
--- |--- |
| ![Ikon för inaktiverad Windows](assets/do-not-localize/win_disabled.png) | Appen startas men är inte ansluten till servern. Vissa resurser kanske väntar på synkronisering. |
| ![Synkroniseringsikon för Windows-fil](assets/do-not-localize/win_sync.png) | Resurserna synkroniseras. Filerna överförs eller hämtas. Du kan se exakta statusvärden och pausa överföringar från fönstret Resursstatus. |
| ![Ikon för återanslutning av Windows](assets/do-not-localize/win_refresh.png) | Programmet försöker återansluta. Nätverksproblemen kan leda till att den kopplas från. |

## Arbeta med dina resurser {#workonassets}

### Ta en titt på resurser från webbgränssnittet [!DNL Experience Manager] {#check-out-assets-from-the-aem-web-interface}

[!DNL Assets] Med kan du checka ut resurser för redigering och checka in dem igen när du har gjort ändringarna. När du har checkat ut en resurs kan bara du redigera, kommentera, publicera, flytta eller ta bort resursen. När du checkar ut en resurs låses den och andra användare kan inte utföra någon av dessa åtgärder. Om du vill kunna checka ut/in resurser måste du ha skrivbehörighet för dem.

Det finns två sätt att checka ut resurser från webbgränssnittet [!DNL Experience Manager]. Mer information om den första metoden finns i [checka in och ut filer från Assets UI](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/check-out-and-submit-assets.html). Följ de här stegen för de andra metoderna för att checka ut och öppna resursen när [!DNL Experience Manager]-datorprogrammet är installerat.

1. Öppna gränssnittet [!DNL Assets] och för pekaren över en mapp eller en resurs för att visa skrivbordsåtgärderna som snabbåtgärder i kortvyn.

   ![Alternativet Egenskaper i kortvyn](assets/desktop_actions_in_card_view.png)

   Dessa skrivbordsåtgärder är också tillgängliga när du klickar/trycker på ikonen Skrivbordsåtgärder i verktygsfältet efter att du har valt resursen eller i verktygsfältet på resurssidan.

1. Om du vill öppna resursen klickar/trycker du på snabbåtgärden Öppna på skrivbordet ![Ikonen Öppna på skrivbordet](assets/do-not-localize/aemassets_icon_openondesktop.png).

   Du kan också välja Öppna på menyn Skrivbordsåtgärder i verktygsfältet.

   >[!NOTE]
   >
   >När du redigerar en fil som just har öppnats och inte är utcheckad, kommer andra användare inte att veta att en resurs uppdateras av dig.

1. Om du vill öppna en resurs för redigering i ett Adobe Creative Cloud-program klickar/trycker du på snabbåtgärden Redigera skrivbord ![Redigera skrivbord-ikon](assets/do-not-localize/aemassets_icon_editdesktop.png). Då checkas även resursen ut för redigering. När du är klar med redigeringen checkar du in resursen för att uppdatera ändringarna i [!DNL Assets].

   Du kan också välja Redigera på menyn Skrivbordsåtgärder i verktygsfältet.

1. Välj menyalternativet Öppna. De valda resurserna öppnas i förhandsgranskningsläge.
1. Om du vill redigera resurserna väljer du alternativet Redigera. Resurserna öppnas i redigeringsläge.

### Ta en titt på resurser från Finder i Mac OS {#check-out-assets-on-mac}

Med appen kan du checka ut resursfiler för att förhindra att andra användare ändrar de filer som du arbetar med.

1. På snabbmenyn i Mac väljer du Öppna AEM Assets-mapp för att öppna Finder.

   ![Alternativ på snabbmenyn för att komma åt och öppna resurser med  [!DNL Experience Manager] skrivbordsappen](assets/aem_desktopapp_mac_context_menu.png)

   *Bild: Alternativ på snabbmenyn för att komma åt och öppna resurser med  [!DNL Experience Manager] skrivbordsappen.*

1. Navigera till resursen som du vill checka ut.
1. Högerklicka på resursen och välj Mer resursinformation på snabbmenyn.
1. I dialogrutan Resursinformation klickar/trycker du på ikonen Checka ut för att checka ut resursen. Ikonen Checka ut växlar till ikonen för incheckning när du har klickat/tryckt på den.

   ![Bläddra till resurs att checka ut](assets/browse_assets_to_checkout.png)

1. Om du vill checka in resursen så att den är tillgänglig för andra användare klickar du på/trycker på incheckningsikonen i dialogrutan Resursinformation.

### Checka ut resurser i Windows {#check-out-assets-on-windows}

Med appen kan du checka ut resursfiler för att förhindra att andra användare ändrar de filer som du arbetar med.

1. Välj Utforska resurser på snabbmenyn för att öppna Utforskaren.
1. I Utforskaren navigerar du till platsen för resursen som du vill checka ut.
1. Högerklicka på resursen och välj Öppna på webben på snabbmenyn.
1. Klicka/tryck på ikonen Checka ut i dialogrutan Resursinformation. Ikonen Checka ut växlar till ikonen Checka in.

   ![Ikonen Checka ut växlar](assets/checkout_icon_toggles.png)

1. Granska resursen i Utforskaren. Låsikonen på resursen ![Ikonen för tillgångslås](assets/do-not-localize/aemassets_icon_lockcheckout.png) anger att du har checkat ut resursen.

   >[!NOTE]
   >
   >Låsikonen kan visas efter en fördröjning. [!DNL Experience Manager] skrivbordsappen cachelagrar resurserna för snabb åtkomst så det kan ta en stund att uppdatera den låsta statusen.

1. Om du vill checka in resursen så att den är tillgänglig för andra användare klickar/trycker du på ikonen för incheckning i dialogrutan **Resursinformation**.

### Checka in en resurs med Finder eller Utforskaren och med webbgränssnittet {#check-in-an-asset-using-finder-or-explorer-and-using-web-interface}

När du är klar med redigeringen av resurserna sparar du resurserna i skrivbordsprogrammet. Välj **Mer resursinformation** på snabbmenyn och klicka på incheckning.

Resurserna överförs till [!DNL Experience Manager]-servern. Du kan också kontrollera överföringsstatus genom att välja **Visa resursstatus** från systemfältsikonen. Du kan också checka in en resurs från webbgränssnittet [!DNL Experience Manager]. Klicka på de utcheckade resurserna eller markera dem. Klicka på ikonen ![incheckning](assets/do-not-localize/aemassets_icon_checkin.png) i verktygsfältet.

En resurs överförs automatiskt till [!DNL Experience Manager] efter att eventuella ändringar har sparats lokalt. Incheckningen gör resursen tillgänglig för andra [!DNL Experience Manager]-användare för redigering.

### Överför resurser och mappar gruppvis till [!DNL Experience Manager]-servern {#bulkupload}

Med [!DNL Experience Manager]-skrivbordsappen kan du överföra en hel mapp som innehåller resurser från den lokala filkatalogen till [!DNL Assets]. På så sätt överförs alla resurser i mappen gruppvis i stället för att behöva överföra dem en åt gången.

1. I resursgränssnittet klickar/trycker du på **Create** i verktygsfältet och väljer **Överför mapp** på menyn.
1. Bläddra till mappen som du vill överföra och markera den.
1. Klicka/tryck på OK. I dialogrutan Resursstatus visas status för överföringen.

   ![Se status för överföringen i fönstret Resursstatus](assets/aem_desktopapp_bulkupload_status.png)

   Se status för överföringen i fönstret Resursstatus

   >[!NOTE]
   >
   >Du kan pausa eller avbryta överföringen manuellt genom att klicka/trycka på lämplig ikon.

1. När mappen har överförts stänger du dialogrutan och navigerar till resursgränssnittet. Den överförda mappen visas i webbgränssnittet.

Adobe rekommenderar inte att du kopierar och klistrar in eller drar ett större antal filer eller kapslade mappar från det lokala filsystemet till nätverksresursområdet. Programmet kan inte styra överföringsprocessen på grund av tekniska begränsningar och prestandan är dålig.

Du kan också välja filer/mappar som du vill överföra till [!DNL Experience Manager] i Finder eller Utforskaren, kopiera dem till systemets Urklipp, navigera till målmappen i nätverksresursområdet och välja [!DNL Experience Manager] på snabbmenyn för skrivbordsappen **Klistra in resurser**. På så sätt börjar [!DNL Experience Manager]-skrivbordsappen överföra de inklistrade resurserna som liknar alternativet **Överför mapp** som är tillgängligt i webbgränssnittet [!DNL Experience Manager].

>[!MORELIKETHIS]
>
>* [ [!DNL Experience Manager] Felsökning av datorprogram](troubleshoot-app-v1.md)

