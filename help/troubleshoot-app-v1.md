---
title: Felsök skrivbordsappens version 1.10.
description: Felsök [!DNL Adobe Experience Manager] datorprogramversion 1.10 för att lösa enstaka problem i samband med installation, uppgradering och konfiguration.
exl-id: 1e1409c2-bf5e-4e2d-a5aa-3dd74166862c
source-git-commit: 32aff5d66f2cb67ab4bb440d7ace747a5cf1dd26
workflow-type: tm+mt
source-wordcount: '3350'
ht-degree: 0%

---

# Felsök [!DNL Adobe Experience Manager]-datorprogrammet v1.x {#troubleshoot-aem-desktop-app}

Felsök AEM datorprogram för att lösa tillfälliga problem som rör installation, uppgradering, konfiguration och så vidare.

[!DNL Adobe Experience Manager] skrivbordsappen innehåller verktyg som hjälper dig att mappa AEM Assets-databasen som en nätverksresurs på skrivbordet (SMB-resurs på Mac OS). Nätverksresursen är en operativsystemsteknik som gör att fjärrkällor kan hanteras som om de var en del av en dators lokala filsystem. När det gäller skrivbordsprogram är AEM DAM-databasstrukturen (Digital Asset Management) avsedd som fjärrfilskälla. I följande diagram beskrivs skrivbordsappens topologi:

![skrivbordsappsdiagram](assets/aem-desktopapp-architecture.png)

Med den här arkitekturen fångar skrivbordsappen upp filsystemanrop (öppna, stänga, läsa, skriva osv.) till den monterade nätverksresursen och översätter dem till interna AEM HTTP-anrop till AEM. Filerna cachelagras lokalt. Mer information finns i [Använd AEM datorprogram v1.x](use-app-v1.md).

## Översikt över komponenten AEM datorprogram {#desktop-app-component-overview}

datorprogrammet innehåller följande komponenter:

* **Skrivbordsprogrammet**: Programmet monterar eller avmonterar DAM som ett fjärrfilsystem och översätter filsystemanrop mellan den lokalt monterade nätverksresursen och den AEM fjärrinstans som det ansluter till.
* **WebDAV/SMB-klient** för operativsystem: Hanterar kommunikation mellan Utforskaren/Finder i Windows och skrivbordsprogrammet. Om en fil hämtas, skapas, ändras, tas bort, flyttas eller kopieras, kommunicerar operativsystemets (OS) WebDAV/SMB-klient den här åtgärden med skrivbordsprogrammet. Efter att ha tagit emot kommunikationen översätter skrivbordsappen det till inbyggda AEM fjärr-API-anrop. Om en användare till exempel skapar en fil i den monterade katalogen, initierar WebDAV/SMB-klienten en begäran som skrivbordsappen översätter till en HTTP-begäran som skapar filen i DAM. WebDAV/SMB-klienten är en inbyggd komponent i operativsystemet. Den är inte på något sätt kopplad till datorprogrammet, AEM eller Adobe.
* **Adobe Experience Manager-instans**: Ger åtkomst till resurser som lagras i AEM Assets DAM-databasen. Dessutom utför programmet åtgärder som begärts av skrivbordsappen för de lokala skrivbordsprogrammen som interagerar med den monterade nätverksresursen. AEM ska köra AEM version 6.1 eller senare. AEM instanser som kör tidigare AEM kan kräva extra funktionspaket och snabbkorrigeringar för att bli fullt fungerande.

## Användningsexempel för AEM datorprogram {#intended-use-cases-for-aem-desktop-app}

AEM datorprogram använder nätverksdelningstekniken för att mappa en AEM till ett lokalt skrivbord. Den är dock inte avsedd som ersättning för en nätverksresurs som innehåller resurser, där användarna utför digitala resurshanteringsåtgärder direkt från sin lokala dator. Det kan vara att flytta eller kopiera flera filer eller dra stora mappstrukturer till AEM Assets-nätverksresursen direkt i Finder/Utforskaren.

