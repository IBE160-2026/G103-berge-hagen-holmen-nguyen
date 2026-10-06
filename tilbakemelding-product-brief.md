# Tilbakemelding på product brief

| | |
|---|---|
| **Gruppe** | G103 – G103-berge-hagen-holmen-nguyen |
| **Product brief** | `productbrief.md` (commit `644c63e`) |
| **Tilbakemelding fra** | Faglærer i IBE160 (utarbeidet med KI-støtte) |
| **Dato** | 2026-10-06 |

## Samlet vurdering

- **Bør revideres før dere går videre.** Rett punktene markert «Endre» før dere lager PRD og arkitektur.

**Det som er bra:**

1. Problemet er godt beskrevet og gjenkjennelig: reiseplanlegging er fordelt på Google Maps, værapper, flyselskaper, arrangementssider og egne budsjettverktøy. Spørsmålslisten («What clothes should I bring?», «How much will the trip approximately cost?») gjør behovet konkret.
2. Brukeropplevelsen er godt illustrert med eksempler: Barcelona-reisen med fotball, lokal mat og 700 €, oppfølgingsspørsmål som «Make day two cheaper», og en eksempelplan for dag 1. Det er lett å se for seg skjermbildene.
3. Dere har allerede flyttet mye ut av v1: booking, betaling, live flypriser, Foodora/Wolt og sosiale funksjoner. Begrunnelsen for å utsette den sosiale funksjonen (personvern, moderering, sikkerhet) viser god vurdering.

**De viktigste endringene:**

1. **V1 er fortsatt for stor.** «In Scope for Version 1» har tolv punkter: innlogging, lagrede reiser, KI-assistent med samtale, KI-generert reiseplan, aktivitetsforslag, vær, kart og ruter, kostnadsestimat, klesforslag, pakkeliste, redigerbar kalender og responsivt grensesnitt. Det er mange funksjonsområder og flere eksterne tjenester. Velg kjerneflyten «opprett reise → KI-generert dagsplan → rediger → lagre», med vær og pakkeliste, og flytt kart og ruter, samtalebasert omplanlegging og kostnadsestimat til senere trinn.
2. **Beskriv hvordan dere kontrollerer KI-ens forslag.** En språkmodell kan foreslå steder som ikke finnes, feil åpningstider og priser som ikke stemmer. Kostnadsestimatet kan bli ren gjetning. Bestem hva som kommer fra faktiske datakilder (vær fra et vær-API) og hva som er KI-forslag, og merk KI-forslagene tydelig i appen.
3. **Gjør suksesskriteriene testbare.** De funksjonelle kriteriene er en god start, men «within a few minutes», «respond quickly» og «store user trips reliably» må bli konkrete. Fjern «Development Approach» med Double Diamond fra briefen, eller koble det til BMAD-flyten dere faktisk skal bruke.

## Vanskelighetsgrad og gjennomførbarhet

### Vurdert vanskelighetsgrad

- **Middels**

**Sammenlignbart med:** 2) AI CV- og søknadsassistent (middels). Begge har flere sammenhengende funksjoner, en KI som lager et personlig resultat brukeren kan justere, og større krav til kvaliteten på KI-svarene. Med alle tolv punktene i v1 og kart- og ruteintegrasjon nærmer arbeidsmengden seg et vanskelig prosjekt.

**Begrunnelse:**

| Faktor | Nivå (lav / middels / høy) | Kommentar |
|---|---|---|
| Domenelogikk – hvor mange og hvor kompliserte regler og beregninger må stemme? | middels | Dagsplan med tidspunkter, budsjettsummering per kategori og regler som «regn gir innendørsaktiviteter». Summeringen er enkel, men grunnlaget for estimatene er usikkert. |
| Datamodell – antall entiteter og relasjoner mellom dem | middels | Bruker, reise, dag, aktivitet, kostnadspost, pakkeliste med avkryssing og eventuelt samtalehistorikk. |
| Brukere, roller og innlogging | middels | Én rolle, men innlogging med lagrede reiser og beskyttelse av kontoinformasjon. |
| KI-funksjonalitet i appen, f.eks. kall til språkmodell, prompts i koden og håndtering av usikre svar | høy | KI-en skal lage og endre en strukturert reiseplan via samtale, foreslå aktiviteter og estimere kostnader. Strukturert output som kan lagres og oppdateres er krevende. |
| Integrasjoner og eksterne tjenester, f.eks. API-er, betaling og e-post | høy | LLM, vær-API og kart/ruter. Hver tjeneste krever nøkler, feilhåndtering og testdata. |
| Sanntid, samtidighet eller flere brukere som påvirker hverandre | lav | Ingen deling mellom brukere i v1. |
| Filhåndtering, f.eks. opplasting, PDF-lesing og eksport | lav | Ikke nevnt. |
| Sikkerhet og personvern | middels | Kontoer, reisemål og datoer. Det er vanlig god praksis, men bør omtales. |

