# Stage Two-plugin voor Claude Code (stack-light)

Je hebt een app die Stage Two voor je heeft gebouwd, of je gaat er zelf een maken, en je
werkt eraan met Claude Code. Deze versie van de plugin is voor **lichte apps**: elke app
draait als één geheel bij **Cloudflare**, met zijn eigen servercode, een eigen database en
een eigen plek voor bestanden. Er komt geen ander systeem bij. Stage Two vertelt je bij de
start welke plugin bij jouw bedrijf hoort.
Deze plugin zorgt dat Claude Code daarbij de werkwijze van Stage Two kent en bewaakt, en
dat je zelf verbeteringen aan die werkwijze kunt ophalen. Ook als Stage Two er niet meer
bij is.

Je hoeft geen programmeur te zijn om dit te gebruiken. De eerste keer loopt Stage Two het
met je door; daarna merk je er weinig van, behalve dat je assistent af en toe iets uitlegt
en je zelf nieuwe apps kunt beginnen.

## Wat de plugin doet

Vier commando's, en een bewaker op de achtergrond:

- **Een begin op een nieuwe computer.** Typ `/stack-light:installatie` en je assistent kijkt wat
  er op je computer ontbreekt, installeert het, helpt je inloggen bij GitHub en vraagt
  daarna wat je wilt doen. Zie hieronder.
- **Zelf een nieuwe app beginnen.** Typ `/stack-light:nieuwe-app`. Je assistent denkt eerst
  met je mee (wat moet de app doen en voor wie) en maakt hem daarna aan uit de nieuwste
  lichte Stage Two-template, onder het GitHub-account van je bedrijf. De beheer-repo van
  je bedrijf zet hem daarna online, achter de deur. Zie hieronder.
- **Verder werken aan een app.** `/stack-light:verder-werken` is de vaste route voor elke
  wijziging, ook aan de database en aan de servercode. Je hoeft het commando niet te
  typen: gewoon vragen wat je wilt werkt ook. De route staat ook in je app beschreven
  (`docs/routes/`). Na de merge gaat alles in één keer live: schermen, servercode en
  databasewijzigingen.
- **Meekijken terwijl je bouwt.** In de Claude-app start je assistent de app vanzelf op
  je eigen computer en laat hij hem zien in het venster naast het gesprek (de preview).
  Hij kijkt daar zelf ook mee om zijn werk te controleren. De preview gebruikt een
  database op je eigen computer, nooit de echte gegevens. Opleveren gaat altijd via een
  pull request.
- **Een bewaker.** Een deel van de bestanden in je app is niet van jou maar van de
  gedeelde werkwijze: de automatische controles, de afspraken, de routes. Vraag je je
  assistent om daar iets in te wijzigen, dan houdt de plugin dat tegen en legt hij uit
  waarom. Zonder plugin houdt de controle op GitHub het alsnog tegen; met plugin hoor je
  het meteen.
- **Een melding als er een nieuwere werkwijze is.** Open je je app en heeft Stage Two de
  gedeelde werkwijze verbeterd, dan zegt je assistent dat één keer, hooguit één keer per
  dag. Meer niet: hij doet niets zonder dat jij het vraagt.
- **Alles updaten met één commando.** Typ `/stack-light:updaten`, en je assistent werkt alles
  bij zoals een update van je computer: de plugin, de programma's op je computer, je app
  naar de nieuwste werkwijze en de pakketten van je app. Wat je app verandert komt als
  voorstel (een pull request) dat jij bekijkt en goedkeurt. Daarna vraagt hij of je
  andere apps ook mee moeten. Je eigen werk raakt hij nooit aan.

Er komt geen wachtwoord, sleutel of computer van Stage Two aan te pas. Alles loopt via je
eigen GitHub-account en je eigen computer.

## Installeren

