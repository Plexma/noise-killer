## [2026-03-18] - Spiegel Mobile-Bugfix "Mehr lesen über" / "Verwandte Artikel"

### Behoben
- **www.spiegel.de**: `section[data-smartfeed-id="further-reads"]` blockierte auf Mobile
  (eingeloggte User) nicht zuverlässig. Filter auf element-agnostisch geändert
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
