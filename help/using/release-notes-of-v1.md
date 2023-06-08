---
title: Versionsinformation om datorprogrammet v1.10
description: Versionsinformation, förbättringar, nya funktioner, kompatibilitet och nedladdningslänkar för AEM program version 1.10.
exl-id: 886864e0-016a-4a17-b3ba-4b18a514214a
source-git-commit: df5283f6bef6adbb007bf93c6dabb3b12e430f58
workflow-type: tm+mt
source-wordcount: '3898'
ht-degree: 0%

---

# [!DNL Adobe Experience Manager] versionsinformation för datorprogram v1.10 {#aem-desktop-app-release-notes}

För datorprogram v1.x är följande hämtningslänkar och AEM kompatibilitetsinformation.

| Produkter | [!DNL Adobe Experience Manager] datorprogram |
|--- |--- |
| Version | 1.10 (1.10.0.6 i Mac och 1.10.0.3 i Windows) |
| Typ | Mindre release |
| Datum | 1.10.0.6 (Mac): 15 april 2020; 1.10.0.3 (Win): 31 augusti 2018 |
| Hämta URL:er | [Mac OS X 64 bitar](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/adobe/aem-desktop-app/aem-desktop-osx-1.10.0.6.dmg); [Windows 32 bitar](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/adobe/aem-desktop-app/aem-desktop-win32-1.10.0.3.exe); [Windows 64 bitar](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/adobe/aem-desktop-app/aem-desktop-win64-1.10.0.3.exe) |
| Kompatibilitet | AEM 6.5.x; AEM 6.4.x; AEM 6.3 SP2, AEM 6.2 SP1 CFP2+; AEM 6.1 SP2 CFP7+ |

>[!NOTE]
>
>Storleksgränsen för cachen används inte. När skrivbordsappen startas beräknas cachestorleken en gång och ett meddelande visas om storleken ligger nära den fördefinierade gränsen.

## Systemkrav och krav {#system-requirements-and-prerequisites}

[!DNL Adobe Experience Manager] skrivbordsappen är kompatibel med följande operativsystem:

* Mac OS X 10.10 eller senare, med de senaste felkorrigeringarna.

* Windows 10 med de senaste servicepaketen och felkorrigeringarna.