AEM är ett bekvämt sätt att komma åt (öppna) och redigera (spara) DAM-resurser mellan AEM Assets Touch-gränssnittet och det lokala skrivbordet. Den länkar resurser på AEM Assets-servern till skrivbordsbaserade arbetsflöden.

Följande exempel visar hur AEM Desktop ska användas:

* En användare loggar in på AEM och använder webbgränssnittet för att hitta en resurs.
* Med skrivbordsfunktionerna i AEM webbgränssnitt kan användaren antingen öppna, visa eller redigera resursen på skrivbordet efter behov.
* AEM Desktop öppnar resursen i standardredigeraren för resursens filtyp.
* Användaren gör önskade ändringar av resursen.
* När en fil har ändrats kan användaren visa filens synkroniseringsstatus i AEM skrivbordets statusfönster för bakgrundssynkronisering.
* Med hjälp av snabbmenyn AEM Desktop checkar användaren in/ut resursen eller återgår till DAM-användargränssnittet.
* När du är klar med ändringarna i filen återgår användaren till AEM webbgränssnitt

Detta är inte det enda användningsexemplet. Det visar dock hur AEM Desktop är en praktisk metod för att få åtkomst till och redigera resurser lokalt. Du uppmanas att använda DAM-webbgränssnittet så mycket som möjligt eftersom det ger en bättre upplevelse. Det ger Adobe större flexibilitet för att uppfylla kundernas krav.

## Begränsningar {#limitations}

Nätverksresursen WebDAV/SMB1 gör det enkelt att arbeta med filer i Utforskaren/Finder-fönstret. Utforskaren/Finder och AEM kommunicera via en nätverksanslutning som har vissa begränsningar. Den tid det tar att kopiera en fil på 1 GB till den monterade WebDAV/SMB-katalogen är ungefär densamma som den tid som krävs för att överföra en fil på 1 GB till en webbplats med en webbläsare. I det tidigare fallet kan varaktigheten vara längre på grund av ineffektivitet i WebDAV/SMB-protokollet och operativsystemets WebDAV/SMB-klienter (särskilt Mac OS X).

Det finns begränsningar för de typer av uppgifter som kan utföras från en monterad katalog. I allmänhet kan det vara svårt att arbeta med stora filer, särskilt när det gäller nätverksanslutningar med låg/hög fördröjning/låg bandbredd, särskilt när du redigerar stora filer.

Adobe rekommenderar att du utför vissa falltester innan du implementerar vissa typer av filer på en klient, så att de kan redigeras på plats från den monterade katalogen.

AEM Desktop lämpar sig inte för intensiv bearbetning av filsystem, inklusive, men inte begränsat till:

* Flytta eller kopiera filer och kataloger
* Lägga till många resurser i AEM
* Söka efter och öppna filer i filsystemet, utom för att bläddra bland mappar
* Komprimera eller dekomprimera filarkiv

På grund av begränsningar i operativsystemet har Windows en filstorleksbegränsning på 4 294 967 295 byte (cirka 4,29 GB). Det beror på en registerinställning som definierar hur stor en fil på en nätverksresurs kan vara. Registerinställningens värde är ett DWORD med en maximal storlek som är lika med det refererade talet.

[!DNL Experience Manager] skrivbordsappen har inget konfigurerbart timeout-värde som kopplar från anslutningen mellan  [!DNL Experience Manager] servern och skrivbordsappen efter ett fast tidsintervall. När du överför stora resurser, och anslutningen får timeout efter en stund, försöker programmet överföra resursen några gånger genom att öka tidsgränsen för överföring. Det finns inget rekommenderat sätt att ändra standardinställningarna för timeout.

## Cachelagring och kommunikation med AEM {#caching-and-communication-with-aem}

