---
title: Felsöka AEM-datorprogrammet version 1.x
description: Felsök version 1.x av AEM-datorprogrammet för att lösa tillfälliga problem som rör installation, uppgradering, konfiguration och så vidare.
uuid: ce98a3e7-5454-41be-aaaa-4252b3e0f8dd
contentOwner: AG
products: SG_EXPERIENCEMANAGER/6.3/ASSETS
discoiquuid: f5eb222a-6cdf-4ae3-9cf2-755c873f397c
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: ab63bfd7eea356be924e1ed62eef387796913e6c

---


# Felsök AEM-skrivbordsappen v1.x {#troubleshoot-aem-desktop-app}

Felsök AEM-skrivbordsappen för att lösa tillfälliga problem som rör installation, uppgradering, konfiguration och så vidare.

Adobe Experience Manager (AEM) innehåller verktyg som hjälper dig att mappa AEM Assets-databasen till en nätverksresurs på en dator (SMB-resurs på Mac OS). Nätverksresursen är en operativsystemsteknik som gör att fjärrkällor kan hanteras som om de var en del av en dators lokala filsystem. När det gäller skrivbordsprogram är en AEM-instansens DAM-databasstruktur (Digital Asset Management) avsedd som fjärrfilskälla. I följande diagram beskrivs skrivbordsappens topologi:

![skrivbordsappsdiagram](assets/aem-desktopapp-architecture.png)

Med den här arkitekturen fångar skrivbordsappen upp filsystemanrop (öppna, stänga, läsa, skriva osv.) till den monterade nätverksresursen och översätter dem till interna AEM HTTP-anrop till AEM-servern. Filerna cachelagras lokalt. Mer information finns i [Använda AEM-datorprogrammet v1.x](use-app-v1.md).

## Översikt över komponenten AEM-skrivbordsapp {#desktop-app-component-overview}

datorprogrammet innehåller följande komponenter:

* **Skrivbordsprogrammet**: Programmet monterar eller avmonterar DAM som ett fjärrfilsystem och översätter filsystemanrop mellan den lokalt monterade nätverksresursen och den fjärr-AEM-instans som det ansluter till.
* **WebDAV/SMB-klient** för operativsystem: Hanterar kommunikation mellan Utforskaren/Finder i Windows och skrivbordsprogrammet. Om en fil hämtas, skapas, ändras, tas bort, flyttas eller kopieras, kommunicerar operativsystemets (OS) WebDAV/SMB-klient den här åtgärden med skrivbordsprogrammet. Efter att ha tagit emot kommunikationen översätter skrivbordsappen det till inbyggda AEM-fjärr-API-anrop. Om en användare till exempel skapar en fil i den monterade katalogen, initierar WebDAV/SMB-klienten en begäran som skrivbordsappen översätter till en HTTP-begäran som skapar filen i DAM. WebDAV/SMB-klienten är en inbyggd komponent i operativsystemet. Den är inte på något sätt kopplad till datorprogrammet, AEM eller Adobe.
* **Adobe Experience Manager-instans**: Ger åtkomst till resurser som lagras i DAM-databasen för AEM Resurser. Dessutom utför programmet åtgärder som begärts av skrivbordsappen för de lokala skrivbordsprogrammen som interagerar med den monterade nätverksresursen. AEM-målinstansen ska köra AEM version 6.1 eller senare. AEM-instanser som kör tidigare AEM-versioner kan kräva extra funktionspaket och snabbkorrigeringar som installeras för att bli fullt fungerande.

## Användningsexempel för AEM-datorprogrammet {#intended-use-cases-for-aem-desktop-app}

AEM-skrivbordsappen använder nätverksdelningstekniken för att mappa en fjärr-AEM-databas till en lokal dator. Den är dock inte avsedd som ersättning för en nätverksresurs som innehåller resurser, där användarna utför digitala resurshanteringsåtgärder direkt från sin lokala dator. Det kan vara att flytta eller kopiera flera filer eller dra stora mappstrukturer till AEM Assets-nätverksresursen direkt i Finder/Utforskaren.

Med AEM-skrivbordsappen kan du enkelt komma åt (öppna) och redigera (spara) DAM-resurser mellan AEM Assets Touch-gränssnittet och det lokala skrivbordet. Den länkar resurser på AEM Assets-servern till dina skrivbordsbaserade arbetsflöden.

Följande exempel visar hur AEM Desktop ska användas:

* En användare loggar in på AEM och använder webbgränssnittet för att hitta en resurs.
* Med hjälp av skrivbordsfunktionerna i AEM-webbgränssnittet kan användaren antingen öppna, visa eller redigera resursen på skrivbordet efter behov.
* AEM Desktop öppnar resursen i standardredigeraren för resursens filtyp.
* Användaren gör önskade ändringar av resursen.
* När en fil har ändrats kan användaren visa filens synkroniseringsstatus i statusfönstret för AEM Desktop-bakgrundssynkronisering.
* Med hjälp av snabbmenyn i AEM Desktop checkar användaren in/ut resursen eller återgår till DAM-användargränssnittet.
* När ändringarna är klara återgår användaren till AEM-webbgränssnittet

Detta är inte det enda användningsexemplet. Det visar dock hur AEM Desktop är en praktisk metod för att få åtkomst till och redigera resurser lokalt. Du uppmanas att använda DAM-webbgränssnittet så mycket som möjligt eftersom det ger en bättre upplevelse. Det ger Adobe större flexibilitet att uppfylla kundernas krav.

## Begränsningar {#limitations}

Nätverksresursen WebDAV/SMB1 gör det enkelt att arbeta med filer i Utforskaren/Finder-fönstret. Utforskaren/Finder och AEM kommunicerar dock över en nätverksanslutning som har vissa begränsningar. Den tid det tar att kopiera en fil på 1 GB till den monterade WebDAV/SMB-katalogen är ungefär densamma som den tid som krävs för att överföra en fil på 1 GB till en webbplats med en webbläsare. I det tidigare fallet kan varaktigheten vara längre på grund av ineffektivitet i WebDAV/SMB-protokollet och operativsystemets WebDAV/SMB-klienter (särskilt Mac OS X).

Det finns begränsningar för de typer av uppgifter som kan utföras från en monterad katalog. I allmänhet kan det vara svårt att arbeta med stora filer, särskilt när det gäller nätverksanslutningar med låg/hög fördröjning/låg bandbredd, särskilt när du redigerar stora filer.

Adobe rekommenderar att du utför vissa falltester innan du bekräftar för en klient att vissa typer av filer kan redigeras på plats från den monterade katalogen.

AEM Desktop lämpar sig inte för omfattande ändringar i filsystemet, inklusive, men inte begränsat till:

* Flytta eller kopiera filer och kataloger
* Lägga till många resurser i AEM
* Söka efter och öppna filer i filsystemet, utom för att bläddra bland mappar
* Komprimera eller dekomprimera filarkiv

På grund av begränsningar i operativsystemet har Windows en filstorleksbegränsning på 4 294 967 295 byte (cirka 4,29 GB). Det beror på en registerinställning som definierar hur stor en fil på en nätverksresurs kan vara. Registerinställningens värde är ett DWORD med en maximal storlek som är lika med det refererade talet.

Experience Manager-skrivbordsappen har inget konfigurerbart tidsgränsvärde som kopplar från anslutningen mellan Experience Manager-servern och skrivbordsappen efter ett fast tidsintervall. När du överför stora resurser, och anslutningen får timeout efter en stund, försöker programmet överföra resursen några gånger genom att öka tidsgränsen för överföring. Det finns inget rekommenderat sätt att ändra standardinställningarna för timeout.

## Cachelagring och kommunikation med AEM {#caching-and-communication-with-aem}

AEM-skrivbordsappen har interna cachnings- och bakgrundsuppladdningsfunktioner som förbättrar slutanvändarens upplevelse. När du sparar en stor fil sparas den först lokalt så att du kan fortsätta arbeta. Efter ett tag (för närvarande 30 sekunder) skickas filen sedan till AEM-servern i bakgrunden.

Till skillnad från Creative Cloud-datorprogrammet eller andra filsynkroniseringslösningar, som Microsoft One Drive, är AEM-datorprogrammet inte en fullständig synkroniseringsklient. Orsaken till detta är att det ger tillgång till hela AEM Resurser-databasen, som kan vara mycket stor (hundratals gigabyte eller terabyte) för en fullständig synkronisering.

Cachelagring ger möjlighet att begränsa nätverks-/lagringskostnaderna till endast en delmängd av resurserna som är relevanta för användaren.

Så här utför AEM-datorprogrammet cachelagring:

* När du öppnar en mapp i Finder och miniatyrbilder/förhandsgranskningar av filer visas, eller när du öppnar en fil i ett program, cachelagras filens binärfil i skrivbordsprogrammet.
* När du lagrar filer via Finder eller andra skrivbordsprogram lagras filen lokalt först (cachelagrat) och operativsystemet meddelas. Filen köas sedan för överföring till servern i bakgrunden och överförs sedan över nätverket. Om ett nätverksfel inträffar försöker skrivbordsappen överföra hela filen igen i högst tre gånger. Om överföringen misslyckas efter tre försök markeras filen som en fil i konflikt och statusen visas i fönstret Status för bakgrundskööverföring. försöker inte uppdatera filen längre. Användaren bör uppdatera filen och överföra den igen när anslutningen har återställts

Alla åtgärder cachelagras inte lokalt. Följande överförs direkt till AEM Server utan lokal cachelagring:

* Åtgärder för mappar, till exempel skapa, ta bort och så vidare
* Mappöverföringsfunktionen som introducerades i version 1.4 överför en lokal mapphierarki utan att cachelagra filerna lokalt

## Individuella operationer {#individual-operations}

När du felsöker deloptimerade prestanda för enskilda användare ska du först granska [Begränsningar](https://helpx.adobe.com/experience-manager/desktop-app/troubleshooting-desktop-app.html#limitations). De följande avsnitten innehåller förslag på hur du kan förbättra prestandan för enskilda användare.

## Bandbreddsrekommendationer {#bandwidth-recommendations}

Den bandbredd som är tillgänglig för en enskild användare spelar en avgörande roll för WebDAV/SMB-klientens prestanda.

Adobe rekommenderar att en enskild användares överföringshastighet är nästan 10 Mbit/s. För trådlösa anslutningar delas bandbredd ofta mellan flera användare. Om flera användare samtidigt utför uppgifter som förbrukar nätverksbandbredd kan prestandan försämras ytterligare. Undvik sådana problem genom att använda en kabelanslutning.

## Windows-specifika konfigurationer {#windows-specific-configurations}

Om du kör AEM i Windows kan du konfigurera Windows för att förbättra WebDAV-klientens prestanda. Mer information finns på [https://support.microsoft.com/en-us/kb/2445570](https://support.microsoft.com/en-us/kb/2445570).

I Windows 7 kan prestandan för WebDAV förbättras om IE-inställningarna ändras. Mer information finns på [http://oddballupdate.com/2009/12/fix-slow-webdav-performance-in-windows-7/](http://oddballupdate.com/2009/12/fix-slow-webdav-performance-in-windows-7/).

## Samtidiga åtgärder {#concurrent-operations}

När du interagerar med en fil lokalt kontrollerar AEM Desktop om en nyare version av filen är tillgänglig i AEM. Om det finns en ny version hämtar programmet en ny kopia av filen till det lokala cacheminnet. AEM Desktop skriver dock inte över en lokalt cachelagrad fil om den har ändrats. Den här funktionen förhindrar att ditt arbete skrivs över av misstag.

När samma fil ändras både lokalt och i AEM skrivs versionen över i AEM med den lokalt ändrade versionen. I det här fallet är den tidigare versionen tillgänglig på resursens tidslinje. Du kan verifiera båda versionerna och lösa eventuella konflikter.

Om en lokal fil inte är kompatibel med den version som finns på servern visas ett meddelande om konflikten i dialogrutan för bakgrundsstatus. Lös problemet genom att öppna filen som är i konflikt och spara den. Om du sparar filen måste AEM Desktop synkronisera dina senaste lokala ändringar till AEM. Du kan visa tidigare versioner av resursen på tidslinjen och lösa eventuella konflikter.

Du bör ta hänsyn till ytterligare faktorer när flera användare försöker arbeta i separata monterade kataloger med samma AEM-instans som mål. Bland annat är följande faktorer viktiga:

* Mängden bandbredd som är tillgänglig i användarens ursprungliga nätverk
* Nätverkskonfiguration, t.ex. brandväggar eller proxies, för det ursprungliga nätverket
* Tillgänglig bandbredd i målets AEM-instansnätverk
* Om det finns en dispatcher före mål-AEM-instansen
* Aktuell inläsning på AEM-målinstansen

## Ytterligare AEM-konfigurationer {#additional-aem-configurations}

Om WebDAV-/SMB-prestanda försämras drastiskt när flera användare arbetar samtidigt kan du konfigurera några saker i AEM, vilket kan förbättra prestandan.

## Uppdatera resursövergående arbetsflöden {#update-asset-transient-workflows}

Du kan förbättra prestandan på AEM-sidan genom att aktivera tillfälliga arbetsflöden för arbetsflödet DAM Update Asset. Om du aktiverar tillfälliga arbetsflöden minskas den processorkraft som krävs för att uppdatera resurser när de skapas eller ändras i AEM.

1. Navigera till `/miscadmin` i den AEM-instans som ska konfigureras (till exempel `http://[Server]:[Port]/miscadmin`).
1. Expandera **Verktyg** > **Arbetsflöde** > **Modeller** > **dam** i navigeringsträdet.
1. Dubbelklicka på **DAM Update Asset**.
1. Gå till fliken **Sida** i den flytande verktygspanelen och klicka sedan på **Sidegenskaper**.
1. Markera kryssrutan **Övergående arbetsflöde** och klicka på **OK**.

### Justera kön för transient Granite-arbetsflöde {#adjust-granite-transient-workflow-queue}

En annan metod för att förbättra AEM-prestanda är att konfigurera värdet för det maximala antalet parallella jobb för jobbet Beviljit Transient Workflow Queue. Det rekommenderade värdet är ungefär hälften av antalet processorer som är tillgängliga på servern. Så här justerar du värdet:

1. Navigera till */system/console/configMgr* i den AEM-instans som ska konfigureras (till exempel <http://&lt;Server&gt;:&lt;Port&gt;/system/console/configMgr>).
1. Sök efter **QueueConfiguration** och klicka för att öppna varje jobb tills du hittar jobbet **Bevilja tillfällig arbetsflödeskö** . Klicka på ikonen Redigera bredvid den.
1. Ändra värdet för **maximalt antal parallella jobb** och klicka på **Spara**.

## AWS-konfiguration {#aws-configuration}

På grund av begränsningar i nätverkets bandbredd kan WebDAV/SMB-prestanda försämras när flera användare arbetar samtidigt. Adobe rekommenderar att storleken på AWS-instansen ökas för en AEM-målinstans som körs på AWS för att förbättra prestandan för WebDAV/SMB.

Den här åtgärden ökar specifikt mängden nätverksbandbredd som är tillgänglig för servern. Här är några detaljer:

* Den mängd nätverksbandbredd som är dedikerad till en AWS-instans ökar när instansens storlek ökar. Mer information om hur mycket bandbredd som är tillgänglig för varje instansstorlek finns i [AWS-dokumentationen](https://aws.amazon.com/ec2/instance-types/).
* Vid felsökning för en stor klient konfigurerade Adobe storleken på AEM-instansen till c4.8xlarge, främst för den dedikerade bandbredden på 4 000 Mbit/s som den erbjuder.
* Om det ligger en dispatcher framför AEM-instansen kontrollerar du att den har rätt storlek. Om AEM-instansen innehåller 4000 Mbit/s men dispatchern bara tillhandahåller 500 Mbit/s är den effektiva bandbredden bara 500 Mbit/s. Det beror på att avsändaren skapar en flaskhals i nätverket.

## Utcheckade filbegränsningar {#checked-out-file-limitations}

Det finns några kända begränsningar för hur du kan interagera med utcheckade filer via Utforskaren/Finder. Om en fil är utcheckad bör den vara skrivskyddad för alla förutom den användare som har filen utcheckad. Implementeringen av WebDAV/SMB1-protokollet i AEM verkställer den här regeln. Operativsystemets WebDAV-/SMB-klienter samverkar dock ofta inte på ett bra sätt med utcheckade filer. Nedan beskrivs några uddpunkter.

### Allmänt {#general}

När du skriver till en utcheckad fil används låset bara i AEM WebDAV-implementeringen. Därför används låset bara av klienter som använder WebDAV, till exempel skrivbordsprogram. Lås används inte via AEM-webbgränssnittet. I AEM-gränssnittet visas bara en låsikon i kortvyn för resurser som är utcheckade. Ikonen är kosmetisk och har ingen effekt på beteendet hos AEM.

I allmänhet fungerar inte WebDAV-klienterna som förväntat. Det kan finnas ytterligare problem. Att uppdatera eller kontrollera mediefilen i AEM är dock ett bra sätt att verifiera att mediefilen inte ändras. Detta beteende är typiskt för operativsystemets WebDAV-klienter, som inte styrs av Adobe.

### Windows {#windows}

Det verkar som om det går att ta bort en fil eftersom den försvinner från filutforskaren i Windows. Om du uppdaterar katalogen och checkar in AEM-resurser visas dock att filen fortfarande finns. Dessutom verkar redigeringen av filer lyckas (inga varningsmeddelanden eller felmeddelanden visas). Om du öppnar filen igen eller checkar in AEM-resurser igen visas dock att filen inte ändras.

#### Mac OS X {#mac-os-x}

Om du ersätter en fil visas ingen varning eller inget fel, men om du markerar resursen i AEM visas det att den inte ändras. Uppdatera eller kontrollera resursen i AEM för att verifiera att den inte ändras.

## Felsöka problem med ikoner för skrivbordsprogram (Mac OS X) {#troubleshooting-desktop-app-icon-issues-mac-os-x}

När du har installerat skrivbordsprogrammet visas menyikonen på menyraden. Om ikonen inte visas utför du följande steg för att lösa problemet:

1. Öppna operativsystemets terminalfönster.
1. Skriv följande kommando i kommandotolken och tryck sedan på Retur:

   ```shell
    cd ../Library/Caches.
   ```

1. Skriv följande kommando och tryck på Retur:

   ```shell
   rm -r com.adobe.aem.assetscompanion 
   ```

1. Skriv följande kommando och tryck på Retur:

   ```shell
   cd ~/Library/Preferences
   ```

1. Skriv följande kommando och tryck på Retur:

   ```shell
   rm com.adobe.aem.assetscompanion.plist
   ```

1. Skriv följande kommando och tryck på Retur:

   ```shell
   rm ~/Library/Group\ Containers/group.com.adobe.aem.desktop/*
   ```

1. Starta om systemet.

AEM Desktop försöker synkronisera en given fil tre gånger. Om filen inte kan synkroniseras efter det tredje försöket anser AEM Desktop att filen är i konflikt och meddelar dig via statusfönstret för bakgrundsuppladdning. Ett konfliktläge anger att dina senaste ändringar fortfarande är tillgängliga lokalt, men inte synkroniseras tillbaka till AEM. AEM-datorprogrammet försöker inte längre synkronisera.

Det enklaste sättet att åtgärda detta är att öppna filen som är i konflikt och spara den igen. Det tvingar AEM Desktop att försöka synkronisera ytterligare tre gånger. Om filen fortfarande inte kan synkroniseras finns mer hjälp i avsnitten nedan.

## Rensar cacheminnet för AEM Desktop {#clearing-aem-desktop-cache}

Att rensa AEM Desktop-cachen är en preliminär felsökningsåtgärd som kan lösa flera problem med AEM Desktop.

Du kan rensa cacheminnet genom att ta bort programmets cachekatalog på följande platser: Windows: %LocalAppData%\Adobe\AssetsCompanion\Cache\

Mac: ~/Library/Group/Containers/group.com.adobe.aem.desktop/cache/

Platsen kan dock ändras beroende på AEM Desktop konfigurerade AEM-slutpunkt. Värdet är en kodad version av mål-URL:en. Om programmet till exempel har som mål `http://localhost:4502`är katalognamnet `http%3A%2F%2Flocalhost%3A4502%2F`.

Ta bort katalogen &lt;Encoded AEM Endpoint> om du vill rensa cacheminnet.

>[!NOTE]
>
>Om du rensar cacheminnet för AEM-skrivbordet går lokala filändringar som inte har synkroniserats till AEM förlorade.

>[!NOTE]
>
>Från och med AEM-skrivbordsappversion 1.5 finns det ett alternativ i datorprogrammets användargränssnitt för att rensa cacheminnet.

## Hitta AEM Desktop-versionen {#finding-the-aem-desktop-version}

Proceduren för att kontrollera om AEM Desktop-versionen är densamma för både Windows och Mac OS.

Klicka på ikonen AEM Desktop och välj sedan **About**. Versionsnumret visas på skärmen.

## Uppgraderar AEM-datorprogrammet på macOS {#upgrading-aem-desktop-app-on-macos}

Ibland kan problem uppstå när du uppgraderar AEM-datorprogrammet på macOS. Detta orsakas av att det inte går att läsa in nya versioner av AEM Desktop korrekt i en äldre systemmapp för AEM-skrivbordsappen. Följande mappar och filer kan tas bort manuellt för att åtgärda problemet.

Innan du utför stegen nedan drar du programmet Adobe Experience Manager Desktop från mappen macOS Applications till Papperskorgen. Öppna sedan terminalen och kör följande kommando för att ange ditt lösenord när du uppmanas till det.

```shell
sudo rm -rf ~/Library/Application\ Support/com.adobe.aem.desktop
sudo rm -rf ~/Library/Preferences/com.adobe.aem.desktop.plist
sudo rm -rf ~/Library/Logs/Adobe\ Experience\ Manager\ Desktop

sudo find /var/folders -type d -name "com.adobe.aem.desktop" | xargs rm -rf
sudo find /var/folders -type d -name "com.adobe.aem.desktop.finderintegration-plugin" | xargs rm -rf
```

## Spara en fil som har checkats ut av andra {#saving-a-file-checked-out-by-others}

Operativsystemets tekniska begränsningar förhindrar att användare får en konsekvent upplevelse när de försöker skriva över en fil som är utcheckad av andra. Hur det ser ut varierar beroende på vilket program som används för att redigera den utcheckade filen. Ibland visas ett felmeddelande i programmet som indikerar ett skrivfel eller ett syntaktiskt eller allmänt fel visas. I andra fall visas inget felmeddelande och åtgärden verkar lyckas.

I så fall kan det hända att innehållet inte ändras när du stänger och öppnar filen igen. I vissa program kan dock en säkerhetskopia av filen sparas så att ändringarna kan tillämpas.

Oavsett hur filen fungerar ändras den inte när du checkar in den. Även om en annan version av filen visas synkroniseras inte ändringarna till AEM.

## Felsöka problem med att flytta filer {#troubleshooting-problems-around-moving-files}

Server-API:t kräver att ytterligare rubriker, X-Destination, X-Depth och X-Overwrite, skickas för att flytt- och kopieringsåtgärderna ska fungera. Avsändaren skickar inte dessa huvuden som standard, vilket gör att dessa åtgärder misslyckas. Mer information finns i [Ansluta till AEM bakom en Dispatcher](install-configure-app-v1.md#connect-to-an-aem-instance-behind-a-dispatcher).

## Felsöka problem med AEM-anslutning till stationära datorer {#troubleshooting-aem-desktop-connection-issues}

### Omdirigeringsproblem för SAML {#saml-redirect-issue}

Den vanligaste orsaken till problem med AEM Desktop som ansluter till din SAML-aktiverade (SSO-enabled) AEM-instans är att SAML-processen inte dirigerar tillbaka till den ursprungligen begärda sökvägen. Alternativt kan anslutningen dirigeras om till en värd som inte är konfigurerad i AEM Desktop. Så här verifierar du inloggningsprocessen:

1. Öppna en webbläsare.
1. Ange URL-adressen i adressfältet `/content/dam.json`.
1. Ersätt till exempel URL:en med mål-AEM-instansen `http://localhost:4502/content/dam.json`.
1. Logga in på AEM.
1. När du har loggat in kontrollerar du webbläsarens aktuella adress i adressfältet. Den ska matcha den URL som du ursprungligen angav.
1. Kontrollera att allt före `/content/dam.json` matchar det AEM-målvärde som konfigurerats i AEM Desktop.

### SSL-konfigurationsproblem {#ssl-configuration-issue}

De bibliotek som används av AEM-datorprogrammet för HTTP-kommunikation använder strikt SSL-kontroll. Ibland kan en anslutning fungera med en webbläsare, men misslyckas med att använda AEM-skrivbordsappen. Installera det saknade mellanliggande certifikatet i Apache om du vill konfigurera SSL korrekt. Se [Så här installerar du ett mellanliggande CA-certifikat i Apache](https://access.redhat.com/solutions/43575).

## Använda AEM Desktop med dispatcher {#using-aem-desktop-with-dispatcher}

AEM Desktop fungerar med AEM-distributioner bakom en dispatcher, som är standardkonfiguration och rekommenderas för AEM-servrar. AEM-utskickare framför AEM-redigeringsmiljöer är vanligtvis konfigurerade att hoppa över cachelagring av DAM-resurser. Det innebär att avsändare inte kan tillhandahålla ytterligare cachning från AEM Desktop-skärmen. Kontrollera att dispatcherns konfiguration är anpassad för att fungera för AEM Desktop. Mer information finns i [Ansluta till AEM bakom en dispatcher](install-configure-app-v1.md#connect-to-an-aem-instance-behind-a-dispatcher).

## Söker efter loggfiler {#checking-for-log-files}

Beroende på vilket operativsystem du har kan du hitta loggfilerna för AEM Desktop på följande platser:

* Windows: `%LocalAppData%\Adobe\AssetsCompanion\Logs`
* Mac: `~/Library/Logs/Adobe\ Experience\ Manager\ Desktop`