>[!NOTE]
>
>Windows 7 stöds inte längre. Se [artikeln om EOL i Windows 7](https://support.microsoft.com/en-us/help/4057281/windows-7-support-ended-on-january-14-2020).

Adobe rekommenderar starkt att du använder den senaste versionen av AEM för att få tillgång till de senaste funktionerna, de senaste felkorrigeringarna och bästa möjliga prestanda.

Den version av AEM program du tänker installera på den lokala datorn kräver en specifik AEM serverversion/ytterligare komponenter på serversidan (Service Pack, hot fixes eller feature packs). Kontrollera att AEM är korrekt konfigurerad innan du ansluter till den för första gången. Kontakta AEM om du behöver hjälp.

Se [detaljerad kompatibilitetsmatris](#compatibilitymatrix) i slutet av det här dokumentet för att utvärdera kraven för din konfiguration.

## Nyheter i datorprogrammet v1.10 {#what-s-new-in-aem-desktop-app}

AEM datorprogram 1.10 fokuserar på att förbättra användarupplevelsen kring stora överföringar, information om bakgrundsåtgärder och optimerad upplevelse när resurser öppnas med länkade filer (som InDesign).

>[!NOTE]
>
>Om du använder macOS 10.15.4 eller senare ska du använda minst version 1.10.0.6 av programmet. Den här korrigeringsversionen överensstämmer med [Krav för Apple-notarius publicus](https://developer.apple.com/news/?id=04102019a).

**Lokal redigering/utcheckning**: Automatiska överföringar av ändringar som sparats till resurser kan inaktiveras i statusfönstret. På så sätt kan användaren fortsätta arbeta med filer och spara ändringar och sedan, när de är klara, bestämma sig för att överföra alla ändringar.

**Fönstret Förenklad resursstatus**. Statusfönstret förenklades. The [!UICONTROL Uploads] visas nu både enskilda resurser och mapp- och bulköverföringar. Fliken Överföringar i grupp har tagits bort.

**Programikon för att indikera massöverföringar**. Programikonen indikerar att en massöverföring pågår genom att visa ett &quot;överföringsöverlägg&quot;.

**Meddelanden om uppdateringskonflikter**. När programmet upptäcker en konflikt när en resurs uppdateras visas ett meddelande så att användaren kan granska den utan att behöva övervaka statusfönstret. När programmet startas görs en sökning efter alla konflikter så att användaren kan lösa dem.

**Bättre hantering av anslutningsförluster**. Massöverföringar pausas om en anslutning bryts och användaren kan återupptas senare. A [!UICONTROL Retry] kan du göra om en misslyckad överföring av en enskild fil.

## Installationsanvisningar {#installation-instructions}

Detaljerade anvisningar finns i [Installera och konfigurera AEM datorprogram](install-configure-app-v1.md).

## Förbättringar i tidigare versioner {#enhancements-in-the-previous-versions}

Den här versionen utökar och ersätter tidigare versioner av [!DNL Experience Manager] skrivbordsappen, som innehåller följande viktiga förbättringar:

* **Version 1.9/1.9.1**: återuppta överföringar, förbättrat statusfönster, programikoner som anger status för programmet/anslutningen, förhämtning av länkade resurser för InDesign-filer.

* **Version 1.8**: bättre kontroll över cachestorleken för användaren, förbättrad inloggningsupplevelse för SAML/SSO i Windows, stöd för .pac-nätverksproxy i Mac samt problem som rapporterats av kunden.

* **Version 1.7**: förbättrad stabilitet och cachelagringslogik, bättre stöd för nätverksproxy och möjlighet att rensa interna filer efter avinstallation.

* **Version 1.6**: förbättringar av inloggningsprocessen för olika AEM säkerhetskonfigurationer samt programmets stabilitet och prestanda.

* **Version 1.5**: programstabilitet och motståndskraft mot olika nätverksproblem, bättre stödbarhet.

* **Version 1.4**: möjlighet att överföra hierarkiska mappar i bakgrunden med förloppsövervakning.

* **Version 1.3**: prestandaförbättringar och stabilitet när det gäller att komma åt filer och spara ändringar i AEM, särskilt från Creative Cloud-program som InDesign, Illustrator eller Photoshop. Det syftade till att ge användarna en mer lokal skrivbordsliknande upplevelse när de arbetade med filer, samtidigt som de hanterade nätverksdataöverföringsåtgärder i bakgrunden.

### Förbättringar har gjorts sedan AEM datorprogram 1.9 {#Enhancements-Available-Since-AEM-Desktop-App-19x}

[!DNL Adobe Experience Manager] skrivbordsapp 1.9.1 var en korrigeringsrelease som åtgärdar några viktiga kundproblem kring utcheckning av resurser och kopiering av filer från nätverksresurs till en lokal katalog.

* Resurser som checkats ut av en användare bör inte vara tillgängliga för ändring för andra användare (CQ-4246009)

* Supportkopia från mappad mapp till lokal mapp när användarmappen finns på en separat diskpartition (CQ-4243978)

AEM program 1.9 fokuserar på att förbättra användarupplevelsen kring stora överföringar, information om bakgrundsåtgärder och optimerad upplevelse när resurser öppnas med länkade filer (som InDesign).

**Återuppladdningsbara överföringar**
För överföringar, särskilt runt stora filer, finns det ett alternativ för att pausa/återuppta dem i det nya fönstret Resursstatus.

**Förbättrat fönster för resursstatus**
Ett förbättrat statusfönster för resurser innehåller följande information om resurser.

[!UICONTROL Changes]

* Visar ändringar som står i kö.

* Visar pågående överföringar, inklusive en förloppsindikator, överföringshastighet, total filstorlek och överföringsstorlek hittills.

* Slutförda överföringar visas med total överförd och slutlig kostnad.

* Misslyckade överföringar visas tillsammans med ett felmeddelande och överföringsinformation, om sådan finns.

* Överföringar som har misslyckats tre gånger visar ett felmeddelande.

* Filer som står i konflikt visas med en ikon som användaren kan klicka på. Om du klickar på ikonen visas en dialogruta med en förklaring och två alternativ:

   * [!UICONTROL Keep Mine] överför filen direkt till servern.

   * [!UICONTROL Overwrite Mine] tar omedelbart bort den lokala filen och hämtar en ny kopia från servern.

[!UICONTROL Downloads]

* Visar pågående hämtningar, inklusive överföringshastighet och storlek som överförts hittills.

* Slutförda nedladdningar visas med total överförd slutfrekvens och en ikon som öppnar filen när du klickar på den (endast tillgängligt för enstaka filer).

* Misslyckade hämtningar visas med ett felmeddelande och överföringsinformation, om sådan finns.

* Sidfoten visar det totala antalet nedladdade filer och den genomsnittliga överföringshastigheten.

* Om en användare väljer att öppna eller redigera flera filer från [!DNL Experience Manager Assets] Webbgränssnittet kommer att grupperas tillsammans. Exempel: myasset.jpeg och ytterligare fyra filer.

* När du hämtar InDesign-dokument, inklusive länkade resurser som lagras i AEM Assets, hämtas alla länkade resurser först av datorprogrammet innan du öppnar [!UICONTROL Adobe InDesign] dokumentera och ange hämtningen av länkade resurser. Exempel: 5 av 24.

[!UICONTROL Bulk Uploads]

Överföra stora mapphierarkier via [!UICONTROL Create] > [!UICONTROL Upload Folder] i AEM webbgränssnitt eller kopiering och om du väljer Klistra in resurser i Finder eller Utforskaren på snabbmenyn för skrivbordsappen, aktiveras användningen av den här dialogrutan.

* Visar pågående överföringar, inklusive en förloppsindikator och namnet på filen som överförs för närvarande.

* Överföringar som pågår innehåller en ikon som avbryter överföringen när användaren klickar på den. Överföringen avbryts när den överförda filen har slutförts.

* Misslyckade överföringsprocesser visas med ett felmeddelande (endast om hela överföringen misslyckas).

* Om en enskild fil inte överförs visas den på fliken som ett fel. Annars visas inte enskilda filer på fliken * bara en post för hela överföringen.

**Ikoner som anger status för bakgrundsåtgärder**

Programikonen visar läget för bakgrundsåtgärderna för att ge användarna bättre visuella referenser. Om programmet till exempel inte är anslutet till AEM kommer ikonen att bli nedtonad och om det finns en aktiv överföring visas en&quot;synkroniseringsövertäckning&quot; osv.

**Förhämtning av länkade resurser**

För att förbättra användarupplevelsen när du arbetar med InDesign-dokument, som innehåller länkade resurser som lagras i AEM, försöker skrivbordsappen hämta dessa länkade filer i förväg till det lokala cacheminnet innan det hämtar och öppnar InDesign-dokumentet. På så sätt kommer användaren att ha de länkade filerna tillgängliga lokalt och behöver inte vänta längre när de öppnas i InDesign (på länkpanelen).
Observera att förhämtning bara fungerar om AEM känner igen länkarna på serversidan. En resurs med kända länkar kommer att ha en lista med &quot;Referenser&quot; i egenskapsvyn för resursen InDesign.

### Förbättringar som är tillgängliga sedan AEM datorprogrammet 1.8.x {#enhancements-available-since-aem-desktop-app-18x}

AEM program 1.8.1 snabbspolning tillkom förbättringar när flera filer öppnas samtidigt från AEM till version 1.8 (CQ-4237747, CQ-4238780). Förbättringar i AEM program 1.8:

* Cachelagring: nytt användargränssnitt för hantering AEM cacheminne för skrivbordsappar (CQ-4208690), inklusive

   * visa aktuell cachestorlek

   * definiera maximal cachestorlek innan ett meddelande skickas

   * Cachestorleken kontrolleras endast vid start av skrivbordsappen och ett meddelande visas om den har nått den konfigurerade gränsen

   * rensningsknappen för cache är nu tillgänglig i det nya användargränssnittet

* Inloggning: (Win) Inloggning till AEM instans som konfigurerats att använda SAML och SSL har korrigerats (CQ-4216353)

* Nätverk:

   * när en AEM förfaller meddelas användaren nu och kan klicka på meddelandet för att logga in igen (CQ-4202028).

   * (Mac) Lägg till stöd för anslutning till AEM via .pac-proxykonfiguration (CQ-4233430).

   * (Win) Åtgärda problem med dialogrutan Avancerat - inloggnings-URL (CQ-4236061).

* Felkorrigeringar:

   * Dialogrutan Mer resursinformation: ibland var åtgärdsfältet inte synligt (CQ-4208540).

   * (Win) Filen kan nu synkroniseras efter återställning till en tidigare version från AEM Assets UI (CQ-4216411).

### Förbättringar som är tillgängliga sedan AEM datorprogram 1.7 {#Enhancements-Available-Since-AEM-Desktop-App-17}

* Stabilitet:

   * Förbättrad stabilitet när AEM datorprogram ansluter till en överlagrad AEM (CQ-4224803).

   * Förbättrad stabilitet när många filer begärs (CQ-4224212).

   * Förbättrad uppdatering av resurser med ytterligare kontroll (CQ-4228291).

* Cachelagring:

   * Åtgärda diskfel och problem med att öppna filer i Photoshop, InDesign, Finder (CQ-4223993, CQ-4217603, CQ-4223717).

   * Förbättrad cachelagring för att undvika binärfiler i nollstorlek (CQ-4216599).

* Inloggning: Tillåt anslutning med strictSSL inaktiverat för specialkonfigurationer (som lokalt utfärdade certifikat) (CQ-4223949).

* Nätverk: Förbättrat stöd för anslutning via nätverksproxy (CQ-4223477, CQ-4221280, CQ-4206854).

* Installation och avinstallation:

   * (Win) Avinstallation av rengöringsmedel (CQ-4220906).

   * [Windows 32 bitar] Det gick inte att installera Microsoft .NET Framework v. 4.5 (CQ-4218084).

   * (Mac) Manuellt skript för att ta bort skrivbordsappfiler helt (CQ-4216489).

>[!NOTE]
>
>Problem som påträffas AEM betaversioner av program 1.7 (som inte fanns i version 1.6 rapporteras inte i versionsinformationen).

### Förbättringar som är tillgängliga sedan AEM datorprogram 1.6 {#Enhancements-Available-Since-AEM-Desktop-App-16}

* Dokumentation: Nytt [Metodtips för v1.x-appen](/help/using/best-practices-for-v1.md) dokumentation.

* Förbättrad inloggningsprocess för AEM:

   * Förbättra SAML-hanteringen * Slappna av i regler (CQ-4202781).

   * Lägg till funktioner för att konfigurera en separat inloggnings-URL i Inställningar (CQ-4214052, CQ-4214051).

* Användbarhet: Meddela användaren när resursen fortfarande laddas ned för större resurser (CQ-4216284).

* Nätverk:

   * DNS-cachning (CQ-4210176).

   * Stöd för anslutning via proxy i Windows (CQ-4206854).

* Cachelagring och åtkomst till nätverksresurs i Finder/Utforskaren:

   * Låsikonen visas nu för utcheckade resurser i Windows 10 (CQ-90957).

   * Mappinnehåll kan försvinna/visas igen i en nätverksresurs (CQ-4209160, CQ-4210180).

   * Fel vid filöverföring på grund av en konflikt som rapporterats i status för överföringskön (CQ-4215727).

   * När du öppnar flera filer från skrivbordsappen i PS kan trunkerade eller ofullständiga meddelanden visas (CQ-4216276).

* Stabilitets- och prestandakorrigeringar:

   * Förbättrade prestanda vid bläddring i mappar med många resurser (CQ-4214933).

   * skrivbordsappen 1.5 kan göra datorn långsammare med tiden (CQ-4209159).

   * Visa endast köstatusfunktionen för den användare som installerade programmet (CQ-4212199).

   * (Windows) Kontrollera att 32-bitars installationsprogram inte innehåller 64-bitarskod (CQ-4217406).

* Utvalda problem som hittats och korrigerats i 1.6 Beta:

   * Hög processoranvändning (CQ-4218070).

   * Dra och släpp-filer genererar fel vid överföring till AEM (CQ-4217006).

### Förbättringar som är tillgängliga sedan AEM datorprogram 1.5 {#Enhancements-Available-Since-AEM-Desktop-App-15}

**Version 1.5.1.5 för Mac OS X:** Version 1.5.1.5 ger följande fördelar:

* Nya funktioner och förbättringar: Lägg till funktionen Kopiera/Klistra in i Finder-integreringen för att möjliggöra direkt överföring från skrivbordet till AEM (CQ-4208158).

* Felkorrigeringar:

   * Korrigerat fel 43 som uppstod ibland vid namnbyte av resurser (CQ-4207900).

   * När du återgår till en äldre version från tidslinjen i AEM uppdateras inte resursen i Finder (CQ-4205194).

   * skrivbordsappen kraschar vid bläddring i stora kapslade kataloger (CQ-4208539).

   * monteringspunkten för skrivbordsappar är nu /Volumes/DAM så den är konsekvent för alla användare (CQ-4208159).

   * När du placerar filen i InDesign för första gången visas en uppdateringsvarning (CQ-4207454).

Kommentarer om länkvarningar: Creative Cloud-program (till exempel InDesign) tar en ögonblicksbild av objektets senaste ändringsdatum när det placeras. Om det datumet ändras vid ett senare tillfälle kommer Adobe Creative Cloud-programmet att rapportera att länkarna är inaktuella. Detta rapporteras på några sätt:

* När Adobe Creative Cloud-appen startas visas en dialogruta som informerar användaren om att de länkade resurserna är inaktuella och uppmanar användaren att vidta åtgärder.

* Om Adobe Creative Cloud-programmet redan körs visas en gul triangelvarningsikon på den länkade resursen.

Det här beteendet är detsamma för resurser på den lokala hårddisken och resurser i en katalog som är monterad AEM Skrivbord, med följande undantag:

* Om en placerad resurs ändras av en annan användare visas varningsikonen första gången som andra användare öppnar ett dokument som innehåller den placerade resursen. Detta händer bara om den placerade resursen redan har cache-lagrats lokalt.

* Om en användare ändrar en placerad resurs via AEM skrivbordskatalog och sedan rensar sin lokala cache, kommer den placerade resursen att rapporteras som inaktuell.

Båda dessa fall förväntas och är biverkningar av arkitekturen&quot;fördröjd synkronisering&quot; i AEM Desktop.

**Version 1.5.0.x för Mac OS X och Windows:** Den här versionen AEM datorprogrammet har följande fördelar:

* Bättre stabilitet och motståndskraft mot nätverksproblem.

   * Mer stabil mappning av AEM Assets-mappar (CQ-103276, CQ-4204669, CQ-4203957).

   * Bättre hantering av cachelagrade filer (CQ-4204336, CQ-4206263).

   * Förbättrad hantering av hämtning/överföring av stora filer som är större än 2 GB (CQ-4206438).

   * Korrigerat &quot;Fel 36&quot; vid flytt eller namnbyte av ett större antal filer i Finder (CQ-4204640).

* Optimeringar i nätverkskommunikation med AEM Server (CQ-4204974, CQ-100903).

* Förbättrad tillförlitlighet för att öppna, placera och spara AEM i Creative Cloud-appar (CQ-4203968, CQ-4205511, CQ-103543, CQ-4207141, CQ-90980).

* Förbättrad stödbarhet: alternativ för att rensa cacheminne (CQ-4202541), enkel åtkomst till loggar (CQ-4202340, CQ-4204673).

* Andra korrigeringar:
   * Bättre stöd för resurser och mappar med japanska tecken i språkinställningarna för namn/icke-engelska (CQ-4195433, CQ-4205793, CQ-4199446).

   * Bättre hantering av inloggning med SSL (CQ-4200217).

   * Säkrare montering av aktier (CQ-4200793).

   * Olika stabilitetsförbättringar (CQ-4207539, CQ-4200378).

   * Bättre hantering av AEM Assets URL i Inställningar (CQ-97388).

### Förbättringar som är tillgängliga sedan AEM datorprogram 1.4 {#Enhancements-Available-Since-AEM-Desktop-App-14}

* Förenklad överföring av hierarkiska mappar med den nya åtgärden Skapa > Överför mapp i Touch-gränssnittet.
   * Åtgärden initierar en mappöverföring som utförs av skrivbordsprogrammet
   * Skrivbordsappen går igenom den angivna mapphierarkin på skrivbordet i bakgrunden och överför filerna till AEM Assets
   * Användaren kan övervaka förloppet i det nya fönstret Status för överföringskö med förloppsindikator för pågående åtgärder
   * Status för överföringskö ger även bättre felsökningsinformation (t.ex. ingen anslutning till server)
* Ny redigeringsåtgärd i Touch UI, som kombinerar åtgärderna Checka ut och Öppna i ett enda
* Optimerad gruppering av skrivbordsrelaterade åtgärder i Touch UI (AEM 6.3)
* Förbättrad kompatibilitet med de senaste operativsystemsversionerna
* Kundrapporterade korrigeringar

### Förbättringar som är tillgängliga sedan AEM datorprogram 1.3 {#Enhancements-Available-Since-AEM-Desktop-App-13}

* Ökad effektivitet. Användarna slipper vänta på att nätverksoperationerna ska slutföras.
* Förbättrad integrering med Finder, som ger bättre stabilitet och åtkomst till funktioner som miniatyrbilder.
* Cachelagring och prestandaförbättringar.
* Bättre stöd för att spara direkt från skrivbordsappar (PS, ID, AI och så vidare).
* Förbättrad integrering med Mac OS (protokoll för lokal nätverksenhet har ändrats från WebDAV till stabilare SMB1).
* Skrivbordsappen ansluter till AEM med AEM HTTP RESTful-protokoll.
* Filerna sparas först lokalt och överförs sedan tillbaka till AEM i bakgrunden efter en fördefinierad tidpunkt (30 sek). Detta minskar tiden det tar att spara filer.
* Bättre hantering av skrivbordsprogram där mellanliggande filåtgärder används för att spara en fil (delvis sparade och tillfälliga filer), vilket gör att tidslinjen för AEM kan visa korrekt information om version och överföring av resurser.
* Dialogrutan visas för att spåra status för bakgrundsuppladdningsuppgifter.

## Ändringslista {#list-of-changes}

### Monteringspunkt på Mac {#mount-point-on-mac}

Sedan MacOS 10.12 (Sierra) har Apple ändrat behörigheterna för mappen /Volumes som används för att montera nätverksenheter och enheter till mer restriktiva. Det krävs administratörsbehörighet för att skapa en ny monteringspunkt. Problemet har åtgärdats i MacOS 10.12.5.

Eftersom AEM datorprogram ska köras för användare som inte har administratörsbehörighet på den lokala datorn ändrades monteringspunkten för AEM Assets-databasen i 1.4 och 1.5 till en DAM-undermapp i användarens lokala mapp på MacOS (CQ-104183).

Eftersom mappen /Volumes inte längre kräver administratörsbehörighet återställs den här ändringen i 1.5.1. Detta gör det även möjligt att dela InDesign-dokument som har placerat AEM resurser mellan MacOS-användare.

### Protokolländring (sedan v1.3) {#protocol-change-since}

* Mac OS X:
   * Det lokala nätverksenhetsprotokollet för OS X-skrivbordsintegrering har ändrats till SMB1 från WebDAV.
   * Den AEM databasen som är monterad med skrivbordsappen visas som en &quot;smb&quot;-nätverksenhet i Finder i stället för en WebDAV-enhet.
* Windows:
   * Det lokala nätverksenhetsprotokollet för Windows skrivbordsintegreringar kvarstår; AEM monteras som en WebDAV-resurs.
* För båda plattformarna (Windows och Mac):
   * Protokollet för åtkomst/hämtning av resurser och för överföring av ändringar i AEM har ändrats till det inbyggda AEM-protokollet, som är ett HTTP-baserat RESTful-protokoll. Den ger bättre kontroll över nätverksoperationer och är mer kompatibel med nätverksinfrastrukturen.

>[!NOTE]
>
>I Mac OS X resulterar ändringen av det lokala nätverksenhetsprotokollet från WebDAV till SMB1 i en annan lokal sökväg till samma resurs i databasen. Detta kan påverka länkar till filer som har placerats i Adobe Creative Cloud-program via kommandot Montera. Se [Använd AEM](use-app-v1.md) för mer information.

### Filhantering (sedan 1.3) {#file-handling-since}

* Mappar uppdateras automatiskt efter en fördefinierad fördröjning (för närvarande 30 sekunder).
* Filer som har checkats ut av andra användare är skrivskyddade.
* Filerna sparas på en nätverksenhet som monterats via skrivbordsappen i två faser.
* I den första fasen sparas en fil lokalt. På så sätt behöver användaren som sparar filen inte vänta tills filen har överförts helt till AEM och kan återuppta arbetet så fort filen har sparats.
* I den andra fasen överför skrivbordsappen en uppdaterad fil till AEM efter en fördefinierad fördröjning (till exempel 30s). Den här åtgärden utförs i bakgrunden. Använd **Visa synkroniseringsstatus för bakgrundsfil** för att visa överföringsåtgärdens status.

## Viktiga meddelanden {#important-notices}

**Mappöverföring.** Vi rekommenderar att du använder den nya funktionen för mappöverföring för att överföra större, hierarkiska mappar till AEM, i stället för att använda en kopia/dra och släpp i en monterad AEM från Finder-/Utforskarnivå. När du använder funktionen för mappöverföring kommunicerar skrivbordsappen direkt med AEM och har därför bättre kontroll över hela processen.

**Håll AEM session tillgänglig.** AEM datorprogram är beroende av en session som är öppen för AEM Assets-servern för att säkerställa att den fungerar som den ska. För användare som arbetar med datorprogram varje dag rekommenderar vi att du avmonterar AEM Assets i slutet av dagen för att tvinga fram utloggning och sedan &quot;Montera AEM Assets&quot; på morgonen för att säkerställa att de är inloggade och att nätverksresursen fungerar.

**Stäng av&quot;Ikonförhandsvisning&quot; i Finder.** Om du vill kunna bläddra i stora mappar med Finder, särskilt om nätverksanslutningen är dålig, måste du se till att både Icon och Icon Preview är inaktiverade. I annat fall börjar Finder hämta varje resurs i en mapp för att generera en liten förhandsvisning, vilket kan leda till sämre prestanda och hög bandbreddsanvändning (CQ-4219779)

* Gå till AEM Assets delade nätverksmapp i Finder
* Högerklicka på DAM-monteringspunkten
* Välj Visa visningsalternativ
* Avmarkera Visa ikonförhandsvisning
* Klicka på Använd som standard

**Rensa cacheminnet vid anslutning till en ny AEM.** Om skrivbordsprogrammet ansluter till en annan AEM med samma URL, rensas inte cachen automatiskt. Rensa cacheminnet manuellt för att säkerställa korrekta åtgärder. Observera att detta vanligtvis sker vid testning, när AEM installationer kan ersättas när de körs på samma URL (CQ-4216982)

**Använd CA-signerade SSL-certifikat.** Observera att AEM datorprogram inte har stöd för självsignerade SSL-certifikat vid anslutning till AEM via en säker HTTPS-anslutning. Ett CA-signerat certifikat krävs på servern för sådana anslutningar. (CQ-87941)

## Kända fel {#known-issues}

* Allmänt:
   * Server-URL:er krävs för att peka mot servern utan sökväg (till exempel: `http://server`, `https://server`, `http://server:port`, eller `https://server:port`). Kontextsökvägar och andra undermappar än /content/dam stöds inte (CQ-89343, CQ-87272)
* Filnamn/lokalisering:
   * Fil- och mappnamn med reserverade tecken hanteras inte korrekt. Se till att använda fil- och mappnamn som uppfyller AEM (CQ-93361, CQ-93308, CQ-89276, CQ-4217183)
   * I vissa program, som Adobe Illustrator, kan filer med namn som inte stöds i AEM skapas. Lägg till exempel till `Converted` efter konvertering av en fil, vilket medför att den inte kan överföras (CQ-4216985)
   * Resurser med internationella namn kan visas och försvinna med några sekunder
* Checka in och Checka ut:
   * En resurs som har checkats ut av en användare kan inte öppnas för en annan användare, antingen genom åtgärden Öppna från Touch-gränssnittet eller direkt på skrivbordet. I vissa program kan det rapporteras som låst, men det kan också vara skadat eller till och med låst när programmet öppnas. (CQ-4199234)
   * Om flera användare ändrar filer samtidigt kan vissa ändringar gå förlorade. Lösningen är att använda funktionerna för in- och utcheckning för att förhindra att flera användare ändrar samma fil (CQ-97035)
   * I vissa program stöds inte den skrivskyddade flaggan korrekt, vilket gör att en användare kan spara en fil som är utcheckad av en annan användare. Den ändrade filen överförs inte förrän den andra användaren checkar in filen. Båda ändringarna är tillgängliga i AEM som olika versioner av tillgången (CQ-89551, CQ-87572, CQ-89615)
   * Statusen utcheckad och skrivskyddad rapporteras separat i Finder. Detta resulterar i två låsikoner när en användare checkar ut en resurs (CQ-89507)
* Integrering med Finder:
   * När du drar/släpper stora filer kan det hända att Finder gör timeout medan filer överförs i bakgrunden. Detta resulterar i en `Error - 36`. Du kan lösa problemet genom att dra/släppa eller öppna resursen igen (CQ-4219628)
   * Manuell mappinläsning fungerar inte alltid. Tillfällig lösning: vänta i 30 sekunder på att mappen uppdateras automatiskt. (CQ-97389)
   * Mer resursinformation... begränsas till val av enstaka filer (CQ-89542, CQ-87656)
   * Öppna i AEM Assets... begränsas till enstaka fil- och mappval (CQ-83382)
   * Ett fel uppstod vid namnbyte av resurser som inte har något tillägg (CQ-4218971)
* Funktionen Kopiera/Klistra in: Klistra in är tillgängligt när ingen resurs har kopierats till Urklipp
* Windows:
   * Filer med ADS (Alternate Data Streams) stöds endast fullt ut på NTFS. Om du kopierar sådana filer till WebDAV-resursen som tillhandahålls av skrivbordsappen visas ett varningsmeddelande om att filen har egenskaper som inte kan kopieras till den nya platsen. Detta är vanligtvis bra eftersom egenskaperna bara är relevanta för ett visst program på användarens skrivbord och inte har något att göra med det faktiska filinnehållet (CQ-103770) (Win)
   * skrivbordsappen i Windows måste installeras av användaren som ska använda den (CQ-4216389) (win)
   * Appen kan krascha när du väljer [!UICONTROL Retry] alternativ för misslyckad överföring under vissa omständigheter efter återupptagen batchöverföring vid frånkoppling (CQ-4251884) (Win)

## Användbara resurser {#helpful-resources}

* [AEM](https://experienceleague.adobe.com/docs/)
* [Använd AEM v1.x](use-app-v1.md)
* [AEM praxis för datorprogram v1.x](best-practices-for-v1.md)

## Kompatibilitetsmatris och krav {#compatibilitymatrix}

AEM kan användas med olika versioner av AEM. Se kompatibilitetsmatrisen för de versioner som stöds.

| Version | Revision | Releasedatum | Kompatibilitet |
|--- |--- |--- |--- |
| 1.10 | 1.10.0.3 (Mac och Win) | 31 aug 2018 | AEM 6.5, AEM 6.4 SP1, AEM 6.3 SP2, AEM 6.2 SP1 CFP2+; AEM 6.1 SP2 CFP7+ |
| 1.9 | 1.9.1.1 (Mac och Win) | 21 juni 2018 | AEM 6.4; AEM 6.3 SP1, AEM 6.2 SP1 CFP2+; AEM 6.1 SP2 CFP7+ |
| 1.8 | 1.8.1.0 (Mac och Win) | 28 mars 2018 | AEM 6.4; AEM 6.3 SP1, AEM 6.2 SP1 CFP2+; AEM 6.1 SP2 CFP7+ |
| 1.7 | 1.7.0.3 (Mac och Win) | 10 jan 2018 | AEM 6.3 SP1, AEM 6.2 SP1 CFP2+; AEM 6.1 SP2 CFP7+ |