AEM datorprogram har funktioner för intern cachelagring och bakgrundsuppladdning för att förbättra slutanvändarens upplevelse. När du sparar en stor fil sparas den först lokalt så att du kan fortsätta arbeta. Efter en stund (för närvarande 30 sekunder) skickas filen sedan till AEM i bakgrunden.

Till skillnad från Creative Cloud Desktop eller andra filsynkroniseringslösningar, som Microsoft One Drive, är AEM inte en fullständig klient för synkronisering av stationära datorer. Orsaken till detta är att det ger tillgång till hela AEM Assets-databasen, som kan vara mycket stor (hundratals gigabyte eller terabyte) för en fullständig synkronisering.

Cachelagring ger möjlighet att begränsa nätverks-/lagringskostnaderna till endast en delmängd av resurserna som är relevanta för användaren.

>[!CAUTION]
>
>Adobe rekommenderar att du stänger av genereringen av miniatyrbilder för att göra bläddringen snabbare. Om du aktiverar förhandsvisning av ikoner cachelagras de digitala resurserna när du navigerar genom den monterade mappen. Programmet hämtar också resurser som användaren kanske inte bryr sig om, vilket lägger till belastning på servern, förbrukar användarens bandbredd och använder mer av användarens diskutrymme.

Så här utför AEM cachelagring:

* När du öppnar en mapp i Finder och miniatyrbilder/förhandsgranskningar av filer visas, eller när du öppnar en fil i ett program, cachelagras filens binärfil i skrivbordsprogrammet.
* När du lagrar filer via Finder eller andra skrivbordsprogram lagras filen lokalt först (cachelagrat) och operativsystemet meddelas. Filen köas sedan för överföring till servern i bakgrunden och överförs sedan över nätverket. Om ett nätverksfel inträffar försöker skrivbordsappen överföra hela filen igen i högst tre gånger. Om överföringen misslyckas efter tre försök markeras filen som en fil i konflikt och statusen visas i fönstret Status för bakgrundskööverföring. försöker inte uppdatera filen längre. Användaren bör uppdatera filen och överföra den igen när anslutningen har återställts

Alla åtgärder cachelagras inte lokalt. Följande överförs direkt till AEM Server utan lokal cachelagring:

* Åtgärder för mappar, till exempel skapa, ta bort och så vidare
* Mappöverföringsfunktionen som introducerades i version 1.4 överför en lokal mapphierarki utan att cachelagra filerna lokalt

## Individuella operationer {#individual-operations}