Je hebt Claude Code nodig: het tabblad **Code** in de Claude-app op je computer, of
Claude Code in een terminal. Op Windows heb je daarnaast **Git** nodig, en dat moet er
eerst zijn: zonder Git kan de plugin niet worden toegevoegd.

**Op Windows, vóór je de Claude-app installeert:** druk op de Windows-toets, typ
`PowerShell`, open het en plak deze regel:

```powershell
winget install -e --id Git.Git
```

Klik op **Ja** als Windows vraagt of dit programma wijzigingen mag aanbrengen. Doe dit
vóór de Claude-app, dan hoeft die daarna niet opnieuw te starten. Op een Mac hoeft dit
niet.

Installeer daarna de Claude-app (claude.ai/download) en log in. Open in het tabblad
**Code** een map (leeg mag, bijvoorbeeld `Documenten\Apps`) en typ in het chatvenster:

```text
/plugin marketplace add Stage-Two-AI/stack-plugin-light
```

Er verschijnt een klein venster met de vraag of je deze bron vertrouwt. Bevestig dat.
Daarna opent een scherm met plugins waarin `stack-light` al klaarstaat: klik op het **plusje**
ernaast om hem te installeren. Dat is alles.

Werk je in een terminal en verschijnt dat scherm niet, typ dan ook nog:

```text
/plugin install stack-light@stagetwo-light
```

**Controleren dat het werkt.** Typ `/stack-light:` en kijk of de vier commando's verschijnen
(installatie, nieuwe-app, verder-werken en updaten). Zie je ze niet, sluit Claude Code dan en open de map opnieuw.

**Bijwerken van de plugin zelf.** Dat gaat vanzelf, zonder dat je iets hoeft te typen.
`/stack-light:installatie` zet het aan; het werkt in elke map. Kort nadat je de Claude-app
hebt geopend en je eerste bericht hebt gestuurd, kijkt Claude Code op de achtergrond of
er een nieuwe versie is en haalt die binnen. Je hoeft de app daarvoor niet open te
houden of opnieuw te starten: de nieuwe versie verschijnt vanzelf.

## Beginnen op een nieuwe computer

Typ `/stack-light:installatie`. Je assistent kijkt wat er ontbreekt (Git, Node, pnpm en de
GitHub-opdrachtregel) en installeert dat. Twee dingen om te weten:

- **Windows vraagt een paar keer om toestemming.** Er verschijnt dan een venster of dit
  programma wijzigingen mag aanbrengen. Klik op **Ja**. Op een Mac kan om je wachtwoord
  worden gevraagd.
- **Inloggen bij GitHub doe je zelf, één keer, in een terminal.** Je assistent legt het
  precies uit: je opent Git Bash (Windows) of Terminal (Mac), typt `gh auth login`,
  kiest GitHub.com, HTTPS, Yes en "Login with a web browser", en typt een code over in
  de browser. **Onthoud die code; kopieer hem niet:** Ctrl+C breekt in dat venster het
  inloggen af. Daarna zeg je "klaar" in het chatvenster.

Soms kent Claude Code een net geïnstalleerd programma nog niet. Je assistent vraagt je
dan de app opnieuw te starten. Dat is normaal en gebeurt maar één keer. Twee dingen
die je daarbij niet vanzelf ziet:

- **Het kruisje sluit de app niet af.** Op Windows blijft hij rechtsonder in het
  systeemvak draaien. Klik daar op het pijltje **^**, klik met de rechtermuisknop op het
  Claude-icoon en kies **Afsluiten**. Open de app daarna opnieuw.
- **Je gesprek opent niet vanzelf.** Klik het aan in de linkerzijbalk en typ
  **ga verder**.

Tot slot zet je assistent je naam in Git, zodat later zichtbaar blijft welke wijziging
van jou is, welke van een collega en welke van Stage Two. Daarna vraagt hij wat je wilt:
een nieuwe app beginnen, verder werken aan een bestaande app, of alles updaten.

## Een nieuwe app beginnen

