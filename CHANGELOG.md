## [2026-03-18] - The Verge Kommentare + Follow-Widget

### Hinzugefügt
- **www.theverge.com**: Kommentar-Links (`duet--article--comments-link`), „12 Comments"-
  Schaltfläche am Artikelende (`#zephr-anchor > span`) und „Follow topics and authors"-
  Widget (`#zephr-anchor > div:has(> span + ul)`) blockiert.

## [2026-03-18] - The Verge erweitert

### Hinzugefügt
- **www.theverge.com**: Native Anzeigen (`duet--ad--native-ad-linkset`, `duet--ad--native-ad-rail`),
  „Most Popular"-Sidebar (`duet--layout--rail`) und Newsletter-Abo-Box (`duet--cta--newsletter`)
  blockiert. Footer-Selector auf semantisches `duet--navigation--footer` präzisiert.

## [2026-03-18] - Spiegel Mobile-Bugfix Leerraum am Artikelende

### Behoben
- **www.spiegel.de**: Mobile Anzeigen-Container (`[data-advertisement~="mobile"]`) reservieren auf
  Mobilgeräten per CSS-Klasse `sm:min-h-632` bis zu 632px Leerraum, wenn keine Werbung lädt
  (z. B. bei Brave). Auf Desktop sind sie bereits durch Spiegels CSS verborgen. Filter
  `[data-advertisement~="mobile"]` entfernt die Platzhalter nun auch auf Mobile.
  Zusätzlich drei Klassen-Selektoren als Fallback für Brave (adblock-rust verarbeitet
  `data-advertisement`-Filter evtl. zu spät) und für ein Platzhalter-Div ohne Attribut:
  `[class~="sm:min-h-352"]`, `[class~="sm:min-h-492"]`, `[class~="sm:min-h-632"]`.

## [2026-03-18] - Spiegel Mobile-Bugfix "Mehr lesen über" / "Verwandte Artikel"

### Behoben
- **www.spiegel.de**: `section[data-smartfeed-id="further-reads"]` blockierte auf Mobile
  nicht zuverlässig. Die Section ist im serverseitigen HTML sichtbar – Alpine.js versteckt
  sie nur auf Desktop. Filter auf element-agnostisch geändert
  (`[data-smartfeed-id="further-reads"]`) + innere Sections als Fallback ergänzt:
  `section:has(> h3:has-text(/^Mehr lesen über$/))` und
  `section:has(> h3:has-text(/^Verwandte Artikel$/))`.

## [2026-03-18] - Tagesschau Kommentare-Button

### Behoben
- **www.tagesschau.de**: `a.btn.btn--text.btn--standard-secondary.btn--fullwidth` hat nur
  den sekundären „Zur Startseite"-Button geblockt. Der primäre „Kommentare zur Meldung"-Button
  (`btn--standard-primary`) blieb sichtbar. Ersetzt durch `ul.buttongroup`, der die
  gesamte Buttongroup am Artikelende sauber entfernt.

## [2026-03-17] - Spiegel Bugfix "Mehr lesen über"

### Behoben
- **www.spiegel.de**: `section:has(> h3:has-text(/^Mehr lesen über$/))` hat nur
  die innere Section getroffen, nicht den äußeren Container – „Mehr lesen über"-Box
  blieb sichtbar und hinterließ einen großen Whitespace. Ersetzt durch
  `section[data-smartfeed-id="further-reads"]`, der den kompletten Container
  sauber entfernt.

## [2026-03-17] - Deutschlandfunk hinzugefügt

### Hinzugefügt
- **www.deutschlandfunk.de**: Footer (footer.b-footer) blockiert