**Hva vanskelighetsgraden betyr for dere:**

- _Middels:_ Et godt balansert valg. Pass på at kjerneflyten blir ferdig og stabil før dere legger til mer. For dere betyr det en stabil flyt fra reiseopplysninger til lagret dagsplan før kart, samtale og kostnadsestimat.

### Gjennomførbarhet med BMAD og Claude Code

Dere skal planlegge med BMAD (product brief → PRD → arkitektur → epics og stories) og implementere med Claude Code. Vurderingen under tar hensyn til at det må være tid til hele denne flyten, og til testing, retting og README til slutt.

| Spørsmål | Vurdering (OK / risiko / stor risiko) | Kommentar |
|---|---|---|
| **Tid og omfang** – kan v1 realistisk bli ferdig og stabil i løpet av semesteret, med tid til flere iterasjoner? | risiko | Tolv punkter med tre eksterne tjenester er mye, også for fire personer. Med redusert v1 er det realistisk. |
| **BMAD-flyten** – er briefen konkret nok til at PRD, arkitektur og stories kan lages uten store hull, og blir det overkommelig mange stories? | risiko | Briefen er konkret om funksjoner, men det er uklart hva som er faktiske data og hva som er KI-forslag. Den beskriver Double Diamond i stedet for BMAD, og BMAD er ikke satt opp i repoet. |
| **Egnet for Claude Code** – bruker løsningen en vanlig, godt dokumentert teknologistakk som Claude Code håndterer godt, eller krever den nisjeteknologi, spesialmaskinvare eller mye manuell konfigurasjon? | OK | En vanlig webapp med database, LLM og vær-API passer godt. Kart og ruter krever mer oppsett. |
| **Kontroll på KI-ens arbeid** – kan gruppen selv avgjøre om koden gjør det riktige? Krever domenet kunnskap gruppen ikke har, f.eks. avanserte beregninger eller fagregler, så er det vanskelig å kvalitetssikre. | risiko | Dere kan vurdere om en plan virker fornuftig, men ikke enkelt kontrollere om steder, åpningstider og priser stemmer for vilkårlige reisemål. |
| **Testbarhet** – finnes det tydelige regler og forventede resultater som tester kan skrives mot? | risiko | Innlogging, lagring, redigering, pakkeliste og budsjettsummering kan testes. KI-planen må testes med faste reisemål og en sjekkliste. |
| **Kjørbar for sensor** – kan appen kjøres lokalt etter README, uten gruppens nøkler, betalte kontoer eller egen infrastruktur? | stor risiko | Tre eksterne tjenester med nøkler. Velg gratis tjenester uten nøkkel der det finnes (for eksempel åpne vær-API-er), og lag en demomodus med lagrede svar. |
| **Avhengigheter og kostnader** – krever løsningen betalte API-er, f.eks. språkmodeller, og finnes det en plan for kostnad, testmodus eller mock-data? | risiko | Ingen plan ennå. Kart- og rute-API-er kan kreve betalingskort selv i gratisnivået. Beskriv hvilke tjenester dere vil bruke og hvordan testing skjer uten kostnad. |

**Konklusjon om gjennomførbarhet:**

- **Gjennomførbart med justert omfang.** Se forslagene under.

**Forslag til justering av omfang eller vanskelighetsgrad:**

1. **V1:** innlogging, opprette og lagre reise, KI-generert dagsplan som kan redigeres manuelt, værvarsel for reisemålet og KI-generert pakkeliste med avkryssing. Merk tydelig hva som er KI-forslag.
2. **Trinn 2 og 3:** «regenerer én dag» og samtalebaserte endringer, deretter kostnadsestimat, kart og ruter, og arrangementer. Legg dem under «Possible Additional Features» i prioritert rekkefølge.

## Hvorfor product brief er viktig for mappen

Product brief er utgangspunktet for PRD, arkitektur, stories og til slutt koden. Del 1 av mappen vurderes blant annet på om sensor kan følge en sporbar vei fra plan til ferdig app. Den vurderes også på om appen gjør det dere har beskrevet, om den er testet, om den er godt designet, og om den kan kjøres etter README. Et uklart, for stort eller for lite brief gjør alt dette vanskeligere senere. Det er mye enklere å rette nå enn sent i semesteret.

## 1. Gjennomgang av briefens deler