Typ `/stack-light:nieuwe-app`. Het eerste deel is een gesprek, en dat is bewust: de keuzes
daar zijn achteraf duur om te veranderen.

1. Is het echt een nieuwe app, of past het bij een app die je al hebt? De regel is: één
   app per verzameling gegevens. Gaat het over gegevens die al in een app zitten, dan is
   het een uitbreiding van die app, en die maak je met `/stack-light:verder-werken`.
2. Wat moet de app doen, voor wie, met welke gegevens, en wat is de eerste versie waar
   iemand echt iets aan heeft?
3. Een naam, de plek (onder het GitHub-account van je bedrijf, in een nieuwe map op je
   computer) en wie erbij mag (een of meer groepen uit de toegangslijst van je bedrijf).

Elke app krijgt een deur (alleen wie op de toegangslijst staat komt erin), een eigen
database en een eigen plek voor bestanden, allebei bij Cloudflare en allebei twee keer:
één voor het echte werk en één voor de previews. Daar hoef je niets voor te kiezen, en het
kost per app vrijwel niets. Losse pagina's (een galerij, een contactformulier) kunnen
later publiek worden; dat regel je met `/stack-light:verder-werken`.

Daarna maakt je assistent de app aan uit de nieuwste template, zet de eerste versie op
GitHub en beschermt de hoofdtak. Hij eindigt met wat er nog open staat en met de
volgende stap: open de nieuwe map in Claude Code en typ `/stack-light:verder-werken`.

De app online zetten, met deur, database en bestanden, doet daarna de workflow **App
inrichten** op GitHub, in de beheer-repo van je bedrijf (`stagetwo-beheer`, Stage Two zet
die bij de start neer). Staat de app nog niet op de toegangslijst, dan opent je assistent
eerst een voorstel (pull request) op die beheer-repo; de eigenaar keurt dat goed, en dan
gaat het verder. Je assistent start de workflow en wacht op het resultaat. Daarna staat er
een pull request op je app die de gegevens van de nieuwe database invult; zodra je die
merget, staat de app echt online. Dat is bewust zo gebouwd: de toegang tot Cloudflare
hoort niet op een werkcomputer te staan. GitHub is de enige plek waar de regels worden
afgedwongen, en zo blijft dat. Heeft je bedrijf nog geen beheer-repo, dan richt Stage Two
de app in.

Laat Stage Two weten dat de app bestaat. Dan komt hij in het overzicht en doet hij mee
met updates van de werkwijze.

## Alles updaten

Zegt je assistent dat er een nieuwere versie van de werkwijze is, of wil je het gewoon
bij de tijd houden, typ dan in de map van je app:

```text
/stack-light:updaten
```

Wat er dan gebeurt, in deze volgorde:

1. **De plugin zelf** wordt bijgewerkt. Een nieuwe versie werkt na het opnieuw openen
   van de app.
2. **De programma's op je computer** (Git, Node, pnpm en de GitHub-opdrachtregel) worden
   bijgewerkt. Op Windows vraagt Windows een paar keer of dat mag; klik op **Ja**.
3. **Je app naar de nieuwste werkwijze.** Je assistent maakt in een tijdelijke kopie van
   je app een voorstel klaar; je eigen bestanden en je lopende werk blijven
   onaangeraakt. Alleen als een bestand van de werkwijze bij jou anders is dan verwacht
   (omdat iemand het ooit heeft aangepast) stelt hij een vraag: de nieuwe versie
   overnemen, of jouw versie houden. Twijfel je? Kies "houden"; dat verandert niets aan
   wat nu werkt, en Stage Two kan er later naar kijken.
4. **De pakketten van je app** worden bijgewerkt, binnen de grenzen die in je app
   staan, als een tweede, los voorstel. Grote sprongen naar een nieuwe hoofdversie
   noemt hij alleen; die pakt Stage Two op.
