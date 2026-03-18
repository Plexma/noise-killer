## [2026-03-18] - Umfangreiche Überarbeitung: 15 Sites gefixt und erweitert

### Behoben
- **arstechnica.com**: `main > div` hat alle Artikel-Gruppen auf der Startseite geblockt. Ersetzt durch `div.ad-wrapper`.
- **www.buffed.de**: Alle Selektoren außer `aside` nicht mehr gefunden (Redesign). Kritischer Filter `header.mainHeader` entfernt (hätte Site-Header geblockt). Nur bestätigte Selektoren behalten + `div.wadtag` ergänzt.
- **www.derstandard.de**: Domain-Fehler – korrekte Domain ist `www.derstandard.at`. `div.story-community-postings` nicht gefunden; ersetzt durch `section.story-community`.
- **www.golem.de**: `div.go-teaser-block` hat alle 25 Artikelgruppen auf der Startseite geblockt. Ersetzt durch gezielte Modifier-Selektoren (`--career`, `--carousel`, `--small-text`).
- **www.ndr.de**: `div.teaser` hat alle Artikel-Cards auf der Startseite geblockt (55 Elemente). Entfernt.
- **www.pcgameshardware.de**: Fünf veraltete Selektoren entfernt (nicht mehr gefunden nach Redesign). Ersetzt durch `aside.innerArticleModule`, `aside.column.right`, `aside.rec_box_bottom`.
- **tarnkappe.info**: `div > div > div[data-nosnippet]` hat Navigationsleisten geblockt. `div.column.is-one-third` hat alle Artikel-Cards auf der Startseite geblockt. Ersetzt durch präzise Selektoren.
- **taz.de**: `section > section` hat Artikel-Teaser-Sections auf der Startseite geblockt. Ersetzt durch `section.outerwrapper.contains-module-article > section:not([x-data])`.

### Hinzugefügt
- **arstechnica.com**: `#comments` (Kommentarsektion).
- **www.gamestar.de**: `#comments` (Kommentarsektion), `div.row:has(> .newsletter-form-container)` (Newsletter-Box).
- **www.handelsblatt.com**: `app-advertisement`, `app-content-advertisement` (Display- und Inline-Werbung), `app-detail-page-footer` (Artikelfooter mit Outbrain).
- **www.heise.de**: Startseiten-Filter via `data-component`: `NewAdModule`, `MarketingTeaserModule`, `HeiseJobsModule`, `PreisvergleichModule`.
- **www.ifun.de**: `#article-single-comments` (Kommentarsektion).
- **www.iphone-ticker.de**: `#article-single-comments` (Kommentarsektion).
- **www.n-tv.de**: `section[class*="widget-teaser"]` (Teaser-Widgets), `div[class*="social-share"]` (Social-Share-Bar).
- **steamdb.info**: `a.support-above-footer` (Support-Button über dem Footer).
- **stadt-bremerhaven.de**: CSS-Injection `div.main-inner.group > div.content:style(width: 100% !important; float: none !important)` – behebt Leerraum rechts nach Sidebar-Blockierung.
- **www.t-online.de**: `aside[data-testid="StreamLayout.Companion"]` (rechte Sidebar), `div[data-testid="nativendo-container"]` (Native Ads), `div[data-testid="Commercial.SDI"]` (Werbeplatz), `div[data-testid="PageFooter"]` (Footer).
- **www.tagesspiegel.de**: `#opinary-automation-placeholder` (Meinungsumfrage-Widget), `#outbrain-container` (Outbrain-Empfehlungen), `button[data-gtm-class="open-community"]` (Kommentare-Button), `a[data-gtm-class="article-home-link"]`, `footer`.
- **www.derstandard.at**: `section.story-recommended` (Taboola-Empfehlungen).

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
