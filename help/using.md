---
title: Använd [!DNL Experience Manager] datorprogrammet
description: Använd [!DNL Adobe Experience Manager] desktop app, to work with [!DNL Adobe Experience Manager] DAM-resurser direkt från Win- eller Mac-datorn och använd i andra program.
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: caf6faf17157a0e9e3bffd40b4bdd0802a71dad7
workflow-type: tm+mt
source-wordcount: '3906'
ht-degree: 0%

---


# Använd [!DNL Adobe Experience Manager]-datorprogrammet {#use-aem-desktop-app-v2}

Använd [!DNL Adobe Experience Manager]-datorprogrammet för att enkelt få åtkomst till digitala resurser som lagras i [!DNL Adobe Experience Manager] DAM-databasen på din lokala dator och använda dessa resurser i alla skrivbordsprogram. Du kan öppna resurserna i skrivbordsprogram och redigera resurserna lokalt - överföra ändringarna tillbaka till [!DNL Experience Manager] med versionskontroll för att dela uppdateringarna med andra användare. Du kan också överföra nya filer och mapphierarkier till [!DNL Experience Manager], skapa mappar och ta bort resurser och mappar från [!DNL Experience Manager] DAM.

Tack vare integreringen kan olika roller i organisationen hantera resurser centralt i [!DNL Experience Manager Assets] och komma åt resurserna på det lokala skrivbordet i de program som används i Windows eller Mac OS.

När du öppnar programmet efter utloggning eller för första gången anger du URL-adressen till din [!DNL Experience Manager]-server i formatet `https://[aem-server-url]:[port]/`. Välj sedan alternativet [!UICONTROL Connect]. Ange autentiseringsuppgifter för att ansluta programmet till servern.

De viktigaste uppgifterna du gör med [!DNL Experience Manager]-datorprogrammet är:

![Arbetsflöden och uppgifter du kan utföra med  [!DNL Experience Manager] datorprogramArbetsflöden och uppgifter du kan utföra ](assets/aem_desktop_app_usecases_v2.png "med  [!DNL Adobe Experience Manager] datorprogramLadda ned ")
  [](assets/aem_desktop_app_usecases_print.pdf) den tryckfärdiga PDF-filen.

## Så här fungerar skrivbordsappen {#how-app-works2}