5. **Je andere apps.** Je assistent laat zien welke andere apps van je bedrijf nog op
   een oudere werkwijze staan, en vraagt welke je nu wilt bijwerken. Die hoeven niet op
   je computer te staan. Elke gekozen app krijgt zijn eigen voorstellen.

Elk voorstel staat op GitHub als pull request, onder jouw naam, met een uitleg in
gewone taal. Daarna is het aan jou, precies zoals bij elke andere wijziging: open de
pull request, wacht tot de controles groen zijn en klik op **Merge**. Zijn de controles rood, dan
voldoet je app niet aan een nieuwe regel. Neem dan contact op met Stage Two en zet de
controle niet uit.

## Als iets niet lukt

| Je ziet | Wat er aan de hand is | Wat je doet |
|---|---|---|
| "log eerst in bij GitHub met `gh auth login`" | Je computer is niet ingelogd bij GitHub | Typ `gh auth login` in een terminal en volg de stappen |
| "de template is niet bereikbaar" | Geen internet, of GitHub is even niet bereikbaar | Later opnieuw proberen |
| "je hebt geen schrijfrecht" | Je account mag niet in deze app schrijven | Vraag de eigenaar van de app je toe te voegen |
| "installeer pnpm" | `pnpm` ontbreekt op je computer | Vraag Stage Two, of installeer het zoals bij de start is uitgelegd |
| "er staat al een pull request open" | Er ligt al een voorstel voor deze versie | Bekijk die pull request en merge hem, of vraag Stage Two |
| Je assistent weigert een bestand te wijzigen | Dat bestand hoort bij de gedeelde werkwijze | Wil je de nieuwste versie: `/stack-light:updaten`. Wil je het anders: vraag het Stage Two |
| "er staat al een voorstel voor de afhankelijkheden open" | De pakketten-PR van een vorige keer is nog niet gemerged | Merge die eerst (als de controles groen zijn), of sluit hem, en typ dan opnieuw `/stack-light:updaten` |
| De preview toont geen gegevens | De database op je eigen computer begint leeg | Voer zelf iets in via de app; de echte gegevens komen nooit op je computer |
| "deze app komt uit de ... template" bij `/stack-light:updaten` | De app hoort bij een ander spoor van Stage Two | Gebruik het commando dat in de melding staat; deze plugin laat die app met rust |
| Na installeren zegt `/stack-light:installatie` nog steeds dat iets ontbreekt | Claude Code kent het nieuwe programma nog niet | De app helemaal afsluiten (Windows: systeemvak rechtsonder, rechtermuisknop op Claude, Afsluiten), opnieuw openen, het gesprek aanklikken in de linkerzijbalk en **ga verder** typen |
| `/plugin marketplace add` lukt niet op Windows | Git ontbreekt | Git installeren zoals onder "Installeren", de app afsluiten via het systeemvak en opnieuw openen |
| `gh auth login` stopt halverwege | Ctrl+C gedrukt om de code te kopiëren; dat breekt het af | Opnieuw `gh auth login` typen en de nieuwe code onthouden in plaats van kopiëren |
| "de repo bestaat al" bij `/stack-light:nieuwe-app` | Er is al een app met die naam | Kies een andere naam |
| "main is nog niet beschermd" na `/stack-light:nieuwe-app` | Het GitHub-account staat op het gratis plan | Vraag Stage Two; de app werkt, alleen de bescherming ontbreekt nog |

Kom je er niet uit, dan is de vraag altijd welkom bij Stage Two. Vertel wat je typte en
wat er terugkwam; de melding is bedoeld om door te geven.

## Voor Stage Two

Alles hieronder is voor wie de plugin en de template onderhoudt.

### Drie sporen

Stage Two heeft sinds 13-10-2026 drie sporen, elk met een eigen template en een eigen plugin
(besluit `Stack/docs/besluiten/2026-10-13-stack-light.md`):

