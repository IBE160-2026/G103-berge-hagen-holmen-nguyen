# Tilbakemelding på PRD

| | |
|---|---|
| **Gruppe** | G103 – G103-berge-hagen-holmen-nguyen |
| **PRD vurdert** | `docs/planning/prd.md` (status i frontmatter mangler; i dokumentet står «Version 1.0 – Final / Approved», sist endret 2026-11-04, commit 9102c2c) |
| **Dato** | 2026-11-12 |
| **Type** | Formativ tilbakemelding, ikke karakter |

## 1. Samlet inntrykk

PRD-en har en tydelig tese (KI-en skal vurdere om et sett aktiviteter faktisk lar seg kombinere, og aldri late som estimater er bekreftede fakta), stabile ID-er og en testplan som kan brukes direkte. Risikoen er omfanget og beslutningene: PRD-en er merket «Approved», men avgjørelsen om hva dere faktisk skal levere, hvilken teknologi dere bruker og hvilke eksterne tjenester som er med, er fortsatt åpen. Neste fase (UX, arkitektur, epics) trenger akkurat de svarene.

## 2. Dette fungerer godt

1. **Ærlighet om hva KI-en vet.** BR-02 («A place appearing in search or on a map is not evidence of bookability»), BR-03 og tilstandsmodellen i §10 (`Confirmed` kun når leverandøren har bekreftet) gjør «ikke finn på» til konkrete regler som kan testes. Dette er PRD-ens sterkeste del.
2. **FR-ene har observerbare akseptkriterier, og testplanen peker tilbake.** Hver FR har en kolonne med forventet utfall, og T-001–T-014 i §15 er koblet til FR-ID-er. FR-014 («a reason and one or more reasonable changes, not a fabricated feasible plan») er et eksempel på et krav som lett blir en test.
3. **Fasedelingen A–D i §13.** Trinn A («Free-text request becomes a structured and editable travel itinerary…») er en fornuftig kjerneflyt, og dere sier åpent at ingen integrasjoner er verifisert (§12, §22).

## 3. Oversikt per dimensjon

| Dimensjon | Vurdering | Kort begrunnelse |
|---|---|---|
| Beslutningsklarhet | svak | «Approved», men D-01–D-08 er åpne og scope-tabellen i §13 står på «Pending» på alle rader. |
| Substans | god | Forretningsregler og reservasjonstilstander er reelle. Brukersegmentene er «inferred», og NFR-012 har ingen tall. |
| Strategisk sammenheng | god | Tesen om gjennomførbarhet og ærlig booking bærer funksjonene. Men P1/P2 trekker mot en bredere plattform enn tesen krever. |
| Testbarhet | god | Observerbare kriterier og en testplan. Flere kriterier bruker fortsatt myke ord («obvious», «reasonable»). |
| Scope og avgrensning | svak | Ingen egen non-goals-seksjon eller MVP in/out. «Not a reduction» (§1) betyr at hele visjonen fortsatt ligger i dokumentet. |
| Brukbarhet for neste fase | god | FR/EP/T-ID-er er sammenhengende. Mangler glossar, navngitte brukerreiser og suksessmål. |
| Formtilpasning | svak | Mye prosess- og vurderingsstoff (§18, §19, §21) i et produktkrav, men ingen brukerreiser med hovedperson. |

## 4. Viktigste forbedringer

### 4.1 Låse scope: «Approved» stemmer ikke med de åpne beslutningene
- **Alvorlighet:** høy
- **Hvor:** forsiden («Status: Approved for project planning»), §13 scope-tabell («Final group decision: **Pending**»), §20.1 (D-01–D-08 «Open», «next planning meeting: 5 November 2026»)
- **Problem og hvorfor det betyr noe:** Arkitektur og epics må vite hva som er med. Nå er selv «Natural-language itinerary creation» satt til Pending. Møtedatoen 5. november er passert uten at statusen er oppdatert.
- **Forslag:** Fyll ut tabellen nå. Eksempel: «Committed: FR-001–004, FR-007, FR-012–014, FR-017–018, FR-021, FR-024, FR-030–031 (trinn A). Conditional: FR-008, FR-011, FR-020 (ett vær-API). Post-course: FR-009, FR-025–029.» Sett statusen til `draft` til dette er gjort, og legg til `status` og `updated` i frontmatter.

### 4.2 Scopet vokser i stedet for å krympe
- **Alvorlighet:** høy
- **Hvor:** §1 («a phased implementation plan, **not a reduction** of the complete TripWeaver AI product vision»), §8.6 (FR-025–029), §13 trinn C
- **Problem og hvorfor det betyr noe:** Tilbakemeldingen på briefen ba om å kutte til én kjerneflyt og flytte booking ut. PRD-en gjør koordinert booking mellom leverandører til produktets «central differentiator» (D-05) og har 32 FR-er, 12 NFR-er og åtte epics. Med fire personer og ett semester vil trinn B–D trolig ikke bli ferdige.
- **Forslag:** Legg til en kort §5 «Non-Goals»: «Vi sender ikke bookinger til leverandører i kurset. Vi viser kun håndoverlenke og status `Action required`.» Flytt FR-009 og FR-025–029 til «Post-course roadmap» i stedet for å beholde dem som P1 i samme tabell.