När du felsöker suboptimerade prestanda för enskilda användare ska du först granska [appbegränsningarna](#limitations). De följande avsnitten innehåller förslag på hur du kan förbättra prestandan för de enskilda användarna.

## Bandbreddsrekommendationer {#bandwidth-recommendations}

Den bandbredd som är tillgänglig för en enskild användare spelar en avgörande roll för WebDAV/SMB-klientens prestanda.

Adobe rekommenderar att en enskild användares överföringshastighet är nästan 10 Mbit/s. För trådlösa anslutningar delas bandbredd ofta mellan flera användare. Om flera användare samtidigt utför uppgifter som förbrukar nätverksbandbredd kan prestandan försämras ytterligare. Undvik sådana problem genom att använda en kabelanslutning.

## Windows-specifika konfigurationer {#windows-specific-configurations}

Om du använder Experience Manager i Windows kan du konfigurera Windows för att förbättra WebDAV-klientens prestanda. Mer information finns på [https://support.microsoft.com/en-us/kb/2445570](https://support.microsoft.com/en-us/kb/2445570).

I Windows 7 kan prestandan för WebDAV förbättras om IE-inställningarna ändras. Mer information finns i [Åtgärda långsamma WebDAV-prestanda i Windows 7](https://oddballupdate.com/2009/12/fix-slow-webdav-performance-in-windows-7/).

<!-- TBD: The above performance tip is for Windows 7 which is not supported by the app anymore. Remove it later.
-->

## Samtidiga åtgärder {#concurrent-operations}

När du interagerar med en fil lokalt kontrollerar AEM om det finns en senare version av filen i AEM. Om det finns en ny version hämtar programmet en ny kopia av filen till det lokala cacheminnet. AEM Skrivbordet skriver dock inte över en lokalt cachelagrad fil om den har ändrats. Den här funktionen förhindrar att ditt arbete skrivs över av misstag.

När samma fil ändras både lokalt och i AEM skrivs versionen över i AEM av den lokalt ändrade versionen. I det här fallet är den tidigare versionen tillgänglig på resursens tidslinje. Du kan verifiera båda versionerna och lösa eventuella konflikter.

Om en lokal fil inte är kompatibel med den version som finns på servern visas ett meddelande om konflikten i dialogrutan för bakgrundsstatus. Lös problemet genom att öppna filen som är i konflikt och spara den. Om du sparar filen måste AEM Skrivbord synkronisera dina senaste lokala ändringar till AEM. Du kan visa tidigare versioner av resursen på tidslinjen och lösa eventuella konflikter.

Du bör ta hänsyn till ytterligare faktorer när flera användare försöker arbeta i separata monterade kataloger som har samma AEM som mål. Bland annat är följande faktorer viktiga:

* Mängden bandbredd som är tillgänglig i användarens ursprungliga nätverk
* Nätverkskonfiguration, t.ex. brandväggar eller proxies, för det ursprungliga nätverket
* Tillgänglig bandbredd i AEM nätverk
* Om det finns en dispatcher före AEM
* Aktuell inläsning på AEM

## Ytterligare AEM {#additional-aem-configurations}

Om WebDAV-/SMB-prestanda försämras drastiskt när flera användare arbetar samtidigt kan du konfigurera några saker i AEM, vilket kan förbättra prestandan.

## Uppdatera resursövergående arbetsflöden {#update-asset-transient-workflows}

Du kan förbättra prestandan AEM sidan genom att aktivera tillfälliga arbetsflöden för DAM Update Asset-arbetsflödet. Om du aktiverar tillfälliga arbetsflöden minskas den processorkraft som krävs för att uppdatera resurser när de skapas eller ändras i AEM.

1. Navigera till `/miscadmin` i Experience Manager-instansen (`https://[aem_server]:[port]/miscadmin`).
1. Expandera **Verktyg** > **Arbetsflöde** > **Modeller** > **dam** i navigeringsträdet.
1. Dubbelklicka på **DAM Update Asset**.
1. Gå till fliken **Sida** på den flytande verktygspanelen och klicka sedan på **Sidegenskaper**.
1. Markera kryssrutan **Transient Workflow** och klicka på **OK**.

### Justera kön för transient Granite-arbetsflöde {#adjust-granite-transient-workflow-queue}

En annan metod för att förbättra AEM prestanda är att konfigurera värdet för det maximala antalet parallella jobb för jobbet Beviljit Transient Workflow Queue. Det rekommenderade värdet är ungefär hälften av antalet processorer som är tillgängliga på servern. Så här justerar du värdet:

1. Navigera till `/system/console/configMgr` i den AEM instansen som ska konfigureras (till exempel `https://[aem_server]:[port]/system/console/configMgr`).
1. Sök efter `QueueConfiguration` och klicka för att öppna varje jobb tills du hittar jobbet **Bevilja tillfällig arbetsflödeskö** och klicka på **Redigera**.
1. Ändra `Maximum Parallel Jobs`-värdet och klicka på **Spara**.

## AWS-konfiguration {#aws-configuration}

På grund av begränsningar i nätverkets bandbredd kan WebDAV/SMB-prestanda försämras när flera användare arbetar samtidigt. Adobe rekommenderar att storleken på AWS-instansen ökas för en AEM som körs på AWS för att förbättra prestandan för WebDAV/SMB.

Den här åtgärden ökar specifikt mängden nätverksbandbredd som är tillgänglig för servern. Här är några detaljer:

* Den mängd nätverksbandbredd som är dedikerad till en AWS-instans ökar när instansens storlek ökar. Mer information om hur mycket bandbredd som är tillgänglig för varje instansstorlek finns i [AWS-dokumentation](https://aws.amazon.com/ec2/instance-types/).
* Vid felsökning för en stor klient konfigurerade Adobe storleken på sin AEM-instans till c4.8xlarge, främst för den dedikerade bandbredden på 4 000 Mbit/s som den erbjuder.
* Om det ligger en dispatcher framför AEM ska den ha rätt storlek. Om AEM innehåller 4000 Mbit/s men dispatchern bara tillhandahåller 500 Mbit/s är den effektiva bandbredden bara 500 Mbit/s. Det beror på att avsändaren skapar en flaskhals i nätverket.

## Utcheckade filbegränsningar {#checked-out-file-limitations}

Det finns några kända begränsningar för hur du kan interagera med utcheckade filer via Utforskaren/Finder. Om en fil är utcheckad bör den vara skrivskyddad för alla förutom den användare som har filen utcheckad. Implementeringen av WebDAV/SMB1-protokollet i AEM verkställer den här regeln. Operativsystemets WebDAV-/SMB-klienter samverkar dock ofta inte på ett bra sätt med utcheckade filer. Nedan beskrivs några uddpunkter.

### Allmänt {#general}

När du skriver till en utcheckad fil används låset bara i AEM WebDAV-implementering. Därför används låset bara av klienter som använder WebDAV, till exempel skrivbordsprogram. Låset används inte via AEM webbgränssnitt. I AEM visas bara en låsikon i kortvyn för resurser som är utcheckade. Ikonen är kosmetisk och har ingen effekt på AEM beteende.

I allmänhet fungerar inte WebDAV-klienterna som förväntat. Det kan finnas ytterligare problem. Att uppdatera eller kontrollera mediefilen i AEM är dock ett bra sätt att verifiera att en mediefil inte ändras. Detta beteende är typiskt för operativsystemets WebDAV-klienter, som inte styrs av Adobe.

### Windows {#windows}

Det verkar som om det går att ta bort en fil eftersom den försvinner från filutforskaren i Windows. Om du uppdaterar katalogen och checkar in AEM resurser visas dock att filen fortfarande finns. Dessutom verkar redigeringen av filer lyckas (inga varningsmeddelanden eller felmeddelanden visas). Om du öppnar filen igen eller checkar in AEM resurser igen visas emellertid att filen är oförändrad.

#### Mac OS X {#mac-os-x}

Om du ersätter en fil visas ingen varning eller ett fel, men om du markerar resursen i AEM visas att den inte ändras. Uppdatera eller kontrollera resursen i AEM för att bekräfta att den inte ändras.

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

AEM försöker synkronisera en given fil tre gånger. Om filen inte kan synkroniseras efter det tredje försöket tolkar AEM Desktop filen som i konflikt och meddelar dig via statusfönstret för bakgrundsuppladdningen. Ett konfliktläge indikerar att dina senaste ändringar fortfarande är tillgängliga lokalt, men de synkroniseras inte tillbaka till AEM. AEM försöker inte längre synkronisera.

Det enklaste sättet att åtgärda detta är att öppna filen som är i konflikt och spara den igen. Det tvingar AEM att försöka synkronisera ytterligare tre gånger. Om filen fortfarande inte kan synkroniseras finns mer hjälp i avsnitten nedan.

## Rensar AEM Skrivbordscache {#clearing-aem-desktop-cache}

Att radera AEM Skrivbordscache är en preliminär felsökningsåtgärd som kan lösa flera AEM problem med skrivbordet.

Du kan rensa cacheminnet genom att ta bort programmets cachekatalog på följande platser.
I Windows: `%LocalAppData%\Adobe\AssetsCompanion\Cache\`

I Mac: `~/Library/Group/Containers/group.com.adobe.aem.desktop/cache/`

Platsen kan dock ändras beroende på AEM datorns konfigurerade AEM. Värdet är en kodad version av mål-URL:en. Om programmet till exempel har `http://localhost:4502` som mål är katalognamnet `http%3A%2F%2Flocalhost%3A4502%2F`.

Ta bort katalogen &lt;Encoded AEM Endpoint> om du vill rensa cacheminnet.

>[!NOTE]
>
>Om du rensar AEM Skrivbordscache går lokala filändringar som inte har synkroniserats till AEM förlorade.

>[!NOTE]
>
>Från och med AEM version 1.5 av skrivbordsappen finns det ett alternativ i användargränssnittet för skrivbordsappen att rensa cacheminnet.

## Söker efter den AEM datorversionen {#finding-the-aem-desktop-version}

Du använder samma procedur för att kontrollera vilken version AEM har för både Windows och Mac OS.

Klicka på ikonen AEM Skrivbord och välj sedan **Om**. Versionsnumret visas på skärmen.

## Uppgraderar AEM på macOS {#upgrading-aem-desktop-app-on-macos}

Ibland kan problem uppstå när du uppgraderar AEM datorprogram på macOS. Detta beror på att det inte går att läsa in nya versioner av AEM som de är i AEM för datorprogrammet. Följande mappar och filer kan tas bort manuellt för att åtgärda problemet.

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

## Felsökning AEM anslutningsproblem med stationära datorer {#troubleshooting-aem-desktop-connection-issues}

### Omdirigeringsproblem för SAML {#saml-redirect-issue}

Den vanligaste orsaken till problem med AEM Skrivbord som ansluter till en SAML-AEM (SSO-enabled) är att SAML-processen inte dirigerar tillbaka till den ursprungligen begärda sökvägen. Alternativt kan anslutningen omdirigeras till en värd som inte konfigurerats i AEM skrivbord. Så här verifierar du inloggningsprocessen:

1. Öppna en webbläsare.
1. Ange URL:en `/content/dam.json` i adressfältet.
1. Ersätt URL:en med AEM, till exempel `https://localhost:4502/content/dam.json`.
1. Logga in på AEM.
1. När du har loggat in kontrollerar du webbläsarens aktuella adress i adressfältet. Den ska matcha den URL som du ursprungligen angav.
1. Kontrollera att allt före `/content/dam.json` matchar AEM som konfigurerats i AEM Desktop.

### SSL-konfigurationsproblem {#ssl-configuration-issue}

De bibliotek som AEM datorprogrammet använder för HTTP-kommunikation använder strikt SSL-kontroll. Ibland kan en anslutning fungera med en webbläsare, men misslyckas AEM skrivbordsappen. Installera det saknade mellanliggande certifikatet i Apache om du vill konfigurera SSL korrekt. Se [Installera ett mellanliggande CA-certifikat i Apache](https://access.redhat.com/solutions/43575).

## Använda AEM Desktop med dispatcher {#using-aem-desktop-with-dispatcher}

AEM Desktop fungerar med AEM driftsättningar bakom en dispatcher, vilket är en standardkonfiguration och rekommenderas för AEM servrar. AEM som skickas framför AEM redigeringsmiljöer är vanligtvis konfigurerade att hoppa över cachelagring av DAM-resurser. Det innebär att avsändare inte kan tillhandahålla ytterligare cachning från AEM Skrivbord. Kontrollera att dispatcherkonfigurationen är anpassad för att fungera för AEM skrivbord. Mer information finns i [Ansluta till AEM bakom en dispatcher](install-configure-app-v1.md#connect-to-an-aem-instance-behind-a-dispatcher).

## Söker efter loggfiler {#checking-for-log-files}

Beroende på vilket operativsystem du har kan du hitta loggfilerna för AEM skrivbord på följande platser:

* Windows: `%LocalAppData%\Adobe\AssetsCompanion\Logs`
* Mac: `~/Library/Logs/Adobe\ Experience\ Manager\ Desktop`