| Spoor | Template | Plugin | Marketplace | `variant` in het manifest |
|---|---|---|---|---|
| Vercel | `Stage-Two-AI/stack-template` | `Stage-Two-AI/stack-plugin` (`stack`) | `stagetwo` | geen |
| Cloudflare + Supabase | `Stage-Two-AI/stack-template-cloudflare` | `Stage-Two-AI/stack-plugin-cloudflare` (`stack-cloudflare`) | `stagetwo-cloudflare` | `"cloudflare"` |
| stack-light | `Stage-Two-AI/stack-template-light` | deze repo (`stack-light`) | `stagetwo-light` | `"light"` |

Een light-app is één Cloudflare Worker: de schermen als statische bestanden, servercode in
`worker/` (Hono, onder `/api`), een D1-database (`migrations/`) en R2 voor bestanden, met
een aparte D1 en R2 voor de previews. Geen Supabase.

Deze repo is begonnen als kopie van `stack-plugin-cloudflare` 1.2.0. Wat anders is:

- de template is `Stage-Two-AI/stack-template-light` (melding, updaten, nieuwe-app, de
  beheerde run);
- de hook, `updaten`, het overzicht en de beheerde run doen alleen iets bij een app met
  `"variant": "light"` in `.claude/stack-manifest.json`. Een app van een ander spoor laten
  ze aan de andere plugin over, ook als alle drie de plugins op één computer staan;
  `updaten` noemt dan het juiste commando;
- `nieuwe-app` kent geen databasekeuze meer (geen `--database`, geen `stack.config.json`):
  elke app heeft D1 en R2. Het script zet in `wrangler.jsonc` de Worker-naam op de
  appnaam, en `database_name` en `bucket_name` op `<naam>` (productie) en `<naam>-test`
  (`env.preview`). De database-id's blijven de nullen uit de template; App inrichten vult
  ze met een pull request. Het weghalen van `nietMeenemen` en het opruimen van de
  omgeving `proef-beheer` zijn weg: de light-template heeft geen `beheer/` en geen
  proef-workflows;
- `--inrichten` werkt zoals op het Cloudflare-spoor: eerst `toegang.json` van
  `<org>/stagetwo-beheer` (terugval op `stack-beheer`), zo nodig een pull request daarop,
  dan de workflow **App inrichten** (`app-inrichten.yml`, inputs `app` en `droogloop`);
- de hook herinnert aan de databaseroute bij schrijven in `migrations/` (niet meer in
  `supabase/migrations/`), en weigert naast `wrangler deploy` ook `wrangler login`,
  `wrangler secret`, `wrangler d1 create/delete`, `wrangler r2 bucket` en elke
  `wrangler d1`/`r2` met `--remote`. De lokale kopie (`pnpm db:lokaal`, `--local`) mag.
  `wrangler dev` valt onder dezelfde regel als `pnpm dev`;
- `verder-werken` heeft geen stap meer om functies uit te rollen: de servercode gaat mee
  met de gewone uitrol na de merge;
- `automatisch-bijwerken.mjs` zet de marketplace `stagetwo-light`.

Een verbetering die voor meer sporen geldt, doe je in elke plugin.

### Wat waar staat

```text
.claude-plugin/    plugin.json (naam stack-light, versie) en marketplace.json (naam stagetwo-light)
hooks/             de bewaker (PreToolUse) en de melding bij sessiestart (SessionStart)
skills/            de vier skills; met een script: updaten (bijwerken.mjs voor de
                   template, afhankelijkheden.mjs, overzicht.mjs), installatie
                   (controle.sh, shell omdat Node kan ontbreken) en nieuwe-app
                   (nieuwe-app.mjs: aanmaken, en --inrichten start de workflow in de
                   beheer-repo van de klant; plus ruleset.json voor main)
lib/               de kern: manifest lezen, toepassen, PR-tekst, git- en PR-stappen
beheer/            de beheerde run over het register van Stage Two; geen skill, alleen voor Stage Two
test/              de geheimenscan over boom en geschiedenis
```