### 4.3 KI-kontroll, kostnad og kjørbarhet uten nøkler er ikke et krav
- **Alvorlighet:** høy
- **Hvor:** §9, §11 (NFR-007, NFR-011), §12 (R-07), §15 (T-001)
- **Problem og hvorfor det betyr noe:** §9 beskriver kontrakten for KI-output godt, men ikke hva som skjer når modellen returnerer ugyldig struktur, hvordan LLM-kostnad begrenses, eller hvordan testene kan kjøres uten at modellen gir ulike svar hver gang. T-001 («Correctly structured dates/duration») er ikke repeterbar mot en levende modell. Briefen ba om demomodus; PRD-en nevner bare «labelled demo fixtures» i R-07.
- **Forslag:** Nytt krav: «**FR-033 / NFR:** Appen kan kjøres i demomodus uten API-nøkler. Da brukes lagrede svar for den faste testreisen (5 dager Italia, 2 000 €), og skjermen viser «Demo – ikke live data». Ugyldig KI-output (mangler `days[]` eller gyldig dato) gir feilmelding og ingen lagret reise.»

### 4.4 Gjør de myke kriteriene målbare
- **Alvorlighet:** medium
- **Hvor:** FR-013 («Detect obvious itinerary conflicts»), FR-030 («discoverable without interpreting raw AI output»), NFR-012 («numeric performance thresholds require a baseline»), ingen suksessmål
- **Problem og hvorfor det betyr noe:** «Obvious» og «discoverable» kan ikke bli testtilfeller, og uten suksessmål vet dere ikke når trinn A er bra nok.
- **Forslag:** FR-013: «Gitt to faste aktiviteter 10:00–12:00 og 11:00–13:00 samme dag, viser systemet en konfliktmelding som navngir begge aktivitetene, og ingen av tidene endres.» Legg til to mål: «SM-1: for de tre faste testreisene har ≥ 90 % av eksplisitte hard constraints (dato, budsjett) riktig merkede verdier. SM-2: ingen status `Confirmed` uten leverandørbekreftelse i testkjøringene.» NFR-012 kan få en foreløpig grense, for eksempel «første plan vises innen 30 s eller fremdriftsindikator vises».

### 4.5 Form: flytt prosess ut, legg brukerreiser og glossar inn
- **Alvorlighet:** medium
- **Hvor:** §18–19 og §21 (vektene i sensorveiledningen, DoR/DoD, endringskontroll), §6 («Main User Journey» uten hovedperson)
- **Problem og hvorfor det betyr noe:** Mye av dokumentet handler om vurderingen av prosjektet i stedet for produktet (§19: «30 % … 20 % …»). Det gjør PRD-en lang (ca. 6 500 ord) og skjuler kravene. Samtidig mangler det UX og stories trenger mest: en navngitt bruker i en konkret situasjon.
- **Forslag:** Flytt §18, §19 og §21 til `docs/process/`. Gjør §5 til UJ-1: «Marte, 24, har 2 000 € og fem dager. Hun skriver inn ønskene sine, ser at bowling og fjelltur havner samme dag, og får forslag til å flytte bowlingen.» Legg til et glossar med `Trip`, `Itinerary item`, `Reservation`, `Booking status`.

## 5. Mekaniske funn

- Frontmatter mangler (`status`, `updated`, `title`). Status står kun i tekst.
- Ingen glossar. «Booking» og «reservation» brukes om hverandre (FR-024 «booking requirements», §10 «Reservation State Model»), og «plan», «trip» og «itinerary» overlapper.
- FR-001–032, EP-01–08, T-001–014 og US-001–003 er sammenhengende, og henvisningene løser seg. Ingen UJ- eller SM-ID-er finnes.
- Avhengighet: FR-017 (P0, revisjoner) bygger på FR-005 (P1, bevare preferanser), som ikke er med i trinn A.
- Ingen `[ASSUMPTION]`-merker. Antakelser står som prosa i §12 og §22.

## 6. Før dere går videre

**Må avklares før UX, arkitektur og epics:** scope-tabellen i §13 (D-02), booking eller håndoverlenke (D-05), kontoer og lagring (D-06), LLM, kart og vær (D-04), og demomodus for sensor.

**Kan vente:** språk og valuta (FR-006), flere alternative planer (FR-016), målbare ytelsestall (D-08) og kartvisning (FR-032).

**Oppfølging av briefen:** *delvis.* Dere har laget en eksplisitt skille mellom fakta og KI-forslag (BR-03), testbare kriterier og BMAD-baserte ID-er. Men v1 er ikke redusert (booking er blitt viktigere, ikke utsatt), demomodus og konkrete tall mangler, og beslutningen om innlogging er ikke tatt. Tilbakemeldingen gjaldt `productbrief.md`, mens PRD-en bygger på `productbrief2.md`. Jeg har ikke vurdert endringene mellom dem.

## 7. Refleksjonsspørsmål

1. §14 og §8 er svært omfattende og formelle. Hvilke deler av teksten har dere selv gått gjennom og prøvd å forsvare, og hvilke godtok dere fra KI-utkastet uten å spørre om dere faktisk kan levere dem?
2. BR-02 og BR-05 er gode regler. Hvordan vil dere sjekke at KI-en i praksis ikke finner opp en bekreftelse eller åpningstid, og hva er den første testen dere kjører mot det?

_Vurdert mot kvalitetsrubrikken i bmad-prd. Dette er veiledning, ikke sensur._