Innan du börjar använda programmet bör du förstå [hur programmet fungerar](release-notes.md#how-app-works). Bekanta dig också med följande termer:

* **[!UICONTROL Desktop Actions]**: Från Assets-webbgränssnittet, från en webbläsare, kan du utforska resursplatserna eller checka ut och öppna resursen för redigering i ditt datorprogram. De här åtgärderna är tillgängliga från webbgränssnittet och använder skrivbordsappsfunktioner. Se [hur du aktiverar skrivbordsåtgärder](using.md#desktopactions-v2).

* Filstatus är **[!UICONTROL Cloud Only]**: Sådana resurser hämtas inte på den lokala datorn och är endast tillgängliga på [!DNL Experience Manager]-servern.

* Filstatus är **[!UICONTROL Available locally]**: Resurserna hämtas och är tillgängliga på den lokala datorn i befintligt skick. Resurserna ändras inte.

* Filstatus är **[!UICONTROL Edited locally]**: Sådana resurser ändras lokalt och ändringarna finns kvar på den överförda servern [!DNL Experience Manager]. När du har överfört filen ändras statusen till [!UICONTROL Available locally]. Se [redigera resurser](using.md#edit-assets-upload-updated-assets).

* Filstatus är **[!UICONTROL Editing conflict]**: Om du och andra användare ändrar en resurs samtidigt indikerar programmet att en redigeringskonflikt har inträffat. Programmet innehåller även alternativ för att behålla eller ignorera ändringarna. Se [hur du undviker redigeringskonflikter](using.md#adv-workflow-collaborate-avoid-conflicts).

* Filstatus är **[!UICONTROL Modified remotely]**: Programmet anger om en resurs som du har hämtat ändras på [!DNL Experience Manager]-servern. Programmet har också möjlighet att hämta den senaste versionen och uppdatera din lokala kopia. Se [hur du undviker redigeringskonflikter](using.md#adv-workflow-collaborate-avoid-conflicts).

* **[!UICONTROL Check-out]**: Om du redigerar en fil eller har för avsikt att redigera en fil, kan du växla status för att checka ut. En låsikon läggs till för resursen i appen och [!DNL Experience Manager] webbgränssnittet. Låsikonen anger för andra användare att de inte behöver redigera samma resurs samtidigt eftersom den leder till en redigeringskonflikt.

* **[!UICONTROL Check-in]**: Markera resursen som säker så att andra användare kan redigera den utan att orsaka en redigeringskonflikt. När du överför dina ändringar tas låsikonen automatiskt bort. Om du växlar incheckningsstatus tas även låsikonen bort, men du rekommenderas att inte checka in manuellt utan att överföra ändringarna. Om du ångrar ändringarna växlar du incheckningen manuellt.

* **[!UICONTROL Open]** åtgärd: Öppna bara resursen om du vill förhandsgranska den i det ursprungliga programmet. Du bör inte redigera resursen med den här åtgärden eftersom den inte checkar ut resursen och andra användare kan göra redigeringar som leder till redigeringskonflikter.

* **[!UICONTROL Edit]** åtgärd: Använd funktionsmakrot för att ändra bilden. När du klickar på [!UICONTROL Edit]-åtgärden checkas resursen ut automatiskt och en låsikon läggs till på resursen. Om du inte vill redigera resursen klickar du på [!UICONTROL Toggle check-in] när du har klickat på Redigera. Om du vill ta bort, byta namn på eller flytta resurser i [!DNL Experience Manager] DAM-mapphierarkin använder du [!DNL Experience Manager]-webbgränssnittsåtgärderna och inte redigeringsåtgärden.

* **[!UICONTROL Download]** åtgärd: Hämta resursen till din lokala dator. Du kan hämta resurserna nu och redigera dem senare. arbeta offline och ladda upp ändringarna senare. Resurserna hämtas i en cachemapp i filsystemet.

* **[!UICONTROL Reveal File]** eller  **[!UICONTROL Reveal Folder]** åtgärd: När resurserna hämtas till en lokal cachemapp härmar programmet en lokal nätverksenhet och tillhandahåller en lokal sökväg för varje resurs. Om du vill veta sökvägen använder du lämpligt visningsalternativ i appen. Du måste utföra åtgärden Visa för att placera resurser i programmet Creative Cloud. Se [placera resurser](using.md#place-assets-in-native-documents).

* **[!UICONTROL Open In Web]** åtgärd: Om du vill visa resursen i  [!DNL Experience Manager] webbgränssnittet öppnar du den på webben. Du kan initiera fler arbetsflöden från [!DNL Experience Manager]-gränssnittet, som att uppdatera metadata eller resursidentifiering.

* **[!UICONTROL Delete]** åtgärd: Ta bort resursen från  [!DNL Experience Manager] DAM-databasen. Åtgärden tar bort originalkopian av resursen på Experience Manager-servern. Om du bara vill ignorera ändringar i den lokala resursen läser du [ignorera ändringar](using.md#edit-assets-upload-updated-assets).

* **[!UICONTROL Upload Changes]**: Skrivbordsappen överför bara den uppdaterade resursen när du uttryckligen överför den till  [!DNL Experience Manager] servern. När du sparar redigeringarna sparas ändringarna bara på den lokala datorn. När du överför en resurs checkas den automatiskt in och låsikonen tas bort. Se [redigera resurser](using.md#edit-assets-upload-updated-assets).

## Aktivera skrivbordsåtgärder i [!DNL Experience Manager]-webbgränssnittet {#desktopactions-v2}

I Assets-användargränssnittet i en webbläsare kan du utforska resursplatserna eller checka ut och öppna resursen för redigering i datorprogrammet. Dessa alternativ kallas [!UICONTROL Desktop Actions] och är inte aktiverade som standard. Följ de här stegen för att aktivera den.

1. Klicka/tryck på ikonen **[!UICONTROL User]** i verktygsfältet i resurskonsolen.
1. Klicka/tryck på **[!UICONTROL My Preferences]** för att visa dialogrutan **[!UICONTROL Preferences]**.
1. Välj **[!UICONTROL Show Desktop Actions For Assets]** i dialogrutan Användarinställningar. Klicka/tryck på **[!UICONTROL Accept]**.

   ![Markera Visa skrivbordsåtgärder för resurser för att aktivera skrivbordsåtgärder](assets/enable_desktop_actions.png)

   Markera [!UICONTROL Show Desktop Actions For Assets] om du vill aktivera skrivbordsåtgärder

## Bläddra bland, söka efter och förhandsgranska resurser {#browse-search-preview-assets}

Du kan bläddra till, söka efter och förhandsvisa de resurser som finns i [!DNL Experience Manager]-databasen, allt inifrån skrivbordsprogrammet. Prova följande i appen:

1. Bläddra till en mapp och se grundläggande information om resurserna som finns i mappen, tillsammans med små miniatyrbilder av alla resurser.

   ![Bläddra bland DAM-filer och -](assets/browse_folder_da2.png "mapparBläddra bland DAM-filer och -mappar")

1. Om du vill visa mer information och en större miniatyrbild av en enskild resurs klickar du på filnamnet.

   ![Se en större förhandsvisning av en resurs och ](assets/large_preview_actions_da2.png "funktionsmakronSe en större förhandsvisning av en resurs och funktionsmakron")

1. Klicka på **[!UICONTROL Open]** eller **[!UICONTROL Edit]** om du vill hämta filen lokalt och bara visa eller redigera den i det ursprungliga programmet.
1. Sök med nyckelord för att hitta en relaterad resurs i [!DNL Experience Manager]-databasen. Använd `?` och `*` som jokertecken. Dessa jokertecken ersätter ett enda tecken eller flera tecken. Filtrera och sortera resultatet efter behov.

   ![Exempelsökning med asterisk ](assets/search_wildcard_da2.png "jokerteckenExempelsökning med asterisk jokertecken")

   ![Ytterligare en exempelsökning med ](assets/search_wildcard2_da2.png "jokertecken för asteriskEn annan exempelsökning med annan placering av jokertecknet för asterisken")

>[!NOTE]
>
>Resurserna visas i programmet genom att sökvillkoren matchas i flera metadatafält, inte bara objektets namn eller filnamn.

## Hämta resurser {#download-assets}

Du kan hämta resurserna på det lokala filsystemet. Programmet hämtar resurserna från [!DNL Experience Manager]-servern och sparar samma kopia i det lokala filsystemet.

Klicka på ![Fler alternativikoner](assets/do-not-localize/more2_da2.png) för alternativ och klicka på ![ikonen Hämta](assets/do-not-localize/download_cloud_da2.png) för att hämta.

![Hämtningsalternativ för en ](assets/download_option_da2.png "resursHämtningsalternativ för en resurs")

>[!NOTE]
>
>När du hämtar eller överför en stor fil eller många filer, inaktiveras åtgärderna för resurser och mappar. Åtgärderna är tillgängliga när hämtningen eller överföringen är klar.

Hämtning av flera resurser kan leda till sämre prestanda om köstorleken är stor eller om du har problem med nätverket. Du kan också ovetande köa många resurser för hämtning när du hämtar en mapp. För att undvika långa väntetider begränsar appen antalet resurser som hämtas på en gång. Mer information om hur du konfigurerar den finns i [Ange inställningar](install-upgrade.md#set-preferences). Även under denna gräns kan programmet ibland behöva be om en bekräftelse innan en till synes stor mapp hämtas.

![Appen bekräftar hämtning av ett relativt stort antal ](assets/download_confirmation_da2.png "resurserAppen bekräftar hämtning av ett relativt stort antal resurser")

Om en eller flera mappar är markerade och hämtade hämtar programmet bara resurser som lagras direkt i mappen/mapparna i [!DNL Experience Manager]. Det hämtar inte resurser från undermappar automatiskt.

## Öppna resurser på skrivbordet {#openondesktop-v2}

Du kan öppna fjärrresurserna för visning i det ursprungliga programmet. Resurserna hämtas till en lokal mapp och startas i det program som är associerat med filformatet. Du kan ändra det inbyggda programmet så att det öppnar specifika filtyper (tillägg) i Mac eller Windows.

Klicka på **[!UICONTROL Open]** på resursmenyn. Resursen hämtas lokalt och öppnas i det ursprungliga programmet. Kontrollera hämtningsförloppet och överföringshastigheten för stora resurser i statusfältet.

<!-- ![Download progress bar for large-sized assets](assets/download_status_bar_da2.png "Download progress bar for large-sized assets")
-->

>[!NOTE]
>
>Om de förväntade ändringarna inte visas i appen klickar du på uppdateringsikonen ![Uppdatera-ikonen](assets/do-not-localize/refresh.png) eller högerklickar i appgränssnittet och klickar på **[!UICONTROL Refresh]**. Åtgärderna är inte tillgängliga medan större hämtningar eller överföringar pågår.

Om du vill öppna den lokala hämtningsmappen för en resurs klickar du på ![Fler åtgärder-ikonen](assets/do-not-localize/more2_da2.png) och klickar på ![Visa-ikonen](assets/do-not-localize/reveal_action2_da2.png) **[!UICONTROL Reveal File]**-åtgärden.

## Använd eller placera resurser i ursprungliga dokument {#place-assets-in-native-documents}

I vissa fall, till exempel när du monterar en resurs i ett internt dokument, kan du få åtkomst till en fil i Utforskaren i Windows eller Finder i Mac. Använd ![Visa-ikonen](assets/do-not-localize/reveal_action2_da2.png) **[!UICONTROL Reveal File]** om du vill gå till filsystemplatsen för den lokalt hämtade filen.

![Visa filåtgärd för en ](assets/revealfile_action_da2.png "resursFunktionen Visa fil för en resurs")

Klicka på **[!UICONTROL Reveal File]** eller **[!UICONTROL Reveal Folder]** i en mapp för att öppna Utforskaren i Windows eller Finder i Mac med filen eller mappen förmarkerad på den lokala datorn. Alternativet är användbart för att t.ex. placera [!DNL Experience Manager]-filerna i de ursprungliga programmen som har stöd för montering eller länkning av lokala filer. Mer information om hur du monterar filer i Adobe InDesign finns i [Montera bilder](https://helpx.adobe.com/indesign/using/placing-graphics.html).

Åtgärden **[!UICONTROL Reveal File]** öppnar en lokal nätverksresurs som endast visar resurser som är tillgängliga lokalt, det vill säga resurser som har visats, hämtats eller öppnats/redigerats med appen. Den lokala nätverksresursen överför inga ändringar till [!DNL Experience Manager]. Om du vill överföra ändringarna ska du explicit använda **[!UICONTROL Upload Changes]** eller **[!UICONTROL Upload]**-åtgärder i appen.

>[!NOTE]
>
>För bakåtkompatibilitet med [!DNL Experience Manager]-datorprogrammet v1.x hanteras de filer som visas från en lokal nätverksresurs, endast lokalt tillgängliga filer visas. Skrivbordssökvägarna för de visade filerna är samma som sökvägarna som skapas i programmet v1.x.

>[!CAUTION]
>
>Använd inte alternativet **[!UICONTROL Reveal File]** för att redigera resurser i inbyggda program. Använd i stället **[!UICONTROL Edit]**-åtgärderna. Mer information finns i [Avancerat arbetsflöde: samarbeta med samma filer och undvika redigeringskonflikter](#adv-workflow-collaborate-avoid-conflicts).

## Redigera resurser och överför uppdaterade resurser till [!DNL Experience Manager] {#edit-assets-upload-updated-assets}

Öppna resurser för redigering när du vill göra ändringar och överföra de uppdaterade resurserna till AEExperience ManagerEM-servern. Om du vill undvika konflikter med redigeringar av andra användare använder du programmet för att starta en redigeringssession. Innan du börjar redigera bör du kontrollera att resursen inte har någon låsikon, det vill säga att en annan användare inte redigerar resursen.

Om du vill redigera en resurs söker du efter resursen eller bläddrar till resursens plats. Klicka på ![Mer ikon](assets/do-not-localize/more2_da2.png) och klicka på **[!UICONTROL Edit]**.

Använd **[!UICONTROL Toggle Check-out]** för att låsa resursen för att förhindra konflikter med redigeringar av andra användare i båda följande situationer:

* Du har börjat redigera en resurs utan att först checka ut den (till exempel genom att öppna den).
* Du har för avsikt att börja redigera en resurs inom kort och vill inte att andra ska kunna redigera den.

När du är klar med redigeringarna visas statusen **[!UICONTROL Edited Locally]** för de ändrade resurserna. Alla ändringar som sparas i resurserna är bara lokala tills du överför ändringarna till [!DNL Experience Manager]. Om du vill överföra en enskild resurs eller ett fåtal resurser klickar du på **[!UICONTROL Upload Changes]** bland alternativen för en resurs. En version av resursen skapas i [!DNL Experience Manager]. Med webbgränssnittet för [!DNL Assets] kan du se resurshistorik i vyn [Tidslinje](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/activity-stream.html).

![Alternativet Överför ändringar i ](assets/upload_changes_single1_da2.png "appenÖverför ändringar i appen")

![Alternativet Överför ändringar när du visar en stor förhandsvisning av en ](assets/upload_changes_single2_da2.png "resursÖverför ändringar när du visar en stor förhandsvisning av en resurs")

Bästa tillvägagångssätt för samverkansbaserad redigering finns i [Avancerat arbetsflöde: samarbeta med samma filer och undvika redigeringskonflikter](#adv-workflow-collaborate-avoid-conflicts).

I följande fall kanske du vill ignorera dina ändringar och redigeringar av den lokala resursen. Klicka på **[!UICONTROL Discard Changes]**.

* Om du inte vill spara dina lokala ändringar i [!DNL Experience Manager].
* Börja göra ändringar i den ursprungliga resursen när du har sparat några ändringar.
* Sluta redigera resursen eftersom den inte längre behövs.

Om det behövs kan du växla utcheckning. Den uppdaterade resursen tas bort från den lokala cachemappen och hämtas igen när du redigerar eller öppnar den.

## Överför och lägg till nya resurser i [!DNL Experience Manager] {#upload-and-add-new-assets-to-aem}

Användare kan lägga till nya resurser i DAM-databasen. Du kan till exempel vara fotograf eller entreprenör på en byrå som vill lägga till ett stort antal foton från en fotografering i [!DNL Experience Manager]-databasen. Om du vill lägga till nytt innehåll i [!DNL Experience Manager] väljer du ![alternativet ](assets/do-not-localize/upload_to_cloud_da2.png) i appens övre fält. Bläddra till resursfilerna i det lokala filsystemet och klicka på **[!UICONTROL Select]**. Du kan också dra filerna eller mapparna i programgränssnittet. Programmet börjar överföra resursen. Om överföringen tar längre tid visas en förloppsindikator längst ned i programmet. Använd inte blanksteg eller ogiltiga tecken när du skapar eller överför mappar. Se en lista över tillåtna tecken på [skapa mappar i [!DNL Assets]](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/manage-assets.html#creating-folders).

<!-- ![Download progress bar for large-sized assets](assets/upload_status_da2.png "Download progress bar for large-sized assets")
-->

Du kan överföra mappar eller enskilda filer från det lokala filsystemet. En mapps hierarki bevaras när den överförs. Innan du överför resurser i grupp ska du läsa [Massöverföringar](#bulk-upload-assets).

Klicka på **[!UICONTROL View]** > **[!UICONTROL Assets transfers]** för att visa listan över resurser som överförts i en given session. I listan kan du visa och snabbt verifiera filöverföringar för den aktuella sessionen.

![Lista över överförda tillgångar i en viss ](assets/assets_transfered_da2.png "sessionLista över överförda tillgångar i en viss session")

Du kan styra samtidighet för överföring (acceleration) i **[!UICONTROL Preferences]** > **[!UICONTROL Upload acceleration]**-inställningen. Mer samtidighet ger vanligtvis snabbare överföringar, men kan vara resurskrävande och förbrukar mer processorkraft på den lokala datorn. Om du upplever ett långsamt system försöker du överföra igen med ett lägre värde av samtidighet.

>[!NOTE]
>
>Överföringslistan är inte beständig och är inte tillgänglig om du avslutar programmet och öppnar det igen.

>[!NOTE]
>
>Om filerna inte kan överföras och om du ansluter till [!DNL Experience Manager] 6.5.1 eller senare ska du läsa denna [felsökningsinformation](troubleshoot.md#upload-fails).

## Arbeta med flera resurser {#work-with-multiple-assets}

Användare kan enkelt arbeta med och hantera flera resurser med åtgärder som att överföra alla redigeringar på en gång eller överföra kapslade mappar med några klick.

### Bläddra i stora mappar {#browse-large-folders}

När du arbetar med mappar som innehåller många resurser bläddrar du för att visa fler resurser. Om du vill rulla med tangentbordet trycker du på Tabb några gånger för att markera resursen längst upp. Observera den markerade resursen för att veta när den är markerad. Använd nu nedåtpilen för att förflytta dig i resurslistan.

### Snabbåtgärder för markerade resurser {#quick-actions-for-selected-assets}

Klicka på miniatyrbilden för några resurser för att markera resurserna. Om du vill markera alla resurser klickar du i kryssrutan i appens övre fält. Den uppsättning åtgärder som gäller för alla markerade resurser tillsammans visas i ett verktygsfält längst ned i programmet.

![Verktygsfältet längst ned visar åtgärder som är relevanta för de valda ](assets/actions_bottom_toolbar1_da2.png "resursernaVerktygsfältet längst ned visar vanliga åtgärder för de valda resurserna")

![Inga åtgärder i verktygsfältet när det inte finns några vanliga åtgärder för ](assets/actions_bottom_toolbar2_da2.png "markeringenInga åtgärder i verktygsfältet när det inte finns några vanliga åtgärder för markeringen")

Vilka åtgärder som är tillgängliga i verktygsfältet längst ned beror på statusen för de valda filerna. Om du till exempel bara väljer **[!UICONTROL Edited Locally]**-filer visas ikonen **[!UICONTROL Upload Changes]**. Om du väljer en blandning av **[!UICONTROL Edited locally]** och **[!UICONTROL Cloud only]** är åtgärden **[!UICONTROL Upload Changes]** inte tillgänglig.

### Sök efter alla redigerade bilder {#find-all-edited-images}

Programmet tillhandahåller en vy med namnet **[!UICONTROL Edited locally]** som ger dig snabb åtkomst till alla filer som du hämtade lokalt (via [!UICONTROL Open] eller [!UICONTROL Edit]-åtgärder) och sedan ändrade. Med appen kan du välja alla lokalt redigerade resurser och överföra ändringarna med några klick. I den här vyn visas även lokalt redigerade resurser som har en redigeringskonflikt.

![Filtrera för att se alla lokalt redigerade ](assets/edited_locally_filter_da2.png "resurserFiltrera för att se alla lokalt redigerade resurser, till exempel för massöverföring av redigeringar")

### Överför resurser gruppvis {#bulk-upload-assets}

Användare eller organisation, t.ex. fotografer eller byråer, kan skapa olika lokala resurser i scenarier som fotografering, retuschering eller urval från en större uppsättning som gjorts utanför [!DNL Experience Manager]. De kan överföra de här stora lokala mapparna till [!DNL Assets] direkt från skrivbordsappen. Mapphierarkierna bevaras och alla kapslade undermappar och inkluderade resurser överförs. De överförda resurserna är omedelbart tillgängliga för andra användare på samma server för användning. Resurser överförs i bakgrunden, så åtgärden är inte kopplad till en webbläsarsession.

![Ladda upp flera lokala mappar från skrivbordet i  [!DNL Experience Manager]](assets/upload_local_folders_da2.png "grupp Överför flera lokala mappar från skrivbordet till Experience Manager")

Om de förväntade ändringarna inte visas i programmet när du har överfört dem klickar du på ikonen Uppdatera ![Uppdatera](assets/do-not-localize/refresh.png).

>[!NOTE]
>
>Använd inte överföringsfunktionalitet för att migrera resurser över två [!DNL Experience Manager]-distributioner. Se i stället [migreringsguiden](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/assets-migration-guide.html).

### Lista över överförda tillgångar {#list-of-transferred-assets}

Om du vill visa en lista över resurser som överförts under en given session läser du i [Överför resurser till [!DNL Experience Manager]](#upload-and-add-new-assets-to-aem).

## Avancerat arbetsflöde: starta från webbgränssnittet [!DNL Assets] {#adv-workflow-start-from-aem-ui}

Om det behövs startar du arbetsflödet från webbgränssnittet Resurser. Skrivbordsappen integreras med [!DNL Experience Manager] för att ta över när det efterfrågas med Skrivbordsåtgärder.

Ett särskilt exempel på hur du startar arbetsflödet från webbgränssnittet är tillgångsidentifiering. Omnissearch bar in Assets-användargränssnittet ger en omfattande och avancerad sökfunktion. Du kanske först vill hitta en resurs på webben och sedan starta arbetsflödet i programmet med [!UICONTROL Desktop Actions]. I vissa exempelfall kan du filtrera sökresultat med hjälp av ansikten, hitta en specifik resurs som licensierats från Adobe Stock eller anpassa den som implementerats av din organisation så att du kan identifiera den bättre i webbgränssnittet.

Funktionen för skrivbordsprogram används när du försöker utföra följande åtgärder i webbgränssnittet Resurser:

* [!UICONTROL Desktop Actions] som tillåter [!UICONTROL Open], [!UICONTROL Edit] och [!UICONTROL Reveal]
* [!UICONTROL Upload folder]
* [!UICONTROL Check-out] eller [!UICONTROL check-in]

De åtgärder på webbgränssnittet som är tillgängliga för en resurs som är utcheckad i programmet är till exempel [!UICONTROL Open], [!UICONTROL Reveal] och [!UICONTROL Check-in].

![Skrivbordsåtgärder i  [!DNL Experience Manager] webbgränssnittet](assets/assets_web_actions_da2.png "Skrivbordsåtgärder i Experience Manager webbgränssnitt")

>[!NOTE]
>
>Webbläsaren kan uppmana dig att tillåta att du startar skrivbordet [!DNL Adobe Experience Manager]. Om du vill att appen ska kunna överföras utan avbrott från webbläsaren till appen markerar du kryssrutan så att appen alltid kan ta över.

Du kan inte hitta följande information eller arbetsflöde med webbgränssnittet. Använd skrivbordsappen eftersom webbgränssnittet inte kan spåra lokala ändringar och inte känner till följande:

* Filer redigerade lokalt.
* Filer som har en redigeringskonflikt och ett sätt att lösa den.
* Överför lokala ändringar till [!DNL Experience Manager].
* Olika statusvärden för de lokalt tillgängliga filerna.

Du kan tvärtom öppna resursen i webbgränssnittet från skrivbordsappen med åtgärden **[!UICONTROL Open In Web]**.

## Avancerat arbetsflöde: samarbeta med samma filer och undvika redigeringskonflikter {#adv-workflow-collaborate-avoid-conflicts}

I samarbetsmiljöer kan flera användare arbeta med samma uppsättning resurser, vilket kan leda till versionskonflikter. Följ dessa metodtips för att förhindra konflikter:

* Redigera inga resurser genom att klicka på [!UICONTROL Open]. Redigera inte lokalt hämtade resurser genom att öppna dem från filsystemmappen. Andra användare vet inte om resursen redigeras.
* Om du vill redigera en resurs klickar du alltid på [!UICONTROL Edit]. Resursen öppnas i det ursprungliga programmet och en låsikon läggs till på resursen, så att de andra användarna vet att resursen redigeras.
* Klicka på [!UICONTROL Toggle Check-in] om du av misstag startar redigeringen utan att klicka på [!UICONTROL Edit]. En låsikon läggs till i resursen. Även om du planerar att redigera en resurs senare men vill undvika att andra redigerar den, klickar du på [!UICONTROL Toggle Check-in] för att låsa resursen.
* Innan du redigerar en resurs måste du se till att andra användare inte redigerar den. Leta efter låsikonen på resursen.
* När du är klar med redigeringarna överför du alla ändringar och checkar sedan in resursen.

![Status för redigeringskonflikterStatus för ](assets/edits_conflicts_status_da2.png "redigeringskonflikter")

Om en lokalt nedladdad resurs uppdateras på [!DNL Experience Manager]-servern visar programmet statusen **[!UICONTROL Modified remotely]**. Du kan antingen ta bort din lokala kopia eller uppdatera den lokala kopian genom att klicka på [!UICONTROL Remove] eller [!UICONTROL Update]. Med länkar i dialogrutan kan du visa båda versionerna av resursen.

![Alternativ för att lösa konflikten när resursen ](assets/modified_remotely_dialog_da2.png "ändras på fjärrbasisAlternativ för att lösa konflikten när resursen ändras på fjärrbasis")

Om en resurs som du redigerar lokalt också uppdateras på servern utan att du vet om det, visas statusen **[!UICONTROL Editing Conflict]** i appen. Du kan behålla en uppsättning av ändringarna - antingen behålla dina uppdateringar (klicka på **[!UICONTROL Keep Mine]**) och ta bort den andra användarens redigering eller ta hänsyn till den andra användarens uppdateringar och ta bort din (**[!UICONTROL Overwrite Mine]**).

![Alternativ för att lösa en ](assets/editing_conflict_dialog_da2.png "redigeringskonfliktAlternativ för att lösa en redigeringskonflikt")

## Avancerat arbetsflöde: placera och länka resurser i InDesign-filen {#adv-workflow-place-assets-indesign}

När du använder [!DNL Experience Manager]-datorprogrammet för att öppna filer med länkade resurser hämtas resurserna i förväg och visas i de ursprungliga programmen. För att det här arbetsflödet ska fungera måste ditt inbyggda program ha stöd för att placera länkar till lokala resurser och [!DNL Experience Manager] måste ha stöd för att lösa länkarna i de binära filerna till serversidans referenser.

[!DNL Experience Manager] skrivbordsappen har stöd för det här arbetsflödet med några utvalda Adobe Creative Cloud-program och -filformat - Adobe InDesign, Adobe Illustrator och Adobe Photoshop. Med arbetsflödet kan du arbeta effektivt med de Creative Cloud-filer som stöds. Om användare A placerar några resurser i en InDesign-fil och checkar in dem i [!DNL Experience Manager] ser användare B resurserna i InDesign-filen även om resurserna inte är en del av filen. Resurserna hämtas lokalt till dator med användare B.

>[!NOTE]
>
>Skrivbordsappen kan mappas till valfri enhet i Windows. För mjuka åtgärder ska du dock inte ändra standardenhetsbokstaven. Om användare i samma organisation använder olika enhetsbokstäver kan de inte se resurser som placerats av andra. De placerade resurserna hämtas inte när sökvägen ändras. De placerade resurserna fortsätter att vara placerade i den binära filen (till exempel INDD) och tas inte bort.

Mer information om begränsningarna i det här arbetsflödet finns i [systemkraven och versionerna som stöds](release-notes.md).

Så här provar du arbetsflödet med en bildresurs och InDesign:

1. Håll en INDD-fil med monterade resurser i [!DNL Experience Manager] användbar. Mer information om hur du skapar en sådan INDD-fil finns i [Placera grafik](https://helpx.adobe.com/indesign/using/placing-graphics.html).
1. I skrivbordsappen **[!UICONTROL Edit]** den INDD-fil som innehåller placerade resurser i [!DNL Experience Manager].
1. Programmet hämtar båda, InDesign-filen och de länkade resurserna. När InDesign öppnar dokumentet är länkarna lösta, resurserna hämtas och resurserna visas i dokumentet InDesign.
1. Om du vill montera en ny bild i InDesign-filen använder du åtgärden **[!UICONTROL Reveal File]** för resursen. Åtgärden hämtar resursen lokalt och öppnar den lokala nätverksresursplatsen i Utforskaren i Windows eller Finder i Mac.
1. Placera den visade resursen i InDesign-dokumentet. Då skapas en länk i dokumentet.
1. När du är klar med redigeringarna i InDesign-dokumentet sparar du det och överför det till [!DNL Experience Manager] med skrivbordsappen.

## Avancerat arbetsflöde: hämta resurserna lokalt {#adv-workflow-download-assets-locally}

I många scenarier hämtas resurserna från [!DNL Experience Manager]-servern lokalt till filsystemet. Nedladdningarna förbrukar bandbredd och diskutrymme. Genom att känna till scenarierna kan du optimera väntetiden för nedladdningen.

Du hämtar resurserna inifrån appen on-demand. Se [Hämta resurser](#download-assets).

När du använder åtgärden [!UICONTROL Open] för att öppna en resurs i ett systemspecifikt skrivbordsprogram hämtas resursen lokalt, om den inte redan är tillgänglig lokalt. Se [Öppna resurser](#openondesktop-v2).

När du visar platsen för en resurs eller en mapp inifrån programmet hämtas resursen eller mappen först lokalt och öppnas sedan på datorn i den lokala nätverksresursen. Se [Öppna resurser](#openondesktop-v2).

När du använder åtgärden [!UICONTROL Edit] för att redigera en resurs i ett systemspecifikt skrivbordsprogram hämtas resursen lokalt, om den inte redan är tillgänglig lokalt. Se [Redigera resurser och överföra uppdaterade resurser till [!DNL Experience Manager]](#edit-assets-upload-updated-assets).

Om programmet är installerat och tillåts att göra det, slutförs åtgärderna när du använder [!UICONTROL Desktop Actions] från [!DNL Experience Manager]-webbgränssnittet. Programmet hämtar resursen först och slutför sedan åtgärden.