`beheer/beheerd.mjs` staat bewust niet onder `bin/`: die map zet Claude Code op het
PATH van elke sessie waarin de plugin aanstaat, ook bij klanten. De beheerde run wordt
gestart vanuit `Stack/bin/stack-sync.mjs`, dat het register en de ruleset meegeeft.

### Hoe het werkt, in het kort

- De bewaker leest de beschermde paden uit `.claude/stack-manifest.json` van de repo
  (de lijst `vervangen`, plus `.github/CODEOWNERS` en alles onder `.github/workflows/`
  en `.claude/`). Zonder manifest, of met een andere `variant` dan `light`, doet hij niets. `STACK_ALLOW_POLICY_EDIT=1` laat
  padbewerkingen door, voor onderhoud aan de template zelf.
- De melding vergelijkt `.claude/stack-version` met de hoogste tag `stack-v<n>` op de
  publieke light-template (één anonieme `git ls-remote`, drie seconden), met een dagstempel
  per repo in `${CLAUDE_PLUGIN_DATA}`.
- Het templatedeel van `/stack-light:updaten` (`bijwerken.mjs`) draait in twee stappen: `--droogloop` (voorcontrole, tijdelijke
  kloon, kern toepassen, resultaat als JSON) en `--werkmap <map>` (keuzes toepassen,
  committen met de identiteit van de gebruiker, pushen als de boom verschilt, PR openen
  of bijwerken). Elke commit draagt de trailer `Stack-bijwerken: v<n>`; een branch met
  een commit zonder die trailer wordt nooit opnieuw opgebouwd. De tijdelijke map
  verdwijnt na de tweede aanroep en bij elke mislukking. Met `--repo eigenaar/naam`
  werkt het een app bij die niet op de computer staat (kloon via de gh-login). De
  branchnaam `stack-bijwerken/v<n>` en de trailer blijven zo heten: de beheerde run en
  de bestaande pull requests van klanten leunen erop.
- `afhankelijkheden.mjs`: `pnpm update --no-save` in een tijdelijke kloon (alleen het
  lockfile verandert, de grenzen in package.json zijn deels van de template), PR op de
  vaste branch `stack-afhankelijkheden`; staat die PR al open, dan stopt hij. Noemt de
  hoofdversies uit `pnpm outdated` en de open Dependabot-PR's.
- `overzicht.mjs`: de light-apps met schrijfrecht, per eigenaar via
  `gh repo list` en de inhoud van `.claude/stack-version`; wijzigt niets.
- De hook geeft bij schrijven in `migrations/` de databaseroute mee als
  `additionalContext` (geen weigering, de gewone toestemmingsvraag blijft).
- De kern (`lib/toepassen.mjs`) controleert zichzelf: raakt er iets buiten het manifest,
  dan stopt hij. Een eigen bestand van de klant wordt nooit stil overschreven of
  verwijderd; het komt in `overgeslagen` met een reden en een keuze.

### Een klant aansluiten (checklist)

Vooraf: de template is publiek, de tag `stack-v<n>` van de nieuwste versie staat, de
accounts van de klant staan (GitHub-organisatie op een betaald plan, Cloudflare met Zero
Trust) en `<klantorg>/stagetwo-beheer` is ingericht met de light-variant van App inrichten
(recept in Stage-Two-AI/stack-beheer), met minstens
één groep in `toegang.json`. De klant heeft Write op stagetwo-beheer, zodat hij de workflow
mag starten; de sleutels staan in de omgeving `beheer` en zijn voor hem niet te lezen.

1. Op Windows eerst Git (`winget install -e --id Git.Git` in PowerShell), dán de
   Claude-app. Plugin installeren zoals hierboven onder "Installeren" (desktop-app: één
   commando, vertrouwen bevestigen, plusje). Zo getest met de andere plugins op
   22-09-2026 en 01-10-2026 op Windows in de desktop-app; voor stack-light nog niet.
