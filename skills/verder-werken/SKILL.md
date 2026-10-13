---
name: verder-werken
description: De vaste route voor een wijziging aan deze app - branch maken, bouwen, testen, pull request openen met preview-link. Gebruik dit bij elk verzoek om iets toe te voegen, te wijzigen of te repareren aan deze applicatie, ook als het een kleinigheid lijkt, ook als er een tabel of kolom bij komt (databasewijziging in migrations/), ook bij servercode in worker/, en ook als de gebruiker tijdens het bouwen wil meekijken.
---

Deze route staat uitgeschreven in `docs/routes/verder-werken.md`. Lees dat bestand nu in
zijn geheel en loop de stappen in volgorde af.

Hier staat bewust geen kopie van de tekst. De route is voor elke agent dezelfde, en
`docs/routes/` is de enige plek waar hij staat, zodat er nooit twee versies zijn die
uit elkaar lopen. Deze skill is alleen de aansluiting voor Claude Code.

Drie dingen die bij deze route horen en die de route zelf ook noemt:

- **Raakt de wijziging de database** (een tabel, kolom of index), lees dan ook
  `docs/routes/databasewijziging.md` in zijn geheel en volg die stappen. Een migratie is
  een nieuw bestand in `migrations/`; de hook van de plugin herinnert je aan de route
  zodra je daar schrijft.
- **Servercode** staat in `worker/` en gaat met de rest van de app mee bij de uitrol na de
  merge. Er is geen aparte stap om hem live te zetten. Zelf `wrangler deploy` of iets met
  `--remote` draaien kan en mag niet: op deze computer is geen Cloudflare-toegang.
- **Meekijken tijdens het bouwen** gaat in de Claude-app via de preview: die start de app
  op deze computer volgens `.claude/launch.json`, met een lokale database en nooit tegen
  productie. Start geen dev-server in Bash. Opleveren blijft altijd de pull request met
  de Cloudflare-preview (de workflow Preview uitrollen zet de link in de PR).
