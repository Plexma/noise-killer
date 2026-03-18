## [2026-03-18] - Bugfixes: arstechnica, tagesschau, pcgameshardware, gamestar

### Behoben
- **arstechnica.com**: Author-Box blockiert nicht vollständig. Selector geändert von `div:has(> a[href*="/author/"])` zu `div.author-mini-bio` (blockiert komplette Bio-Box inkl. Avatar und Text).
- **www.tagesschau.de**: "Zur Startseite"-Button nicht blockiert. Selector war `ul.buttongroup`, aber Element ist `div.buttongroup`.
- **www.pcgameshardware.de**: Comment-Sprechblase am Anfang und Ende nicht blockiert. `div.commentIcon` ergänzt.
- **www.gamestar.de**: Inline-Werbung "Auch spannend" nicht blockiert. `div:has(> h3:has-text(/auch spannend/i))` ergänzt.

## [2026-03-18] - Bugfixes: mydealz.de, n-tv.de, ndr.de, stadt-bremerhaven.de

### Behoben
- **www.mydealz.de**: „Ähnliche Gutscheine"-Abschnitt blockiert via `[data-t="main"] div:has(> h3:has-text(/Gutschein/))`.
- **www.n-tv.de**: Artikel-Tags am Artikelende blockiert (`[class*="article-detail-footer_tags"]`); CSS-Grid-Wrapper per `:style(display:block)` auf Block-Layout gesetzt, damit der rechte Leerraum (reservierte Grid-Spalte für die blockierte Aside) kollabiert.
- **www.ndr.de**: Artikel-Tags am Artikelende blockiert (`div.tagbox`).
- **stadt-bremerhaven.de**: Whitespace-Fix verbessert – `max-width: 100% !important` zur `:style()`-Injection ergänzt, um hartcodierten `max-width`-Wert zu überschreiben.

## [2026-03-18] - Bugfixes: ifun.de, iphone-ticker.de, mydealz.de komplett neu

### Behoben
- **www.ifun.de / www.iphone-ticker.de**: `#article-single-stats` ergänzt – enthält Kommentar-Link und Mastodon-Share-Button am Artikelanfang.
- **www.mydealz.de**: Kompletter Neuaufbau. `div.stickyBar-bottom` und `section[role][data-t]` nicht mehr gefunden (Redesign). Neue Selektoren auf Basis stabiler `data-t`-Attribute: Kommentare, Related Deals, Share-Button, Subscribe, Keyword-Widget, Vote-Erklärung, internalLinking, App-Download und Footer blockiert.

## [2026-03-18] - Bugfixes: pcgameshardware.de, gamestar.de, derstandard.de, handelsblatt.com

### Behoben
- **www.pcgameshardware.de**: `##footer` blockierte nichts (kein `<footer>`-Element vorhanden). Footer ist `div.header2.footer3`; Print/Abo-Werbung in `ul.rowAlt.footer2` ergänzt.
- **www.gamestar.de**: `div.contentteaser.row.box.contentmediaitem-box` deckte nur „Beliebt"/„Aktuell" ab, nicht „Empfohlen" (`contentitem-box`). Selector vereinfacht auf `div.contentteaser.row.box`. `a.do-toggle-comments` (Kommentar-Link im Artikelkopf, außerhalb `#comments`) und `ul.taglist` (Artikel-Tags) ergänzt.
- **www.derstandard.de**: Eigenständige Domain (`.de`) hatte keine Filter. Alle Selektoren von `www.derstandard.at` gespiegelt. `a.article-postingcount` (Posting-Count-Button im Artikelkopf) für beide Domains ergänzt. `div.story-tool` (floating Panel mit Posting-Count + Social-Share-Buttons inkl. Bluesky) für beide Domains ergänzt.
- **www.handelsblatt.com**: `app-embed.ng-star-inserted > app-iframe > iframe` ließ den äußeren Container sichtbar (leere Newsletter-Box). Vereinfacht auf `app-embed`.

## [2026-03-18] - Bugfix: tagesspiegel.de Opinary-Widget

### Behoben
- **www.tagesspiegel.de**: Opinary-Widget renderte sich trotz geblockem `#opinary-automation-placeholder` neu in `#opinary-root` + `#opinary-iframe`. Beide IDs ergänzt.

## [2026-03-18] - Bugfixes: tarnkappe.info, tagesspiegel.de, t-online.de

### Behoben
- **tarnkappe.info**: `div.sonderwerbemittel` hat den gesamten Artikelbereich blockiert (wraps `#primary`). Entfernt.
- **www.tagesspiegel.de**: Floating Share-/Mail-Button (sticky `ul`) blockiert via `ul:has([data-gtm-class="article-social-link"])`; Themen-Buttons am Artikelende blockiert via `p:has(> a[data-gtm-class="article-home-link"]) ~ ul`; P mit „Zur Startseite"-Link nun komplett blockiert statt nur das A-Element.
- **www.t-online.de**: `div[data-testid="Page.PageStages"]` blockiert – enthält „Neueste Artikel"-Teaser, „Themen"-Pills und „Internationale Politik von A bis Z"-Navigation am Artikelende.

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