2. `/stack-light:installatie` samen doorlopen: installaties, de terminalstap voor `gh auth login`,
   de git-identiteit. Leg vooraf uit: de UAC-vensters, dat de code van `gh auth login`
   overgetypt wordt (Ctrl+C breekt af), en dat een herstart via het systeemvak gaat en
   het gesprek daarna via de linkerzijbalk terugkomt ("ga verder").
3. Controleer dat de vier skills verschijnen als `/stack-light:<naam>`.
4. Open een light-app en controleer dat de bewaker vuurt: vraag de agent
   één regel te wijzigen in `.github/workflows/ci.yml`; dat moet geweigerd worden.
5. Controleer dat de plugin zichzelf bijwerkt. `/stack-light:installatie` (stap 5) zet dat op
   gebruikersniveau aan, in `~/.claude/settings.json`: `env.FORCE_AUTOUPDATE_PLUGINS = "1"`
   en `extraKnownMarketplaces.stagetwo-light.autoUpdate = true`. Beide zijn nodig. De desktop-app
   start Claude Code met `DISABLE_AUTOUPDATER=1`, en dat zet ook het bijwerken van plugins
   uit; een marketplace die de klant zelf toevoegt, krijgt bovendien geen `autoUpdate`
   (standaard uit). De `autoUpdate` in `.claude/settings.json` van een app (template v11)
   is daarom in de desktop-app niet genoeg. Vastgesteld en bewezen op 02-10-2026 op de
   Windows-VM (met de Vercel-plugin): na de instelling, één herstart en één bericht kwam
   de nieuwe versie binnen, zonder nog een herstart. Controle: vraag de assistent `~/.claude/plugins/installed_plugins.json`
   te tonen.
6. Loop de melding en `/stack-light:updaten` één keer samen door, en `/stack-light:nieuwe-app` als
   de klant zelf apps gaat starten. Worker, deur, D1 en R2 richt de workflow "App
   inrichten" in `<klantorg>/stagetwo-beheer` in; die toegang komt nooit op de computer
   van de klant (besluit 22-09-2026).
7. Zet in `Stack/projecten.json` de `route` van het project op `plugin`; een app die de
   klant zelf met `/stack-light:nieuwe-app` maakte, voeg je toe zodra hij hem meldt.

### Een nieuwe versie uitbrengen

Volgorde bij elke release: eerst de plugin, dan de template. Een oude plugin stopt op
een nieuwer manifestformaat; een nieuwe plugin kan altijd met een oudere template
overweg.

1. Plugin: versie in `.claude-plugin/plugin.json` ophogen, pull request, groene check,
   merge naar `main`. Alleen een hoger versienummer laat een klant een update zien.
2. Template: wijzigingen als pull request op `stack-template-light`, met
   `.claude/stack-version` en `stackVersion` in het manifest opgehoogd. Een bestand uit
   `vervangen` wijzigt alleen samen met zo'n versieverhoging.
3. Na de merge de tag zetten: `git tag stack-v<n> && git push origin stack-v<n>`. Pas
   dan bestaat de versie voor de melding en de skill. Een tag wordt nooit verplaatst;
   de ruleset op de template weigert dat.
4. Registerprojecten: `node bin/stack-sync.mjs --status` in Stack, dan de droogloop,
   dan `--doe-het`.

### De repo beschermen

De ruleset op `main` (`.github/ruleset.json`) staat: geen directe push, pull request
met de check `Tests` groen. Opnieuw zetten na een herinrichting:

```sh
gh api repos/Stage-Two-AI/stack-plugin-light/rulesets -X POST --input .github/ruleset.json
```

### Tests

```sh
npm test
claude plugin validate .
```

Licentie: MIT (zie `LICENSE`). De naam Stage Two en de huisstijl vallen daar niet onder.