| Del av brief | Status | Kommentar |
|---|---|---|
| Executive Summary – er det klart hva appen er, og hvilket problem den løser? | OK | Tydelig: én plattform der hele reisen kan planlegges, med en KI-assistent. |
| The Problem – er problemet konkret, med reelle situasjoner og brukere? | OK | Godt beskrevet med konkrete tjenester og spørsmål. |
| The Solution – beskriver løsningen brukeropplevelsen, ikke bare teknologi? | OK | Godt beskrevet med eksempler. «Core Features» og «Seasonal Travel Information» gjør likevel briefen lang og blander v1 med senere ideer. |
| What Makes This Different – er vurderingen ærlig og realistisk? | Juster | Fornuftige punkter, men vurder eksisterende KI-reiseplanleggere som allerede lager dagsplaner. Hva gjør dere bedre eller annerledes? |
| Who This Serves – er primærbrukerne tydelige, og vet vi hva de trenger? | Juster | Primærbrukeren omfatter studenter, unge voksne, par, familier og soloreisende. Velg én, for eksempel studenter på en kort byferie med stramt budsjett. |
| Success Criteria – kan kriteriene faktisk sjekkes eller testes? | Juster | De funksjonelle kriteriene er gode. «Within a few minutes» og «respond quickly» må tallfestes. |
| Scope – er det klart hva som er med i første versjon, og hva som ikke er det? | Endre | Tydelig struktur med In, Additional og Out, men v1 er for stor. Reduser til kjerneflyten. |
| Vision – henger visjonen sammen med resten uten å blåse opp omfanget? | OK | Visjonen er tydelig, og booking og sosiale funksjoner er klart plassert i fremtiden. |

## 2. Utgangspunkt for del 1 av mappen

Punktene følger kriteriene i sensorveiledningen for del 1. Vektene i parentes viser hvor mye hvert kriterium teller i del 1.

| Kriterium i del 1 | Hva briefen bør legge til rette for | Status | Kommentar |
|---|---|---|---|
| **1. Prosess og KI-styring** (30 %) | Brief som er presis nok til at PRD og stories kan bygges direkte på den, slik at krav kan spores fra brief til kode. | Juster | Briefen er lastet opp i én commit og beskriver Double Diamond i stedet for BMAD. Sett opp BMAD i repoet og la PRD og stories bygge på briefen. |
| **2. Funksjonalitet og omfang** (20 %) | Realistisk omfang for gruppen og semesteret: en tydelig kjerneflyt som kan bli ferdig og stabil, og nok innhold til å vise reell funksjonalitet. | Endre | For mange funksjonsområder i v1. Reduser som foreslått. |
| **3. Kvalitetssikring og testing** (15 %) | Suksesskriterier og funksjoner som er konkrete nok til å bli testtilfeller. | Juster | Lag faste testreiser (for eksempel Barcelona, 4 dager, regn dag 2) med forventet oppførsel, og test lagring og redigering automatisk. |
| **4. Design og brukeropplevelse** (10 %) | Tydelige brukere og brukssituasjoner som designet kan bygges rundt, gjerne med de viktigste skjermbildene eller flytene skissert. | OK | Dashbord, dagsplan og pakkeliste er godt beskrevet. Crazy 8-arbeidet er et godt utgangspunkt for skisser. Lagre skissene i repoet. |
| **5. Kodekvalitet og arkitektur** (10 %) | Teknologivalg som er begrunnet og ikke mer komplekse enn appen trenger. | Juster | Ingen teknologi er valgt. Bestem tidlig hvordan KI-planen lagres som strukturerte data, slik at den kan redigeres. |
| **6. README og kjørbarhet** (10 %) | Løsning som andre kan kjøre lokalt uten betalte kontoer, og uten tilgang til gruppens egne tjenester og nøkler. | Endre | Planlegg demomodus med lagrede KI- og værsvar, `.env.example` og testbruker med en ferdig reise. |
| **7. Ryddighet i repoet** (5 %) | En plan for hvor hemmeligheter, testdata og dokumentasjon skal ligge. | Juster | Flytt briefen til en planleggingsmappe, og planlegg hvor nøkler (ikke i Git) og lagrede testsvar skal ligge. |

## 3. Neste steg for gruppen

1. Reduser «In Scope for Version 1» til kjerneflyten, og flytt resten til «Possible Additional Features» i prioritert rekkefølge.
2. Skriv inn i briefen hvilke data som kommer fra faktiske kilder og hvilke som er KI-forslag, og hvordan dere vil sjekke KI-planene (faste testreiser med sjekkliste).
3. Sett opp BMAD i repoet, erstatt Double Diamond-avsnittet med en kort beskrivelse av arbeidsflyten, og lag PRD.

Oppdater product brief i repoet når dere har gjort endringene, slik at historikken viser hvordan planen utviklet seg. Det er en del av prosessen sensor ser etter.
